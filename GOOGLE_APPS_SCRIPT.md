# 🔧 Google Apps Script - Kode Lengkap

Copy-paste seluruh kode di bawah ini ke editor Google Apps Script Anda.

---

## PENTING: Sebelum Copy Code

1. Buat folder baru di Google Drive (nama bebas, misal "Dokumen Universitas Upload")
2. Catat ID folder dari URL: `https://drive.google.com/drive/folders/[ID_DISINI]/`
3. Biar Anda siap ganti `FOLDER_ID` di baris pertama kode di bawah

---

## 📋 Google Apps Script Code

Salin kode berikut ke file `Code.gs` di Google Apps Script:

```javascript
// ===== START CODE =====
// ============================================
// UPLOAD DOKUMEN UNIVERSITAS FALETEHAN
// Google Apps Script Version
// ============================================

// --------------------------------------------------
// KONFIGURASI
// 1. Folder induk (default) tempat dokumen disimpan bila
//    kategori tidak dikenali. Anda boleh menggantinya atau
//    membiarkannya kosong.
// 2. Map kategori → folder untuk menyimpan file berdasarkan
//    pilihan pengguna. Tambahkan/mutakhirkan sesuai
//    kebutuhan.
// --------------------------------------------------
const FOLDER_ID = "1JjG9tN2qJ3L6slYNpwjO8wby21FldLB9"; // folder default (gunakan hanya sebagai cadangan)
const SHEET_NAME = "Dokumen Metadata"; // Nama sheet untuk menyimpan metadata

// jika Anda ingin memisahkan file ke subfolder berdasarkan kategori,
// gunakan objek di bawah ini. Kunci harus sesuai dengan nilai kategori
// yang dikirim dari frontend (lihat <select id="category" di upload.html).
const CATEGORY_FOLDERS = {
  "Senat": "1neje7RkRDlB42OmgToLdsWeJNfz-piYD",
  "Akademik Fakultas": "1YbYq8puZZnO74o3qhwtcysoWbGjegJ66",
  "S2 Kesehatan Masyarakat": "1XEviX-ahRVemRh46sEIU9hmyEHk73aGn",
  "S1 Kesehatan Masyarakat": "1ESbg4hCJCijrqPUqJf50mxWoYRG_kCjp",
  "S1 Keperawatan dan Profesi Ners": "1o8wXIeowfCnXcixyRQq6C6LoCRDDEZx1",
  "S1 Kebidanan dan Pendidikan Profesi Bidan": "1xv28pveMRUJrg2PR-HEAOuwHYnSbdwGD",
  "D III Keperawatan": "144DrRs2F6UhX5TUM1xj6JMHWWGWbHTi9",
  "Tambahan": "1-A9h8Tihrn4I-NPCNx3dSIv_Tn1PEYAE"
};

// ============================================
// MAIN HANDLER - Entry Point
// ============================================

function doPost(e) {
  try {
    const data = JSON.parse(e.postData.contents);
    
    if (data.action === 'delete') {
      return deleteDocument(data.fileId);
    } else {
      return uploadDocument(data);
    }
  } catch (error) {
    Logger.log('Error in doPost: ' + error);
    return ContentService.createTextOutput(JSON.stringify({
      status: 'error',
      message: 'Error: ' + error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet(e) {
  try {
    if (e.parameter.action === 'list') {
      return listDocuments();
    } else {
      return ContentService.createTextOutput(JSON.stringify({
        status: 'error',
        message: 'Invalid action'
      })).setMimeType(ContentService.MimeType.JSON);
    }
  } catch (error) {
    Logger.log('Error in doGet: ' + error);
    return ContentService.createTextOutput(JSON.stringify({
      status: 'error',
      message: 'Error: ' + error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}

// ============================================
// UPLOAD DOCUMENT
// ============================================

function uploadDocument(data) {
  try {
    // Decode base64 file
    const fileData = Utilities.newBlob(
      Utilities.base64Decode(data.fileData),
      data.fileType,
      data.fileName_
    );

    // Determine destination folder based on category map
    let targetFolderId = FOLDER_ID; // default
    if (data.category && CATEGORY_FOLDERS[data.category]) {
      targetFolderId = CATEGORY_FOLDERS[data.category];
    }

    // Get folder (falls back to default if map missing)
    const folder = DriveApp.getFolderById(targetFolderId);

    // Upload file
    const file = folder.createFile(fileData);

    // Get file info
    const fileId = file.getId();
    const fileUrl = file.getUrl();
    const fileSize = formatBytes(file.getSize());

    // Save metadata to spreadsheet
    const metadata = {
      fileId: fileId,
      fileName: data.fileName,
      category: data.category,
      description: data.description || '',
      uploadDate: new Date().toISOString(),
      uploadedBy: Session.getUser().getEmail(),
      fileUrl: fileUrl,
      originalFileName: data.fileName_,
      fileSize: fileSize
    };

    saveMetadata(metadata);

    return ContentService.createTextOutput(JSON.stringify({
      status: 'success',
      message: 'File berhasil diupload',
      fileId: fileId
    })).setMimeType(ContentService.MimeType.JSON);

  } catch (error) {
    Logger.log('Upload error: ' + error);
    return ContentService.createTextOutput(JSON.stringify({
      status: 'error',
      message: 'Error upload: ' + error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}

// ============================================
// LIST DOCUMENTS
// ============================================

function listDocuments() {
  try {
    const sheet = getMetadataSheet();
    const data = sheet.getDataRange().getValues();

    const documents = [];
    
    // Skip header row
    for (let i = 1; i < data.length; i++) {
      const row = data[i];
      
      // Skip empty rows
      if (!row[0]) continue;

      documents.push({
        fileId: row[0],
        fileName: row[1],
        category: row[2],
        description: row[3],
        uploadDate: row[4],
        uploadedBy: row[5],
        fileUrl: row[6],
        originalFileName: row[7],
        fileSize: row[8]
      });
    }

    return ContentService.createTextOutput(JSON.stringify({
      status: 'success',
      documents: documents,
      total: documents.length
    })).setMimeType(ContentService.MimeType.JSON);

  } catch (error) {
    Logger.log('List error: ' + error);
    
    // If sheet doesn't exist, create it
    if (error.toString().includes('Sheet')) {
      createMetadataSheet();
      return ContentService.createTextOutput(JSON.stringify({
        status: 'success',
        documents: [],
        total: 0,
        message: 'Spreadsheet created, no documents yet'
      })).setMimeType(ContentService.MimeType.JSON);
    }

    return ContentService.createTextOutput(JSON.stringify({
      status: 'error',
      message: 'Error: ' + error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}

// ============================================
// DELETE DOCUMENT
// ============================================

function deleteDocument(fileId) {
  try {
    const file = DriveApp.getFileById(fileId);
    file.setTrashed(true);

    // Remove from metadata
    removeMetadata(fileId);

    return ContentService.createTextOutput(JSON.stringify({
      status: 'success',
      message: 'File berhasil dihapus'
    })).setMimeType(ContentService.MimeType.JSON);

  } catch (error) {
    Logger.log('Delete error: ' + error);
    return ContentService.createTextOutput(JSON.stringify({
      status: 'error',
      message: 'Error delete: ' + error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}

// ============================================
// METADATA SHEET FUNCTIONS
// ============================================

function getMetadataSheet() {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  let sheet = ss.getSheetByName(SHEET_NAME);

  if (!sheet) {
    sheet = createMetadataSheet();
  }

  return sheet;
}

function createMetadataSheet() {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const sheet = ss.insertSheet(SHEET_NAME);

  // Set header
  sheet.getRange('A1:I1').setValues([[
    'File ID',
    'Nama Dokumen',
    'Kategori',
    'Deskripsi',
    'Tanggal Upload',
    'Diupload Oleh',
    'File URL',
    'Nama File Original',
    'Ukuran File'
  ]]);

  // Format header
  sheet.getRange('A1:I1').setBackground('#1e3c72').setFontColor('#ffffff').setFontWeight('bold');

  // Set column width
  sheet.setColumnWidths(1, 9, 150);

  Logger.log('Metadata sheet created');
  return sheet;
}

function saveMetadata(metadata) {
  const sheet = getMetadataSheet();
  sheet.appendRow([
    metadata.fileId,
    metadata.fileName,
    metadata.category,
    metadata.description,
    metadata.uploadDate,
    metadata.uploadedBy,
    metadata.fileUrl,
    metadata.originalFileName,
    metadata.fileSize
  ]);

  Logger.log('Metadata saved for: ' + metadata.fileName);
}

function removeMetadata(fileId) {
  const sheet = getMetadataSheet();
  const data = sheet.getDataRange().getValues();

  // Find and delete row
  for (let i = 1; i < data.length; i++) {
    if (data[i][0] === fileId) {
      sheet.deleteRow(i + 1);
      Logger.log('Metadata removed for fileId: ' + fileId);
      break;
    }
  }
}

// ============================================
// UTILITY FUNCTIONS
// ============================================

function formatBytes(bytes) {
  if (bytes === 0) return '0 Bytes';
  const k = 1024;
  const sizes = ['Bytes', 'KB', 'MB', 'GB'];
  const i = Math.floor(Math.log(bytes) / Math.log(k));
  return Math.round(bytes / Math.pow(k, i) * 100) / 100 + ' ' + sizes[i];
}

// Test function - run ini untuk test
function testUpload() {
  Logger.log('Google Apps Script is working!');
  Logger.log('Folder ID: ' + FOLDER_ID);
  
  // Test list
  const result = listDocuments();
  Logger.log('List result: ' + result);
}

// ============================================
// END OF SCRIPT
// ============================================
// ===== END CODE =====
```

---

## 📝 Penjelasan Kode

### Main Functions

| Function | Deskripsi |
|----------|-----------|
| `doPost(e)` | Handle POST request (upload & delete) |
| `doGet(e)` | Handle GET request (list) |
| `uploadDocument(data)` | Upload file ke Google Drive |
| `listDocuments()` | List semua dokumen |
| `deleteDocument(fileId)` | Hapus dokumen |

### Metadata Storage

- **Spreadsheet**: Simpan metadata dokumen di Google Sheets
- **Columns**: File ID, Nama, Kategori, Deskripsi, dll
- **Auto-create**: Jika sheet belum ada, akan dibuat otomatis

### API Endpoints

```
POST /macros/d/{ID}/userweb
Body: JSON object dengan action
- uploadDocument: Upload file baru
- deleteDocument: Hapus file

GET /macros/d/{ID}/userweb?action=list
Response: JSON array dokumen
```

---

## 🔄 Flow Diagram

```
Frontend (upload.js)
    ↓
fetch(GAS_WEB_APP_URL, POST)
    ↓
Google Apps Script (doPost)
    ↓
Upload File ke Google Drive (folder)
    ↓
Save Metadata ke Spreadsheet
    ↓
Return JSON {status, fileId}
    ↓
Frontend update UI
```

---

## ⚙️ Konfigurasi

### 1. Change Folder ID

Edit baris pertama:
```javascript
const FOLDER_ID = "GANTI_DENGAN_FOLDER_ID_ANDA";
```

Ambil dari URL folder Google Drive:
```
https://drive.google.com/drive/folders/1JjG9tN2qJ3L6slYNpwjO8wby21FldLB9
                                       ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
                                       Copy ID ini
```

### 2. Change Spreadsheet Name

Edit baris:
```javascript
const SHEET_NAME = "Dokumen Metadata"; // Ubah nama sheet jika mau
```

---

## 🧪 Testing

### Test di Google Apps Script

1. Buka Google Apps Script editor
2. Cari function `testUpload()`
3. Klik garis nomor untuk pilih function
4. Klik play button ▶️
5. Lihat log di **Execution log**

Expected output:
```
Google Apps Script is working!
Folder ID: 1JjG9tN2qJ3L6slYNpwjO8wby21FldLB9
...
```

---

## 📊 Database Schema

### Spreadsheet Columns

| Column | Type | Contoh |
|--------|------|--------|
| A | File ID | `1a2b3c4d5e6f7g8h9i...` |
| B | Nama Dokumen | `SK Pengangkatan 2026` |
| C | Kategori | `Senat` |
| D | Deskripsi | `Surat Keputusan Pengangkatan Anggota Senat` |
| E | Tanggal Upload | `2026-02-19T10:30:00Z` |
| F | Diupload Oleh | `user@gmail.com` |
| G | File URL | `https://drive.google.com/file/d/1a2b...` |
| H | Nama File Original | `SK_Pengangkatan.pdf` |
| I | Ukuran File | `2.5 MB` |

---

## 🔒 Permissions Required

Google Apps Script memerlukan akses:
- ✅ Google Drive (upload, delete, read)
- ✅ Google Sheets (create, write, read)
- ✅ User email (untuk logging)

Saat pertama kali jalankan, Google akan minta approval.

---

## 📈 Scalability

- **Files**: Unlimited (Google Drive storage)
- **Metadata**: 5 juta rows per sheet
- **Request rate**: 30 requests per minute
- **File size**: 5GB max per file
- **Upload limit**: ~25MB recommended via fetch

---

**Last Updated**: 19 Februari 2026  
**Version**: 1.0
