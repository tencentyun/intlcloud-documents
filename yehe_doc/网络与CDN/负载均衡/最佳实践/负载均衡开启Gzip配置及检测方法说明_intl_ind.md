Untuk instance **CLB jaringan publik atau CLB jaringan publik dengan IP tetap**, kompresi Gzip diaktifkan untuk protokol **HTTP dan HTTPS** secara default.Fitur-fitur Gzip mengompres situs web sehingga mengurangi volume data secara efektif dalam transmisi jaringan dan mempercepat akses peramban klien.Perhatikan hal-hal berikut:

### Catatan

- **Anda harus mengaktifkan kompresi Gzip pada instance CVM yang sinkron**
Untuk kontainer layanan Nginx umum, Anda harus mengaktifkan Gzip di file konfigurasinya (nginx.conf secara default) dan memulai ulang layanannya
```
gzip on;
```
- **Saat ini, berikut adalah jenis-jenis file yang didukung oleh CLB.Anda dapat menentukan jenis file untuk kompresi di item konfigurasi gzip_types **
```
application/atom+xml application/javascript application/json application/rss+xml application/vnd.ms-fontobject application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/svg+xml image/x-icon text/css text/plain text/x-component;
```
>!Anda harus mengaktifkan sinkronisasi Gzip untuk jenis file di atas di perangkat lunak bisnis instance CVM CLB.
- **Permintaan klien harus berisi pengidentifikasi permintaan kompresi**
Untuk mengaktifkan kompresi Gzip, permintaan klien harus berisi pengidentifikasi berikut:
```
Accept-Encoding: gzip,deflate,sdch
```

### Contoh pengaktifan Gzip di Instance CVM

Contoh lingkungan runtime CVM:Debian 6

1.Gunakan Vim untuk membuka file konfigurasi Nginx berdasarkan path user:
```
vim /etc/nginx/nginx.conf
```
2.Temukan kode berikut:
```
gzip on;
gzip_min_length 1k;
gzip_buffers 4 16k;
gzip_http_version 1.1;
gzip_comp_level 2;
gzip_types text/html application/json;
```
Deskripsi sintaks kode di atas:
- gzip: petunjuk untuk mengaktifkan atau menonaktifkan modul Gzip.
Sintaks: `gzip on/off`
Lingkup: http, server, lokasi
	
- gzip_min_length: menetapkan jumlah byte minimum ketika mengompres halaman.Jumlah byte dapat dilihat di Content-Length pada header HTTP.Nilai default-nya adalah 1k.
Sintaks: `gzip_min_length length`
Lingkup: http, server, lokasi
	
- gzip_buffers: menetapkan unit buffer untuk menyimpan aliran data hasil kompresi Gzip. 16k berarti sebanyak 16k digunakan sebagai unit, dan memori 4 kali lebih besar dari ukuran data asli (dalam 16k) akan diterapkan.
Sintaks: `gzip_buffers number size`
Lingkup: http, server, lokasi
	
- gzip_http_version: menetapkan versi HTTP terendah yang dapat menggunakan Gzip.Configure HTTP/1.0 berarti versi HTTP terendah yang membutuhkan Gzip adalah 1.0 sehingga Gzip dapat kompatibel dengan HTTP/1.1 atau versi lebih tinggi.Ini tidak perlu diubah karena Tencent Cloud mendukung HTTP/1.1 di seluruh jaringan.
Sintaks: `gzip_http_version 1.0 | 1.1;`
Lingkup: http, server, lokasi

- gzip_comp_level: menetapkan rasio kompresi Gzip dengan rentang nilai: 1–9. Angka 1 adalah rasio kompresi terkecil dengan kecepatan pemrosesan paling cepat, sementara angka 9 adalah rasio kompresi terbesar dengan kecepatan pemrosesan paling lambat (transmisi cepat dengan tingkat konsumsi CPU tinggi).
Sintaks: `gzip_comp_level 1..9`
Lingkup: http, server, lokasi

- gzip_types: menunjukkan jenis Ekstensi Surat Internet Multiguna (Multipurpose Internet Mail Extensions/MIME) untuk kompresi, dan jenis "text/html" akan dikompres secara default.Selain itu, Gzip untuk Nginx tidak mengompres file sumber daya statis, seperti JavaScript dan gambar, secara default.Anda dapat mengonfigurasi gzip_types untuk menentukan jenis MIME yang ingin dikompres.Jenis yang tidak ditentukan tidak akan dikompres.**Misalnya, untuk mengompres data dalam format JSON, Anda perlu menambahkan application/json ke kalimat ini**
Berikut adalah jenis yang didukung:
```
text/html text/plain text/css application/x-javascript text/javascript application/xml
```
Sintaks: `gzip_types mime-type [mime-type ...]`
Lingkup: http, server, lokasi

3.Untuk memodifikasi konfigurasi, simpan dan tutup file, buka direktori file bin Nginx, dan jalankan perintah berikut untuk memuat ulang Nginx:
```
./nginx -s reload
```
4.Gunakan perintah curl untuk melihat apakah Gzip telah berhasil diaktifkan:
```
curl -I -H "Accept-Encoding: gzip, deflate" "http://cloud.tencent.com/example/"
```
