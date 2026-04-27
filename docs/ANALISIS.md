# Analisis Refactor Webstory

## Ringkasan
Proyek asli berupa satu file HTML tunggal dengan CSS, JavaScript, dan gambar base64 yang semuanya tertanam di dalam satu dokumen. Versi baru ini menjaga tampilan dan fungsi utama tetap sama, tetapi struktur dipisahkan agar lebih mudah dibaca, diedit, dan dikembangkan.

## Temuan dari file asli
- File ZIP hanya berisi satu file: `index.html`.
- File `index (2).html` yang diunggah terpisah sama persis dengan `index.html` di dalam ZIP.
- Terdapat 1 blok CSS besar di dalam tag `<style>`.
- Terdapat 1 blok JavaScript besar di dalam tag `<script>`.
- Terdapat 29 gambar base64 di dalam atribut `src`, semuanya sudah diekstrak menjadi file gambar di `assets/images/`.
- CSS memiliki beberapa lapisan redesign berturut-turut, termasuk blok `BRIGHT FOOD EDITORIAL REDESIGN V4`, `V5 CLEAN RESPONSIVE BRIGHT FOOD LAYOUT`, dan `V6 FINAL POLISH`. Ini masih dipertahankan agar tampilan tidak berubah, tetapi bisa dirapikan lebih lanjut jika ingin versi produksi yang lebih kecil.

## Struktur file baru
```text
hidden-cost-webstory-v6-separated/
├── index.html
├── css/
│   └── styles.css
├── js/
│   └── script.js
├── assets/
│   └── images/
│       ├── food-sticker-01.png
│       ├── food-sticker-02.png
│       └── ...
└── docs/
    ├── ANALISIS.md
    └── manifest.json
```

## Perubahan yang dilakukan
- Memindahkan seluruh CSS inline ke `css/styles.css`.
- Memindahkan seluruh JavaScript inline ke `js/script.js`.
- Mengubah `<style>...</style>` menjadi `<link rel="stylesheet" href="css/styles.css" />`.
- Mengubah `<script>...</script>` menjadi `<script src="js/script.js"></script>`.
- Mengekstrak semua gambar base64 menjadi file `.png` di folder `assets/images/`.
- Memperbarui semua atribut `src` agar mengarah ke file gambar lokal.
- Menambahkan dokumentasi proyek dan manifest teknis.

## Catatan kualitas
- File baru lebih ringan untuk diedit karena CSS dan JS sudah terpisah.
- Struktur folder sudah lebih standar untuk proyek web statis.
- Aset gambar tidak lagi memenuhi file HTML, sehingga HTML lebih mudah dibaca.
- CSS masih mengandung beberapa deklarasi ulang variabel karena versi desain lama sampai V6 dipertahankan. Ini aman untuk tampilan, tetapi bisa dioptimasi lagi bila ingin file CSS lebih ramping.

## Cara menjalankan
Buka `index.html` langsung di browser, atau jalankan server lokal sederhana dari folder proyek:

```bash
python3 -m http.server 8000
```

Lalu buka `http://localhost:8000`.
