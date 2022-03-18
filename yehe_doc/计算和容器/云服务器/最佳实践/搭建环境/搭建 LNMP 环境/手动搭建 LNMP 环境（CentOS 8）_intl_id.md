## Ikhtisar
Lingkungan LNMP adalah arsitektur server situs web yang terdiri dari Nginx, MySQL atau MariaDB, dan PHP yang berjalan di Linux. Dokumen ini menjelaskan cara menyiapkan lingkungan LNMP secara manual di CVM Tencent Cloud.

Untuk mengatur lingkungan LNMP secara manual, pahami perintah umum Linux dan pahami penggunaan dan kompatibilitas versi perangkat lunak yang akan diinstal.

## Perangkat Lunak
Perangkat lunak berikut digunakan untuk membangun lingkungan LNMP.
CentOS adalah distribusi dari sistem operasi Linux. Dokumen ini menggunakan CentOS 8.0 sebagai contoh.
Nginx adalah server web. Dokumen ini menggunakan Nginx 1.18.0 sebagai contoh.
MySQL adalah perangkat lunak database. Dokumen ini menggunakan MySQL 8.0.21 sebagai contoh.
PHP adalah bahasa skrip. Dokumen ini menggunakan PHP 7.4.11 sebagai contoh.

## Prasyarat
CVM Linux diperlukan untuk menyiapkan lingkungan LNMP. Jika Anda belum membeli CVM Linux, lihat [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).

## Petunjuk
### Langkah 1: login ke instans Linux
Lihat [Login ke Instans Linux Menggunakan Metode login Standar](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang lebih nyaman bagi Anda:
- [Login ke Instans Linux melalui Fitur Login Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32502)
- [Login ke Instans Linux melalui Kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Langkah 2: instal dan konfigurasikan Nginx
1. Jalankan perintah berikut untuk menginstal Nginx.
>?Dokumen ini menggunakan penginstalan Nginx 1.18.0 sebagai contoh. Anda dapat melihat [paket penginstalan Nginx](http://nginx.org/packages/centos/8/x86_64/RPMS/?spm=a2c4g.11186623.2.31.557423bfYPMd6u) untuk mendapatkan lebih banyak versi yang kompatibel dengan CentOS 8.
>
```
dnf -y install http://nginx.org/packages/centos/8/x86_64/RPMS/nginx-1.18.0-1.el8.ngx.x86_64.rpm
```
2. Jalankan perintah berikut untuk melihat versi Nginx.
```
nginx -v
```
Jika hasil berikut ditampilkan, ini menunjukkan bahwa Nginx telah berhasil diinstal.
```
nginx version: nginx/1.18.0
```
3. Jalankan perintah berikut untuk memeriksa jalur file konfigurasi Nginx.
```
cat /etc/nginx/nginx.conf
```
`/etc/nginx/conf.d/*.conf` pada bagian item konfigurasi `include` menunjukkan jalur default file konfigurasi Nginx.
4. Jalankan perintah berikut secara berurutan untuk mencadangkan file konfigurasi pada bagian jalur default.
```
cd /etc/nginx/conf.d
```
```
cp default.conf default.conf.bak
```
5. Jalankan perintah berikut untuk membuka file `default.conf`.
```
vim default.conf
```

6. Tekan **i** (i) untuk beralih ke mode edit untuk mengubah file `default.conf`.
  1. Tambahkan “index.php” ke `index` pada bagian `location`, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/32df0b8ba82278cd96cf86152738677e.png)
  2. Hapus awalan `#` dari `location ~ \\.php$` dan ubah item konfigurasi berikut:
    - Ubah `root` ke direktori root situs web Anda. Dokumen ini menggunakan `/usr/share/nginx/html;` sebagai contoh.
    - Ubah `fastcgi_pass` menjadi `unix:/run/php-fpm/www.sock;`. Konfigurasi ini harus sama dengan `listen` di file `/etc/php-fpm.d/www.conf`, karena Nginx diasosiasikan dengan PHP-FPM melalui soket UNIX.
    - Ganti `/scripts$fastcgi_script_name;` setelah `fastcgi_param SCRIPT_FILENAME` dengan `$document_root$fastcgi_script_name;`.
    Hasilnya harus sebagai berikut:
![](https://main.qcloudimg.com/raw/2e4bff09d70399881bfbf995390a58d3.png) 
7. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.
8. Jalankan perintah berikut secara berurutan untuk mengaktifkan Ngnix autostart.
```
systemctl start nginx
```
```
systemctl enable nginx
```

### Langkah 3: instal dan konfigurasikan MySQL
1. Jalankan perintah berikut untuk menginstal MySQL.
```
dnf -y install @mysql
```
2. Jalankan perintah berikut untuk melihat versi MySQL.
```
mysql -V
```
Jika hasil berikut ditampilkan, ini menunjukkan bahwa MySQL telah berhasil diinstal.
```
mysql Ver 8.0.21 untuk Linux di x86_64 (Distribusi sumber)
```
3. Jalankan perintah berikut sebagai konsekuensi untuk mengaktifkan MySQL autostart.
```
systemctl enable --now mysqld
```
```
systemctl status mysqld
```
4. Jalankan perintah berikut untuk menyelesaikan konfigurasi keamanan dan mengatur kata sandi untuk MySQL
```
mysql_secure_installation
```
Lakukan langkah-langkah berikut:
  1. Masukkan `y` dan tekan **Enter** (Enter) untuk memulai konfigurasi.
  2. Pilih kebijakan kata sandi. Sebaiknya gunakan kebijakan kata sandi yang ketat. Masukkan `2` dan tekan **Enter** (Enter).
    - 0: menunjukkan kebijakan yang longgar.
    - 1: menunjukkan kebijakan yang sedang.
    - 2: menunjukkan kebijakan yang ketat.
  3. Tetapkan kata sandi untuk MySQL dan tekan **Enter** (Enter). Kata sandi yang Anda masukkan tidak akan ditampilkan secara default.
  4. Masukkan kembali kata sandi Anda, tekan **Enter** (Enter) dan masukkan `y` untuk mengonfirmasi kata sandi.
  5. Masukkan `y` dan tekan **Enter** (Enter) untuk menghapus pengguna anonim.
  6. Konfigurasikan apakah akan menonaktifkan koneksi jarak jauh ke MySQL:
    - Ya: masukkan `y` dan tekan **Enter** (Enter).
    - Tidak: masukkan `n` dan tekan **Enter** (Enter).
  7. Masukkan `y` dan tekan **Enter** (Enter) untuk menghapus pustaka pengujian dan izin aksesnya.
  8. Masukkan `y` dan tekan **Enter** (Enter) untuk memuat ulang tabel otorisasi.

### Langkah 4: instal dan konfigurasikan PHP
1. Jalankan perintah berikut secara berurutan untuk menambahkan dan memperbarui repositori EPEL.
```
dnf -y install epel-release
```
```
dnf update epel-release
```
2. Jalankan perintah berikut secara berurutan untuk menghapus paket perangkat lunak yang tidak diperlukan dalam cache dan memperbarui repositori perangkat lunak.
```
dnf clean all
```
```
dnf makecache
```
3. Jalankan perintah berikut untuk menginstal repositori REMI.
>?Lewati langkah ini jika Anda menginstal PHP versi selain 7.4.11.
>
```
dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
```
4. Jalankan perintah berikut untuk memulai komponen PHP 7.4.
```
dnf module install php:remi-7.4
```
5. Jalankan perintah berikut untuk menginstal komponen PHP yang diperlukan.
```
dnf install php php-curl php-dom php-exif php-fileinfo php-fpm php-gd php-hash php-json php-mbstring php-mysqli php-openssl php-pcre php-xml libsodium
```
6. Jalankan perintah berikut untuk melihat versi PHP.
```
php -v
```
Jika hasil berikut ditampilkan, ini menunjukkan bahwa PHP telah berhasil diinstal.
```
PHP 7.4.11 (cli) (built: Sep 29 2020 10:17:06) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Zend OPcache v7.4.11, Copyright (c), by Zend Technologies
```
7. Jalankan perintah berikut untuk membuka file `www.conf`.
```
vi /etc/php-fpm.d/www.conf
```
8. Tekan **i** (i) untuk beralih ke mode edit dan memodifikasi file `www.conf `.
9. Ubah `user = apache` menjadi `user = nginx` dan `group = apache` menjadi `group = nginx`, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/ceb9c202ebe56c9bd9265e86c0ad2333.png)
10. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.
4. Jalankan perintah berikut secara berurutan untuk memulai PHP-FPM dan mengaktifkan PHP-FPM autostart.
```
systemctl start php-fpm
```
```
systemctl enable php-fpm
```

## Memverifikasi Konfigurasi Lingkungan
1. Jalankan perintah berikut untuk membuat file pengujian.
>? Dokumen ini menggunakan `/usr/share/nginx/html` yang Anda konfigurasikan untuk direktori root situs web Anda di Nginx sebagai contoh.
>
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Masukkan URL berikut di browser Anda dan verifikasi apakah lingkungan telah berhasil dikonfigurasi. Untuk informasi selengkapnya tentang cara mendapatkan alamat IP publik instans, lihat [Mendapatkan Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/17940).
```
http://Public IP alamat instans CVM/index.php
```
Jika hasil berikut muncul, artinya lingkungan telah berhasil dikonfigurasi.
![](https://main.qcloudimg.com/raw/182c0f73df20d66216a9b73d571b2093.png)

## Operasi yang Relevan
Setelah lingkungan LNMP dibangun, Anda dapat [membangun situs web WordPress secara manual](https://intl.cloud.tencent.com/document/product/213/8044) untuk mempelajari CVM dan fiturnya.

## Pertanyaan Umum

Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah yang diperlukan:

- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Port](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).

