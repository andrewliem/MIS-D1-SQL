# Akademik Dashboard (MIS & Cloudflare D1 SQL)

Projek ini adalah materi pembelajaran praktikum Sistem Informasi Manajemen (MIS) / Sistem Informasi untuk mengajarkan integrasi antara aplikasi web modern dengan database relasional serverless menggunakan **Cloudflare D1** (berbasis SQLite) dan **Cloudflare Workers**.

Aplikasi ini berupa dashboard akademik interaktif yang menampilkan data statistik mahasiswa, daftar program studi, mata kuliah, nilai, serta kartu rencana studi (KRS) secara real-time langsung dari database D1.

---

## 📂 Struktur Repositori

Untuk memudahkan pembelajaran, repositori ini disusun dengan struktur yang rapi sebagai berikut:

```text
.
├── db/                       # Folder Database (SQL)
│   ├── schema.sql           # Struktur tabel database (Fakultas, Prodi, Mahasiswa, KRS, dll.)
│   ├── seed.sql             # Data dummy/awal untuk pengisian tabel (50+ baris data)
│   └── queries.sql          # Kumpulan contoh query SQL (JOIN, GROUP BY, CASE WHEN) untuk latihan
├── public/                   # Frontend / Client-side (HTML, CSS, JS Browser)
│   └── index.html           # Tampilan dashboard akademik interaktif
├── src/                      # Backend / Server-side (Cloudflare Workers)
│   └── index.js             # API Gateway & Logika bisnis yang terhubung ke D1 Database
├── wrangler.jsonc            # File konfigurasi Cloudflare Wrangler & binding D1
├── package.json              # Konfigurasi dependensi project (Node.js)
└── TUTORIAL.md               # Panduan belajar lengkap langkah demi langkah
```

---

## ⚡ Fitur Utama Dashboard

1. **KPI Cards (Statistik Utama)**:
   - Total Mahasiswa & Mahasiswa Aktif.
   - Total Program Studi.
   - Rata-rata IPK (GPA) mahasiswa yang dihitung dinamis menggunakan query SQL `CASE WHEN` dan `AVG`.
2. **Daftar Mahasiswa**:
   - Pencarian mahasiswa berdasarkan nama/NIM secara dinamis.
   - Informasi detail Program Studi dan Fakultas (menggunakan `LEFT JOIN`).
3. **Daftar Mata Kuliah**:
   - Statistik jumlah mahasiswa yang mengambil setiap mata kuliah.
   - Rata-rata nilai ujian per kelas.
4. **Data KRS & Transkrip Nilai**:
   - Riwayat pengambilan mata kuliah beserta nilai angka dan konversi huruf mutu (A, AB, B, dst.).

---

## 🚀 Cara Menjalankan Project Secara Lokal

Ikuti langkah cepat berikut untuk menjalankan simulasi database dan server lokal di komputer Anda:

1. **Instal Dependensi**:
   ```bash
   npm install
   ```
2. **Hubungkan dengan Akun Cloudflare**:
   ```bash
   npx wrangler login
   ```
3. **Buat Database D1**:
   ```bash
   npx wrangler d1 create akademik-db
   ```
   *Salin database ID yang didapatkan, lalu tempel di kolom `database_id` pada file `wrangler.jsonc`.*

4. **Inisialisasi Tabel & Data Dummy**:
   ```bash
   # Buat struktur tabel
   npx wrangler d1 execute akademik-db --local --file=./db/schema.sql

   # Isi data simulasi
   npx wrangler d1 execute akademik-db --local --file=./db/seed.sql
   ```

5. **Jalankan Aplikasi**:
   ```bash
   npm run dev
   ```
   *Buka browser dan akses **http://localhost:8787**.*

---

## 📖 Panduan Lengkap

Untuk panduan mendalam tentang arsitektur Frontend vs Backend, cara deploy aplikasi ke Cloud, serta latihan tugas mandiri SQL query, silakan baca dokumentasi lengkap di:
👉 **[TUTORIAL.md](file:///Users/andrewtannyliem/Downloads/MIS-D1-SQL/TUTORIAL.md)**

---
*Dibuat untuk bahan ajar Kelas Sistem Informasi / Management Information Systems (MIS).*
