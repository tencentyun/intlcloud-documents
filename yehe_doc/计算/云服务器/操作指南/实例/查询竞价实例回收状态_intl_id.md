
Instans spot dapat diambil alih oleh Tencent Cloud karena alasan harga atau inventaris. Untuk memungkinkan pengguna melakukan operasi kustom sebelum kepemilikan kembali instans, kami menyediakan API untuk memperoleh informasi tentang status kepemilikan kembali melalui mekanisme metadata internal.

## Metadata
Metadata instans mengacu pada data yang relevan dengan sebuah instans. Metadata ini dapat digunakan untuk mengonfigurasi atau mengelola instans operasi. Anda dapat mengakses dan mendapatkan metadata instans melalui sebuah instans. Untuk informasi selengkapnya, lihat [Metadata Instans](http://intl.cloud.tencent.com/document/product/213/4934).


## Menggunakan metadata untuk mendapatkan informasi tentang status kepemilikan kembali instans spot
Untuk mendapatkan informasi tentang status kepemilikan kembali instans spot, Anda dapat mengakses metadata dengan menggunakan alat cURL atau permintaan HTTP GET.
```
curl metadata.tencentyun.com/latest/meta-data/spot/termination-time
```
- Jika informasi berikut ditampilkan, hal ini menunjukkan waktu kepemilikan kembali instans spot.
```
2018-08-18 12:05:33
```
- Jika kode kesalahan 404 ditampilkan, artinya instans bukan instans spot atau kepemilikan kembali belum dipicu.

Untuk informasi selengkapnya, lihat [Metadata Instans](http://intl.cloud.tencent.com/document/product/213/4934).
