# ⚡ QUICK START - Setup Sistem dalam 15 Menit

Panduan cepat setup sistem upload dokumen tanpa detail teknis.

---

## 🎯 3 Langkah Utama

### ✅ LANGKAH 1: Setup Google (5 Menit)

**1.1 Buat folder di Google Drive**
- Buka Google Drive
- Klik **New** → **Folder** 
- Nama folder: "Dokumen Upload Universitas"
- Klik folder → Copy ID dari URL

**1.2 Buat Google Apps Script**
- Buka [script.google.com](https://script.google.com/)
- Klik **New project**
- Rename ke: "Upload Dokumen Universitas"

**1.3 Paste code**
- Buka file [GOOGLE_APPS_SCRIPT.md](GOOGLE_APPS_SCRIPT.md)
- Copy seluruh kode
- Di Google Apps Script, paste ke `Code.gs`
- **Ganti** baris pertama:
  ```javascript
  const FOLDER_ID = "COPY_ID_FOLDER_ANDA_DISINI";
  ```

**1.4 Test**
- Klik **▶️ Run** 
- Approve permissions
- Klik ✅ jika sukses

---

### ✅ LANGKAH 2: Deploy Google Apps Script (5 Menit)

**2.1 Deploy**
- Klik **Deploy** (tombol biru atas)
- Pilih **New deployment**
- Pilih icon ⚙️ → **Web app**
- Klik **Deploy**

**2.2 Copy URL**
- URL muncul di dialog
- Copy seluruh URL
- Contoh: `https://script.google.com/macros/d/1aO-Xn9k2L_7M_5P2N0Q9R8S7T6U5V4W3X/userweb`

---

### ✅ LANGKAH 3: Update Website (5 Menit)

**3.1 Update file upload.js**
- Buka file `upload.js`
- Cari baris:
  ```javascript
  const GAS_WEB_APP_URL = "https://script.google.com/...";
  ```
- Ganti dengan URL dari LANGKAH 2.2

**3.2 Upload ke GitHub**
```bash
cd c:\xampp\htdocs\pusatdokumen

git add .
git commit -m "Add deployment URL"
git push origin main
```

**3.3 Selesai!**
- Website live dalam ~1 menit
- Buka: `https://[USERNAME].github.io/pusatdokumen/upload.html`
- Test upload dokumen 🎉

---

## 🧪 Quick Test

1. Buka https://[USERNAME].github.io/pusatdokumen/
2. Klik **📤 Upload Dokumen**
3. Isi form (nama, kategori, file)
4. Klik **Upload Dokumen**
5. File muncul di list dalam 5 detik
6. Download file dari list
7. Cek file di Google Drive folder

---

## ❌ Jika Ada Error

| Error | Solusi |
|-------|--------|
| "Cannot upload" | Copy URL deployment dengan benar |
| "File not showing" | Refresh page atau cek Google Drive |
| "Permission denied" | Deploy ulang dengan "Who has access: Anyone" |
| "404 Not Found" | Tunggu 1 menit dan refresh |

---

## 📁 File yang Perlu Diubah

| File | Edit Bagian | Contoh |
|------|------------|--------|
| `GOOGLE_APPS_SCRIPT.md` | Baris pertama `FOLDER_ID` | Ganti dengan ID folder Anda |
| `upload.js` | `GAS_WEB_APP_URL` | Ganti dengan URL deployment |

**Itu saja! 🎊**

---

## 🚀 Deploy ke GitHub

Jika belum upload ke GitHub:

```bash
cd c:\xampp\htdocs\pusatdokumen

git init
git add .
git commit -m "Initial: sistem upload dokumen"
git branch -M main
git remote add origin https://github.com/[USERNAME]/pusatdokumen.git
git push -u origin main
```

Habis itu, aktifkan GitHub Pages di Settings → Pages

---

## 📞 Bantuan

- **Upload gagal?** → Cek console (F12) → bagian Networks
- **File tidak muncul?** → Refresh → Cek Google Drive
- **URL tidak jalan?** → Cek URL sudah benar dan "Anyone" access aktif

---

**Selesai! Sistem sudah siap pakai! 🎉**

Untuk dokumentasi lengkap, baca:
- [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md) - Detail setup
- [GOOGLE_APPS_SCRIPT.md](GOOGLE_APPS_SCRIPT.md) - Kode & penjelasan
- [UPLOAD_GUIDE.md](UPLOAD_GUIDE.md) - User guide
