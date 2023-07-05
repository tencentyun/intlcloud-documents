### Ikthisar

Instans Cadangan (RI) adalah diskon penagihan yang diterapkan pada penggunaan instans CVM bayar sesuai pemakaian di akun Anda. Instans CVM ini harus sama persis dengan atribut RI yang Anda beli untuk mendapatkan keuntungan dari diskon penagihan selama jangka waktu RI. RI memberi Anda diskon yang signifikan dibandingkan dengan penagihan bayar sesuai pemakaian.
>? 
>- Login ke Tencent Cloud Console dan buka [Kalkulator Harga](https://intl.cloud.tencent.com/pricing/cvm) untuk menanyakan harganya.

>- Saat ini, pembayaran biaya RI tidak dapat dikembalikan.
>
>- Konfigurasi RI tidak dapat diubah setelah pembelian. Diskon penagihan RI tidak lagi berlaku untuk instans yang cocok jika Anda mengubah konfigurasinya.
>
>- Diskon penagihan RI akan tetap berlaku untuk instans CVM yang cocok bahkan setelah instans tersebut menjalankan pematian secara proaktif atau paksa.

#### Atribut

- [Wilayah](https://intl.cloud.tencent.com/document/product/213/6091): lokasi fisik IDC, seperti Silicon Valley.
- [Zona ketersediaan](https://intl.cloud.tencent.com/document/product/213/6091): Tencent Cloud IDC dengan dengan sumber daya listrik dan jaringan independen di wilayah di atas, seperti Silicon Valley Zona 1.
- [Jenis instans](https://intl.cloud.tencent.com/document/product/213/11518): jenis keluarga instans Tencent Cloud CVM, seperti Standar.
- [Spesifikasi](https://intl.cloud.tencent.com/document/product/213/11518): Spesifikasi RI, seperti S4.SMALL. 
- Sistem operasi: OS Linux

> Instans CVM bayar sesuai pemakaian harus sama persis dengan atribut RI untuk mendapatkan manfaat diskon penagihan selama jangka waktu RI.

#### Perbandingan konsep

| Item | RI | Instans bayar sesuai pemakaian |
| -------- | ---------- | ---------- |
| Konsep | Diskon untuk instans bayar sesuai pemakaian.       | Instans yang dibeli menggunakan opsi penagihan [bayar sesuai pemakaian](https://intl.cloud.tencent.com/document/product/213/2179), contohnya, komputer virtual yang sedang berjalan. |
| Penggunaan | RI tidak dapat digunakan secara terpisah; sebagai gantinya, ini hanya dapat digunakan dengan instans bayar sesuai pemakaian yang cocok untuk mengimbangi bagian dari tagihan bayar sesuai pemakaian. | CVM dapat dikelola dan dikonfigurasi secara independen sebagai server web sederhana atau sebagai bagian dari solusi cloud yang tangguh bersama produk Tencent Cloud lainnya. |

#### Batas penggunaan

Untuk memeriksa zona ketersediaan yang mendukung RI, gunakan [DescribeReservedInstancesOfferings](https://intl.cloud.tencent.com/document/product/213/30575) API.

Sistem operasi: saat ini, RI hanya mendukung instans CVM Linux.

Metode pembayaran: ada tiga opsi pembayaran, yaitu **All Upfront** (Lunas di Muka), **Partial Upfront** (Sebagian Di Muka), dan **No Upfront** (Tanpa Pembayaran Di Muka).

Jangka Waktu: 1 tahun(365 hari)

Kuota: setiap pengguna dapat memiliki hingga 20 RI dalam satu zona ketersediaan.
