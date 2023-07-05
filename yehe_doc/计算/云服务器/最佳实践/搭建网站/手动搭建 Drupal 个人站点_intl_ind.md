## Skenario
Drupal adalah kerangka kerja manajemen konten sumber terbuka dan gratis yang ditulis dalam PHP dan didistribusikan di bawah Lisensi Publik Umum GNU. Drupal menyediakan kerangka kerja back-end untuk setidaknya 2,3% dari semua situs web di seluruh dunia – mulai dari blog pribadi hingga situs perusahaan. Artikel ini menjelaskan cara menyiapkan Drupal secara manual di CVM. 

Untuk menyiapkan situs web pribadi berbasis Drupal secara manual, pahami perintah Linux, seperti [menggunakan YUM untuk menginstal perangkat lunak di CentOS](https://intl.cloud.tencent.com/document/product/213/2046). Anda juga harus memahami penggunaan dan kompatibilitas perangkat lunak.

## Perangkat Lunak
Artikel ini menjelaskan cara menginstal perangkat lunak berikut
- Sistem operasi Linux. Artikel ini menggunakan CentOS 7.6.
- Apache adalah perangkat lunak server web. Artikel ini menggunakan Apache 2.4.6.
- MariaDB adalah sistem manajemen database. Artikel ini menggunakan MariaDB 10.4.8.
- PHP adalah bahasa skrip. Artikel ini menggunakan PHP 7.0.33.
- Drupal adalah kerangka kerja manajemen konten. Artikel ini menggunakan Drupal 8.1.1.


## Prasyarat
Anda memerlukan CVM Linux. Jika Anda belum membelinya, lihat [artikel ini](http://intl.cloud.tencent.com/document/product/213/2936) untuk informasi tentang cara memulai CVM Linux.


## Petunjuk
### Langkah 1 Login ke instans Linux
[Login ke instans Linux menggunakan WebShell (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang nyaman bagi Anda:
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Langkah 2 Menyiapkan LAMP
Setelah login, siapkan LAMP agar Anda dapat menjalankan Drupal. Lihat [artikel ini](https://intl.cloud.tencent.com/document/product/213/34813) untuk mengetahui detailnya.

### Langkah 3 Mengunduh dan menginstal Drupal
1. Jalankan perintah berikut untuk mengunduh paket penginstalan Drupal ke direktori root situs web Anda.
```
cd /var/www/html/
```
```
wget wget http://ftp.drupal.org/files/projects/drupal-8.1.1.zip
```
2. Jalankan perintah berikut untuk mendekompresi paket penginstalan dan mengganti nama direktori.
```
unzip drupal-8.1.1.zip 
```
```
mv drupal-8.1.1/ drupal/
```

### Langkah 4 Mengonfigurasi Drupal 
1. Jalankan perintah berikut untuk membuka file konfigurasi Apache.
```
vi /etc/httpd/conf/httpd.conf
```
2. Tekan **i** (i) untuk masuk ke mode edit. Cari `AllowOverride None` di `Directory "/var/www/html"></Directory>` dan ganti dengan berikut ini:
```
AllowOverride All
```
Hasilnya ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c68f918f22d9c29607d59fe1847eff69.png)
3. Tekan **Esc** (Esq) untuk keluar dari mode edit dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali.
4. Jalankan perintah berikut untuk mengubah izin akses direktori root situs web untuk pengguna `apache`.
```
chown -R apache:apache /var/www/html
```
5. Jalankan perintah berikut untuk melakukan boot ulang pada layanan Apache.
```
systemctl restart httpd
```

#### Mengonfigurasi database untuk Drupal<span id="database"></span>
>Petunjuk cara mengonfigurasi kredensial pengguna MariaDB dapat berbeda-beda tergantung pada versi yang berbeda. Lihat [situs web resmi MariaDB](https://downloads.mariadb.org/) untuk mengetahui detailnya.
>
1. Jalankan perintah berikut untuk masuk ke MariaDB.
```
mysql
```
2. Jalankan perintah berikut untuk membuat database bernama `drupal`.
```
CREATE DATABASE drupal;
```
3. Jalankan perintah berikut untuk membuat `user` pengguna baru dan atur kata sandinya ke `123456`.
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. Jalankan perintah berikut dan berikan `user` semua hak istimewa ke `drupal`.
```
GRANT ALL PRIVILEGES ON drupal.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. Jalankan perintah berikut untuk menerapkan semua konfigurasi.
```
FLUSH PRIVILEGES;
```
6. Jalankan perintah berikut untuk keluar dari MariaDB.
```
\q
```

#### Mengonfigurasi `root`
1.  Jalankan perintah berikut untuk masuk ke MariaDB.
```
mysql
```
2. Jalankan perintah berikut untuk mengatur kata sandi untuk `root`.
>MariaDB 10.4 untuk CentOS sekarang memungkinkan akun `root` untuk login tanpa kata sandi. Jalankan perintah berikut untuk menetapkan kata sandi untuk `root` dan mencatatnya di lokasi yang aman.
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('your_pasword');
```
3. Jalankan perintah berikut untuk keluar dari MariaDB.
```
\q
```

### Langkah 5 Menginstal dan mengonfigurasi Drupal
1. Buka jendela browser di komputer lokal Anda dan kunjungi alamat berikut untuk menginstal Drupal.
```
http://CVM_Public_IP/drupal
```
2. Pilih bahasa pilihan Anda dan klik **Save and continue** (Simpan dan lanjutkan)
3. Pilih **Standard installation** (Penginstalan standar) dan klik **Save and continue** (Simpan dan lanjutkan)
4. Masukkan informasi database yang relevan yang dikonfigurasi di [Mengonfigurasi database untuk Drupal](#database). Klik **Save and continue** (Simpan dan lanjutkan)
>Penginstalan Drupal sekarang akan memeriksa untuk melihat apakah semua kriteria penginstalan terpenuhi. Jika sudah terpenuhi, penginstalan akan dimulai. Jika tidak, pesan kesalahan akan muncul. Selesaikan kesalahan sebelum melanjutkan.
>

5. Halaman konfigurasi dimuat secara otomatis setelah penginstalan selesai. Masukkan informasi dan klik **Save and continue** (Simpan dan lanjutkan)
>Catat nama pengguna dan kata sandi pemeliharaan Anda.
>

6. Beranda Drupal Anda dimuat secara otomatis. Gunakan nama pengguna dan kata sandi pemeliharaan untuk login
Anda sekarang telah berhasil menyiapkan situs web Drupal Anda. Sesuaikan pengalaman Anda dengan keinginan Anda.

## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah berdasarkan situasi aktual Anda.
- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).
