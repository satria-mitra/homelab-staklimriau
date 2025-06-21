<h1><p align="center">LAPORAN AKSI IMPLEMENTASI</p></h1>
<h2><p align="center"=>PELATIHAN AAWS, AWS & ARG</p></h2>

---

## 1. Informasi Umum

- **Nama Peserta**: Satria Mitra Utama
- **Instansi / UPT BMKG**: Stasiun Klimatologi Riau
- **Nama Pelatihan**: Pelatihan Peralatan AWS dan ARG
- **Topik Aksi Implementasi**: Pengembangan Dashboard Monitoring ALOPTAMA berbasis teknologi terbuka (open-source software) dengan MPNG (MQTT, PostgreSQL, Node-RED, Grafana) stack
- **Tanggal Implementasi**: 23 Juni 2025

## 2. Latar Belakang Singkat

<p align="justify">Stasiun Klimatologi Riau memiliki tugas dalam melakukan pengamatan, pengolahan, analisis, dan penyebarluasan data iklim serta informasi klimatologi secara berkelanjutan. Dalam menunjang pelaksanaan tugas tersebut, diperlukan sistem monitoring yang efisien, real-time, dan mudah diakses untuk memantau kondisi peralatan observasi otomatis seperti ALOPTAMA (AAWS, AWS, dan ARG).
</p>

<p align="justify">Pengembangan dashboard untuk memantau kondisi peralatan ALOPTAMA dapat membantu tugas UPT dalam meningkatkan kualitas dan efektivitas pemantauan data observasi klimatologi secara visual, integratif, dan real-time. Hal ini juga merupakan bentuk dukungan terhadap amanat Undang-Undang Nomor 31 Tahun 2009 tentang Meteorologi, Klimatologi, dan Geofisika, khususnya:</p>

- Pasal 5 ayat (1): BMKG menyelenggarakan pengamatan, pengolahan, analisis, dan penyebarluasan informasi MKG.

- Pasal 7 ayat (2): Dalam pelaksanaan tugasnya, BMKG bertanggung jawab menyediakan informasi MKG secara cepat, tepat, akurat, dan mudah dipahami.

- Pasal 15: Pengamatan MKG harus dilakukan secara berkesinambungan dan sesuai standar yang berlaku.
  
<p align="justify">Pelatihan Teknis Peralatan ARG dan AWS tahun 2025 memberikan wawasan serta keterampilan teknis dalam mengelola dan mengembangkan sistem pengamatan otomatis. Dalam pelatihan ini, teknologi (stack) yang diajarkan dalam membuat sistem monitoring ALOPTAMA adalah Node-RED dan MySQL. Cukup menggunakan kedua software ini, setiap UPT sudah mampu unyuk memiliki sistem pengamatan otomatis yang sesuai standar yang diterapkan oleh UPT percontohan Stasiun Klimatologi Banten. </p> 

<p align="justify">Selanjutnya, dalam pengembangan implementasi pelatihan ini, penulis mengembangkan dashboard monitoring berbasis stack MPNG (MQTT, PostgreSQL, Node-RED, Grafana). Stack ini dipilih karena bersifat FOSS (Free & Open Source Software), ringan, modular, handal, dan dapat dengan mudah di-deploy dan diduplikasi dalam lingkungan jaringan lokal UPT BMKG.
</p>

<p align="justify">Dengan demikian, aksi ini berkontribusi langsung dalam meningkatkan kapasitas operasional dan pelayanan informasi klimatologi berbasis teknologi di UPT.</p>

## 3. Tujuan Aksi Implementasi

- Mengembangkan dashboard monitoring yang dapat menampilkan status operasional dan data observasi dari perangkat ALOPTAMA secara visual, interaktif, dan informatif menggunakan stack MPNG (MQTT, PostgreSQL, Node-RED, Grafana).
- Meningkatkan efisiensi pemantauan kondisi alat observasi otomatis ALOPTAMA secara real-time melalui pemanfaatan protokol MQTT (Message Queuing Telemetry Transport) dan aplikasi FOSS (Free & Open Source Software).
- Mendukung tugas operasional UPT dalam pengolahan dan penyebaran informasi klimatologi, sesuai amanat Undang-Undang No. 31 Tahun 2009 tentang MKG.
- Membangun sistem yang skalabel dan mudah direplikasi di UPT BMKG lainnya sebagai model pengembangan sistem monitoring internal berbasis teknologi terbuka.
  
## 4. Deskripsi Aplikasi

- **Nama Aplikasi**: Dashboard ALOPTAMA berbasis teknologi terbuka dengan stack MPNG
- **Tech stack aplikasi yang digunakan**: Docker, MQTT, PostgreSQL, Node-RED, Grafana



***Fungsi Utama:***

<p align="justify">Aplikasi ini merupakan sistem monitoring untuk memantau kondisi operasional dan data observasi dari peralatan otomatis ALOPTAMA secara real-time. Aplikasi ini dirancang untuk berjalan di lingkungan lokal UPT menggunakan teknologi open-source, serta dapat dengan mudah dikembangkan atau direplikasi oleh unit kerja lainnya.</p>

***Dashboard ini menampilkan:***

- Data realtime dari sensor
- Visualisasi data cuaca (suhu, kelembapan, kecepatan & arah angin, tekanan udara & hujan)
- Peta & warning center status peralatan
- Presentase ketersediaan data harian (data availbility)
- Tegangan dan kondisi baterai

***Penjelasan Setiap Komponen Stack DPNG***

1. [Docker](https://www.docker.com/) – Platform Kontainerisasi.

<p align="justify">Docker digunakan untuk menjalankan seluruh aplikasi dalam bentuk kontainer (isolasi). Memudahkan instalasi, deployment, dan pemeliharaan aplikasi tanpa perlu memikirkan dukungan operating system (OS). Jika suatu kontainer dapat berjalan di suatu PC, maka kontainer yang sama dapat juga berjalan di PC lain yang menggunakan OS yang sama atau bahkan berbeda. </p>

<p align="justify">Seluruh layanan (Grafana, PostgreSQL, Node-RED, Mosquitto MQTT) dijalankan sebagai kontainer terpisah dalam satu virtual Machine (VM) Ubuntu. </p>

2. [MQTT](https://mqtt.org/) - Protokol komunikasi IoT

<p align="justify">MQTT adalah protokol komunikasi ringan dengan sistem publish/subscribe yang dirancang untuk perangkat dengan konektivitas terbatas atau bandwidth rendah — sangat ideal untuk sistem IoT seperti ARG dan AWS. </p>
3. [Node-RED](https://nodered.org/) – Sistem integrasi data

<p align="justify">Digunakan untuk mengatur aliran data dari perangkat AWS/ARG/AAWS yang menggunakan protokol MQTT agar dapat tersimpan ke dalam sistem database. Memungkinkan pemrosesan data (filter, format JSON, injeksi SQL) tanpa perlu coding kompleks. Antarmuka drag-and-drop memudahkan integrasi sensor, logger, atau MQTT ke PostgreSQL.
</p>

3. [PostgreSQL](https://www.postgresql.org/) (dengan ekstensi [TimescaleDB](https://github.com/timescale/timescaledb)) – Time-Series Database

<p align="justify">PostgreSQL dengan ekstensi pengembangan TimescaleDB, adalah database yang dioptimalkan untuk penyimpanan data time-series. Menyimpan data observasi cuaca seperti suhu, kelembapan, tekanan, dan curah hujan secara efisien dengan menggunakan key timestamp. 
Ekstensi TimescaleDB mendukung proses query yang cepat dan performa tinggi untuk jutaan baris data, dibandingkan dengan menggunakan database relational traditional[^1].</p>


4. [Grafana](https://grafana.com/) – Dashboard Visualisasi
   
<p align="justify">Digunakan untuk membuat panel visual yang menampilkan data time-series dari PostgreSQL dalam bentuk angka, grafik, tabel dan indikator. Dashboard dapat dikustomisasi untuk setiap parameter atau peralatan.</p>

***Manfaat Utama Aplikasi***

- Real-time: Monitoring langsung status alat dan data cuaca.
- Open-source: Tanpa lisensi komersial, fleksibel dan gratis.
- Portabel: Bisa dijalankan di laptop, server lokal, atau cloud.
- Visual & Dinamis: Data dapat diolah dan diproses secara cepat oleh operator dan analis.

## 5. Arsitektur Sistem


> Sensor AWS/AAWS/ARG → Publish ke MQTT Broker → Aplikasi (Subscribe) → Visualisasi & Penyimpanan

_Lampirkan diagram jika ada._

---

## 6. Hasil Implementasi di Lapangan

- **Aplikasi diuji coba di lokasi**: ..........................................
- **Data yang berhasil ditampilkan**: Suhu, curah hujan, tekanan udara
- **Aplikasi berjalan stabil selama uji coba ±___ jam**

**Masukan dari rekan kerja/operator:**

> "Aplikasi ini sangat membantu karena kami bisa langsung pantau data dari kantor tanpa harus turun ke stasiun alat."

---

## 7. Tantangan dan Solusi

| Tantangan                                        | Solusi                                                 |
| ------------------------------------------------ | ------------------------------------------------------ |
| Koneksi MQTT terputus saat jaringan tidak stabil | Menambahkan fitur reconnect otomatis                   |
| Visualisasi tidak muncul di browser lama         | Mengganti framework dengan dukungan browser lebih luas |
| Data dari sensor belum sesuai format             | Menambahkan script parsing data sebelum ditampilkan    |

---

## 8. Dampak dan Manfaat

Efisiensi waktu/operator. Kesiapan data real-time untuk early warning. Potensi pengembangan lebih lanjut di UPT. dll

---

## 9. Rencana Tindak Lanjut

Ke depan, aplikasi ini akan diuji lebih lanjut pada dua titik stasiun AWS/AAWS/ARG tambahan dan akan ditingkatkan dengan fitur notifikasi WhatsApp/SMS/Telegram otomatis.

---

## 10. Penutup (Kesimpulan)

Implementasi aplikasi MQTT ini membuktikan bahwa sistem pemantauan AWS/AAWS/ARG dapat dibuat lebih efisien.

Terima kasih kepada fasilitator dan tim penyelenggara pelatihan. Ilmu dan praktik yang diperoleh sangat bermanfaat dan langsung dapat diterapkan di unit kerja kami.

---

## Lampiran

### Dokumentasi Kegiatan  
  _(Lampirkan tangkapan layar aplikasi, kode program, dan dokumentasi kegiatan seperti pelatihan internal atau uji coba lapangan)_


[^1]: https://www.tigerdata.com/blog/time-series-data-why-and-how-to-use-a-relational-database-instead-of-nosql-d0cd6975e87c

---

## 
## Poin-Poin Presentasi

1. Judul & Identitas  
2. Latar Belakang  
3. Tujuan  
4. Fitur Aplikasi  
5. Arsitektur Sistem  
6. Hasil Implementasi  
7. Tantangan & Solusi  
8. Dampak & Manfaat  
9. Rencana Ke Depan  
10. Penutup
