# KiosKoe 🏪
**Aplikasi Manajemen Keuangan UMKM Kios**

> Skripsi S1 — Universitas Nusa Cendana, NTT, Indonesia  
> Penulis: Priskila Doko  
> Target Pengguna: Pemilik Kios Kecil di Kelurahan Fatukoa, Kupang, NTT

---

## 📱 Tentang Aplikasi

**KiosKoe** adalah aplikasi Android untuk membantu pemilik kios kecil mencatat dan memantau keuangan usaha mereka secara **offline penuh** tanpa memerlukan koneksi internet. Dirancang khusus untuk pengguna non-teknis di daerah dengan keterbatasan infrastruktur digital.

### Fitur Utama
- ✅ Catat pemasukan dan pengeluaran harian
- ✅ Ringkasan saldo otomatis
- ✅ Laporan harian dan bulanan
- ✅ Format mata uang Rupiah
- ✅ Bekerja 100% offline (SQLite lokal)
- ✅ Konfirmasi sebelum hapus data
- ✅ Desain motif Tenun Ikat NTT

---

## 🛠️ Cara Setup di Android Studio

### Prasyarat
- **Android Studio** Hedgehog (2023.1.1) atau lebih baru
- **JDK 8** atau lebih baru
- **Git** (opsional, untuk clone)

### Langkah Instalasi

1. **Buka Android Studio**
   ```
   Buka Android Studio → File → Open
   ```

2. **Pilih folder proyek**
   ```
   Navigasi ke folder KiosKoe/ → Klik OK
   ```

3. **Sync Gradle**
   - Tunggu Android Studio mendownload dependencies (butuh internet pertama kali)
   - Jika muncul dialog "Sync Now" → klik

4. **Run Aplikasi**
   - Colok HP Android lewat kabel USB (aktifkan USB Debugging di HP)
   - Atau gunakan Android Emulator (AVD Manager → buat device baru)
   - Klik tombol ▶️ Run (Shift+F10)

### Persyaratan Perangkat
- Android 5.0 (Lollipop) ke atas
- RAM minimal 1GB
- Storage minimal 50MB

---

## 🔐 Kredensial Default

| Field | Nilai |
|-------|-------|
| Username | `admin` |
| Password | `admin123` |
| Nama Toko | `Kios Saya` |
| Nama Pemilik | `Priskila Doko` |

> **Catatan:** Kredensial bisa diubah di halaman **Profil Toko** setelah login.

---

## 📂 Struktur Proyek

```
KiosKoe/
├── app/
│   ├── src/main/
│   │   ├── java/com/kioskoe/
│   │   │   ├── activities/          # Semua halaman (Activity)
│   │   │   │   ├── SplashActivity.java      # Layar pembuka (2 detik)
│   │   │   │   ├── LoginActivity.java       # Login dengan username+password
│   │   │   │   ├── DashboardActivity.java   # Layar utama & ringkasan
│   │   │   │   ├── TambahTransaksiActivity.java  # Form tambah transaksi
│   │   │   │   ├── LaporanActivity.java     # Laporan harian/bulanan
│   │   │   │   └── ProfilTokoActivity.java  # Edit profil toko
│   │   │   ├── database/
│   │   │   │   └── DatabaseHelper.java      # Pengelola SQLite (CRUD)
│   │   │   ├── model/
│   │   │   │   ├── User.java                # Model data pengguna
│   │   │   │   └── Transaksi.java           # Model data transaksi
│   │   │   └── adapter/
│   │   │       └── TransaksiAdapter.java    # Adapter untuk RecyclerView
│   │   └── res/
│   │       ├── layout/              # File XML tampilan
│   │       ├── drawable/            # Gambar, ikon, motif tenun XML
│   │       ├── values/              # Warna, teks, tema, dimensi
│   │       └── menu/                # Menu overflow toolbar
│   └── build.gradle                 # Konfigurasi modul app
├── build.gradle                     # Konfigurasi project
├── settings.gradle                  # Pengaturan nama proyek
└── README.md                        # File ini
```

---

## 🗄️ Struktur Database

Database SQLite tersimpan di internal storage perangkat (`/data/data/com.kioskoe/databases/kioskoe.db`).

### Tabel `users`
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INTEGER PK | ID otomatis |
| username | TEXT UNIQUE | Nama pengguna unik |
| password | TEXT | Password login |
| nama_toko | TEXT | Nama kios |
| nama_pemilik | TEXT | Nama pemilik kios |

### Tabel `transaksi`
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | INTEGER PK | ID otomatis |
| tipe | TEXT | "pemasukan" atau "pengeluaran" |
| nominal | REAL | Jumlah uang (Rupiah) |
| keterangan | TEXT | Catatan transaksi |
| tanggal | TEXT | Format: "yyyy-MM-dd" |
| created_at | TEXT | Waktu input (otomatis) |

---

## 🎨 Desain Visual

### Palet Warna
| Nama | Kode Hex | Fungsi |
|------|----------|--------|
| Primary Blue | `#1565C0` | Toolbar, tombol utama |
| Accent Orange | `#FF8F00` | FAB, aksen |
| Green Income | `#2E7D32` | Pemasukan |
| Red Expense | `#C62828` | Pengeluaran |
| Tenun Gold | `#F9A825` | Motif tenun dekoratif |

### Motif Tenun Ikat NTT
Motif tenun diimplementasikan sebagai **XML Vector Drawable** murni, terinspirasi dari:
- Motif geometris belah ketupat (diamond) khas tenun Timor
- Warna tradisional: biru-emas-merah khas kain NTT
- Digunakan sebagai: header toolbar, border splash screen, divider halaman

---

## 📚 Teknologi yang Digunakan

| Teknologi | Versi | Fungsi |
|-----------|-------|--------|
| Java | 8 | Bahasa pemrograman utama |
| Android SDK | Min 21, Target 34 | Platform Android |
| SQLite | Bawaan Android | Database lokal offline |
| Material Design Components | 1.11.0 | Library UI modern |
| AndroidX AppCompat | 1.6.1 | Kompatibilitas backward |
| RecyclerView | 1.3.2 | Daftar transaksi |
| CardView | 1.0.0 | Kartu ringkasan keuangan |

---

## 🐛 Troubleshooting

### Build Error: "Minimum SDK version"
Pastikan file `app/build.gradle` memiliki:
```gradle
minSdk 21
compileSdk 34
```

### Database tidak bisa dibuka
- Uninstall aplikasi dari HP
- Install ulang → database akan dibuat ulang dengan data default

### Gradle sync gagal
```
File → Invalidate Caches / Restart → Invalidate and Restart
```

---

## 📞 Informasi Pengembang

- **Nama:** Priskila Doko
- **Institusi:** Universitas Nusa Cendana, Kupang, NTT
- **Program:** Skripsi S1 Informatika
- **Tahun:** 2024

---

*KiosKoe dikembangkan sebagai bagian dari penelitian skripsi untuk membantu digitalisasi UMKM di Kelurahan Fatukoa, Kupang, Nusa Tenggara Timur.*
