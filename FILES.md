# 📋 PROJECT FILES - Penjelasan Setiap File

Dokumentasi lengkap semua file yang ada di project.

---

## 📁 Struktur Final Project

```
pusatdokumen/
├── 📄 HTML FILES
│   ├── index.html                    ← Halaman beranda (59 dokumen existing)
│   └── upload.html                   ← Halaman upload dokumen (BARU)
│
├── 🎨 CSS FILES
│   ├── style.css                     ← CSS beranda
│   └── upload-style.css              ← CSS upload page (BARU)
│
├── 🔧 JAVASCRIPT FILES
│   └── upload.js                     ← Upload functionality (BARU)
│
├── 📚 DOCUMENTATION
│   ├── README.md                     ← Overview project ← BACA INI DULU
│   ├── QUICK_START.md                ← Setup cepat 15 menit ← UNTUK ADMIN
│   ├── UPLOAD_GUIDE.md               ← User guide lengkap
│   ├── GOOGLE_APPS_SCRIPT.md         ← Code & technical docs
│   ├── DEPLOYMENT_GUIDE.md           ← Setup step-by-step
│   └── FILES.md                      ← File ini (penjelasan setiap file)
│
└── .git/                             ← Git repository (auto-generated)
```

---

## 🎯 HTML Files

### index.html
**Deskripsi:** Halaman utama/beranda website

**Isi:**
- Header dengan judul universitas
- Link ke halaman upload dokumen
- 7 section dengan kategori dokumen:
  - Dokumen Senat (8 items)
  - Dokumen Akademik Fakultas (6 items + dropdown pedoman)
  - S2 Kesehatan Masyarakat (9 items)
  - S1 Kesehatan Masyarakat (9 items)
  - S1 Keperawatan & Profesi Ners (9 items)
  - S1 Kebidanan & Pendidikan Profesi Bidan (9 items)
  - D III Keperawatan (9 items)
- Footer dengan copyright

**Fitur:**
- Responsive grid layout
- Link langsung ke Google Drive
- Dropdown untuk pedoman 11 jenis
- Meta tags untuk SEO

**Edit jika ingin:**
- Menambah dokumen baru
- Mengubah judul section
- Mengubah kategori

---

### upload.html (BARU ✨)
**Deskripsi:** Halaman untuk upload dan manage dokumen

**Isi:**
1. **Upload Form**
   - Input nama dokumen
   - Dropdown kategori (7 pilihan)
   - Textarea deskripsi
   - File input dengan drag & drop support
   - Submit button

2. **Upload Status**
   - Pesan success/error
   - File info (nama, ukuran)

3. **Documents List**
   - Filter by kategori
   - List dokumen yang sudah diupload
   - Download & Delete button untuk setiap dokumen
   - Metadata (nama, kategori, tanggal, ukuran)

**Fitur:**
- Drag & drop support
- Real-time file info display
- Category filter
- Responsive design
- Loading states
- Error handling

**Edit jika ingin:**
- Menambah kategori baru
- Mengubah max file size
- Mengubah accepted file types

---

## 🎨 CSS Files

### style.css
**Deskripsi:** Styling untuk halaman beranda (index.html)

**Bagian Utama:**
- Global styles (*, html, body)
- Header styling (gradient background)
- Navigation styles
- Section & card styling
- Grid layout responsive
- Button & link styles
- Footer styling
- Responsive breakpoints (1024px, 768px, 480px)
- Accessibility features
- Print styles

**Warna Tema:**
- Primary: #1e3c72 (Biru Tua)
- Secondary: #2a5298 (Biru)
- Background: #f8f9fa (Abu-abu Terang)
- Text: #333 (Abu-abu Gelap)

**Edit jika ingin:**
- Mengubah warna tema
- Mengubah font
- Mengubah spacing
- Menambah animasi

---

### upload-style.css (BARU ✨)
**Deskripsi:** Styling untuk halaman upload (upload.html)

**Bagian Utama:**
- Global styles
- Header & navigation styling
- Upload form styling
- File upload area (drag & drop)
- Form inputs & labels
- Buttons (primary, small, download, delete)
- Document item cards
- Status messages
- Filter dropdown
- Responsive design
- Mobile-friendly styles

**Fitur Khusus:**
- Drag & drop visual feedback
- Form validation styling
- Loading states
- Success/error message colors
- Touch-friendly buttons (min 44-48px)
- Print styles

**Edit jika ingin:**
- Mengubah upload form layout
- Mengubah document card design
- Mengubah button colors
- Menambah animations

---

## 🔧 JavaScript Files

### upload.js (BARU ✨)
**Deskripsi:** Frontend logic untuk upload dan manage dokumen

**Fungsi Utama:**

| Fungsi | Deskripsi |
|--------|-----------|
| `handleUpload()` | Upload file ke Google Apps Script |
| `loadDocuments()` | Fetch dokumen dari GAS |
| `deleteDocument(fileId)` | Hapus dokumen |
| `fileToBase64(file)` | Convert file to base64 |
| `updateFileInfo()` | Update display file info |
| `escapeHtml(text)` | Escape HTML special chars |

**Fitur:**
- Drag & drop support
- Form validation
- File size check (max 25MB)
- File type validation
- Base64 encoding
- Fetch API untuk komunikasi dengan GAS
- Error handling
- Loading states
- Auto-refresh dokumen list

**Config yang Perlu Diubah:**
```javascript
// Baris awal file
const GAS_WEB_APP_URL = "https://script.google.com/macros/d/{DEPLOYMENT_ID}/userweb";
```

**Edit jika ingin:**
- Menambah validasi
- Mengubah error messages
- Menambah fitur (edit, share, dll)
- Mengubah polling interval

---

## 📚 Documentation Files

### README.md
**Tujuan:** Overview project dan quick reference

**Isi:**
- Project description
- Fitur utama
- Teknologi yang digunakan
- Struktur file
- Quick start instructions
- Kategori dokumen
- Troubleshooting
- Statistics
- Links ke dokumentasi lain

**Baca untuk:** Understand project secara umum

---

### QUICK_START.md (BARU ✨)
**Tujuan:** Setup sistem dalam 15 menit (untuk admin)

**Isi:**
- 3 langkah utama
- Setup Google (folder, Apps Script, paste code)
- Deploy GAS
- Update website
- Quick test
- Error solutions
- Deploy ke GitHub

**Baca untuk:** Admin yang ingin setup sistem dengan cepat

---

### UPLOAD_GUIDE.md (BARU ✨)
**Tujuan:** Panduan penggunaan sistem untuk end-user

**Isi:**
- Table of contents
- Teknologi yang digunakan
- Struktur file
- Setup Google Apps Script (detail)
- Deploy GAS (detail)
- Konfigurasi website
- Upload ke GitHub Pages (detail)
- Penggunaan sistem (upload, download, filter, hapus)
- Troubleshooting lengkap
- Spesifikasi teknis
- Security notes
- Maintenance procedures

**Baca untuk:** User guide lengkap, admin reference

---

### GOOGLE_APPS_SCRIPT.md (BARU ✨)
**Tujuan:** Kode Google Apps Script dan dokumentasi teknis

**Isi:**
- Instruksi sebelum copy code
- Seluruh kode Google Apps Script (copy-paste ready)
- Penjelasan kode
- Main functions
- API endpoints
- Flow diagram
- Konfigurasi
- Testing
- Database schema
- Permissions required
- Scalability info

**Baca untuk:** Developer, technical reference, understanding GAS code

---

### DEPLOYMENT_GUIDE.md (BARU ✨)
**Tujuan:** Panduan deployment step-by-step dari awal

**Isi:**
- Deployment checklist
- STEP 1: Setup Google Apps Script
- STEP 2: Deploy GAS sebagai Web App
- STEP 3: Update website code
- STEP 4: Upload ke GitHub
- STEP 5: Enable GitHub Pages
- STEP 6: Testing
- File structure
- Security notes
- Troubleshooting
- Monitoring dashboard
- Update procedures
- Next steps

**Baca untuk:** First-time setup, admin yang deploy dari scratch

---

### FILES.md
**Tujuan:** Penjelasan setiap file di project (file ini)

**Isi:**
- Struktur project
- Penjelasan HTML files
- Penjelasan CSS files
- Penjelasan JavaScript files
- Penjelasan Documentation files
- Map of documentation
- Best practices
- Who should read what

**Baca untuk:** Understand project structure, know which file to edit

---

## 🗺️ Documentation Map

Untuk **Admin Setup Sistem:**
1. ➡️ [QUICK_START.md](QUICK_START.md) - Setup dalam 15 menit
2. ➡️ [GOOGLE_APPS_SCRIPT.md](GOOGLE_APPS_SCRIPT.md) - Copy code
3. ➡️ [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md) - Jika ada trouble

Untuk **End-User:**
1. ➡️ [UPLOAD_GUIDE.md](UPLOAD_GUIDE.md) - Bagaimana pakai sistem
2. ➡️ [README.md](README.md) - Overview features

Untuk **Developer:**
1. ➡️ [README.md](README.md) - Project overview
2. ➡️ [FILES.md](FILES.md) - File structure (file ini)
3. ➡️ [GOOGLE_APPS_SCRIPT.md](GOOGLE_APPS_SCRIPT.md) - Technical details
4. ➡️ [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md) - Setup details
5. ➡️ [UPLOAD_GUIDE.md](UPLOAD_GUIDE.md) - Full reference

---

## 💡 Quick Edit Guide

### Ingin menambah kategori dokumen?

Edit di **3 tempat:**

1. **upload.html** (baris ~40):
```html
<select id="category">
    ...
    <option value="NewCategory">Nama Kategori Baru</option>
</select>
```

2. **upload.html** (baris ~105):
```html
<select id="categoryFilter">
    ...
    <option value="NewCategory">Nama Kategori Baru</option>
</select>
```

3. **index.html** (jika perlu ditambah di bereanda):
```html
<h3 class="program-title">Kategori Baru</h3>
<div class="category-grid">
    ...
</div>
```

### Ingin mengubah Google Apps Script URL?

Edit **upload.js** baris pertama:
```javascript
const GAS_WEB_APP_URL = "URL_DARI_DEPLOYMENT_ANDA";
```

### Ingin mengubah warna tema?

Edit **style.css** atau **upload-style.css**:
```css
/* Primary color */
#1e3c72 → ubah ke warna baru
/* Secondary color */
#2a5298 → ubah ke warna baru
```

---

## ✅ Quality Checklist

- ✅ HTML semantic dan valid
- ✅ CSS responsive (desktop, tablet, mobile)
- ✅ JavaScript error handling
- ✅ Google Apps Script secure
- ✅ Documentation lengkap
- ✅ Code comments
- ✅ Performance optimized
- ✅ Accessibility features
- ✅ SEO friendly
- ✅ Print friendly

---

## 📊 File Statistics

| File | Type | Lines | Size | Purpose |
|------|------|-------|------|---------|
| index.html | HTML | ~350 | ~14KB | Beranda |
| upload.html | HTML | ~130 | ~6KB | Upload page |
| style.css | CSS | ~300 | ~10KB | Beranda styling |
| upload-style.css | CSS | ~400 | ~14KB | Upload styling |
| upload.js | JS | ~300 | ~10KB | Upload logic |
| README.md | Markdown | ~150 | ~6KB | Overview |
| QUICK_START.md | Markdown | ~100 | ~4KB | Setup cepat |
| UPLOAD_GUIDE.md | Markdown | ~300 | ~12KB | User guide |
| GOOGLE_APPS_SCRIPT.md | Markdown | ~200 | ~8KB | GAS code |
| DEPLOYMENT_GUIDE.md | Markdown | ~400 | ~16KB | Deployment |
| FILES.md | Markdown | ~300 | ~12KB | File info |

**Total:** ~3MB (dengan dokumentasi)

---

## 🚀 Next Steps

1. ✅ Pahami struktur file ini
2. ✅ Baca QUICK_START.md untuk setup
3. ✅ Setup Google Apps Script
4. ✅ Deploy ke GitHub
5. ✅ Test sistem
6. ✅ Share dengan users

---

**Last Updated:** 19 Februari 2026  
**Version:** 1.0  
**Maintenance:** Ongoing

Selamat! Anda sudah paham struktur project! 🎉
