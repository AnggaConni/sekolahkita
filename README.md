# 🛡️ SekolahAman — DRR & Inspeksi Sarpras

> Aplikasi inspeksi keselamatan sekolah berbasis web — offline-first, mobile-friendly, tanpa instalasi.

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![HTML](https://img.shields.io/badge/Built%20with-HTML%2FJS-orange)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![Leaflet](https://img.shields.io/badge/Maps-Leaflet.js-199900)](https://leafletjs.com/)

---

## 📖 Tentang Proyek

**SekolahAman** adalah sistem inspeksi lapangan Pengurangan Risiko Bencana (DRR) dan Sarana Prasarana (Sarpras) untuk satuan pendidikan. Dirancang untuk digunakan oleh inspektur di lapangan langsung dari perangkat mobile, tanpa perlu koneksi internet saat pengisian data.

Proyek ini terdiri dari dua file HTML mandiri:

| File | Fungsi |
|---|---|
| `sekolahaman.html` | Aplikasi lapangan untuk inspektur (input data, peta GIS, triase gedung) |
| `dashboard.html` | Command center untuk pengawas/dinas (aggregasi data dari Google Sheets) |

---

## ✨ Fitur Utama

### 📱 Aplikasi Lapangan (`sekolahaman.html`)
- **Profil Sekolah** — konfigurasi NPSN, nama, provinsi, dan nama inspektur
- **Entri Inspeksi** — formulir untuk struktur bangunan (kondisi + status listrik) maupun inventaris/aset (jumlah baik vs. rusak)
- **Riwayat Historis** — setiap objek memiliki timeline kondisi dari waktu ke waktu
- **Peta GIS** — gambar area gedung (poligon) atau titik lokasi aset langsung di atas citra satelit
- **Triase Gedung** — kalkulator skor risiko keruntuhan berbasis checklist visual
- **Offline-First** — semua data tersimpan di `localStorage`, tidak perlu server
- **Export / Import JSON** — backup data ke file dan muat ulang di perangkat lain
- **Sinkronisasi ke Google Form** — kirim data ke Google Sheets melalui endpoint `formResponse`
- **Cetak Laporan PDF** — ekspor ringkasan kondisi terkini ke file PDF

### 🖥️ Command Center (`dashboard.html`)
- **Ringkasan Global** — metrik agregat: total sekolah, objek unik, status kritis, total log
- **Peta Persebaran** — visualisasi seluruh objek dari semua sekolah dalam satu peta (Leaflet + ESRI Satellite)
- **Filter Multi-Level** — saring berdasarkan provinsi, sekolah, jenis objek, kondisi, dan auditor
- **Distribusi Kondisi** — progress bar proporsi Aman / Rusak Ringan / Rusak Sedang / Rusak Berat
- **Top Perlu Perhatian** — ranking sekolah berdasarkan jumlah objek bermasalah
- **Timeline Analisis** — riwayat lengkap per objek dengan deteksi tren (membaik / memburuk / stagnan)
- **Deteksi Isu Listrik** — indikator khusus untuk gedung dengan masalah kelistrikan
- **Viewer Foto Bukti** — modal preview foto dengan dukungan link Google Drive

---

## 🚀 Cara Penggunaan

### Setup Cepat

Tidak ada proses build. Cukup buka file HTML di browser.

```bash
# Clone repository
git clone https://github.com/AnggaConni/sekolahkita.git

# Enter project directory
cd sekolahkita

# Run locally
# Open sekolahaman.html for field interface
# Open dashboard.html for centralized dashboard
```

### Alur Penggunaan Lengkap

```
Inspektur di Lapangan                    Pengawas / Dinas
─────────────────────                    ─────────────────
1. Buka sekolahaman.html             →   Buka dashboard.html
2. Isi profil sekolah (sekali)       →   Segarkan data (tarik dari Google Sheets)
3. Entri inspeksi bangunan/aset      →   Filter & analisis per provinsi/sekolah
4. Tandai area/lokasi di peta GIS    →   Lihat peta persebaran kondisi
5. Kirim ke Google Form              →   Review timeline & tren kondisi
6. (Opsional) Cetak laporan PDF      →   Ekspor laporan untuk rapat dinas
```

### Konfigurasi Google Form (Untuk Sinkronisasi)

Buat Google Form dengan field berikut, lalu salin URL `formResponse`-nya:

| Entry ID | Isi |
|---|---|
| `entry.1347795599` | Nama Sekolah |
| `entry.1966222058` | Provinsi |
| `entry.1547462533` | NPSN |
| `entry.1695999318` | Nama Inspektur |
| `entry.598227848` | Data JSON Bagian 1 |
| `entry.2131421782` | Data JSON Bagian 2 |
| `entry.1283761055` | Data JSON Bagian 3 |

Untuk dashboard, update variabel `CSV_URL` di `dashboard.html` dengan URL publikasi Google Sheets (`/pub?output=csv`).

---

## 🛠️ Teknologi

| Library | Versi | Kegunaan |
|---|---|---|
| [Tailwind CSS](https://tailwindcss.com/) | CDN | Styling & layout |
| [Phosphor Icons](https://phosphoricons.com/) | CDN | Ikon UI |
| [Leaflet.js](https://leafletjs.com/) | 1.9.4 | Peta interaktif |
| [Leaflet.draw](https://github.com/Leaflet/Leaflet.draw) | 1.0.4 | Gambar poligon & titik di peta |
| [html2pdf.js](https://github.com/eKoopmans/html2pdf.js) | 0.10.1 | Ekspor PDF |
| [PapaParse](https://www.papaparse.com/) | 5.3.2 | Parse CSV dari Google Sheets |
| ESRI World Imagery | - | Tile citra satelit |

Tidak ada framework JavaScript, tidak ada Node.js, tidak ada proses build.

---

## 📁 Struktur Proyek

```
sekolahaman/
├── sekolahaman.html     # Aplikasi inspeksi lapangan (self-contained)
├── dashboard.html       # Command center monitoring (self-contained)
└── README.md
```

---

## 🗺️ Roadmap

- [ ] Dukungan multi-gedung dalam satu peta (layer toggle)
- [ ] Notifikasi push untuk objek yang belum diupdate >30 hari
- [ ] Export Excel (XLSX) dari dashboard
- [ ] Mode PWA (Progressive Web App) untuk installasi di home screen
- [ ] Autentikasi inspektur berbasis PIN

---

## 🤝 Kontribusi

Kontribusi sangat disambut! Silakan:

1. Fork repositori ini
2. Buat branch baru: `git checkout -b fitur/nama-fitur`
3. Commit perubahan: `git commit -m 'Tambah fitur X'`
4. Push ke branch: `git push origin fitur/nama-fitur`
5. Buka Pull Request

Untuk pelaporan bug atau saran fitur, gunakan [GitHub Issues](../../issues).

---

## 📄 Lisensi

Proyek ini dilisensikan di bawah **GNU General Public License v3.0**.

Anda bebas menggunakan, memodifikasi, dan mendistribusikan ulang perangkat lunak ini, selama setiap turunannya juga dirilis dengan lisensi yang sama. Lihat file [LICENSE](LICENSE) atau kunjungi [gnu.org/licenses/gpl-3.0](https://www.gnu.org/licenses/gpl-3.0) untuk detail lengkap.

```
SekolahAman — Sistem Inspeksi DRR & Sarpras
Copyright (C) 2024  Kontributor SekolahAman

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.
```

---

<p align="center">Dibuat dengan ❤️ untuk keselamatan sekolah Indonesia</p>
