# Jumbara PMR — Aplikasi Digitalisasi Jumpa Bakti Gembira

Aplikasi PWA mobile-first untuk mendigitalkan alur Jumbara PMR: pendaftaran kontingen, penilaian per pos oleh Juri, leaderboard publik, TV live tracking, struk thermal ber-QR ke PDF dinamis, juara per pos, dan juara umum per jenjang.

Dibangun dengan **GitHub Pages + Supabase** (biaya nol untuk skala kegiatan).

## 📚 Dokumentasi

- [Rancangan Lengkap](docs/rancangan.md) — konsep, pengguna, alur, keputusan
- [Skema Database](docs/skema-database.md) — tabel, relasi, RLS
- [Edge Functions](docs/edge-functions.md) — daftar fungsi & tanggung jawab
- [Tema & UI](docs/tema-ui.md) — warna, mode gelap/terang, animasi
- [Alur Cetak Thermal](docs/cetak-thermal.md) — Web Bluetooth & struk
- [Panduan Setup](docs/setup.md) — menjalankan proyek

## ✨ Fitur Utama

- Pendaftaran mandiri kontingen (jenjang → kecamatan → sekolah → akun → kode otomatis).
- Kode kontingen `MU001`/`MA001`/`WI001`; peserta `MU00101`.
- QR peserta per kegiatan untuk scan kehadiran/riwayat.
- Penilaian per komponen (Teori/Praktik) dengan rubrik berbobot.
- Multi-juri fleksibel: `sum`, `average`, `persentase`.
- Auto-final: simpan = final = tayang = cetak.
- Struk thermal + QR ke PDF dinamis.
- Cetak ulang & riwayat penilaian Juri.
- Leaderboard publik & TV: urut kode, tanpa sorting nilai.
- Juara per pos & juara umum per jenjang (internal Admin).
- Mode gelap/terang, warna resmi PMI.
- No hardcode: konfigurasi dari database.

## 👥 Pengguna

| Pengguna | Login | Ringkasan |
| :--- | :---: | :--- |
| Admin | Ya | Kelola event, pos, komponen, rubrik, penugasan Juri, koreksi, laporan |
| Kontingen | Ya | Daftar, tambah peserta, lihat data sendiri |
| Juri | Ya | Hubungkan printer → scan → nilai → simpan → cetak; riwayat |
| Public | Tidak | Leaderboard nilai final, TV live tracking |

> **Android wajib** untuk Juri (Web Bluetooth tidak didukung iOS Safari).

## 🧱 Stack

PWA (React/Vue) + Supabase (Postgres, Auth, Realtime, Edge Functions) + Web Bluetooth + GitHub Pages.

## 📁 Struktur
/app → PWA frontend
/public → Halaman publik & TV
/supabase
/functions → Edge Functions (TypeScript)
/migrations → SQL migrasi
/docs → Dokumentasi
README.md

## 🗺️ Status

- [x] Rancangan konseptual & teknis (v1.3)
- [x] Skema tabel awal + RLS
- [x] Daftar Edge Functions
- [ ] Implementasi migrasi SQL final
- [ ] Edge Functions inti
- [ ] PWA Juri
- [ ] Halaman publik/TV
- [ ] PWA Admin & Kontingen
- [ ] Uji lapangan

## 📜 Lisensi

Internal use — PMR.



