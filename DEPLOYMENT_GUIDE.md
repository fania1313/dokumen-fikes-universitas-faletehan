# 🚀 PANDUAN DEPLOYMENT & SETUP LENGKAP

Dokumentasi step-by-step untuk setup sistem upload dokumen dari awal sampai live.

---

## 📋 Checklist Deployment

- [ ] Create Google Apps Script project
- [ ] Setup Google Drive folder
- [ ] Copy & configure GAS code
- [ ] Test GAS script
- [ ] Deploy GAS as Web App
- [ ] Get deployment URL
- [ ] Update upload.js with URL
- [ ] Test upload functionality
- [ ] Create GitHub repository
- [ ] Push files to GitHub
- [ ] Enable GitHub Pages
- [ ] Test live website

---

## 🎯 STEP 1: Setup Google Apps Script

### Step 1.1: Buat Project Baru

1. Buka [https://script.google.com/](https://script.google.com/)
2. Klik **+ New project** (atau **Projek Baru** jika bahasa Indonesia)
3. Rename project:
   - Klik nama project di atas
   - Ganti menjadi: "Upload Dokumen Universitas"
   - Tekan Enter

### Step 1.2: Setup Google Drive Folder

1. Buka [Google Drive](https://drive.google.com/)
2. **New** → **Folder**
3. Beri nama: "Dokumen Universitas Upload"
4. Klik kanan folder → **Share**
5. Ubah sharing ke "Anyone with the link"
6. Ambil **Folder ID** dari URL:
   ```
   https://drive.google.com/drive/folders/[COPY_BAGIAN_INI]/usp=sharing
   ```

### Step 1.3: Copy Code ke Google Apps Script

1. Buka file [GOOGLE_APPS_SCRIPT.md](GOOGLE_APPS_SCRIPT.md)
2. Copy seluruh kode dari section **Google Apps Script Code**
3. Di Google Apps Script editor, paste ke file `Code.gs`
4. **Ganti baris pertama:**
   ```javascript
   const FOLDER_ID = "GANTI_DENGAN_FOLDER_ID_ANDA";
   ```
   Dengan folder ID yang sudah dicatat:
   ```javascript
   const FOLDER_ID = "1JjG9tN2qJ3L6slYNpwjO8wby21FldLB9";
   ```

### Step 1.4: Test Script

1. Di Google Apps Script, cari function `testUpload()`
2. Pilih function dari dropdown di toolbar
3. Klik **▶️ Run**
4. Approve permissions saat diminta
5. Lihat log di **Execution log** (harus success)

---

## 🔧 STEP 2: Deploy Google Apps Script

### Step 2.1: Deploy sebagai Web App

1. Di Google Apps Script, klik **Deploy** (tombol biru atas kanan)
2. Klik **New deployment** (atau **Deployment baru**)
3. Klik icon ⚙️ **Select type**
4. Pilih **Web app**
5. Atur pengaturan:
   ```
   Execute as:        [Email account Anda]
   Who has access:    Anyone
   ```
6. Klik **Deploy**
7. Dialog muncul dengan **Deployment ID**

### Step 2.2: Copy Deployment URL

1. Dari dialog deployment, copy URL yang ada
2. Format URL:
   ```
   https://script.google.com/macros/d/[DEPLOYMENT_ID]/userweb
   ```
3. **Simpan URL ini** - dibutuhkan untuk step berikutnya

### Step 2.3: Verify Authorization

Google akan meminta access:
1. Klik **Review permissions**
2. Pilih akun Google Anda
3. Klik **Allow** untuk berikan akses

---

## 💻 STEP 3: Update Website Code

### Step 3.1: Update upload.js

1. Buka file `upload.js` (di repository/server Anda)
2. Cari baris:
   ```javascript
   const GAS_WEB_APP_URL = "https://script.google.com/macros/d/{DEPLOYMENT_ID}/userweb";
   ```
3. Ganti dengan URL deployment Anda:
   ```javascript
   const GAS_WEB_APP_URL = "https://script.google.com/macros/d/1aO-Xn9k2L_7M_5P2N0Q9R8S7T6U5V4W3X2Y1Z/userweb";
   ```
4. **Save file**

### Step 3.2: Test Upload Locally

Jika pakai XAMPP/local server:

1. Copy semua file ke folder:
   ```
   c:\xampp\htdocs\pusatdokumen\
   ```

2. Buka browser: `http://localhost/pusatdokumen/upload.html`

3. Test upload:
   - Isi form
   - Upload file test (PDF/DOC)
   - Cek apakah file muncul di list
   - Cek di Google Drive apakah file tersimpan

---

## 📤 STEP 4: Upload ke GitHub

### Step 4.1: Setup GitHub

1. Buat akun [GitHub.com](https://github.com/) jika belum ada
2. Buat **New repository**
   - Repository name: `pusatdokumen`
   - Visibility: **Public**
   - Do not initialize with README
3. Klik **Create repository**

### Step 4.2: Push File ke GitHub

Buka Command Prompt/PowerShell, jalankan:

```bash
# Masuk ke folder
cd c:\xampp\htdocs\pusatdokumen

# Initialize git
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit: sistem upload dokumen universitas"

# Set main branch
git branch -M main

# Add remote repository
git remote add origin https://github.com/[USERNAME]/pusatdokumen.git

# Push ke GitHub
git push -u origin main
```

**Catatan:** Ganti `[USERNAME]` dengan username GitHub Anda

### Step 4.3: Verify di GitHub

1. Refresh halaman repository GitHub
2. Cek apakah semua file ada (index.html, upload.html, upload.js, style.css, upload-style.css)

---

## 🌐 STEP 5: Enable GitHub Pages

### Step 5.1: Configure GitHub Pages

1. Di repository, buka **Settings**
2. Klik **Pages** (sidebar kiri)
3. **Source**:
   - Branch: `main`
   - Folder: `/ (root)`
4. Klik **Save**

### Step 5.2: Get GitHub Pages URL

1. Tunggu ~1 menit untuk deployment
2. Baca pesan di halaman Pages
3. URL Anda: `https://[USERNAME].github.io/pusatdokumen`

---

## ✅ STEP 6: Testing

### Test Checklist

- [ ] Buka website: https://[USERNAME].github.io/pusatdokumen
- [ ] Navigasi ke Upload Dokumen
- [ ] Upload test file (PDF/DOC)
- [ ] File muncul di daftar dokumen
- [ ] Download file dari list
- [ ] Filter dokumen by kategori
- [ ] Test di mobile (responsive)
- [ ] Cek file di Google Drive

### Test Upload

```
✓ Upload PDF → Check hasil download
✓ Upload DOCX → Lihat di metadata spreadsheet
✓ Upload XLSX → Cek size dan tanggal
✓ Delete file → Verify di Google Drive & spreadsheet
```

---

## 📁 File Structure

```
pusatdokumen/
│
├── 📄 index.html                  ← Halaman beranda
├── 📄 upload.html                 ← Halaman upload (BARU)
│
├── 🎨 style.css                   ← CSS beranda
├── 🎨 upload-style.css            ← CSS upload (BARU)
│
├── 🔧 upload.js                   ← JavaScript upload (BARU)
│─ Contains: GAS_WEB_APP_URL configuration
│
├── 📚 README.md                   ← Dokumentasi beranda
├── 📚 UPLOAD_GUIDE.md             ← Panduan penggunaan (BARU)
├── 📚 GOOGLE_APPS_SCRIPT.md       ← Kode GAS (BARU)
├── 📚 DEPLOYMENT_GUIDE.md         ← File ini
│
└── .git/                          ← Git repository (auto)
    └── ...
```

---

## 🔐 Security Notes

### What's NOT Exposed

- ❌ Google Drive credentials
- ❌ Folder ID di frontend
- ❌ Email addresses
- ❌ Private file URLs

### What's Protected

- ✅ Google Apps Script handles auth
- ✅ Drive API secured with OAuth 2.0
- ✅ File access via Web App only
- ✅ Metadata in protected Google Sheet

---

## 🛠️ Troubleshooting

### Problem: "Cannot read property 'postData' of undefined"

**Solution:** 
- Pastikan GAS endpoint sudah di-deploy
- Check URL di upload.js benar

### Problem: "Error: Missing FOLDER_ID"

**Solution:**
- Edit Google Apps Script
- Ganti `const FOLDER_ID` dengan ID folder Anda

### Problem: "File upload 500 error"

**Solution:**
- Check GAS quota (Script quotas → Dashboard)
- Wait for GAS service recovery
- Retry upload

### Problem: GitHub Pages not updating

**Solution:**
```bash
# Delete .git folder dan re-setup
rm -r .git
git init
git add .
git commit -m "Reinitialize repository"
git branch -M main
git remote add origin https://github.com/USERNAME/pusatdokumen.git
git push -u origin main
```

---

## 📊 Monitoring Dashboard

Monitor sistem dengan:

1. **Google Drive** - Check files uploaded: 
   - Folder Dokumen Universitas Upload

2. **Google Sheets** - Check metadata:
   - Open Spreadsheet by extension in GAS
   - Sheet "Dokumen Metadata"

3. **GitHub** - Check code updates:
   - Repository commits

4. **Google Apps Script** - Check logs:
   - Executions tab → View logs

---

## 🔄 Update Procedures

### Update Website Code

1. Edit file lokal
2. Test di localhost
3. Push ke GitHub:
   ```bash
   git add .
   git commit -m "Update: deskripsi perubahan"
   git push origin main
   ```
4. GitHub Pages otomatis update (~1 menit)

### Update Google Apps Script

1. Edit code di Google Apps Script editor
2. Deploy → Manage deployments
3. Edit existing deployment
4. Klik Deploy atau buat new version

---

## 🎓 Learning Resources

- [Google Apps Script Documentation](https://developers.google.com/apps-script)
- [Google Drive API](https://developers.google.com/drive/api)
- [GitHub Pages Guide](https://pages.github.com/)
- [Fetch API MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

---

## 📞 Support & Issues

### Common Issues

1. **Upload fails silently**
   - Check browser console (F12)
   - Check GAS execution logs

2. **File not showing in list**
   - Refresh page
   - Check metadata spreadsheet
   - Check Google Drive folder

3. **URL not working**
   - Verify deployment URL benar
   - Check "Who has access" = Anyone
   - Redeploy jika perlu

### Getting Help

1. Check error message di browser console (F12)
2. Check GAS logs di Google Apps Script
3. Open GitHub Issues dengan:
   - Screenshots error
   - Console output
   - Step-by-step reproduction

---

## ✨ Next Steps

1. ✅ Deploy sistem
2. ✅ Test functionality
3. Create user account system (optional)
4. Add file preview (optional)
5. Create admin panel (optional)
6. Add more document types (optional)

---

**Last Updated:** 19 Februari 2026  
**Version:** 1.0  
**Status:** Production Ready

Selamat! Sistem Anda sudah live! 🎉
