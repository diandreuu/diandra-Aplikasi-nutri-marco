# PRD — NutriMacro: Web App Kalkulator Gizi

| | |
|---|---|
| **Versi** | 1.0 (Draft) |
| **Tanggal** | 20 Oktober 2026 |
| **Platform** | Web app responsif (mobile-first) |
| **Bahasa antarmuka** | Bahasa Indonesia |
| **Referensi desain** | `DESIGN.md` (sistem desain "Vibrant Health & Nutrition") dan `code.html` (prototipe halaman Kalkulator Harian) |

---

## 1. Ringkasan Produk

**NutriMacro** adalah web app untuk menghitung kebutuhan gizi harian dan mencatat asupan makanan, minuman, serta air. Pengguna menetapkan target kalori dan makronutrien (protein, karbohidrat, lemak), lalu mencatat makanan per waktu makan dan melihat progresnya secara langsung lewat cincin kalori, progress bar makro, dan ringkasan harian.

**Nilai utama:** pencatatan yang cepat (minimal ketukan), data makro yang jelas sekilas pandang, dan database makanan yang akrab dengan menu Indonesia (nasi, tempe, tahu, dll.).

## 2. Latar Belakang & Masalah

- Aplikasi pencatat kalori sering terasa ribet dan membuat pengguna merasa bersalah, sehingga mereka berhenti memakainya.
- Database makanan pada aplikasi global kurang mencakup makanan Indonesia dan takaran lokal (mangkuk, piring, potong, butir).
- Pengguna butuh jawaban cepat: "Sisa kalori dan protein saya hari ini berapa?"

## 3. Tujuan & Non-Tujuan

### Tujuan
1. Pengguna dapat menghitung target kalori dan makro harian berdasarkan profil dan tujuan mereka.
2. Pengguna dapat mencatat makanan dalam waktu kurang dari 15 detik per item.
3. Dashboard menampilkan status kalori, makro, dan hidrasi secara real-time.
4. Pengguna dapat melihat riwayat dan tren nutrisi.
5. Menyediakan database makanan Indonesia yang bisa dicari dan ditambah sendiri.

### Non-Tujuan (di luar cakupan v1)
- Rekomendasi medis atau diagnosis (aplikasi hanya sebagai alat bantu, bukan pengganti ahli gizi/dokter).
- Pemindaian foto makanan dengan AI.
- Fitur sosial, komunitas, atau gamifikasi kompetitif.
- Integrasi perangkat wearable.
- Pelacakan mikronutrien (vitamin/mineral) dan gula/serat/natrium (dipertimbangkan v2).

## 4. Target Pengguna

| Persona | Kebutuhan |
|---|---|
| **Individu aktif / fitness** | Memantau protein dan kalori untuk menjaga massa otot atau defisit ringan |
| **Pencari gaya hidup sehat** | Memahami asupan harian tanpa angka yang rumit |
| **Pencatat pemula** | Input cepat, tampilan ramah, tidak menghakimi |

## 5. Ruang Lingkup & Struktur Halaman

Berdasarkan navigasi pada desain, aplikasi memiliki 4 halaman utama:

| Halaman | Status pada desain | Prioritas |
|---|---|---|
| **Kalkulator Harian** | Sudah didesain (code.html) | P0 (MVP) |
| **Target & Goal** | Belum didesain (ada tautan "Ubah Target") | P0 (MVP) |
| **Database Makanan** | Belum didesain | P0 (MVP, versi sederhana) |
| **Riwayat Nutrisi** | Belum didesain | P1 |
| Panduan Nutrisi, Pusat Bantuan, Privasi (footer) | Belum didesain | P2 |

> Halaman yang belum didesain perlu dibuatkan desain mengikuti `DESIGN.md` sebelum dikembangkan.

## 6. Kebutuhan Fungsional

Prioritas: **P0** = wajib untuk MVP, **P1** = penting setelah MVP, **P2** = opsional.

### 6.1 Kalkulator Harian (Dashboard)

| ID | Kebutuhan | Prioritas |
|---|---|---|
| FR-01 | Menampilkan kartu **Kalori Harian**: cincin progres (SVG donut), total kalori masuk, target, persentase pencapaian, dan lencana sisa kalori ("460 kcal Tersisa"). | P0 |
| FR-02 | Jika kalori melebihi target, lencana berubah menjadi "X kcal Lebih" dengan warna peringatan (`error-container`), dan cincin memakai warna `#EF4444`. | P0 |
| FR-03 | Menampilkan 3 kartu makro (Protein, Karbohidrat, Lemak): nilai konsumsi / target (gram), teks sisa, progress bar, persentase, dan kontribusi kalori. | P0 |
| FR-04 | Kontrol tanggal: tombol hari sebelumnya/berikutnya serta label tanggal aktif; memuat log pada tanggal terpilih. | P0 |
| FR-05 | Menampilkan label tujuan aktif pengguna (misal "Pemeliharaan Massa Otot (Defisit Ringan)"). | P1 |
| FR-06 | Empat kartu waktu makan: **Sarapan, Makan Siang, Makan Malam, Camilan & Ekstra**. Tiap kartu menampilkan jam, subtotal (kcal, P, K, L), dan dapat dilipat/dibuka (accordion). | P0 |
| FR-07 | Daftar item per waktu makan: nama, takaran, dan chip kalori + P/K/L. Tombol hapus muncul saat hover (desktop) dan tersedia lewat geser/menu pada mobile. | P0 |
| FR-08 | Keadaan kosong (empty state) pada kartu yang belum berisi, dengan ajakan mencatat. | P0 |
| FR-09 | **Catat Makanan Cepat** (modal): pilih waktu makan, cari nama makanan, atur porsi, lihat kalori dan makro, lalu simpan. | P0 |
| FR-10 | **Pintasan Cepat Makanan** (favorit): satu ketukan menambah item ke waktu makan yang dipilih pengguna. | P0 |
| FR-11 | **Pelacak Hidrasi**: target (default 2,5 L = 10 gelas @250 ml; desain contoh memakai 8 gelas), grid gelas yang dapat diketuk, tombol "+1 Gelas Air", cincin progres. | P0 |
| FR-12 | **Kartu Tips Makronutrisi** yang dinamis berdasarkan sisa makro hari itu (misal protein tersisa). | P1 |
| FR-13 | **Ringkasan Harian**: ekspor ringkasan hari itu ke PDF. | P2 |
| FR-14 | Edit item yang sudah dicatat (ubah porsi, otomatis menghitung ulang nilai). | P1 |
| FR-15 | Salin makanan dari hari/waktu makan lain ("catat ulang"). | P1 |
| FR-16 | Toast konfirmasi untuk setiap aksi (simpan, hapus, perbarui). | P0 |

### 6.2 Target & Goal

| ID | Kebutuhan | Prioritas |
|---|---|---|
| FR-20 | Formulir profil: jenis kelamin, usia, tinggi (cm), berat (kg), tingkat aktivitas. | P0 |
| FR-21 | Pilihan tujuan: **turun berat badan, pertahankan, naik massa otot**, dengan tingkat intensitas (ringan/sedang). | P0 |
| FR-22 | Hitung otomatis BMR, TDEE, target kalori, dan target makro (lihat Bagian 8). | P0 |
| FR-23 | Pengguna dapat mengubah target secara manual (override) untuk kalori dan tiap makro. | P0 |
| FR-24 | Peringatan lembut jika target kalori berada di bawah batas aman (lihat Bagian 8.4). | P0 |
| FR-25 | Target hidrasi dapat diatur. | P1 |
| FR-26 | Pelacakan berat badan (catat berat dari waktu ke waktu). | P2 |

### 6.3 Database Makanan

| ID | Kebutuhan | Prioritas |
|---|---|---|
| FR-30 | Pencarian makanan dengan *autocomplete* (nama Indonesia, toleran salah ketik ringan). | P0 |
| FR-31 | Data awal makanan Indonesia dengan takaran lokal (piring, mangkuk, potong, butir, gelas) dan nilai per 100 g. | P0 |
| FR-32 | Perhitungan otomatis kalori dan makro berdasarkan porsi (gram/ml atau takaran lokal). | P0 |
| FR-33 | Makanan kustom buatan pengguna (nama, per-porsi, kalori, P/K/L). | P0 |
| FR-34 | Tandai makanan sebagai **Favorit** (mengisi Pintasan Cepat). | P0 |
| FR-35 | Makanan terakhir/sering dipakai muncul di urutan atas hasil pencarian. | P1 |
| FR-36 | Resep/kombinasi makanan (simpan sebagai satu paket). | P2 |
| FR-37 | Pemindai barcode (ikon sesuai `DESIGN.md`, "Quick-Search Prepend"). | P2 |

### 6.4 Riwayat Nutrisi

| ID | Kebutuhan | Prioritas |
|---|---|---|
| FR-40 | Tampilan riwayat per hari: kalori vs target, makro, hidrasi. | P1 |
| FR-41 | Grafik tren 7 dan 30 hari (kalori, protein, karbohidrat, lemak). | P1 |
| FR-42 | Indikator konsistensi/streak pencatatan (aksen amber sesuai desain). | P1 |
| FR-43 | Ekspor data (CSV/PDF). | P2 |

### 6.5 Umum & Akun

| ID | Kebutuhan | Prioritas |
|---|---|---|
| FR-50 | Penyimpanan data (lihat Bagian 9: lokal dulu, akun menyusul). | P0 |
| FR-51 | Onboarding singkat: isi profil, lalu target otomatis dihitung. | P0 |
| FR-52 | Registrasi/login dan sinkronisasi antarperangkat. | P1 |
| FR-53 | Pengingat (notifikasi) makan dan minum. Ikon lonceng sudah ada di header. | P2 |
| FR-54 | Halaman statis: Panduan Nutrisi, Pusat Bantuan, Kebijakan Privasi. | P2 |

## 7. Alur Pengguna Utama

**A. Pengguna baru**
1. Buka aplikasi → onboarding (profil + tujuan) → target dihitung otomatis → pengguna meninjau dan menyetujui → masuk dashboard.

**B. Mencatat makanan (jalur cepat)**
1. Dashboard → ketuk **+ Tambah** pada kartu waktu makan (atau "Catat Makanan Cepat").
2. Ketik nama makanan → pilih dari hasil → atur porsi → nilai gizi muncul otomatis.
3. **Simpan** → item muncul di daftar, cincin kalori dan progress makro ter-update, toast konfirmasi.

**C. Memakai pintasan favorit**
1. Ketuk item di "Pintasan Cepat Makanan" → makanan masuk ke waktu makan aktif → dashboard ter-update.

**D. Meninjau progres**
1. Buka **Riwayat Nutrisi** → pilih rentang 7/30 hari → lihat tren dan hari yang melebihi/kurang dari target.

## 8. Logika Perhitungan

### 8.1 BMR (Mifflin-St Jeor)
- Pria: `BMR = 10 × berat(kg) + 6,25 × tinggi(cm) − 5 × usia + 5`
- Wanita: `BMR = 10 × berat(kg) + 6,25 × tinggi(cm) − 5 × usia − 161`

### 8.2 TDEE
`TDEE = BMR × faktor aktivitas`

| Tingkat aktivitas | Faktor |
|---|---|
| Sedentari (jarang olahraga) | 1,2 |
| Ringan (1–3×/minggu) | 1,375 |
| Sedang (3–5×/minggu) | 1,55 |
| Berat (6–7×/minggu) | 1,725 |
| Sangat berat (fisik berat/2×/hari) | 1,9 |

### 8.3 Target kalori berdasarkan tujuan (nilai default, dapat diubah)
| Tujuan | Penyesuaian |
|---|---|
| Turun berat badan (ringan / sedang) | −10% / −20% dari TDEE |
| Pertahankan | 0% |
| Naik massa otot (ringan / sedang) | +5% / +10% dari TDEE |
| Pemeliharaan otot dengan defisit ringan (seperti pada desain) | −10% |

### 8.4 Target makro (default, dapat diubah)
- **Protein:** 1,6–2,0 g per kg berat badan (default 1,8 g/kg untuk tujuan otot atau defisit; 1,2–1,6 g/kg untuk lainnya).
- **Lemak:** ±25–30% dari kalori target.
- **Karbohidrat:** sisa kalori setelah protein dan lemak.
- Konversi energi: **protein 4 kcal/g, karbohidrat 4 kcal/g, lemak 9 kcal/g**.

**Batas aman (peringatan, bukan pemblokiran):** target kalori di bawah ±1.200 kcal (wanita) atau ±1.500 kcal (pria) menampilkan peringatan agar pengguna berkonsultasi dengan tenaga kesehatan.

### 8.5 Perhitungan dashboard
- `kalori tersisa = target − konsumsi` (jika negatif → tampil sebagai "Lebih").
- `persentase = min(100, konsumsi / target × 100)`; progres makro dihitung dengan cara sama per makro.
- `kontribusi kalori makro = gram × (4 | 4 | 9)` ditampilkan pada kartu makro.
- Subtotal waktu makan = jumlah seluruh item di kartu tersebut; total harian = jumlah semua subtotal.
- **Aturan konsistensi:** kalori sebuah makanan idealnya sama dengan `4P + 4K + 9L`. Jika pengguna mengisi kalori manual yang selisihnya > 15%, tampilkan petunjuk lembut ("Kalori tidak sesuai dengan makro, periksa kembali").

## 9. Data & Penyimpanan

### 9.1 Entitas data (garis besar)

| Entitas | Atribut utama |
|---|---|
| **UserProfile** | id, jenis_kelamin, usia, tinggi, berat, aktivitas, tujuan, intensitas |
| **Target** | kalori, protein_g, karbo_g, lemak_g, air_ml, aktif_sejak |
| **Food** | id, nama, per_100g (kcal, P, K, L), daftar takaran (nama, gram), sumber (bawaan/kustom), favorit |
| **LogEntry** | id, tanggal, waktu_makan (`sarapan`/`siang`/`malam`/`camilan`), food_id/nama, porsi_gram, kcal, P, K, L, dibuat_pada |
| **WaterLog** | tanggal, jumlah_ml |
| **WeightLog** | tanggal, berat (P2) |

> Nilai gizi pada `LogEntry` disimpan sebagai *snapshot* agar riwayat tidak berubah ketika data master makanan diedit.

### 9.2 Strategi penyimpanan
- **MVP:** penyimpanan di sisi klien (IndexedDB atau `localStorage`), tanpa akun. Cocok untuk tahap belajar dan validasi cepat.
- **Tahap berikutnya:** backend + autentikasi untuk sinkronisasi antarperangkat dan cadangan data.

### 9.3 Sumber data makanan
- Data awal dikurasi manual dari sumber resmi, misalnya **Tabel Komposisi Pangan Indonesia (TKPI, Kemenkes)**, dengan pencantuman sumber.
- Pengguna dapat menambah makanan kustom.

## 10. Kebutuhan Desain (Mengacu pada DESIGN.md)

- **Font:** Plus Jakarta Sans (400/600/700/800); angka metrik memakai `font-feature-settings: 'tnum' on`.
- **Warna:** token Material dari `DESIGN.md` (primer ungu `#6C2BD9`, sekunder amber `#F59E0B`, tersier lavender `#A78BFA`, netral `#1E1B2E`); latar `#FAF9FD`, kartu `#FFFFFF`.
- **Bentuk:** kartu `rounded 16px`, permukaan besar `24px`, tombol dan chip berbentuk pil (`9999px`), input `8px`.
- **Elevasi:** bayangan ungu lembut Level 1–3; border halus `#F1EDFA`.
- **Layout responsif:** Mobile (<768px) satu kolom; Tablet (768–1023px) 8 kolom; Desktop (≥1024px) 12 kolom dengan lebar maksimum 1.200 px (kalori 5 kol + makro 7 kol; makanan 8 kol + sidebar 4 kol pada prototipe).
- **Ikon:** Material Symbols Outlined.
- **Mikro-interaksi:** transisi cincin/bar 500–700 ms, tombol `active:scale-95`, toast otomatis hilang ±2,6 dtk.

### Catatan konsistensi desain yang perlu diputuskan sebelum pengembangan
1. **Warna makro:** `DESIGN.md` menetapkan Kalori = amber, Protein = ungu, Karbohidrat = biru aqua `#0EA5E9`, Lemak = koral `#F43F5E`. Pada `code.html`, karbohidrat memakai amber dan lemak memakai ungu. Perlu ditetapkan satu acuan (disarankan mengikuti `DESIGN.md` agar tidak membingungkan dengan warna kalori).
2. **Tombol utama:** `DESIGN.md` memakai amber `#F59E0B` dengan teks gelap; prototipe memakai `secondary-container` (`#fea619`). Selaraskan token.
3. **Target hidrasi:** label 2,5 L tetapi logika 8 gelas × 250 ml = 2 L. Tentukan satu angka (10 gelas = 2,5 L, atau ubah label menjadi 2 L).
4. **Konsistensi angka kalori:** pada prototipe, total 1.640 kcal tidak sama dengan 4×110 + 4×185 + 9×42 = 1.558 kcal. Terapkan aturan pada 8.5.
5. **Tanggal contoh:** header menampilkan 2025, footer 2026; gunakan tanggal dinamis.
6. **Pintasan cepat:** pada prototipe selalu masuk ke "Siang"; v1 harus masuk ke waktu makan yang sedang aktif atau yang dipilih pengguna.

## 11. Kebutuhan Non-Fungsional

| Area | Target |
|---|---|
| **Performa** | Halaman utama interaktif < 2,5 dtk pada jaringan 4G; pembaruan UI setelah simpan item < 100 ms |
| **Responsif** | Berfungsi baik pada lebar 360 px hingga desktop; area ketuk minimal 44×44 px |
| **Aksesibilitas** | Mengacu WCAG 2.1 AA: kontras teks ≥ 4,5:1, label formulir, navigasi keyboard, `aria-label` pada tombol ikon, tidak hanya mengandalkan warna untuk status |
| **Kompatibilitas** | Chrome, Safari, Firefox, Edge versi dua rilis terakhir; Safari iOS dan Chrome Android |
| **Keamanan & privasi** | Data kesehatan bersifat sensitif: HTTPS, tidak menjual data, penghapusan data atas permintaan, patuh UU Pelindungan Data Pribadi (UU PDP) bila ada akun/backend |
| **Offline** | Pencatatan tetap berjalan tanpa internet (PWA, disarankan P1) |
| **Lokalisasi** | Format angka dan tanggal Indonesia (`id-ID`, misal 1.640), zona waktu WIB (menyesuaikan perangkat) |
| **Keandalan data** | Tidak ada kehilangan data saat tab ditutup; konfirmasi sebelum menghapus massal |
| **Keamanan front-end** | Hindari penyisipan input pengguna langsung ke `innerHTML` (prototipe saat ini melakukannya); lakukan *escaping* atau pakai pembuatan elemen DOM/framework |

## 12. Disclaimer & Etika Produk

- Tampilkan pernyataan: *"NutriMacro adalah alat bantu informasi dan bukan pengganti saran medis."*
- Hindari bahasa yang menyalahkan; tonjolkan pencapaian dan konsistensi (sesuai nada "tanpa rasa bersalah" pada `DESIGN.md`).
- Jangan menyarankan target kalori yang tidak aman; sediakan batas bawah dan peringatan (FR-24).
- Pertimbangkan pengguna di bawah 18 tahun, ibu hamil/menyusui, dan kondisi medis tertentu: tampilkan anjuran konsultasi, bukan target otomatis agresif.

## 13. Metrik Keberhasilan

| Metrik | Target awal (3 bulan setelah rilis) |
|---|---|
| Penyelesaian onboarding | ≥ 70% |
| Waktu rata-rata mencatat satu item | ≤ 15 detik |
| Pengguna aktif yang mencatat ≥ 5 hari/minggu | ≥ 30% |
| Retensi D7 / D30 | ≥ 35% / ≥ 20% |
| Pencarian makanan yang berujung pilihan (bukan input manual) | ≥ 75% |
| Skor kepuasan (survei singkat) | ≥ 4/5 |

## 14. Rencana Rilis (Roadmap)

| Fase | Isi | Hasil |
|---|---|---|
| **Fase 0 — Persiapan** | Lengkapi desain halaman Target & Goal, Database Makanan, Riwayat; putuskan catatan konsistensi (Bagian 10); kurasi 100–200 makanan Indonesia awal | Desain final + dataset awal |
| **Fase 1 — MVP** | Dashboard harian, catat makanan (pencarian + kustom + favorit), hidrasi, kalkulator target, penyimpanan lokal, responsif | Aplikasi dapat dipakai harian tanpa akun |
| **Fase 2 — Wawasan** | Riwayat & grafik tren, edit/salin item, tips dinamis, PWA/offline | Pengguna melihat kemajuan |
| **Fase 3 — Akun & Skala** | Login, sinkronisasi, ekspor PDF/CSV, pengingat, pelacakan berat | Multi-perangkat |
| **Fase 4 — Lanjutan** | Barcode, resep, mikronutrien, integrasi lain | Pendalaman fitur |

## 15. Kriteria Penerimaan (MVP)

1. Setelah menyimpan item baru, kalori total, makro, subtotal waktu makan, cincin, dan progress bar ter-update tanpa muat ulang halaman.
2. Menghapus item mengembalikan semua nilai seperti sebelum item itu ditambahkan, dan tidak pernah menjadi negatif.
3. Saat kalori melebihi target, lencana dan warna cincin berubah ke status peringatan.
4. Data tetap ada setelah halaman dimuat ulang.
5. Pengguna dapat mengisi profil dan mendapat target kalori + makro yang dapat diubah manual.
6. Mengganti tanggal menampilkan log hari tersebut (atau empty state jika kosong).
7. Layout benar pada 360 px, 768 px, dan 1280 px tanpa scroll horizontal.
8. Semua kontrol dapat dioperasikan dengan keyboard dan memiliki label aksesibilitas.

## 16. Risiko & Mitigasi

| Risiko | Dampak | Mitigasi |
|---|---|---|
| Data gizi tidak akurat | Kepercayaan pengguna turun | Gunakan sumber resmi (TKPI), cantumkan sumber, izinkan koreksi |
| Cakupan makanan Indonesia kurang | Pengguna harus input manual | Fitur makanan kustom + penambahan dataset bertahap |
| Pencatatan terasa melelahkan | Pengguna berhenti | Favorit, "catat ulang", makanan terakhir, input minimal |
| Target tidak aman untuk sebagian pengguna | Risiko kesehatan | Batas aman, peringatan, disclaimer |
| Kehilangan data (penyimpanan lokal dihapus) | Riwayat hilang | Ekspor data sejak awal, akun + sinkronisasi di Fase 3 |
| Ketergantungan CDN (Tailwind CDN, Google Fonts) | Gagal tampil / lambat | Untuk produksi, build Tailwind sendiri dan host font secara lokal |

## 17. Pertanyaan Terbuka

1. Apakah v1 sepenuhnya tanpa akun (lokal), atau langsung dengan login?
2. Satuan target hidrasi: 2 L (8 gelas) atau 2,5 L (10 gelas)?
3. Apakah kalori ditentukan dari makro (4/4/9) atau boleh diinput bebas dengan peringatan?
4. Sumber dataset makanan: hanya TKPI, atau ditambah data kurasi sendiri?
5. Perlu dukungan bahasa lain, atau tetap Bahasa Indonesia saja?
6. Tingkat detail yang akan dilacak ke depan: gula, serat, natrium?
7. Apakah mode gelap (`darkMode: "class"` sudah disiapkan di Tailwind config) masuk v1?
8. Kerangka kerja pengembangan: tetap HTML + Tailwind + JavaScript murni seperti prototipe, atau memakai framework (React/Vue/Svelte)?

---

*Dokumen ini disusun berdasarkan `DESIGN.md` dan `code.html`. Hal yang belum tercakup oleh desain ditandai pada Bagian 5 dan dapat disesuaikan setelah desain halaman lainnya selesai.*
