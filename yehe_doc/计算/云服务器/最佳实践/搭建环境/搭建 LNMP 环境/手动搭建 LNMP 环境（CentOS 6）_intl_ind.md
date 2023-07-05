## Pengantar
Lingkungan LNMP adalah arsitektur server situs web yang berjalan di Linux dan terdiri dari Nginx, MySQL atau MariaDB, dan PHP. Artikel ini menjelaskan cara menyiapkan LNMP di CVM.

Untuk menyiapkan lingkungan LNMP, pahami perintah umum Linux, seperti [Menginstal Perangkat Lunak melalui YUM di CentOS](https://intl.cloud.tencent.com/document/product/213/2046) untuk beberapa contoh), dan pahami versi perangkat lunak yang diinstal.

## Perangkat Lunak
Perangkat lunak berikut akan digunakan:
CentOS adalah distribusi dari sistem operasi Linux. Kami menggunakan CentOS 6.9 dalam artikel ini.
Nginx adalah server web. Kami menggunakan Nginx 1.17.5 dalam artikel ini.
MySQL adalah perangkat lunak database. Kami menggunakan MySQL 5.1.73.
PHP adalah bahasa skrip. Kami menggunakan PHP 7.1.32 dalam artikel ini.

## Prasyarat

Anda memerlukan CVM Linux. Jika Anda belum membelinya, lihat [Memulai CVM Linux](http://intl.cloud.tencent.com/document/product/213/2936).


## Petunjuk
### Langkah 1: Login ke instans Linux
[Login ke instans Linux menggunakan WebShell (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang nyaman bagi Anda:
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501).

### Langkah 2: Menginstal Nginx
1. Jalankan perintah berikut untuk membuat file bernama `nginx.repo` pada bagian `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/nginx.repo
```
2. Tekan **i** (i) untuk masuk ke mode edit dan masukkan nilai berikut.
```
[nginx]
name = nginx repo
baseurl=https://nginx.org/packages/mainline/centos/6/$basearch/
gpgcheck=0
enabled=1
```
3. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali.
4. Jalankan perintah berikut untuk menginstal Nginx.
```
yum install -y nginx
```
5. Jalankan perintah berikut untuk membuka `default.conf`.
```
vim /etc/nginx/conf.d/default.conf
```
6. Tekan **i** (i) untuk beralih ke mode edit.
7. Cari `server{...}` dan ganti konten di dalam kurung kurawal dengan konten berikut:
   Langkah ini akan membatalkan pemantauan alamat IPv6 dan mengonfigurasi Nginx untuk berinteraksi dengan PHP.

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
8. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali.
9. Jalankan perintah berikut untuk memulai Nginx.
```
service nginx start
```
10. Jalankan perintah berikut untuk mengatur Nginx untuk memulai secara otomatis ketika sistem dimulai.
```bash
chkconfig --add nginx
```
```
chkconfig  nginx on
```
11. Di browser lokal, kunjungi URL berikut untuk memverifikasi bahwa layanan Nginx berfungsi dengan benar.
```
http://[Alamat IP publik dari instans CVM]
```
Jika muncul hasil berikut, Nginx telah berhasil diinstal dan dikonfigurasi.
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### Langkah 3: Menginstal MySQL
1. Jalankan perintah berikut untuk memeriksa apakah MySQL sudah diinstal.
```
rpm -qa | grep -i mysql
```
 - Jika muncul hasil berikut, MySQL sudah terinstal.
![](https://main.qcloudimg.com/raw/74e544638637d39209cc1e474083d11d.png)
Untuk menghindari konflik antara versi yang berbeda, jalankan perintah berikut untuk menghapus MySQL yang sudah ada.
```
yum -y remove [Package name]
``` 
 - Jika tidak ada hasil yang ditampilkan, artinya MySQL tidak terinstal. Dalam hal ini, lanjutkan ke langkah berikutnya.
2. Jalankan perintah berikut untuk menginstal MySQL.
```
yum install -y mysql-devel.x86_64 mysql-server.x86_64 mysql-libs.x86_64
```
3. Jalankan perintah berikut untuk memulai MySQL.
```
service mysqld start 
```
4. Jalankan perintah berikut untuk mengatur MySQL untuk memulai secara otomatis ketika sistem malakukan boot.
```bash
chkconfig --add mysqld
```
```
chkconfig mysqld  on 
```
5. Jalankan perintah berikut untuk memverifikasi penginstalan MySQL.
```
mysql
```
Jika muncul hasil berikut, artinya MySQL telah berhasil diinstal.
![](https://main.qcloudimg.com/raw/9c9347ad0264ddad5e98c8dd48adcc6a.png)
6. Jalankan perintah berikut untuk keluar dari MySQL.
```
\q
```

### Langkah 4: Menginstal dan mengonfigurasi PHP
1. Jalankan perintah berikut untuk memperbarui sumber perangkat lunak PHP di Yum.
```
rpm -Uvh https://mirrors.cloud.tencent.com/epel/epel-release-latest-6.noarch.rpm
```
```
rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm
```
2. Jalankan perintah berikut untuk menginstal paket yang diperlukan untuk PHP 7.1.32.
```
yum -y install mod_php71w.x86_64 php71w-cli.x86_64 php71w-common.x86_64 php71w-mysqlnd php71w-fpm.x86_64
```
3. Jalankan perintah berikut untuk memulai layanan PHP-FPM.
```
service php-fpm start
```
4. Jalankan perintah berikut untuk mengatur layanan PHP-FPM untuk memulai secara otomatis.
```bash
chkconfig --add php-fpm  
```
```
chkconfig php-fpm on
```


## Memverifikasi Konfigurasi Lingkungan
1. Jalankan perintah berikut untuk membuat file pengujian.
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Jalankan perintah berikut untuk memulai ulang Nginx.
```
service nginx restart
```
3. Di browser lokal, buka URL berikut untuk memeriksa apakah konfigurasi lingkungan berhasil.
```
http://[Alamat IP publik dari instans CVM]
```
Jika muncul hasil berikut, artinya konfigurasi lingkungan berhasil.
![](https://main.qcloudimg.com/raw/64af927320f2121ae4daf15cf2eaba39.png)



## Operasi Terkait

Setelah lingkungan LNMP dibuat, Anda dapat [memulai situs web WordPress](https://intl.cloud.tencent.com/document/product/213/8044).

## Pertanyaan Umum

Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah berdasarkan situasi aktual Anda.

- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).



