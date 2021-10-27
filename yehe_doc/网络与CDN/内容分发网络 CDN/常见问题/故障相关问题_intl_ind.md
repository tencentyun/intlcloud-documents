### Apa yang harus saya lakukan jika kesalahan 423 dilaporkan di CDN?
Kode status 423 adalah kode status khusus Tencent Cloud CDN.CDN akan melaporkan kesalahan 423 jika mendeteksi permintaan loopback.Kami sarankan Anda memeriksa hal berikut:
1.Periksa server asal yang dikonfigurasikan di [Konsol CDN](https://console.cloud.tencent.com/cdn).Jika server asal Anda juga merupakan nama domain akselerasi Tencent Cloud CDN, hal itu dapat menyebabkan permintaan loopback.
2.Jika server asal Anda dikonfigurasikan dengan pengalihan HTTP 301/302 ke HTTP dan ikuti 301/302 diaktifkan di Konsol CDN, kesalahan 423 bisa terjadi.Kami sarankan Anda menonaktifkan ikuti 301/302.
>!Catatan: Jika Anda menggunakan metode ini, kami sarankan Anda mengaktifkan konfigurasi HTTPS untuk memaksa pengalihan HTTPS dan mengubah metode tarik-asal menjadi ikuti protokol.Jika tidak, pengalihan ganda bisa terjadi.Untuk prosedur konfigurasi, silakan lihat [Panduan Konfigurasi Akselerasi HTTPS](https://intl.cloud.tencent.com/document/product/228/35213).

### Apa yang harus saya lakukan jika kode status 514 dikembalikan di CDN?

Ini disebabkan oleh batas akses IP yang dikonfigurasikan di Konsol CDN seperti diperlihatkan di bawah ini:
![](https://main.qcloudimg.com/raw/6422e6288811635c64052ab8daa389fc.png)

>? 
> - Batas akses IP dirancang untuk membatasi lama waktu IP diizinkan untuk mengakses suatu simpul dalam satu detik.Jika batas tersebut terlewati, kesalahan 514 akan dikembalikan.
> - Pengaturan batas yang rendah dapat memengaruhi penggunaan bisnis Anda oleh pengguna normal frekuensi tinggi.Karena itu, silakan atur ambang batas yang wajar.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Batas Akses IP](https://intl.cloud.tencent.com/document/product/228/6420).

### Apa yang harus saya lakukan jika kode status 404 dikembalikan oleh nama domain CDN?
Periksa hal berikut ini:
1.Periksa apakah server asal dapat diakses secara normal.
2.Periksa apakah informasi server asal dan domain asal telah diubah di Konsol CDN.Ini dapat menyebabkan kesalahan 404 saat tarik-asal.


### Apakah CDN mendukung perpindahan ke non-tarik-asal secara otomatis dan mengembalikan konten yang ter-cache pada simpul jika terjadi kelainan server asal?
Jika terjadi kelainan server asal, jika cache pada simpul CDN yang diakses oleh permintaan pengguna belum kedaluwarsa, simpul tersebut akan langsung mengembalikan konten yang diminta kepada klien.Jika cache sudah kedaluwarsa, simpul tersebut tidak akan merespons dan permintaan tarik-asal akan dimulai.
