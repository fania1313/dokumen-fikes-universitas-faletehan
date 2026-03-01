# 📚 AKADEMIK FAKULTAS ILMU KESEHATAN UNIVERSITAS FALETEHAN

Website dokumentasi akademik dan sistem manajemen dokumen untuk Fakultas Ilmu Kesehatan Universitas Faletehan.

---

## ✨ Fitur Utama

### 📖 Halaman Beranda
- Browse dokumen dari 7 kategori program
- Link langsung ke Google Drive folder
- Interface yang rapi dan user-friendly
- Responsive design (mobile & desktop)


### 📱 Responsive & Mobile-Friendly
- Optimal di semua ukuran layar
- Touch-friendly buttons
- Fast loading
- Accessible design

---


---

## 🛠️ Teknologi

| Layer | Teknologi | Keterangan |
|-------|-----------|-----------|
| Frontend | HTML5 | Struktur halaman |
| Styling | CSS3 | Responsive design |
| Interaktif | JavaScript | Upload, list, filter |
| Backend | Google Apps Script | Server-side logic |
| Storage | Google Drive | File storage |
| Database | Google Sheets | Metadata storage |
| Hosting | GitHub Pages | Static hosting |

---

## 📁 Struktur File

```
pusatdokumen/
│
├── 📄 HTML FILES
│   ├── index.html                 ← Halaman beranda
│
├── 🎨 CSS FILES
│   ├── style.css                  ← CSS beranda
<!-- upload-style.css removed -->
│
├── 🔧 JAVASCRIPT FILES
│   <!-- upload.js removed -->
│
├── 📚 DOCUMENTATION
│   ├── README.md                  ← File ini
│   │   (upload guide now obsolete)
│   ├── GOOGLE_APPS_SCRIPT.md      ← GAS code & docs
│   └── DEPLOYMENT_GUIDE.md        ← Setup & deployment
│
└── .git/                          ← Git repository
```

---

## 🚀 Quick Start


### Untuk Developer (Setup Local)

```bash
# Clone repository
git clone https://github.com/[USERNAME]/pusatdokumen.git

# Navigate to folder
cd pusatdokumen

# Open in browser (if using XAMPP)
# http://localhost/pusatdokumen

# Or use Python server
python -m http.server 8000
# Then open http://localhost:8000
```

### Untuk Admin (Setup System)

1. Baca file [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md)
2. Buat Google Apps Script project
3. Setup Google Drive folder
4. Deploy sebagai Web App
5. Update URL di `upload.js`

---

## 📖 Dokumentasi

### User Guide
Baca [UPLOAD_GUIDE.md](UPLOAD_GUIDE.md) untuk:
- Cara menggunakan sistem upload
- Troubleshooting
- FAQ
- Maintenance

### Technical Docs
Baca [GOOGLE_APPS_SCRIPT.md](GOOGLE_APPS_SCRIPT.md) untuk:
- Kode Google Apps Script lengkap
- API endpoints
- Database schema
- Security notes

### Setup & Deployment
Baca [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md) untuk:
- Step-by-step setup dari awal
- Google Apps Script deployment
- GitHub Pages configuration
- Testing procedures

---

## 🎓 Kategori Program

Website mencakup dokumentasi dari:

1. **Dokumen Senat Fakultas** (8 dokumen)
2. **Dokumen Akademik Fakultas** (6 sub-kategori)
3. **Program S2 Kesehatan Masyarakat** (9 dokumen)
4. **Program S1 Kesehatan Masyarakat** (9 dokumen)
5. **Program S1 Keperawatan & Profesi Ners** (9 dokumen)
6. **Program S1 Kebidanan & Pendidikan Profesi Bidan** (9 dokumen)
7. **Program D III Keperawatan** (9 dokumen)

---

## 💾 Fitur Upload Details

### Format File Diterima
- ✅ PDF (application/pdf)
- ✅ DOC (application/msword)
- ✅ DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document)
- ✅ XLS (application/vnd.ms-excel)
- ✅ XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet)

### Limit Ukuran
- Max: 25 MB per file
- Google Drive: Unlimited storage

### Metadata Tersimpan
- File ID (Google Drive)
- Nama dokumen
- Kategori
- Deskripsi
- Tanggal upload (otomatis)
- User yang upload (otomatis)
- File URL (Google Drive)
- Ukuran file (otomatis)

---

## 🔒 Keamanan

### Yang Dilindungi
- ✅ Google Drive auth via OAuth 2.0
- ✅ File hanya bisa diakses melalui Web App
- ✅ Metadata di Google Sheet yang protected
- ✅ No sensitive data di frontend

### Yang Tidak Exposed
- ❌ Google Drive credentials
- ❌ API keys
- ❌ Email addresses di frontend
- ❌ User credentials

---

## 📊 Statistics

| Item | Detail |
|------|--------|
| **Total Dokumen** | 59 initial + unlimited uploads |
| **Storage** | Unlimited (Google Drive) |
| **File Types** | 5 format |
| **Categories** | 7 program |
| **Max File Size** | 25 MB |
| **Uptime** | 99.9% (Google SLA) |
| **Response Time** | < 1 second |

---

## 🔄 Update Log

### Version 1.0 (19 Februari 2026)
- ✅ Halaman beranda dengan 59 dokumen
- ✅ Sistem upload dengan Google Drive integration
- ✅ Metadata storage di Google Sheets
- ✅ Responsive design mobile & desktop
- ✅ GitHub Pages hosting
- ✅ Full documentation

---

## 🆘 Troubleshooting

### Upload Fails
- Check browser console (F12)
- Check GAS execution logs
- Verify GAS_WEB_APP_URL di upload.js

### File Not Showing
- Refresh halaman
- Check metadata spreadsheet
- Check Google Drive folder

### Permission Error
- Verify "Who has access: Anyone" di GAS deployment
- Re-deploy GAS jika perlu

Untuk troubleshooting lengkap, baca [UPLOAD_GUIDE.md](UPLOAD_GUIDE.md#troubleshooting)

---

## 🌐 Live URL

Website sudah live di:
```
https://[USERNAME].github.io/pusatdokumen
```

Ganti `[USERNAME]` dengan username GitHub Anda.

---

## 📞 Support

### Issues & Bugs
- Create issue di repository GitHub

### Questions
- Check documentation files
- Create discussion di repository

### Contact
- Email: [Contact admin untuk setup]

---

## 🤝 Contributing

Ingin berkontribusi? 

1. Fork repository
2. Create feature branch
3. Commit changes
4. Push to branch
5. Create Pull Request

---

## 📄 License

© 2026 Universitas Faletehan. Semua hak dilindungi.

---

## 🎉 Terima Kasih!

Terimakasih telah menggunakan Sistem Manajemen Dokumen Universitas Faletehan.

**Happy uploading! 📤**

---

**Last Updated**: 19 Februari 2026  
**Version**: 1.0  
**Status**: Production Ready ✅

Dokumentasi lengkap tersedia di file-file berikut:
- [UPLOAD_GUIDE.md](UPLOAD_GUIDE.md) - Panduan penggunaan
- [GOOGLE_APPS_SCRIPT.md](GOOGLE_APPS_SCRIPT.md) - Technical docs
- [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md) - Setup guide

