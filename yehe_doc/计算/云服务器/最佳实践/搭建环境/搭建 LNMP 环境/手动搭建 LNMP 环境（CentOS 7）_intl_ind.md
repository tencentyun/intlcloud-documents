## Skenario
LNMP mengacu pada arsitektur server web umum yang terdiri dari Nginx, MySQL atau MariaDB, dan PHP yang berjalan di Linux. Artikel ini menjelaskan cara men-deploy LNMP di Tencent Cloud Virtual Machine (CVM).

Untuk membangun lingkungan LNMP secara manual, Anda harus memahami perintah Linux (lihat [Menginstal Perangkat Lunak Menggunakan YUM di Lingkungan CentOS](https://intl.cloud.tencent.com/document/product/213/2046) untuk beberapa contoh), penggunaan, dan kompatibilitas versi perangkat lunak yang akan diinstal.

## Contoh Versi Perangkat Lunak
Dalam contoh ini, versi perangkat lunak berikut digunakan untuk membangun lingkungan LNMP:
- Linux: Sistem operasi Linux. Dalam contoh ini, CentOS 7.6 digunakan.
- Nginx: server web. Dalam contoh ini, Nginx 1.17.7 digunakan.
- MariaDB: database. Dalam contoh ini, MariaDB 10.4.8 digunakan.
- PHP: bahasa skrip. Dalam contoh ini, PHP 7.2.22 digunakan.


## Prasyarat
Anda telah membeli CVM Linux.


## Petunjuk

### Langkah 1: Login ke instans Linux
[Login ke instans Linux dalam mode standar (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain berdasarkan persyaratan Anda:
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502)
- [Login ke instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Langkah 2: Menginstal Nginx
1. Jalankan perintah berikut untuk membuat file bernama `nginx.repo` pada bagian `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/nginx.repo
```
2. Tekan i untuk beralih ke mode pengeditan dan masukkan nilai berikut.
```
[nginx] 
name = nginx repo 
baseurl = https://nginx.org/packages/mainline/centos/7/$basearch/ 
gpgcheck = 0 
enabled = 1
```
3. Tekan Esc, masukkan **:wq** (:wq), lalu simpan file dan kembali.
4. Jalankan perintah berikut untuk menginstal Nginx.
```
yum install -y nginx
```
5. Jalankan perintah berikut untuk membuka `nginx.conf`.
```
vim /etc/nginx/nginx.conf
```
6. Tekan i untuk beralih ke mode pengeditan, dan edit file `nginx.conf`.
7. Cari `server{...}` dan ganti string di dalam kurung kurawal dengan nilai berikut. Langkah ini untuk membatalkan pendengaran alamat IPv6 dan mengonfigurasi Nginx untuk mewujudkan koneksi dengan PHP.
> Anda dapat menggunakan `Ctrl+F` untuk halaman bawah dan `Ctrl+B` untuk halaman atas guna melihat file.
>
```
server {
	listen       80;
	root   /usr/share/nginx/html;
	server_name  localhost;
	#charset koi8-r;
	#access_log  /var/log/nginx/log/host.access.log  main;
	#
	location / {
		  index index.php index.html index.htm;
	}
	#error_page  404              /404.html;
	#redirect server error pages to the static page /50x.html
	#
	error_page 500 502 503 504 /50x.html;
	location = /50x.html {
	  root   /usr/share/nginx/html;
	}
	#pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
	#
	location ~ .php$ {
	  fastcgi_pass   127.0.0.1:9000;
	  fastcgi_index  index.php;
	  fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
	  include        fastcgi_params;
	}
}
```
Jika Anda tidak dapat menemukan `server{...}` di `nginx.conf`, tambahkan nilai berikut ini sebelum `include /etc/nginx/conf.d/*conf;`, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/901a3957ccd992c2fb345287271c4bef.png)
7. Tekan Esc, masukkan **:wq** (:wq), lalu simpan file dan kembali.
8. Jalankan perintah berikut untuk meluncurkan Nginx.
```
systemctl start nginx
```
9. Jalankan perintah berikut untuk mengonfigurasi peluncuran otomatis Nginx saat startup.
```
systemctl enable nginx 
```
10. Di browser lokal, kunjungi URL berikut untuk memverifikasi bahwa layanan Nginx berfungsi dengan benar.
```
http://<Public IP address of the CVM instance>
```
Jika muncul berikut ini, Nginx telah berhasil diinstal dan dikonfigurasi.
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### Langkah 3: Menginstal database
1. Jalankan perintah berikut untuk memeriksa apakah MariaDB sudah diinstal. 
```
rpm -qa | grep -i mariadb
```
 - Jika muncul hasil berikut, artinya MariaDB telah terinstal.
![](https://main.qcloudimg.com/raw/6fa7fb51de4a61f4da08eb036b6c3e85.png)
Untuk menghindari konflik antara versi yang berbeda, jalankan perintah berikut untuk menghapus MariaDB yang diinstal.
```
yum -y remove <Package name>
```
 - Jika hasil yang ditampilkan kosong, artinya MariaDB tidak terinstal. Dalam hal ini, lanjutkan ke langkah berikutnya.
2. Jalankan perintah berikut untuk membuat file `MariaDB.repo` pada bagian `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/MariaDB.repo
```
3. Tekan i untuk beralih ke mode pengeditan dan masukkan nilai berikut untuk menambahkan MariaDB.
> Sistem operasi yang berbeda menggunakan versi MariaDB yang berbeda. Untuk informasi penginstalan tentang versi sistem operasi lain, buka [situs web MariaDB](https://downloads.mariadb.org).
>
```
# Daftar repositori MariaDB 10.4 CentOS - dibuat 05-11-2019 11:56 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
4. Tekan Esc, masukkan **:wq** (:wq), lalu simpan file dan kembali.
5. Jalankan perintah berikut untuk menginstal MariaDB. Harap perhatikan kemajuan penginstalan dan tunggu hingga penginstalan selesai.
```
yum -y install MariaDB-client MariaDB-server
```
6. Jalankan perintah berikut untuk meluncurkan layanan MariaDB.
```
systemctl start mariadb
```
7. Jalankan perintah berikut untuk mengonfigurasi peluncuran otomatis MariaDB saat startup.
```
systemctl enable mariadb
```
8. Jalankan perintah berikut untuk memverifikasi bahwa MariaDB berhasil diinstal.
```
mysql
```
Jika muncul hasil berikut, artinya MariaDB telah berhasil diinstal.
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
2. Jalankan perintah berikut untuk menginstal paket yang diperlukan untuk PHP 7.2.
```
yum -y install mod_php72w.x86_64 php72w-cli.x86_64 php72w-common.x86_64 php72w-mysqlnd php72w-fpm.x86_64
```
3. Jalankan perintah berikut untuk meluncurkan layanan PHP-FPM.
```
systemctl start php-fpm
```
4. Jalankan perintah berikut untuk mengonfigurasi peluncuran otomatis layanan PHP-FPM saat startup.
```
systemctl enable php-fpm
```

## Memverifikasi Penyiapan Anda
Setelah menyelesaikan konfigurasi lingkungan, selesaikan langkah-langkah berikut untuk memverifikasi bahwa lingkungan LNMP telah berhasil dibuat.
1. Jalankan perintah berikut untuk membuat file pengujian.
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Jalankan perintah berikut untuk memulai ulang layanan Nginx.
```
systemctl restart nginx
```
3. Di browser lokal, buka URL berikut untuk memeriksa apakah konfigurasi lingkungan berhasil.
```
http://<Public IP address of the CVM instance>
```
Jika hasil berikut muncul, artinya konfigurasi lingkungan berhasil.
![](https://main.qcloudimg.com/raw/640812413941a61efe29d7faa546ad80.png)


## Operasi yang Relevan
Setelah lingkungan LNMP dibuat, Anda dapat [membangun situs web WordPress](https://intl.cloud.tencent.com/document/product/213/8044).

## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah berdasarkan situasi aktual Anda.
- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah mengenai disk CVM, lihat [Disk Sistem dan Disk Data](https://intl.cloud.tencent.com/document/product/213/17351).




