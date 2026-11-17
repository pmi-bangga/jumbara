Dokumentasi Rancangan Aplikasi Jumbara PMR
Versi: 1.3
Platform: PWA Mobile-First (Android wajib)
Stack: GitHub + Supabase (biaya nol)
Perubahan dari 1.2: Tambah juara per pos (peringkat kontingen di satu pos, per jenjang, dengan tiebreaker per pos), dihitung on-demand di laporan Admin; tidak ditampilkan di leaderboard publik.

1. Ringkasan Proyek
Aplikasi Jumbara PMR mendigitalkan alur Jumpa Bakti Gembira: pendaftaran mandiri kontingen, penilaian per pos oleh Juri, leaderboard publik tanpa sorting berbasis kode, TV live tracking di aula, struk thermal ber-QR ke PDF dinamis per pos, juara per pos, serta juara umum per jenjang berbasis prioritas urutan pos.
Prinsip utama:
Mobile-first, Android wajib.
Biaya nol (GitHub Pages + Supabase Free Plan).
No hardcode: konfigurasi dinamis dari database.
Publik tanpa login; Juri/Kontingen/Admin login.
Simpan nilai = final = tayang publik = cetak struk.
PDF hasil tidak disimpan sebagai file statis; dibuat saat diakses.

2. Pengguna & Hak Akses
Pengguna
Login
Hak Akses
Admin
Ya
Set tahun Jumbara & jenjang aktif; kelola pos, komponen pos, rubrik, penugasan Juri (per komponen), setting pos (metode gabung, timer/bidak, tiebreaker, prioritas urutan); impor master kecamatan/sekolah (CSV); cetak QR peserta per kegiatan; pemantauan; koreksi nilai (alasan wajib + audit); laporan (termasuk juara per pos dan juara umum); pengaturan tampilan publik/TV.
Kontingen
Ya
Daftar mandiri (jenjang → kecamatan → sekolah → username/password → kode otomatis); login; tambah peserta; lihat data sendiri (peserta, status, jadwal, nilai final kontingennya).
Juri
Ya
Hanya data sendiri dan penugasan (per komponen); wajib menghubungkan printer sebelum menilai; scan QR peserta (kehadiran/riwayat); input nilai per rubrik di komponennya; input timer/bidak jika dibutuhkan; simpan = final + tayang + cetak; cetak ulang struk; riwayat penilaian; tidak melihat nilai Juri lain.
Public
Tidak
Leaderboard nilai final, urut kode kontingen (MU→MA→WI, hanya jenjang aktif), tanpa sorting nilai; identitas kode; aktif sejak lomba dimulai; TV live tracking di aula. Tidak menampilkan juara per pos maupun juara umum.


3. Pendaftaran & Kode
Alur kontingen: pilih jenjang → pilih kecamatan → pilih sekolah (dari master CSV) → buat username/password → kode otomatis → login → tambah peserta.
Kode kontingen: MU001, MA001, WI001 (jenjang + 3 digit urut per jenjang).
Kode peserta: MU00101 (kode kontingen + 2 digit urut peserta).
QR peserta: dibuat per kegiatan (per tahun Jumbara), dicetak Admin.
Data peserta: termasuk tanggal lahir/usia (untuk tiebreaker usia termuda).

4. Pos, Komponen, Rubrik, dan Juri
4.1 Pos dan Komponen
Jumlah pos tak terbatas; Admin menambah pos sesuai kebutuhan.
Cakupan jenjang per pos: daftar jenjang yang dilayani, diatur Admin (fleksibel, bisa semua).
Komponen pos: setiap pos memiliki satu atau lebih komponen (misal: Teori, Praktik). Pos sederhana cukup satu komponen (default).
Bobot komponen: tiap komponen punya bobot persen; total bobot per pos = 100% (divalidasi sistem).
Metode gabung multi-juri di dalam komponen: sum, average, atau persentase (weighted), diatur Admin per komponen.
4.2 Rubrik
Rubrik melekat pada komponen, bukan langsung pada pos.
Tiap rubrik punya bobot dan rentang skor, diatur Admin.
Gabung rubrik → nilai komponen: sum berbobot.
Juri menilai komponen secara utuh (semua rubrik); tidak diizinkan menilai sebagian rubrik dalam satu komponen—jika perlu dipecah, buat komponen terpisah.
4.3 Juri
Juri ditugaskan ke komponen (bukan hanya ke pos).
Juri per komponen: 1, 2, 3, atau lebih.
Metode gabung multi-juri berlaku di level komponen: sum, average, atau persentase.
Jika persentase, bobot per Juri disimpan di penugasan; total bobot per komponen = 100% (divalidasi).
Dua Juri menilai kedua komponen: diizinkan; metode gabung berlaku independen per komponen.
Juri pengganti: nilai lama dipertahankan + audit; perubahan lewat koreksi Admin beralasan.
Penggabungan oleh sistem; Juri tidak melihat nilai Juri lain.
4.4 Timer/Bidak, Tiebreaker, Prioritas
Timer/bidak: hanya untuk komponen/pos yang butuh; diinput Juri; tidak masuk total nilai; terekam, tercetak, dan ditampilkan terpisah.
Tiebreaker per pos: tidak seragam (usia termuda dalam jenjang, timer, bidak, dsb.), diatur Admin dengan urutan kriteria eksplisit.
Prioritas urutan pos: menentukan juara umum; diatur Admin per tahun (semua pos masuk urutan).

5. Alur Penilaian (Auto-Final)
Juri login → wajib menghubungkan printer (printer thermal Bluetooth BLE).
Pilih penugasan (per komponen).
Scan QR peserta → kehadiran/riwayat per peserta tercatat (bebas, tanpa batas jumlah, boleh di beberapa pos).
Input nilai per rubrik di komponennya; input timer/bidak jika berlaku.
Simpan → konfirmasi ringkasan → nilai komponen final.
Nilai pos dihitung saat semua komponen wajib pos tersebut sudah terisi; setelah itu nilai pos tayang ke leaderboard publik + TV.
Sistem otomatis mencetak struk thermal di printer pos: nilai komponen/pos untuk kontingen + QR code → PDF dinamis.
Cetak ulang: Juri dapat mencetak ulang dari riwayat penilaian selama printer terhubung; tidak mengubah nilai.
Riwayat penilaian: daftar penilaian yang pernah disimpan; menampilkan nilai yang diinput Juri tersebut; selama kegiatan aktif; cetak ulang dicatat ringan untuk audit.
Koreksi hanya oleh Admin, alasan wajib, berjejak audit; leaderboard, TV, dan PDF terkait diperbarui.
Catatan: tidak ada draft, tidak ada tombol "Selesai" terpisah; simpan = final = cetak. Validasi ketat + konfirmasi sebelum simpan. Timer menggunakan waktu server (now() Supabase).

6. Output
6.1 Struk Thermal + QR (di tiap pos)
Otomatis tercetak saat simpan komponen; dapat dicetak ulang dari riwayat Juri.
QR menautkan ke endpoint Edge Function yang membuat PDF saat diakses, dengan token acak.
PDF selalu menampilkan data terbaru; koreksi Admin otomatis tercermin.
Isi PDF: kode kontingen, nama pos, nama komponen, daftar kode peserta + nilai per rubrik + nilai komponen, timer/bidak (jika ada), waktu simpan, identitas Juri/komponen. Tanpa sorting.
Pratinjau struk di PWA selalu terang (putih-hitam).
6.2 Leaderboard Publik & TV
Isi: nilai per lomba (pos) dan total mentah per kontingen; timer/bidak ditampilkan terpisah.
Urutan: berdasarkan kode kontingen (MU→MA→WI, hanya jenjang aktif, lalu digit urut).
Tanpa sorting nilai; kontingen tanpa nilai final tetap tampil dengan tanda "—".
Refresh: tiap ada perubahan (Supabase Realtime).
Aktif: sejak lomba dimulai; mode "menunggu nilai final" saat kosong; penanda "terakhir diperbarui".
TV: font besar, kolom sedikit, auto-refresh.
Tidak menampilkan juara per pos maupun juara umum.
6.3 Juara per Pos
Peringkat kontingen di satu pos, berdasarkan nilai pos.
Dihitung per jenjang (kontingen dari jenjang yang dilayani pos tersebut).
Seri diselesaikan dengan tiebreaker per pos (usia termuda dalam jenjang, timer, bidak, sesuai urutan kriteria).
Hanya nilai_pos yang lengkap = true yang dihitung.
Internal Admin; tidak ditampilkan di publik/TV.
Default mengambil peringkat 1–3 per pos per jenjang; dihitung on-demand saat laporan dibuka (tidak disimpan), kecuali Admin ingin arsip.
6.4 Juara Umum & Tiebreaker
Juara umum dihitung per jenjang, berbasis prioritas urutan pos (leksikografis berlapis): bandingkan nilai pos prioritas tertinggi; seri → pos berikutnya.
Tiebreaker dipakai di per pos dan antar pos, sesuai aturan per pos.
Total mentah (publik) dan hasil juara per pos / juara umum (internal Admin) ditampilkan terpisah di laporan Admin.
6.5 Laporan Admin
Rekap nilai per lomba/kontingen (termasuk rincian per komponen).
Juara per pos (per jenjang, peringkat 1–3).
Juara umum per jenjang.
Riwayat peserta (pos yang diikuti, waktu scan).
Tracking siswa tergiat (berdasarkan kehadiran/riwayat).
Laporan per tahun Jumbara (multi-tahun).

7. Arsitektur Teknis
7.1 Stack
Komponen
Teknologi
Frontend
PWA (React/Vue), deploy GitHub Pages
Database
Supabase Postgres
Auth
Supabase Auth (Admin, Juri, Kontingen)
Realtime
Supabase Realtime (TV & leaderboard)
Logika backend
Supabase Edge Functions (TypeScript/Deno)
PDF hasil
Dibuat dinamis oleh Edge Function saat diakses (tidak disimpan di Storage)
Cetak thermal
Web Bluetooth API di PWA (Android Chrome/Edge), printer BLE
QR code
Library JS (qrcode) untuk generate; kamera perangkat untuk scan

7.2 Alur Data
text
[Juri PWA Android] --scan QR, input nilai, Web Bluetooth--> [Supabase Edge Function]
                                                                  |
                                              +-------------------+-------------------+
                                              |                   |                   |
                                       [Postgres]        [Realtime Broadcast]   [PDF dinamis]
                                              |                   |                   |
                                      [Leaderboard/TV]   [Halaman Publik/TV]   [QR → PDF saat diakses]
7.3 Batasan Teknis yang Diakui
Web Bluetooth hanya mendukung BLE, bukan Bluetooth Classic (SPP). Printer harus BLE.
Pemilihan printer harus dipicu interaksi pengguna; tidak bisa otomatis di latar belakang.
iOS Safari tidak mendukung Web Bluetooth → Android wajib.
Supabase Free Plan: proyek dijeda setelah 7 hari tanpa aktivitas; Edge Functions CPU 2 detik → pembuatan PDF dan perhitungan juara harus ringan.
Timer: server mencatat started_at via now(); frontend menghitung selisih.
PDF dinamis: respons sedikit lebih lambat dari file statis, tetapi ukuran PDF struk kecil.

8. Prinsip No Hardcode
8.1 Masuk Database (Dikelola Admin)
Data
Tabel
Tahun Jumbara & jenjang aktif
jumbara
Urutan tampilan jenjang
jenjang
Pos
pos
Komponen pos
komponen_pos
Rubrik per komponen
rubrik
Tiebreaker per pos
tiebreaker_pos
Penugasan Juri (per komponen, bobot_persen)
penugasan_juri
Master kecamatan/sekolah
kecamatan, sekolah
Kontingen & peserta
kontingen, peserta
Nilai & kehadiran
nilai_juri, nilai_komponen, nilai_pos, kehadiran
Koreksi & audit
koreksi
Log cetak ulang
log_cetak_ulang
Pengaturan tema
pengaturan_tema

Tidak ada tabel pdf_hasil — PDF dibuat saat diakses. Juara per pos dan juara umum dihitung on-demand (tidak disimpan), kecuali Admin ingin arsip.
8.2 File Konstanta (Dipusatkan)
Warna brand default PMI (rgb(226,10,22) dll.).
Font brand (Trebuchet MS).
Pola format kode (2+3+2).
Aturan inti: "simpan = final = cetak", "QR per kegiatan", "PDF dinamis".
Label/teks antarmuka (file i18n).
8.3 Environment Variables
SUPABASE_URL, SUPABASE_ANON_KEY (frontend).
SUPABASE_SERVICE_KEY (hanya Edge Functions).
QR_TOKEN_SECRET (HMAC untuk token QR PDF).
Konfigurasi cetak (jika perlu).

9. Tema & UI
9.1 Warna Resmi PMI
Nama
RGB
Penggunaan
Merah PMI
rgb(226, 10, 22)
Tombol utama, navigasi, penekanan
Merah Muda
rgb(235, 83, 92)
Hover, grafik sekunder
Merah Muda Terang
rgb(244, 167, 162)
Label, area nonaktif
Merah Muda Pucat
rgb(253, 231, 232)
Latar belakang halaman (mode terang)
Putih
rgb(255, 255, 255)
Kartu, teks di tombol merah
Hitam
rgb(0, 0, 0)
Teks utama

Aturan logo: palang merah dengan latar putih; tidak diletakkan di latar berwarna lain; dalam mode gelap, logo ditempatkan pada kartu putih.
9.2 Mode Gelap/Terang
Deteksi otomatis via prefers-color-scheme, plus sakelar manual (localStorage).
Warna utama merah PMI dipertahankan di kedua mode; latar belakang dan teks dibalik.
Kontras teks memenuhi WCAG AA (minimal 4.5:1).
Pratinjau struk selalu terang.
9.3 Animasi
Transisi 150–200ms, ease-out.
Tidak berlebihan; target sentuh minimal 44×44px.
Animasi sukses singkat (≤300ms), tidak diulang tanpa henti.

10. Keamanan & Audit
Autentikasi per peran (Supabase Auth); Juri hanya akses penugasan komponennya.
RLS aktif: tabel nilai hanya via Edge Functions/service role; tabel publik read-only untuk anon.
Koreksi wajib alasan + jejak audit (nilai lama, baru, alasan, waktu, siapa).
QR PDF: endpoint Edge Function dengan token HMAC; konten tanpa data pribadi sensitif.
QR peserta: token per kegiatan, dapat dicabut/diperbarui Admin.
Log cetak ulang: waktu, id_juri, id_nilai_juri.

11. Non-Fungsional
Keandalan lapangan: timer berbasis server; cetak ulang jika printer gagal tanpa menggagalkan penyimpanan nilai; halaman TV fetch ulang saat Realtime putus.
Responsivitas TV: pembaruan berbasis event (Realtime), bukan polling.
Kemudahan pakai: target sentuh besar, alur Juri minimal.
Biaya: GitHub Pages gratis; Supabase Free Plan cukup untuk skala Jumbara; Android PWA tanpa biaya distribusi.

12. Struktur Repositori (GitHub)
text
/app          → PWA frontend (Admin, Juri, Kontingen)
/public       → Halaman publik & TV
/supabase
  /functions  → Edge Functions (TypeScript), termasuk generator PDF dinamis & juara-pos
  /migrations → SQL migrasi tabel
/docs         → Dokumentasi ini

13. Keputusan yang Sudah Dikunci
Jenjang aktif dinamis per tahun (bisa hanya Mula, Madya+Wira, atau ketiganya).
Urutan tampilan jenjang: MU → MA → WI (hanya jenjang aktif).
Kode kontingen MU001; kode peserta MU00101.
QR peserta per kegiatan.
Cakupan jenjang per pos diatur Admin.
Pos dapat memiliki satu atau lebih komponen; total bobot komponen per pos = 100%.
Rubrik melekat pada komponen; gabung rubrik → nilai komponen: sum berbobot.
Juri ditugaskan ke komponen; metode gabung multi-juri: sum, average, persentase.
Jika persentase, bobot per Juri di penugasan; total bobot per komponen = 100%.
Nilai pos dihitung saat semua komponen wajib terisi, lalu tayang ke publik/TV.
Timer/bidak: tidak masuk total; terekam, tercetak, ditampilkan terpisah.
Tiebreaker per pos (usia termuda dalam jenjang, timer, bidak), dipakai di per pos dan antar pos.
Juara umum per jenjang, berbasis prioritas urutan pos.
Juara per pos: peringkat kontingen di satu pos, per jenjang, berdasarkan nilai pos, dengan tiebreaker per pos; internal Admin; default peringkat 1–3; dihitung on-demand.
Leaderboard publik: total mentah, urut kode kontingen, tanpa sorting nilai; tidak menampilkan juara per pos/juara umum.
Simpan = final = tayang = cetak; koreksi hanya Admin dengan alasan wajib.
Juri wajib menghubungkan printer sebelum menilai (Web Bluetooth, BLE, Android).
Timer menggunakan waktu server.
Tema: warna resmi PMI, mode gelap/terang, animasi ringan.
No hardcode: konfigurasi dinamis dari database; konstanta brand & aturan inti dipusatkan.
PDF hasil dibuat dinamis saat diakses; QR menautkan ke endpoint Edge Function dengan token.
Juri memiliki fasilitas cetak ulang dan riwayat penilaian.
Juri menilai komponen secara utuh (tidak sebagian rubrik); dua Juri menilai kedua komponen diizinkan; juri pengganti: nilai lama dipertahankan + audit.

14. Langkah Berikutnya
Skema tabel lengkap Supabase (SQL migrasi) + RLS — sudah ada kerangka awal; perlu penyesuaian final.
Daftar Edge Functions beserta tanggung jawab — sudah ada; perlu tambah juara-pos.
Rancangan alur cetak thermal (Web Bluetooth) di PWA.
Rancangan halaman publik/TV + langganan Realtime.
Prototipe alur Juri (hubungkan printer → scan → nilai komponen → simpan → riwayat → cetak ulang).

Dokumen ini adalah acuan konseptual dan teknis awal. Perubahan keputusan harus dicatat sebagai revisi versi.

