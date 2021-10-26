## Ikhtisar
Konfigurasi SEO adalah fitur yang memecahkan masalah bobot yang salah untuk pencarian nama domain karena perubahan IP yang sering dilakukan oleh CDN setelah nama domain terhubung ke CDN. Dengan mengidentifikasi apakah IP akses menginduk ke mesin pencarian atau tidak, Anda dapat memilih untuk menarik sumber daya secara langsung dari server asal sehingga dapat menjamin stabilitas bobot mesin pencarian.

> !
> - Karena IP mesin pencarian sering berubah, CDN Tencent Cloud hanya dapat menjamin bahwa sebagian besar, tetapi tidak semua, IP mesin pencarian dapat diidentifikasi.
> - Fitur konfigurasi SEO hanya tersedia jika nama domain yang terhubung adalah **milik Anda**. Setelah fitur ini diaktifkan, jika nama domain memiliki beberapa alamat server asal, alamat yang pertama akan menjadi alamat tarik-asal default.

## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Anda akan menemukan konfigurasi SEO di tab **Advanced Configuration (Konfigurasi Lanjutan)**. Ini dinonaktifkan secara default:
![](https://main.qcloudimg.com/raw/44f35a715f922cda12191d50e1cfc723.png)

### Memodifikasi konfigurasi
Anda dapat mengalihkan switch untuk mengaktifkan atau menonaktifkan konfigurasi SEO:
![](https://main.qcloudimg.com/raw/8ea737dbd456397286f3ef8ff965aaf2.png)

>! Fitur konfigurasi SEO saat ini tidak tersedia di wilayah di luar Tiongkok Daratan. Jika wilayah akselerasi nama domain Anda berada di luar Tiongkok Daratan, fitur ini tidak dapat diaktifkan. Jika nama domain Anda dikonfigurasi untuk akselerasi global, konfigurasi SEO hanya akan diterapkan di Tiongkok Daratan.

