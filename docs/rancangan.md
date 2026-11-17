# Rancangan Aplikasi Jumbara PMR

**Versi**: 1.3
**Platform**: PWA Mobile-First (Android wajib)
**Stack**: GitHub + Supabase (biaya nol)

## 1. Tujuan

Mendigitalkan alur Jumbara PMR: pendaftaran mandiri kontingen, penilaian per pos oleh Juri, leaderboard publik tanpa sorting berbasis kode, TV live tracking, struk thermal ber-QR ke PDF dinamis, juara per pos, dan juara umum per jenjang berbasis prioritas urutan pos.

**Prinsip**:
- Mobile-first, Android wajib.
- Biaya nol.
- No hardcode: konfigurasi dari database.
- Publik tanpa login.
- Simpan nilai = final = tayang = cetak.
- PDF dibuat dinamis saat diakses.

## 2. Pengguna & Hak Akses

| Pengguna | Login | Hak Akses |
| :--- | :---: | :--- |
| Admin | Ya | Event, pos, komponen, rubrik, penugasan Juri, koreksi (alasan wajib + audit), laporan, pengaturan tampilan. |
| Kontingen | Ya | Daftar mandiri, tambah peserta, lihat data sendiri. |
| Juri | Ya | Penugasan per komponen; wajib hubungkan printer; scan QR; input nilai; simpan = final + cetak; cetak ulang; riwayat. |
| Public | Tidak | Leaderboard nilai final, urut kode, tanpa sorting; TV live tracking. |

## 3. Pendaftaran & Kode

- Alur: jenjang → kecamatan → sekolah → username/password → kode otomatis → login → tambah peserta.
- Kode kontingen: `MU001`, `MA001`, `WI001`.
- Kode peserta: `MU00101`.
- QR peserta per kegiatan.
- Data peserta termasuk tanggal lahir (tiebreaker usia termuda).

## 4. Pos, Komponen, Rubrik, Juri

- Pos tak terbatas; cakupan jenjang per pos diatur Admin.
- Pos punya satu/lebih komponen (Teori/Praktik), bobot total 100%.
- Rubrik melekat pada komponen; gabung rubrik → nilai komponen: sum berbobot.
- Juri ditugaskan ke komponen; metode gabung: sum/average/persentase.
- Juri menilai komponen utuh (tidak sebagian rubrik).
- Dua Juri menilai kedua komponen: diizinkan.
- Juri pengganti: nilai lama dipertahankan + audit.
- Timer/bidak: tidak masuk total; terekam, tercetak, ditampilkan terpisah.
- Tiebreaker per pos: usia termuda (dalam jenjang), timer, bidak.
- Prioritas urutan pos: untuk juara umum.

## 5. Alur Penilaian

1. Juri login → hubungkan printer BLE.
2. Pilih penugasan (komponen).
3. Scan QR peserta → kehadiran/riwayat.
4. Input nilai per rubrik (+ timer/bidak jika ada).
5. Simpan → konfirmasi → final.
6. Nilai pos dihitung saat semua komponen wajib terisi → tayang.
7. Struk thermal tercetak; QR → PDF dinamis.
8. Cetak ulang dari riwayat.
9. Koreksi hanya Admin, alasan wajib, audit.

## 6. Output

- **Struk/PDF**: kode kontingen, pos, komponen, nilai per rubrik + nilai komponen, timer/bidak, waktu, identitas Juri. Tanpa sorting. Pratinjau selalu terang.
- **Leaderboard publik/TV**: nilai per pos + total mentah; urut kode (MU→MA→WI); tanpa sorting nilai; refresh Realtime; aktif sejak lomba dimulai; tidak menampilkan juara.
- **Juara per pos**: per jenjang, berdasarkan nilai pos, tiebreaker per pos, peringkat 1–3, internal Admin, on-demand.
- **Juara umum**: per jenjang, prioritas urutan pos (leksikografis berlapis), tiebreaker.
- **Laporan Admin**: rekap nilai, juara per pos, juara umum, riwayat peserta, tracking tergiat, multi-tahun.

## 7. Keputusan yang Dikunci

1. Jenjang aktif dinamis per tahun.
2. Urutan jenjang MU→MA→WI.
3. Kode kontingen `MU001`; peserta `MU00101`.
4. QR peserta per kegiatan.
5. Cakupan jenjang per pos diatur Admin.
6. Pos punya komponen; bobot total 100%.
7. Rubrik melekat pada komponen; sum berbobot.
8. Juri per komponen; metode sum/average/persentase.
9. Persentase: bobot per Juri; total 100%.
10. Nilai pos tayang saat semua komponen wajib lengkap.
11. Timer/bidak tidak masuk total; terekam & tampil terpisah.
12. Tiebreaker per pos.
13. Juara umum per jenjang, prioritas urutan pos.
14. Juara per pos: per jenjang, nilai pos, tiebreaker, internal Admin, on-demand.
15. Leaderboard publik: total mentah, urut kode, tanpa sorting; tanpa juara.
16. Simpan = final = tayang = cetak; koreksi Admin beralasan.
17. Juri wajib hubungkan printer (BLE, Android).
18. Timer pakai waktu server.
19. Tema resmi PMI, mode gelap/terang, animasi ringan.
20. No hardcode.
21. PDF dinamis via endpoint bertoken.
22. Juri punya cetak ulang & riwayat.
23. Juri menilai komponen utuh; dua Juri dua komponen diizinkan; juri pengganti: nilai lama + audit.
