# Alur Cetak Thermal (Web Bluetooth)

## Prasyarat

- Android + Chrome/Edge (Web Bluetooth).
- Printer thermal **BLE** (bukan Bluetooth Classic/SPP).
- HTTPS (GitHub Pages sudah).

## Alur

1. Juri login → wajib klik "Hubungkan Printer" → pilih perangkat BLE.
2. Izin diingat browser; kunjungan berikutnya coba reconnect.
3. Scan QR peserta → input nilai → simpan.
4. Edge Function `siapkan-struk` mengembalikan teks struk + URL QR.
5. PWA mengirim perintah cetak ke printer BLE (ESC/POS).
6. QR menautkan ke `pdf-hasil` (PDF dinamis).

## Cetak Ulang

- Dari riwayat penilaian; panggil `cetak-ulang`; cetak ke printer terhubung.
- Tidak mengubah nilai; dicatat di `log_cetak_ulang`.

## Kegagalan

- Jika printer gagal, nilai tetap tersimpan.
- Job cetak dapat diulang dari riwayat.

## Batasan

- Pemilihan printer harus dipicu interaksi pengguna.
- iOS Safari tidak mendukung Web Bluetooth → Android wajib.
- Pratinjau struk selalu terang (putih-hitam).
