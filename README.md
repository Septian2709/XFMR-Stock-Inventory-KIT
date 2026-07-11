
# ============================================
# 6. README.md - Documentation
# ============================================
readme_md = '''# 📦 InventarisKu - PWA Manajemen Inventaris

Aplikasi manajemen inventaris barang berbasis **Progressive Web App (PWA)** dengan sinkronisasi ke **Google Drive**.

## ✨ Fitur

| Fitur | Deskripsi |
|-------|-----------|
| 🔐 **Login Page** | Autentikasi user dengan session persisten |
| 📋 **Dashboard** | Daftar barang lengkap dengan pencarian real-time |
| 📜 **Riwayat Penggunaan** | Catatan transaksi masuk/keluar barang per user |
| ➕ **CRUD Barang** | Tambah, edit, hapus barang dengan detail lengkap |
| ☁️ **Google Drive Sync** | Sinkronisasi database ke Google Sheets |
| 📱 **PWA Ready** | Install ke homescreen, works offline |
| 🔔 **Stok Alert** | Indikator visual untuk stok rendai/habis |
| 📤 **Export JSON** | Backup data ke file JSON |

## 🚀 Cara Deploy

### 1. Hosting Statis (Gratis)

#### Vercel
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
cd inventaris-pwa
vercel --prod
```

#### Netlify
```bash
# Install Netlify CLI
npm i -g netlify-cli

# Deploy
cd inventaris-pwa
netlify deploy --prod --dir=.
```

#### GitHub Pages
1. Push folder `inventaris-pwa` ke repository GitHub
2. Settings > Pages > Source: Deploy from branch > Main > / (root)
3. Akses via `https://username.github.io/repo-name/`

### 2. Local Server
```bash
cd inventaris-pwa
# Python 3
python -m http.server 8080
# Node.js
npx serve .
# PHP
php -S localhost:8080
```

Buka `http://localhost:8080` di browser.

## 🔧 Setup Google Drive

### Langkah 1: Buat Google Spreadsheet
1. Buka [Google Sheets](https://sheets.google.com)
2. Buat spreadsheet baru
3. Rename sheet 1 jadi `Items`
4. Klik `+` di bawah, buat sheet 2 jadi `History`
5. **File > Share > Anyone with the link** → pilih **Viewer**

### Langkah 2: Dapatkan Spreadsheet ID
Dari URL: `https://docs.google.com/spreadsheets/d/`**`1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms`**`/edit`

Copy bagian tebal (ID) tersebut.

### Langkah 3: Buat API Key
1. Kunjungi [Google Cloud Console](https://console.cloud.google.com)
2. Buat project baru atau pilih existing
3. **APIs & Services > Library** → Cari "Google Sheets API" → **Enable**
4. **APIs & Services > Credentials** → **Create Credentials > API Key**
5. Copy API Key yang muncul

### Langkah 4: Masukkan ke Aplikasi
1. Buka aplikasi InventarisKu
2. Login dengan demo: `admin` / `admin123`
3. Pindah ke tab **Pengaturan**
4. Paste **Spreadsheet ID** dan **API Key**
5. Tap **Simpan Pengaturan**
6. Tap **🧪 Test Koneksi** untuk verifikasi
7. Jika berhasil, tap menu profil > **Sinkron ke Google Drive**

## 📱 Install sebagai Aplikasi

| Platform | Cara |
|----------|------|
| **Android (Chrome)** | Menu ⋮ → **Add to Home Screen** |
| **iOS (Safari)** | Share → **Add to Home Screen** |
| **Desktop Chrome** | Address bar kanan → **Install InventarisKu** |

## 📁 Struktur Folder

```
inventaris-pwa/
├── index.html          # Halaman utama aplikasi
├── app.js              # Logika aplikasi (state, CRUD, sync)
├── sw.js               # Service Worker (offline caching)
├── manifest.json       # Konfigurasi PWA
├── icons/
│   ├── icon-72x72.png
│   ├── icon-96x96.png
│   ├── icon-128x128.png
│   ├── icon-144x144.png
│   ├── icon-152x152.png
│   ├── icon-192x192.png
│   ├── icon-384x384.png
│   └── icon-512x512.png
└── README.md           # Dokumentasi ini
```

## 🗄️ Struktur Data

### LocalStorage Keys
| Key | Isi |
|-----|-----|
| `inv_items` | Array barang (nama, kategori, qty, satuan, minStock, lokasi) |
| `inv_history` | Array riwayat (barang, jenis, jumlah, catatan, waktu, user) |
| `inv_user` | Session user (username, name, role) |
| `inv_settings` | Konfigurasi Google Drive (sheetId, apiKey) |

### Google Sheets Format

**Sheet: Items**
| A | B | C | D | E | F | G | H |
|---|---|---|---|---|---|---|---|
| ID | Nama Barang | Kategori | Jumlah | Satuan | Min Stok | Lokasi | Terakhir Update |

**Sheet: History**
| A | B | C | D | E | F | G | H |
|---|---|---|---|---|---|---|---|
| ID | Item ID | Nama Barang | Jenis | Jumlah | Catatan | Tanggal | User |

## 🔒 Keamanan

- ⚠️ API Key disimpan di **localStorage** browser (tidak aman untuk produksi)
- 🔐 Untuk produksi, gunakan **backend server** untuk menyimpan credentials
- 🛡️ Pastikan spreadsheet Google Drive di-set ke **"Anyone with link - Viewer"**
- 🔑 Jangan bagikan file `inv_settings` dari localStorage ke publik

## 🛠️ Pengembangan Lebih Lanjut

### Fitur yang bisa ditambahkan:
- [ ] Multi-user dengan role-based access
- [ ] QR Code scanner untuk input barang
- [ ] Notifikasi push saat stok habis
- [ ] Grafik/statistik penggunaan barang
- [ ] Export ke Excel/PDF
- [ ] Dark mode
- [ ] Multi-language support

### Tech Stack:
- **Frontend**: Vanilla HTML5, CSS3, JavaScript (ES6+)
- **Storage**: localStorage + Google Sheets API v4
- **PWA**: Service Worker, Web App Manifest
- **Icons**: Generated with Pillow (Python)

## 📄 Lisensi

MIT License - Bebas digunakan untuk personal maupun komersial.

---

Dibuat dengan ❤️ untuk memudahkan manajemen inventaris Anda.
'''

with open(f"{output_dir}/README.md", "w", encoding="utf-8") as f:
    f.write(readme_md)

# ============================================
# 7. .gitignore
# ============================================
gitignore = '''# OS
.DS_Store
Thumbs.db

# Editor
.vscode/
.idea/
*.swp
*.swo

# Dependencies
node_modules/
package-lock.json
yarn.lock

# Build
*.log
dist/
build/

# Environment
.env
.env.local
'''

with open(f"{output_dir}/.gitignore", "w", encoding="utf-8") as f:
    f.write(gitignore)

# ============================================
# 8. List all files
# ============================================
import os

print("📁 Generated Files:")
print("=" * 50)
for root, dirs, files in os.walk(output_dir):
    level = root.replace(output_dir, '').count(os.sep)
    indent = '  ' * level
    folder = os.path.basename(root)
    if folder:
        print(f"{indent}📂 {folder}/")
    subindent = '  ' * (level + 1)
    for file in files:
        filepath = os.path.join(root, file)
        size = os.path.getsize(filepath)
        size_str = f"{size:,} bytes" if size < 1024 else f"{size/1024:.1f} KB"
        print(f"{subindent}📄 {file} ({size_str})")

print("\n" + "=" * 50)
print(f"✅ Total: {sum(len(f) for _, _, f in os.walk(output_dir))} files")
print(f"📍 Location: {output_dir}")
