# 📋 (DEPRECATED) Sistem Upload Dokumen - Panduan Lengkap

> **Catatan:** sistem upload sudah dinonaktifkan; file ini hanya untuk arsip.

Panduan lengkap untuk setup sistem upload dokumen dengan Google Apps Script dan Google Drive.

---

## 📝 Daftar Isi

1. [Teknologi yang Digunakan](#teknologi)
2. [Struktur File](#struktur-file)
3. [Setup Google Apps Script](#setup-gas)
4. [Deploy Google Apps Script](#deploy-gas)
5. [Konfigurasi Website](#konfigurasi)
6. [Upload ke GitHub Pages](#github-pages)
7. [Penggunaan Sistem](#penggunaan)
8. [Troubleshooting](#troubleshooting)

---

## <a name="teknologi"></a>🛠️ Teknologi yang Digunakan

- **Frontend**: HTML, CSS, JavaScript
- **Backend**: Google Apps Script
- **Storage**: Google Drive
- **Hosting**: GitHub Pages (static)
- **API Communication**: Fetch API (JSON)

---

## <a name="struktur-file"></a>📁 Struktur File

```
pusatdokumen/
├── index.html                    # Halaman beranda (dokumen existing)
├── style.css                     # CSS halaman beranda
├── upload.html                   # Halaman upload dokumen
├── upload-style.css              # CSS upload page
├── upload.js                     # JavaScript upload page
├── README.md                     # Dokumentasi ini
├── GOOGLE_APPS_SCRIPT.md         # Kode Google Apps Script
└── .github/
    └── DEPLOY_GUIDE.md           # Panduan deployment
```

---

## <a name="setup-gas"></a>⚙️ Setup Google Apps Script

### Langkah 1: Buat Project Google Apps Script

1. Buka [Google Apps Script](https://script.google.com/)
2. Klik **Projek Baru**
3. Rename project menjadi "Upload Dokumen Universitas"

### Langkah 2: Copy Code Google Apps Script

Buka file [GOOGLE_APPS_SCRIPT.md](GOOGLE_APPS_SCRIPT.md) dan copy seluruh kode ke editor Google Apps Script.

### Langkah 3: Setup Google Drive Folder

1. Buat folder baru di Google Drive dengan nama "Dokumen Universitas Upload"
2. Catat **Folder ID** dari URL:
   ```
   https://drive.google.com/drive/folders/[FOLDER_ID_DISINI]/
   ```
3. Di Google Apps Script, ganti baris:
   ```javascript
   const FOLDER_ID = "GANTI_DENGAN_FOLDER_ID_ANDA";
   ```

### Langkah 4: Test Code

1. Klik tombol **▶️ Run** di Google Apps Script
2. Akan muncul popup **Authorization required**
3. Klik **Review permissions**
4. Pilih akun Google Anda
5. Klik **Allow** untuk memberikan akses

---

## <a name="deploy-gas"></a>🚀 Deploy Google Apps Script

### Langkah 1: Deploy sebagai Web App

1. Di Google Apps Script, klik **Deploy** (tombol biru di atas)
2. Pilih **New deployment**
3. Klik icon **⚙️** dan pilih **Web app**
4. Atur konfigurasi:
   - **Project version**: Latest
   - **Execute as**: [Email akun Anda]
   - **Who has access**: Anyone
5. Klik **Deploy**
6. **PENTING**: Copy URL deployment yang diberikan

### Langkah 2: Update URL di JavaScript

1. Buka file `upload.js`
2. Cari baris:
   ```javascript
   const GAS_WEB_APP_URL = "https://script.google.com/macros/d/{DEPLOYMENT_ID}/userweb";
   ```
3. Ganti dengan URL deployment Anda:
   ```javascript
   const GAS_WEB_APP_URL = "https://script.google.com/macros/d/1aO-Xn9k2L_7M_5P2N0Q9R8S7T6U5V4W3X2Y1Z/userweb";
   ```

---

## <a name="konfigurasi"></a>⚙️ Konfigurasi Website

### Edit Kategori Dokumen

Jika ingin menambah atau mengubah kategori, edit di 2 tempat:

**1. Di upload.html (baris ~40)**
```html
<select id="category" name="category" required>
    <option value="">-- Pilih Kategori --</option>
    <option value="Senat">Dokumen Senat</option>
    <option value="Akademik Fakultas">Dokumen Akademik Fakultas</option>
    <!-- Tambah kategori di sini -->
</select>
```

**2. Di upload.html (baris ~105)**
```html
<select id="categoryFilter" class="filter-select">
    <option value="">Semua Kategori</option>
    <option value="Senat">Dokumen Senat</option>
    <option value="Akademik Fakultas">Dokumen Akademik Fakultas</option>
    <!-- Sama dengan di atas -->
</select>
```

### Edit Link ke Google Drive

Skrip default mengupload semua file ke satu folder. Jika Anda ingin
memecah dokumen ke dalam subfolder berbeda berdasarkan kategori, silakan
sesuaikan `CATEGORY_FOLDERS` di `GOOGLE_APPS_SCRIPT.md`.

Contoh konfigurasi di dalam file (telah ditambahkan otomatis):

```javascript
const FOLDER_ID = "1JjG9tN2qJ3L6slYNpwjO8wby21FldLB9"; // folder default

const CATEGORY_FOLDERS = {
  "Senat": "1neje7RkRDlB42OmgToLdsWeJNfz-piYD",
  "Akademik Fakultas": "1YbYq8puZZnO74o3qhwtcysoWbGjegJ66",
  // ... dst. sesuaikan dengan kebutuhan ...
};
```

Struktur ini memastikan file yang diunggah dengan kategori tertentu akan
masuk ke folder Drive yang spesifik; apabila kategori tidak dikenali, file
akan tetap masuk ke `FOLDER_ID` default.

Untuk menambahkan kategori baru, cukup:

1. Perbarui opsi `<select id="category">` di `upload.html` (nilai dan teks).
2. Tambahkan pasangan `"Nama Kategori": "ID_FOLDER_GOOGLE"` ke objek
   `CATEGORY_FOLDERS` di script GAS.



---

## <a name="github-pages"></a>📤 Upload ke GitHub Pages

### Langkah 1: Buat Repository GitHub

1. Buka [GitHub.com](https://github.com/)
2. Klik **New repository**
3. Nama: `pusatdokumen` (atau sesuai preferensi)
4. Pilih **Public**
5. Klik **Create repository**

### Langkah 2: Upload File

```bash
cd c:\xampp\htdocs\pusatdokumen

# Inisialisasi git
git init
git add .
git commit -m "Initial commit: sistem upload dokumen"
git branch -M main
git remote add origin https://github.com/[USERNAME]/pusatdokumen.git
git push -u origin main
```

### Langkah 3: Aktifkan GitHub Pages

1. Di repository GitHub, buka **Settings**
2. Scroll ke **GitHub Pages**
3. Pilih branch: **main**
4. Pilih folder: **/ (root)**
5. Klik **Save**
6. Website akan tersedia di: `https://[USERNAME].github.io/pusatdokumen`

---

## <a name="penggunaan"></a>💡 Penggunaan Sistem

### Fitur Upload

1. Buka halaman **Upload Dokumen**
2. Isi form:
   - **Nama Dokumen**: Nama deskriptif untuk dokumen
   - **Kategori**: Pilih kategori dokumen
   - **Deskripsi**: Penjelasan tambahan (opsional)
   - **File**: Pilih atau drag-drop file
3. Klik **Upload Dokumen**
4. File otomatis disimpan ke Google Drive

### Fitur Download

1. Scroll ke **Daftar Dokumen Terbaru**
2. Klik **⬇️ Download** untuk mengunduh dokumen
3. File otomatis diunduh dari Google Drive

### Fitur Hapus

1. Klik **🗑️ Hapus** untuk menghapus dokumen
2. Dokumen akan dihapus dari Google Drive

### Filter Dokumen

1. Gunakan dropdown **Kategori** untuk filter
2. Dokumen akan ditampilkan sesuai kategori pilihan

---

## <a name="troubleshooting"></a>🔧 Troubleshooting

### Error: "URL Google Apps Script belum benar"

**Solusi:**
1. Pastikan URL di `upload.js` sudah benar dan lengkap
2. Pastikan separator `?` dan parameter ada di URL
3. Contoh URL yang benar:
   ```
   https://script.google.com/macros/d/1aO-Xn9k2L_7M_5P2N0Q9R8S7T6U5V4W3X2Y1Z/userweb
   ```

### Error: "Google Apps Script belum di-deploy"

**Solusi:**
1. Buka Google Apps Script
2. Klik **Deploy** → **Manage deployments**
3. Pastikan ada 1 deployment aktif dengan type "Web app"
4. Jika tidak ada, buat deployment baru

### File tidak muncul di list

**Solusi:**
1. Refresh halaman
2. Pastikan folder ID di Google Apps Script benar
3. Cek di Google Drive apakah file ada
4. Buka console browser (F12) untuk melihat error detail

### File gagal upload

**Solusi:**
1. Pastikan file < 25MB
2. Format file harus: PDF, DOC, DOCX, XLS, XLSX
3. Cek kuota Google Drive Anda
4. Jika masih error, cek console browser untuk detail error

### "Who has access: Anyone" harus diatur di Google Apps Script

**Solusi:**
1. Buka Google Apps Script
2. Klik **Deploy** → **Manage deployments**
3. Edit deployment
4. Ubah "Who has access" menjadi "Anyone"
5. Simpan

---

## 📊 Spesifikasi Teknis

| Aspek | Detail |
|-------|--------|
| Ukuran Max File | 25 MB |
| Format File | PDF, DOC, DOCX, XLS, XLSX |
| Penyimpanan | Google Drive (unlimited) |
| Database | Google Sheets (auto-generated) |
| Bandwidth | Unlimited |
| Availability | 99.9% (Google Drive SLA) |
| Security | OAuth 2.0 (Google) |

---

## 🔒 Keamanan

1. **Google Apps Script** dilindungi dengan OAuth 2.0
2. **File di Google Drive** privat dan hanya bisa diakses melalui aplikasi
3. **URL Web App** hanya bisa mengakses file yang di-create oleh script
4. **CORS**: Web App Google mengizinkan akses dari website manapun

---

## 📅 Maintenance

### Backup Data

Google Drive otomatis backup file. Untuk backup metadata dokumen:

1. Buka Google Apps Script
2. Buka Sheet "Dokumen Metadata"
3. Download sebagai CSV/Excel

### Monitor Storage

1. Buka Google Drive
2. Klik tombol **Storage** di sidebar
3. Monitor penggunaan penyimpanan

### Update Kategori

Untuk menambah kategori baru:

1. Edit `upload.html` di kedua tempat (baris 40 dan 105)
2. Update di Google Apps Script jika diperlukan
3. Commit ke GitHub

---

## 🎓 Tutorial Video

*(Video tutorial akan ditambahkan)*

---

## 📞 Support

Untuk bantuan teknis atau pertanyaan:

1. Buka `/issues` di GitHub repository
2. Attach screenshot error
3. Copy-paste console error (F12)
4. Jelaskan langkah yang Anda lakukan

---

**Versi**: 1.0  
**Last Updated**: 19 Februari 2026  
**Status**: Production Ready
