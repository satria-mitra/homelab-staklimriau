# 🚀 Dashboard Monitoring ALOPTAMA – Staklim Riau

Dashboard monitoring berbasis teknologi terbuka untuk pemantauan real-time peralatan ALOPTAMA (AAWS, AWS, ARG) di UPT Stasiun Klimatologi Riau. Dibangun menggunakan stack **MPNG**: **MQTT**, **PostgreSQL**, **Node-RED**, dan **Grafana**, serta dikelola dengan **Docker Compose** untuk kemudahan deployment dan replikasi.


Saat ini berjalan di Ubuntu VM dengan spesifikasi RAM 10 GB, 2 Core CPU dan 20GB local disk.

Adapun hardware Proxmox berjalan diatas mesin HPE ProLiant DL380 Gen10. Intel Xeon @2.1Ghz 16 Core, 16GB RAM, 2x300GB HDD Hardware RAID1 Controller

---

## 📂 Struktur Repositori

```
homelab-staklimriau/
├── apps/                # Seluruh aplikasi berjalan dalam container
│   ├── grafana/
│   ├── postgres/
│   ├── nodered/
│   └── mosquitto/
├── docs/                # Laporan aksi implementasi dan dokumentasi pendukung
│   └── laporan_implementasi.pdf
├── .env                 # Variabel lingkungan (tidak disertakan di Git)
├── docker-compose.yml  # File utama untuk deployment Docker Stack
└── README.md
```

---

## 🧰 Tech Stack

- **Docker & Docker Compose** – Menjalankan seluruh layanan dalam container
- **MQTT (Mosquitto)** – Protokol komunikasi data observasi dari perangkat
- **Node-RED** – Integrasi aliran data dari sensor ke database
- **PostgreSQL + TimescaleDB** – Penyimpanan time-series untuk data klimatologi
- **Grafana** – Visualisasi data observasi dalam bentuk dashboard interaktif
- **Portainer** *(opsional)* – UI untuk memantau container Docker
- **pgAdmin** *(opsional)* – UI manajemen PostgreSQL

---

## 📦 Cara Instalasi & Penggunaan

### 🔧 1. Prasyarat

Pastikan Anda telah menginstal:
- Docker & Docker Compose
- Git
- VM Ubuntu (minimal 2 vCPU, 8 GB RAM)

### 📥 2. Clone Repository

```bash
git clone https://github.com/username/homelab-staklimriau.git
cd homelab-staklimriau
```

### ⚙️ 3. Konfigurasi `.env` (opsional)

Buat file `.env` di setiap directory aplikasi. Lihat `docker-compose.yml` untuk meliahat konfigurasi file .env\
Contoh file .env :

```env
POSTGRES_USER=yourusername
POSTGRES_PASSWORD=yourpassword
```

### 🚀 4. Jalankan Stack

Contoh menjalankan Node-Red

```bash
docker compose -f apps/nodered/docker-compose.yml up -d
```

Layanan akan berjalan dengan port default:
- Grafana → `http://localhost:3000`
- Node-RED → `http://localhost:1880`
- PostgreSQL → `localhost:5432`
- MQTT Broker → `localhost:1883`

---

## 🔁 Duplikasi / Replikasi

Untuk menduplikasi sistem ini di lingkungan UPT lain:

1. Fork atau clone repo ini ke server lokal Anda.
2. Edit `docker-compose.yml` dari setiap directory aplikasi
3. Tambahkan file `.env` pada setiap folder directory dan tambahkan konfigurasi berdasarkan file `docker-compose.yml`
4. Jalankan dan modifikasi flow Node-RED sesuai kebutuhan lokal.
5. Gunakan jaringan VLAN atau LAN internal untuk konektivitas perangkat.
6. Dokumentasi lebih lanjut tersedia di folder [`docs/`](./docs).

---

## 📄 Laporan Implementasi

Dokumen aksi implementasi dan presentasi tersedia di:

> 📁 [`docs/laporan_implementasi.pdf`](./docs/laporan.pdf)

> 📁 [`docs/laporan_implementasi.pdf`](./docs/presentasi.pptx)


Berisi latar belakang, tujuan, arsitektur, hasil uji coba, dan rencana tindak lanjut pengembangan dashboard ALOPTAMA.

---

## 🛠 Contoh Arsitektur Sistem

![Network Architecture](./docs/assets/network_architecture.svg)
<p align="center"><em>Diagram Arsitektur Jaringan Virtual dan Docker</em></p>

---

## 📬 Kontak & Kredit

Pengembang: **Satria Mitra Utama**  
Instansi: **Stasiun Klimatologi Riau**  
Email: satriamitrautama@gmail.com




