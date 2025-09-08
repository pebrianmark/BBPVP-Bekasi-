# Riset Scraping Harga Komoditas

## 1. URL Halaman yang Dianalisa
- **Detik** (contoh query beras): `https://www.detik.com/search/searchall?query=beras%20harga%20komoditas`
- **Detik** (umum): `https://www.detik.com/search/searchall?query=<commodity> harga komoditas`
- **Bappebti**: `https://infoharga.bappebti.go.id/harga_komoditi_petani/`

---

## 2. Screenshot Struktur Halaman HTML

### Detik
![Struktur HTML Detik](6878e25c-9647-4d07-90c6-eae954905ed6.png)

### Bappebti
![Struktur HTML Bappebti](e15ee284-fae9-4c73-b68e-9b1f419b9f56.png)

### Detik (kode HTML)
```html
<article class="list-content__item">
  <h3 class="media__title">
    <a href="LINK" dtr-ttl="...">Judul</a>
  </h3>
  <h2 class="media__subtitle">Subjudul</h2>
  <div class="media__date">
    <span>Tanggal / Waktu</span>
  </div>
</article>
```

### Bappebti (kode HTML)
```html
<h5>Daftar harga komoditi ...</h5>
<div class="panel">
  <div class="panel-body">
    <h5>Nama Komoditas</h5>
    <h3>Rp. 10.000</h3>
  </div>
</div>
```

---

## 3. Daftar Selector CSS Potensial

### Detik
- Artikel kontainer: `article.list-content__item`
- Judul: `h3.media__title a`
- Subjudul: `h2.media__subtitle`
- Atribut judul khusus: `h3.media__title a[dtr-ttl]`
- Tanggal/Waktu: `div.media__date span`
- Link artikel: `h3.media__title a[href]`

### Bappebti
- Tanggal update: `h5:contains("Daftar harga komoditi")`
- Panel data komoditas: `.panel`
- Nama komoditas: `.panel-body h5`
- Harga: `.panel-body h3`

---

## 4. Kesimpulan Singkat
- **Detik** memberikan akses ke berita/artikel terkait harga komoditas. Data yang bisa diambil meliputi judul, subjudul, tanggal/waktu, dan link artikel. Namun data ini bersifat informatif (berita), bukan harga aktual.
- **Bappebti** memberikan data harga komoditas langsung dari sumber resmi. Data lebih terstruktur dan relevan untuk analisis harga (ada tanggal update, nama komoditas, dan harga).
- **Contoh hasil nyata**:
  - Dari endpoint **Bappebti** (`/prices?commodity=jagung`) → menghasilkan JSON berisi *tanggal update, nama komoditas (“JAGUNG – TASIKMALAYA”), dan harga (“5.500”)*.
  - Dari endpoint **Detik** (`/prices?commodity=beras`) → menghasilkan JSON berisi daftar artikel terkait harga beras, lengkap dengan *judul berita, subjudul, waktu terbit, dan link sumber*.
- **Perbedaan utama**: hasil Bappebti adalah data harga terukur yang bisa dipakai untuk analisis statistik, sedangkan hasil Detik adalah informasi pendukung berupa berita/tren pasar.
- **Akurasi data**: Bappebti lebih akurat karena dikelola lembaga resmi. Detik bisa dipengaruhi sudut pandang berita/penulisan.
- **Frekuensi update**: Detik lebih sering update karena mengikuti arus berita harian, tapi tidak selalu representatif untuk harga. Bappebti update sesuai periode resmi.
- **Kemudahan scraping**: Struktur Bappebti lebih sederhana, sedangkan Detik butuh filter ekstra karena banyak elemen iklan/atribut lain.
- **Potensi integrasi**: Bappebti cocok sebagai sumber harga valid, sementara Detik bisa dipakai untuk tren berita, sentimen, dan analisis pasar.
- **Keterbatasan**: Jika situs resmi sedang tidak bisa diakses, data alternatif dari Detik bisa membantu, meskipun kualitas dan validitasnya berbeda.
- **Rekomendasi**: Kombinasikan kedua sumber — Bappebti untuk harga aktual dan validasi, Detik untuk insight tambahan tentang isu pasar.
