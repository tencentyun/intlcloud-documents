## Ikhtisar Fitur

Anda dapat mengonfigurasi halaman kesalahan khusus, dan mengalihkan permintaan dengan kode status yang ditentukan ke URL yang ditentukan.

Kode status yang saat ini didukung adalah sebagai berikut:
- 4XX: 400, 403, 404, 405, 414, 416, dan 451
- 5XX: 500, 501, 502, 503, dan 504

>! Fitur ini mungkin tidak tersedia di beberapa platform. Kami akan menyelesaikan peningkatan server sesegera mungkin.

## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan alihkan ke tab **Advanced Configuration** (Konfigurasi Lanjutan) untuk menemukan bagian **Custom Error Page Configuration** (Konfigurasi Halaman Kesalahan Khusus).

Konfigurasi halaman kesalahan khusus dinonaktifkan secara default.
![](https://main.qcloudimg.com/raw/ad8f4340f2f7c67247e9730a12e6d27b.png)



### Menambahkan aturan

Anda dapat mengeklik **Add Rule** (Tambahkan Aturan) untuk menambahkan aturan halaman kesalahan khusus sesuai kebutuhan.
![](https://main.qcloudimg.com/raw/7af17d161ec2f4e499a5740383d4658e.jpg)



**Batasan konfigurasi**

- Setiap kode status hanya dapat memiliki satu aturan unik.
- Pengalihan: 301 atau 302.
- URL Tujuan: `http://` atau `https://` diperlukan.
- Konten dapat berisi hingga 1.024 karakter dan karakter bahasa Mandarin tidak didukung.
