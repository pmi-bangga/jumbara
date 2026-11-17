# Panduan Setup

## Prasyarat

- Node.js 18+
- Akun Supabase (Free Plan)
- Akun GitHub
- Android + printer thermal BLE (uji cetak)

## Langkah

1. Clone repo:
   ```bash
   git clone https://github.com/<username>/<repo>.git
   cd <repo>
   Supabase:

Buat proyek.

Jalankan migrasi SQL di supabase/migrations.

Aktifkan Realtime untuk nilai_pos, nilai_komponen.

Salin SUPABASE_URL, SUPABASE_ANON_KEY.

Environment frontend (.env):

text
VITE_SUPABASE_URL=...
VITE_SUPABASE_ANON_KEY=...
Secret Edge Functions:

text
SUPABASE_SERVICE_KEY=...
QR_TOKEN_SECRET=...
Jalankan frontend:

bash
cd app
npm install
npm run dev
Deploy:

Frontend: push ke main → GitHub Actions → GitHub Pages.

Edge Functions: supabase functions deploy.

Uji Cetak
Buka PWA di Android Chrome.

Hubungkan printer BLE.

Simpan nilai uji → pastikan struk tercetak & QR mengarah ke PDF.
