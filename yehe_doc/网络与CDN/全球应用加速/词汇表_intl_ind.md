

### Koneksi Bersamaan Maks

Ini mengacu pada jumlah maksimum koneksi akses bersamaan yang didukung oleh koneksi GAAP.



### Rekaman CNAME

Rekaman CNAME (Nama Kanonikal) merujuk pada rekaman alias di dalam resolusi nama domain.
Misalnya, sebuah server bernama `host.example.com` memberikan layanan WWW dan MAIL sekaligus. Untuk lebih memudahkan pengguna dalam mengakses layanan tersebut, dua rekaman CNAME (`www.example.com` dan `mail.example.com`) dapat ditambahkan untuk server ini di penyedia layanan DNS-nya sehingga semua permintaan untuk mengakses dua rekaman CNAME ini akan diteruskan ke `host.example.com`.



### GAAP

Untuk informasi selengkapnya, harap lihat [Global Application Acceleration Platform](#GAAP1).



### Pendengar

Pendengar digunakan untuk menyediakan fitur konfigurasi untuk kebijakan penerusan permintaan, termasuk konfigurasi protokol, port, kebijakan penjadwalan di antara beberapa server asal, dan pemeriksaan kesehatan. Permintaan akan diteruskan ke server asal backend sesuai dengan kebijakan yang dikonfigurasi pada pendengar.

### Wilayah Akselerasi

Ini mengacu pada wilayah tempat pengguna berada. Pengguna di wilayah akselerasi dapat mengakses server bisnis di wilayah server asal melalui koneksi akselerasi.



### Global Application Acceleration Platform

Global Application Acceleration Platform (GAAP) Tencent adalah produk PaaS yang mencapai latensi akses global yang optimal. Ini menggunakan koneksi berkecepatan tinggi, penerusan kluster, dan perutean cerdas di antara node global untuk memungkinkan pengguna di berbagai wilayah mengakses node terdekat, sehingga lalu lintas permintaan mereka dapat diteruskan ke server asal, mengurangi keterlambatan akses dan latensi.



### Server Asal

Ini adalah server bisnis pelanggan dan dapat berupa server yang dibuat sendiri atau bucket Tencent Cloud [COS](https://intl.cloud.tencent.com/product/cos).
