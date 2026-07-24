# 🌾 KKL Kuala Secapah 1 — Dashboard Kegiatan & Keuangan

Website satu-halaman (single-file) untuk KKL Kuala Secapah 1 (IAIN Pontianak). Data tersimpan di **Firebase Firestore** secara realtime — jadi semua anggota yang buka link akan melihat data yang sama dan selalu update.

- **Mode Anggota** (tanpa login): semua orang yang buka link bisa **melihat** data saja — semua tombol tambah/ubah/hapus tersembunyi, dan setiap field pengaturan otomatis terkunci (disabled). Bahkan jika seseorang mencoba mengakalinya lewat inspect element, penyimpanan tetap ditolak oleh **Firestore Security Rules** di server, bukan cuma disembunyikan di tampilan — jadi benar-benar aman.
- **Mode Bendahara** (login email/password): bisa **tambah/ubah/hapus** data anggota, transaksi, dan proker.
- **Logo dibangun 100% dari kode** (SVG langsung di dalam `index.html`, bukan file gambar) — lengkap dengan efek bevel, emboss, gradasi, dan lapisan gem 3D bertekstur facet. Ditampilkan versi kecil di sidebar, versi animasi 3D berputar saat loading pertama kali, dan versi besar interaktif (bisa dimiringkan dengan mouse/sentuhan) di halaman Beranda.
- **Tampilan neumorphism 3D yang lebih hidup** — kartu statistik, kartu proker, dan kalender kini punya efek *tilt* 3D mengikuti gerakan mouse (khusus perangkat non-sentuh), ikon melayang saat hover, dan bayangan yang lebih dalam.
- **Menu Kalender** (tab baru) — kalender bulanan yang otomatis sinkron dengan data yang sudah dimasukkan: menandai rentang hari KKL, tanggal transaksi (pemasukan/pengeluaran), dan tanggal pelaksanaan proker. Klik satu tanggal untuk melihat detail kegiatan di hari itu.
- **Batas maksimal iuran per anggota Rp700.000** — iuran wajib tetap dihitung dari jumlah hari × nominal per hari di Pengaturan, tapi kini otomatis dibatasi (di-cap) maksimal Rp700.000 per anggota, walau hasil perkaliannya lebih besar.
- **Program Kerja mengikuti format Matriks Rencana Aksi Detail (RAD)** — setiap proker sekarang punya kolom: Tujuan Spesifik (Output/Outcome), Sasaran/Peserta (Jumlah & Kriteria), Metode Pelaksanaan, Waktu & Tempat, Penanggung Jawab (Nama Mahasiswa), Kebutuhan Sumber Daya, dan Indikator Keberhasilan — plus anggaran & realisasi seperti sebelumnya. Tab Program Kerja punya dua tampilan: **Kartu** (ringkas, tombol "Detail RAD" untuk lihat lengkap) dan **Tabel RAD** (tabel matriks lengkap seperti dokumen RAD, cocok untuk dicetak/laporan).
- Kredit sistem: **AL-HAZA™** ditampilkan di layar loading, sidebar, dan kartu logo Beranda.

Firebase project yang dipakai: **`kkl-2026-c133e`** (config sudah tertanam di `index.html`, tidak perlu diubah).

---

## 🚀 Langkah 1 — Aktifkan Firestore Database

1. Buka [Firebase Console](https://console.firebase.google.com/) → pilih project **kkl-2026-c133e**.
2. Di menu kiri: **Build → Firestore Database → Create database**.
3. Pilih **Start in production mode** → pilih lokasi server (contoh: `asia-southeast2 (Jakarta)`) → **Enable**.
4. Setelah dibuat, buka tab **Rules**, hapus isi default, lalu **copy-paste** isi dari `firestore.rules` (ada di folder ini) → klik **Publish**.

## 🔐 Langkah 2 — Aktifkan Login Bendahara

1. Di Firebase Console: **Build → Authentication → Get started**.
2. Pilih tab **Sign-in method** → aktifkan provider **Email/Password** → Save.
3. Pindah ke tab **Users** → **Add user** → isi email & password untuk **bendahara** (bisa dibuat lebih dari satu akun, misal ketua & bendahara).
4. Akun inilah yang dipakai untuk login lewat tombol **"Masuk Bendahara"** di website.

> Anggota biasa **tidak perlu akun** — mereka cukup buka link website dan langsung bisa melihat semua data.

## 📤 Langkah 3 — Deploy ke GitHub Pages

1. Buat repository baru di GitHub (bisa publik atau private, tapi GitHub Pages gratis butuh repo publik kecuali punya GitHub Pro).
2. Upload **semua isi folder ini** (`index.html`, `README.md`, `firestore.rules`) ke repo tersebut. Cara termudah lewat browser:
   - Buka repo → **Add file → Upload files** → drag semua file/folder → **Commit changes**.
   - Atau lewat terminal:
     ```bash
     git init
     git add .
     git commit -m "Deploy dashboard KKL Kuala Secapah 1"
     git branch -M main
     git remote add origin https://github.com/USERNAME/NAMA_REPO.git
     git push -u origin main
     ```
3. Di repo GitHub: **Settings → Pages**.
4. Pada **Source**, pilih **Deploy from a branch** → Branch: **main**, folder **/ (root)** → **Save**.
5. Tunggu 1–2 menit, GitHub akan memberi link seperti:
   `https://USERNAME.github.io/NAMA_REPO/`
6. Selesai! Bagikan link itu ke semua anggota KKL (bisa juga ditaruh di bio Instagram [@kkl.kualasecapah_1](https://www.instagram.com/kkl.kualasecapah_1)).

### ⚠️ Penting: Authorized Domain
Setelah dapat link GitHub Pages, tambahkan domain tersebut ke Firebase supaya login bisa berfungsi:
1. Firebase Console → **Authentication → Settings → Authorized domains → Add domain**.
2. Masukkan domain GitHub Pages kamu, contoh: `USERNAME.github.io`.

---

## ✏️ Cara Pakai Setelah Live

1. Buka link GitHub Pages kamu.
2. Klik **Masuk Bendahara** (sidebar kiri bawah) → login pakai akun yang dibuat di Langkah 2.
3. Ke tab **Pengaturan** → isi nama KKL, lokasi, tanggal mulai & selesai, nominal iuran per hari, link Instagram/Drive → **Simpan Pengaturan**.
4. Tambahkan anggota di tab **Anggota**.
5. Catat pemasukan/pengeluaran di tab **Keuangan** — status lunas/belum tiap anggota otomatis terhitung dari total hari × iuran per hari.
6. Tambahkan program kerja di tab **Program Kerja** menggunakan format RAD (Tujuan Spesifik, Sasaran/Peserta, Metode Pelaksanaan, Waktu & Tempat, Penanggung Jawab, Kebutuhan Sumber Daya, Indikator Keberhasilan) — realisasi anggaran otomatis dihitung dari transaksi pengeluaran yang ditautkan ke proker tersebut. Gunakan tombol **Tabel RAD** untuk melihat semua proker dalam bentuk matriks siap cetak.
7. Buka tab **Kalender** untuk melihat rekap harian — tanggal yang berada dalam periode KKL, tanggal transaksi, dan tanggal proker akan otomatis ditandai. Klik tanggal mana pun untuk melihat detailnya di panel sebelah kanan.
8. Anggota lain tinggal buka link yang sama tanpa login untuk memantau — semua berubah realtime.

## 💾 Backup Data

Di tab **Pengaturan → Cadangkan Data**, ada tombol **Unduh Backup (JSON)** — bisa dipakai kapan saja (tidak perlu login) untuk menyimpan salinan data. Tombol **Impor Backup** (khusus bendahara) untuk memulihkan data dari file backup.

## 🎨 Tentang Tampilan

Desain menggunakan gaya **neumorphism** (efek timbul/tenggelam lembut) dengan mode terang & gelap (toggle di sidebar), animasi transisi antar tab, grafik donat pengeluaran, progress bar hari KKL, serta animasi loading 3D dengan logo resmi KKL saat pertama kali dibuka.

## 🧩 Struktur Data di Firestore

```
settings/main   → identitas KKL, tanggal, iuran per hari (wajib per anggota otomatis dibatasi maks. Rp700.000), kategori
anggota/{id}    → nama, jabatan, kontak
transaksi/{id}  → jenis, kategori, tanggal, jumlah, keterangan, anggotaId, prokerId
proker/{id}     → nama, tujuan (Tujuan Spesifik), sasaran (Sasaran/Peserta), metode (Metode Pelaksanaan),
                   tanggal, tempat (Waktu & Tempat), pic (Penanggung Jawab), kebutuhan (Kebutuhan Sumber Daya),
                   indikator (Indikator Keberhasilan), anggaran, status
```

> Tab **Kalender** tidak menyimpan data baru — ia hanya membaca ulang `transaksi` dan `proker` yang sudah ada berdasarkan field `tanggal`, jadi otomatis sinkron tanpa perlu koleksi tambahan.

## 🛟 Mode Demo Lokal

Jika suatu saat `firebaseConfig` di `index.html` kosong/rusak, website otomatis jatuh ke **Mode Demo Lokal** (data tersimpan di `localStorage` browser saja, tanpa login) supaya website tetap bisa dicoba. Saat ini konfigurasi sudah terisi dengan project `kkl-2026-c133e`, jadi mode ini seharusnya tidak aktif.
