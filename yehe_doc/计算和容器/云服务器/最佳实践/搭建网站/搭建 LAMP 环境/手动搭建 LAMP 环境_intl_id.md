## Skenario
LAMP adalah arsitektur layanan web umum yang berjalan di Linux dan terdiri dari Apache, MySQL/MariaDB, dan PHP. Artikel ini menjelaskan cara menyiapkan LAMP di CVM Linux.

Anda harus memahami perintah Linux yang umum, seperti [Menginstal Perangkat Lunak melalui YUM di Lingkungan CentOS](https://intl.cloud.tencent.com/document/product/213/2046), dan memahami versi perangkat lunak yang diinstal.

## Perangkat Lunak
Berikut adalah perangkat lunak yang digunakan:
- CentOS adalah distribusi dari sistem operasi Linux. Kami akan menggunakan versi 7.6 dalam artikel ini.
- Apache adalah perangkat lunak server web. Kami akan menggunakan versi 2.4.6 dalam artikel ini.
- MariaDB adalah sistem manajemen database. Kami akan menggunakan versi 10.4.8 dalam artikel ini.
- PHP adalah bahasa skrip. Kami akan menggunakan versi 7.0.33 dalam artikel ini.

## Prasyarat
Anda memerlukan CVM Linux. Jika Anda belum membelinya, lihat [Memulai CVM Linux](http://intl.cloud.tencent.com/document/product/213/2936).

## Petunjuk
### Langkah 1: Login ke instans Linux
[Login ke instans Linux menggunakan WebShell (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang nyaman bagi Anda:
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke Instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Langkah 2: Menginstal Apache
1. Jalankan perintah berikut untuk menginstal Apache.
```
yum install httpd -y
```
2. Jalankan perintah berikut untuk memulai Apache dan mengaturnya untuk memulai secara otomatis ketika sistem dimulai.
```
systemctl start httpd
```
```
systemctl enable httpd
```
3. Buka jendela browser dan kunjungi URL berikut untuk memverifikasi bahwa Apache berfungsi dengan benar.
```
http://[Alamat IP publik dari instans CVM]
```
Berikut ini akan muncul jika Apache diinstal dengan benar:
![](https://main.qcloudimg.com/raw/f9dc3992f4d6e7e94bb63330fd5cadfe.png)


### Langkah 3: Menginstal MariaDB
1. Jalankan perintah berikut untuk memeriksa apakah MariaDB sudah diinstal.
```
rpm -qa | grep -i mariadb
```
 - Jika muncul hasil berikut, MariaDB sudah terinstal.
 ![](https://main.qcloudimg.com/raw/6fa7fb51de4a61f4da08eb036b6c3e85.png)
Jika demikian, jalankan perintah berikut untuk menghapus MariaDB untuk menghindari konflik antara versi yang berbeda.
```
yum -y remove [Package name]
```
 - Jika tidak ada hasil yang ditampilkan, artinya MariaDB tidak terinstal. Dalam hal ini, lanjutkan ke langkah berikutnya.
2. Jalankan perintah berikut untuk membuat file bernama `MariaDB.repo` pada bagian `/etc/yum.repos.d/`. 
```
vi /etc/yum.repos.d/MariaDB.repo
```
3. Tekan **i** (i) untuk beralih ke mode edit dan masukkan yang berikut ini.
```
# Daftar repositori MariaDB 10.4 CentOS - dibuat 05-11-2019 11:56 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
>Untuk informasi penginstalan versi lain, kunjungi [situs web resmi MariaDB](https://downloads.mariadb.org).
>
5. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali.
6. Jalankan perintah berikut untuk menginstal MariaDB.
```
yum -y install MariaDB-client MariaDB-server
```
7. Jalankan perintah berikut untuk memulai MariaDB dan atur agar mulai secara otomatis saat sistem dimulai.
```
systemctl start mariadb
```
```
systemctl enable mariadb
```
8. Jalankan perintah berikut untuk memverifikasi bahwa MariaDB berhasil diinstal.
```
mysql
```
Jika muncul hasil berikut, artinya MariaDB berhasil diinstal.
![](https://main.qcloudimg.com/raw/bfe9a604457f6de09933206c21fde13b.png)
9. Jalankan perintah berikut untuk keluar dari MariaDB.
```
\q
```

### Langkah 4: Menginstal dan mengonfigurasi PHP
1. Jalankan perintah berikut untuk memperbarui sumber perangkat lunak PHP di Yum.
```
rpm -Uvh https://mirrors.cloud.tencent.com/epel/epel-release-latest-7.noarch.rpm 
```
```
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```
2. Jalankan perintah berikut untuk menginstal paket yang diperlukan untuk PHP 7.0.33.
```
yum -y install php70w php70w-opcache php70w-mbstring php70w-gd php70w-xml php70w-pear php70w-fpm php70w-mysql php70w-pdo
```
3. Jalankan perintah berikut untuk mengedit file konfigurasi Apache.
```
vi /etc/httpd/conf/httpd.conf
```
4. Tekan **i** (i) untuk masuk ke mode edit dan lakukan perubahan berikut:
![](https://main.qcloudimg.com/raw/0b478ca5aa21124a531cfd5c8860cb70.png)
![](https://main.qcloudimg.com/raw/aeeb6fff1af9cf71735cae558455ee94.png)
![](https://main.qcloudimg.com/raw/cc840587150c3282c972a6b23e0c1a68.png)
![](https://main.qcloudimg.com/raw/de36e94d0e4791d1d84f141120125456.png)
 1. Cari `ServerName www.example.com:80` dan mulai baris baru di bawahnya. Masukkan nilai berikut:
 ```
ServerName localhost:80
```
 2. Cari `Require all denied` di `<Directory>` dan ubah ke `Require all granted`.
 3. Cari `<IfModule dir_module>` dan ubah kontennya menjadi `DirectoryIndex index.php index.html`.
 4. Mulai baris baru di bawah `AddType application/x-gzip .gz .tgz` dan masukkan nilai berikut:
```
AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .phps
```
5. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali.
6. Jalankan perintah berikut untuk memulai ulang Apache.
```
systemctl restart httpd
```

## Memverifikasi Konfigurasi Lingkungan
1. Jalankan perintah berikut untuk membuat file pengujian.
```
echo "<?php phpinfo(); ?>" >> /var/www/html/index.php
```
2. Buka jendela browser di komputer lokal Anda dan kunjungi URL berikut untuk memeriksa apakah konfigurasi lingkungan berhasil.
```
http://CVM Public IP/index.php
```
Jika hasil berikut muncul, lingkungan LAMP berhasil dikonfigurasi.
![](https://main.qcloudimg.com/raw/64681fb76bad29072de9ddc3250e66d1.png)

## Operasi yang Relevan
Setelah lingkungan LAMP dibuat, Anda dapat [mengatur situs web Drupal secara manual](https://intl.cloud.tencent.com/document/product/213/34814).


## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah berdasarkan situasi aktual Anda.
- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).

