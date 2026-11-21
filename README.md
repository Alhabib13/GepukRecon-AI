# GepukRecon-AI 

> **Sistem Rekonsiliasi Stok Digital dan Prediksi Kebutuhan Stok Harian pada UMKM Ayam Gepuk Bandar**  
> *Solusi operasional berbasis Web & AI untuk meminimalisir selisih stok saat closing toko serta mengoptimalkan estimasi persediaan bahan baku harian.*

---

[![Node.js](https://img.shields.io/badge/Node.js-v22-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express.js](https://img.shields.io/badge/Express.js-v4-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![Vite](https://img.shields.io/badge/Vite-v5-646CFF?logo=vite&logoColor=white)](https://vitejs.dev/)
[![React](https://img.shields.io/badge/React-v18-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-v16-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Postman](https://img.shields.io/badge/Postman-API_Tested-FF6C37?logo=postman&logoColor=white)](https://www.postman.com/)
[![Built with AI](https://img.shields.io/badge/Built_with-Antigravity_CLI_by_Google_DeepMind-8E24AA?logo=google&logoColor=white)](#-pengembangan-berbasis-ai)

---

##  Pengembangan Berbasis AI (AI-Assisted Development)

Repositori dan arsitektur aplikasi ini dirancang dan dikembangkan dengan kolaborasi bersama **Antigravity CLI** (Agentic AI Assistant oleh tim **Google DeepMind**). 

Antigravity CLI bertindak sebagai **Senior AI Fullstack Developer** yang membantu:
* Merancang arsitektur monorepo modular (*Express.js REST API* & *Vite React Dashboard*).
* Mendesain skema relasional database PostgreSQL untuk pencatatan stok dan rekonsiliasi.
* Mengembangkan algoritma rekonsiliasi otomatis (*matching engine*) antara stok fisik keluar dan total omset penjualan.
* Membangun modul *AI Forecasting* untuk estimasi kebutuhan stok harian berbasis data historis transaksi.
* Menyusun koleksi pengujian otomatis API menggunakan **Postman Collection & Environment**.

---

##  Informasi Program & Tim Capstone

Proyek ini merupakan bagian dari program **Asah 2026** yang diselenggarakan oleh **Dicoding** dan didukung oleh **GoTo**.

* **ID Tim**: `A26-CS192`
* **Mitra UMKM**: Ayam Gepuk Bandar (Bidang *Food and Beverage*)
* **Repository**: [https://github.com/Alhabib13/GepukRecon-AI.git](https://github.com/Alhabib13/GepukRecon-AI.git)

###  Anggota Tim A26-CS192:
| ID Anggota | Nama | Alur Pembelajaran (Path) | Peran dalam Proyek |
| :--- | :--- | :--- | :--- |
| `A26-CS192-1` | **Rahmat Nuril Mustofa** | Data Science | Data Preprocessing & Feature Engineering |
| `A26-CS192-2` | **Alhabib Husein Alaydrus** | Full-stack Developer | Frontend Development & REST API Integration |
| `A26-CS192-3` | **Mohammad Wildan Abdurrahman** | Full-stack Developer | Backend Architecture & Reconciliation Engine |
| `A26-CS192-4` | **Risda Sifa Hasna** | Data Science | Data Analytics & Dashboard Reporting |
| `A26-CS192-5` | **Muhammad Varel Al Khatran Savero** | AI Engineering | AI Model Training & Stock Forecasting Pipeline |
| `A26-CS192-6` | **Mila Cahaya Rani** | AI Engineering | AI Model Evaluation & Model API Serving |

---

##  Latar Belakang & Masalah

Pada UMKM **Ayam Gepuk Bandar**, proses pencatatan stok bahan baku keluar serta rekonsiliasi dengan pendapatan omset harian masih dilakukan secara manual oleh *crew* toko di buku catatan atau lembar terpisah. Hal ini menimbulkan kendala operasional:
1. **Waktu Closing yang Lama**: Proses tutup toko (*closing*) memakan waktu lama karena pencocokan manual antara porsi keluar dengan pendapatan kasir.
2. **Resiko Human Error**: Rentan terjadi selisih (*discrepancy*) yang sulit terlacak penyebabnya.
3. **Ketidakpastian Stok Harian**: Belum tersedianya sistem prediksi stok menyebabkan bahan baku (ayam, sambal racikan, tahu/tempe) kerap habis terlalu cepat di jam sibuk atau sebaliknya menumpuk hingga kualitas kesegarannya menurun.

---

##  Solusi & Fitur Utama

**GepukRecon-AI** hadir sebagai aplikasi web internal (*back-office operations dashboard*) dengan fitur:

1. **Input & Rekapitulasi Stok Digital**: Crew toko dapat mencatat stok menu keluar dan omset harian secara cepat dengan validasi data instan.
2. **Modul Rekonsiliasi Otomatis (Instant Match Engine)**: Mencocokkan data barang keluar dengan omset dalam waktu `< 5 detik` dan mendeteksi status `MATCH` (sinkron) atau `DISCREPANCY` (ada selisih).
3. **Modul AI Prediksi Kebutuhan Stok (Horizon 2–3 Hari)**: Menggunakan model *Machine Learning / Time Series* untuk memberikan estimasi kebutuhan stok menu harian agar kesiapan bahan baku terukur.
4. **Dashboard Visualisasi Kepala Toko**: Menampilkan riwayat rekonsiliasi, tren omset vs stok, serta grafik rekomendasi stok secara interaktif.

>  **Catatan Batasan Sistem**: Sistem ini merupakan *management dashboard* internal, bukan aplikasi kasir perorangan (*live POS customer checkout*), tidak menyediakan *payment gateway*, dan tidak terhubung otomatis ke supplier PO.

---

##  Arsitektur Teknologi

```
┌─────────────────────────────────────────────────────────────┐
│                       Client Side                           │
│             Vite + React.js + Tailwind CSS                  │
│       (Dashboard Kepala Toko & Form Input Crew Toko)        │
└──────────────────────────────┬──────────────────────────────┘
                               │ HTTP / JSON
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                       Server Side                           │
│               Node.js + Express.js REST API                 │
│  ├── Controllers (Stok, Rekonsiliasi, Prediksi AI, Auth)   │
│  ├── Services (Kalkulasi Discrepancy & Logic Engine)        │
│  └── Middlewares (Validasi Request & Error Handling)       │
└──────────────┬──────────────────────────────┬───────────────┘
               │                              │
               ▼                              ▼
┌──────────────────────────────┐ ┌────────────────────────────┐
│      Database Layer          │ │       AI / ML Module       │
│        PostgreSQL            │ │ Python FastAPI / ML Service│
│ (Relational Tables & Logs)   │ │ (Model Prediksi Time Series)│
└──────────────────────────────┘ └────────────────────────────┘
```

---

##  Struktur Repositori

```text
GepukRecon-AI/
├── backend/                  # REST API Server (Node.js & Express.js)
│   ├── src/
│   │   ├── config/           # Konfigurasi Database PostgreSQL
│   │   ├── controllers/      # Controller bisnis (Stock, Recon, Forecast)
│   │   ├── middlewares/      # Validasi & autentikasi
│   │   ├── models/           # Query & definisi tabel database
│   │   ├── routes/           # Endpoint API Express (/api/v1/...)
│   │   ├── services/         # Algoritma Rekonsiliasi & Integrasi AI
│   │   └── server.js         # Entry point aplikasi backend
│   ├── .env.example          # Template konfigurasi environment backend
│   └── package.json
│
├── frontend/                 # Client Web Application (Vite + React)
│   ├── public/               # Asset statis & logo Ayam Gepuk Bandar
│   ├── src/
│   │   ├── assets/           # Ikon & style tambahan
│   │   ├── components/       # Komponen UI (Navbar, Card, Modal, Tabel)
│   │   ├── pages/            # Halaman Dashboard, Input Stok, Laporan
│   │   ├── services/         # API Client (Axios / Fetch Helper)
│   │   ├── App.jsx           # Routing & Layout utama
│   │   └── main.jsx          # Entry point React
│   ├── index.html
│   ├── tailwind.config.js    # Konfigurasi styling Tailwind CSS
│   ├── vite.config.js        # Konfigurasi build Vite
│   └── package.json
│
├── postman/                  # Dokumentasi & Pengujian API
│   ├── GepukRecon_Collection.json   # Postman Collection lengkap
│   └── GepukRecon_Environment.json  # Environment variabel (baseUrl, token)
│
├── docs/                     # Dokumentasi pendukung & hasil interview
├── .gitignore
└── README.md
```

---

##  Dokumentasi & Pengujian API (Postman)

Koleksi Postman telah disediakan di dalam folder `postman/` untuk mempermudah tim melakukan pengujian *endpoint*:

1. **Import ke Postman**:
   * Buka aplikasi Postman.
   * Klik tombol **Import**, lalu pilih file `postman/GepukRecon_Collection.json` dan `postman/GepukRecon_Environment.json`.
   * Pilih environment **GepukRecon-Local**.
2. **Daftar Endpoint Utama**:
   * `POST /api/v1/auth/login` — Autentikasi Crew & Kepala Toko
   * `GET  /api/v1/menus` — Mendapatkan daftar master menu & bahan
   * `POST /api/v1/stocks/out` — Mencatat stok barang keluar harian
   * `POST /api/v1/revenues/daily` — Mencatat total omset harian kasir
   * `POST /api/v1/reconcile` — Memicu rekonsiliasi otomatis (stok vs omset)
   * `GET  /api/v1/reconcile/history` — Riwayat rekonsiliasi penutupan toko
   * `GET  /api/v1/ai/predict-stock` — Mengambil hasil rekomendasi stok 2–3 hari ke depan

---

##  Panduan Instalasi & Menjalankan Lokal

### Prasyarat:
* [Node.js](https://nodejs.org/) (versi 18 ke atas, disarankan v22+)
* [PostgreSQL](https://www.postgresql.org/) (versi 14+)
* [Git](https://git-scm.com/)

### 1. Clone Repositori
```bash
git clone https://github.com/Alhabib13/GepukRecon-AI.git
cd GepukRecon-AI
```

### 2. Setup Backend (Express.js)
```bash
cd backend
npm install

# Salin file environment dan sesuaikan kredensial PostgreSQL Anda
cp .env.example .env

# Jalankan server dalam mode development
npm run dev
```
*Backend default berjalan pada: `http://localhost:5000`*

### 3. Setup Frontend (Vite + React)
```bash
cd ../frontend
npm install

# Jalankan server frontend
npm run dev
```
*Frontend default berjalan pada: `http://localhost:5173`*

---

##  Rencana Pengerjaan (Timeline 4 Minggu)

* **Minggu 1 (30 Okt – 5 Nov 2026)**: Inisiasi proyek, analisis kebutuhan, pembuatan data sintetis, perancangan ERD database, wireframe UI/UX, dan setup repository.
* **Minggu 2 (6 – 12 Nov 2026)**: Pengembangan API Express.js (CRUD stok & rekonsiliasi), pembuatan halaman Front-End (Vite), serta eksplorasi dan pelatihan model Machine Learning.
* **Minggu 3 (13 – 19 Nov 2026)**: Integrasi modul AI dengan REST API Express.js, visualisasi grafik prediksi stok di dashboard, dan pengujian alur utama MVP.
* **Minggu 4 (20 – 26 Nov 2026)**: *System Integration Testing*, UAT, perbaikan *bug*, penyusunan dokumen *User Manual*, serta demonstrasi dan feedback ke Kepala Toko Ayam Gepuk Bandar.

---

## 📄 Lisensi & Hak Cipta

Proyek ini dikembangkan untuk keperluan akademik dan penerapan langsung pada UMKM mitra dalam rangkaian program **Asah 2026 (Dicoding & GoTo)** oleh **Tim A26-CS192**.
