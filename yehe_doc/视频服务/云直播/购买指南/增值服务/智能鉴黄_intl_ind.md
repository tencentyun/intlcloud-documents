CSS menyediakan deteksi pornografi. Karena CSS perlu mengambil tangkapan layar dalam streaming langsung untuk mendeteksi konten pornografi, penggunaan deteksi pornografi akan dikenai [biaya deteksi pornografi](#check_price) dan [biaya tangkapan layar](https://intl.cloud.tencent.com/document/product/267/39606). Deteksi pornografi adalah fitur berbayar dan **dikenai tagihan berdasarkan total jumlah tangkapan layar deteksi pornografi yang diambil selama bulan yang dimaksud**.

### Catatan

- Deteksi pornografi dinonaktifkan secara default dan dapat diaktifkan di konsol.
- Tangkapan layar yang dihasilkan disimpan di COS dan akan dikenai biaya penyimpanan COS. Untuk informasi selengkapnya, silakan pelajari [COS Pricing (Harga COS)](https://intl.cloud.tencent.com/pricing/cos).
- Deteksi pornografi adalah fitur berbayar. **Setiap bulan, 1.000 tangkapan layar deteksi pornografi pertama yang diambil tidak akan dikenai biaya. Biaya akan dikenakan untuk tangkapan layar yang diambil setelahnya**.



[](id:check_price)

### Harga


| Tangkapan Layar Deteksi Pornografi | Harga (USD/Ribu tangkapan layar) | Catatan |
| -------- | --------------- | ------------------------ |
| ≤ 1000 |0 | Sebanyak 1.000 tangkapan layar pertama setiap bulan tidak dikenai biaya |
|＞ 1000|0,2294| Total jumlah tangkapan layar akan dibulatkan ke atas hingga 1.000 terdekat |

>? 
>- Untuk tangkapan layar yang disimpan dalam [COS](https://intl.cloud.tencent.com/document/product/436/6222) di luar Tiongkok Daratan, biaya akan dikenakan untuk tambahan lalu lintas downstream jaringan publik. Untuk perincian harga berbagai item COS spesifik yang dapat dikenai tagihan, silakan baca [COS Pricing (Harga COS)](https://buy.cloud.tencent.com/price/cos/overview).
>- Untuk informasi seputar wilayah yang mendukung penyimpanan tangkapan layar langsung, silakan baca [Service Region (Wilayah Layanan)](https://intl.cloud.tencent.com/document/product/267/38285).

[](id:description)

### Ikhtisar Penagihan

- Item yang dapat dikenai tagihan: jumlah tangkapan layar untuk deteksi pornografi.
- Mode penagihan: bayar sesuai pemakaian.
- Siklus penagihan: siklus penagihan bulanan. Tagihan bulan berjalan akan dibuat antara tanggal 1 dan 5 bulan berikutnya. Silakan baca laporan penagihan aktual Anda untuk keterangan detail.
- Aturan penagihan: biaya dihitung dengan mengalikan total jumlah tangkapan layar (dengan pengurangan 1.000 tangkapan layar gratis pertama) yang diambil dalam satu bulan kalender untuk deteksi pornografi dan harga unit.

[](id:example)

### Contoh Penagihan

Misalnya, Anda menggunakan layanan deteksi pornografi dari 1 Januari hingga 1 Februari 2021, dan total 168.000 tangkapan layar untuk deteksi pornografi dibuat selama bulan tersebut. Biaya deteksi pornografi yang harus Anda bayar pada 2 Februari 2021 adalah sebagai berikut:
Biaya deteksi pornografi untuk Januari = 0,2294 (USD/Ribu tangkapan layar) × (168 - 1) Ribu tangkapan layar = 38,3098 USD.
