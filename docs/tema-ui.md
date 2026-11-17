# Tema & UI

## Warna Resmi PMI

| Nama | RGB | Penggunaan |
| :--- | :--- | :--- |
| Merah PMI | `rgb(226, 10, 22)` | Tombol utama, navigasi, penekanan |
| Merah Muda | `rgb(235, 83, 92)` | Hover, grafik sekunder |
| Merah Muda Terang | `rgb(244, 167, 162)` | Label, area nonaktif |
| Merah Muda Pucat | `rgb(253, 231, 232)` | Latar belakang (mode terang) |
| Putih | `rgb(255, 255, 255)` | Kartu, teks di tombol merah |
| Hitam | `rgb(0, 0, 0)` | Teks utama |

**Logo**: palang merah latar putih; tidak di latar berwarna lain; mode gelap → kartu putih.

## Mode Gelap/Terang

- Deteksi `prefers-color-scheme` + sakelar manual (`localStorage`).
- Merah PMI dipertahankan; latar & teks dibalik.
- Kontras WCAG AA (≥4.5:1).
- Pratinjau struk selalu terang.

## Animasi

- Transisi 150–200ms, `ease-out`.
- Target sentuh ≥44×44px.
- Animasi sukses ≤300ms, tidak berulang.

## CSS Variables (contoh)

```css
:root {
  --pmi-red: rgb(226,10,22);
  --bg: rgb(253,231,232);
  --card: #fff;
  --text: #000;
}
@media (prefers-color-scheme: dark) {
  :root {
    --bg: rgb(18,18,18);
    --card: rgb(30,30,30);
    --text: #f0f0f0;
  }
}
