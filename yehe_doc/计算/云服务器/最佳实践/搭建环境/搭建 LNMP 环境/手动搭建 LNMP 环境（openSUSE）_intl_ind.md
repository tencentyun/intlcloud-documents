## Pengantar
LNMP mengacu pada arsitektur server web umum yang terdiri dari Nginx, MySQL atau MariaDB, dan PHP yang berjalan di Linux. Artikel ini menjelaskan cara men-deploy LNMP di Tencent Cloud Virtual Machine (CVM).
Anda perlu menginstal beberapa paket perangkat lunak di Linux. Jika Anda tidak tahu cara melakukan penginstalan perangkat lunak di Linux, lihat [artikel ini](https://intl.cloud.tencent.com/document/product/213/2047).

## Perangkat Lunak
Artikel ini menggunakan perangkat lunak berikut untuk membangun lingkungan LNMP:
- OS: openSUSE 42.3
- Server web: Nginx 1.14.2
- Database: MySQL 5.6.43
- Prosesor hypertext: PHP 7.0.7

##  Prasyarat
Anda telah membeli CVM Linux. Jika Anda belum melakukannya, lihat [Memulai CVM Linux](http://intl.cloud.tencent.com/document/product/213/2936).

## Petunjuk
### Langkah 1: Login ke instans Linux
- [Login ke instans Linux dalam mode login standar (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain sesuai kebutuhan:
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke instans Linux melalui SSH](https://intl.cloud.tencent.com/document/product/213/32501).

### Langkah 2: Menambahkan sumber citra
1. Login ke CVM Anda.
2. Jalankan perintah berikut untuk menambahkan sumber citra:
```
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/oss suseOss
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/non-oss suseNonOss
```
3. Jalankan perintah berikut untuk memperbarui sumber yang baru saja Anda tambahkan.
```
zypper ref
```

### Langkah 3: Menginstal dan mengonfigurasi Nginx
1. Jalankan perintah berikut untuk menginstal Nginx.
``` 
zypper install -y nginx
```
2. Jalankan perintah berikut untuk memulai server Ngnix dan atur ke mulai otomatis saat CVM dijalankan.
```
systemctl start nginx
systemctl enable nginx
```
3. Jalankan nilai berikut untuk mengedit file konfigurasi Nginx.
```
Vi /etc/nginx/nginx.conf
```
4 Tekan **i** (i) untuk beralih ke mode edit.
5. Cari **server{...}** (server{...}) dan ganti dengan konten berikut:
```
server {
	listen       80;
	server_name  localhost;
	#access_log  /var/log/nginx/log/host.access.log  main;
	location / {
			root   /srv/www/htdocs/;
			index index.php index.html index.htm;
	}
	#error_page  404              /404.html;
	#redirect server error pages to the static page /50x.html
	error_page 500 502 503 504 /50x.html;
	location = /50x.html {
			root   /srv/www/htdocs/;
	}
	#pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    location ~ .php$ {
			root           /srv/www/htdocs/;
			fastcgi_pass   127.0.0.1:9000;
			fastcgi_index  index.php;
			fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
			include        fastcgi_params;
	}
}
```
7. Setelah selesai, tekan **Esc** (Esc) untuk keluar dari mode edit. Kemudian, masukkan **:wq** (:wq) untuk menyimpan file dan keluar dari Vi.
8. Jalankan perintah berikut untuk memulai ulang layanan Nginx.
```
systemctl restart nginx
```
9. Jalankan perintah berikut untuk membuat halaman indeks bernama `index.html`.
```
vi /srv/www/htdocs/index.html
```
10. Tekan **i** (i) untuk beralih ke mode edit dan masukkan konten berikut.
```html
<p> hello world!</p>
```
11. Setelah selesai, tekan **Esc** (Esc) untuk keluar dari mode edit. Kemudian, masukkan **:wq** (:wq) untuk menyimpan file dan keluar dari Vi.
12. Akses IP publik CVM Anda di browser untuk memeriksa apakah Nginx Anda berjalan dengan benar.
Jika muncul berikut ini, Nginx telah berhasil diinstal dan dikonfigurasi.
![](https://main.qcloudimg.com/raw/df09d1fe6baed50cebd89ef7402db4b2.png)

## Langkah 4: Menginstal dan mengonfigurasi MySQL
1. Jalankan perintah berikut untuk menginstal MySQL.
```
zypper install -y mysql-community-server mysql-community-server-tools
```
2. Jalankan perintah berikut untuk memulai layanan MySQL dan atur ke mulai otomatis saat CVM Anda dijalankan.
```
systemctl start mysql 
systemctl enable mysql
```
3. Jalankan perintah berikut untuk login ke MySQL.
> Saat Anda login untuk pertama kalinya, MySQL akan meminta Anda untuk menyiapkan kata sandi. Jika Anda tidak ingin melakukannya, tekan **Enter** (Enter) untuk melewati langkah ini.
>
```
mysql -u root -p
```
Jika muncul hasil berikut, artinya Anda telah berhasil login.
![](https://main.qcloudimg.com/raw/1e9daf876fb08c70674789865688f695.png)
4. Jalankan perintah berikut untuk mengubah kata sandi root.
```
update mysql.user set password = PASSWORD('NEW_PASSWORD') where user='root';
```
5. Jalankan perintah berikut untuk menerapkan konfigurasi:
```
flush privileges;
```
6. Jalankan perintah berikut untuk keluar dari MySQL.
```
\q
```

### Langkah 5: Menginstal PHP
Jalankan perintah berikut untuk menginstal PHP:
```
zypper install -y php7 php7-fpm php7-mysql
```

### Langkah 6: Mengonfigurasi Nginx dengan PHP-FPM
1. Jalankan perintah berikut untuk membuka `/etc/php7/fpm` dan ganti nama `php-fpm.conf.default` menjadi `php-fpm.conf`.
```
cd /etc/php7/fpm
cp php-fpm.conf.default php-fpm.conf
``` 
2. Jalankan perintah berikut untuk membuka `/etc/php7/fpm/php-fpm.d` dan ganti nama `www.conf.default` menjadi `www.conf`.
```
cd /etc/php7/fpm/php-fpm.d
cp www.conf.default www.conf
```
3. Jalankan perintah berikut untuk memulai PHP-FPM dan atur ke mulai otomatis saat CVM Anda dimulai.
```
systemctl start php-fpm
systemctl enable php-fpm
```

## Memverifikasi Penyiapan Anda
1. Jalankan perintah berikut untuk membuat file bernama index.php.
```
Vi /srv/www/htdocs/index.php
```
2. Tekan **i** (i) untuk beralih ke mode edit dan masukkan konten berikut:
```
<?php
	echo "hello new world!";
?>
```
3. Tekan **Esc** (Esc) untuk keluar dari mode edit. Kemudian, masukkan **:wq** (:wq) untuk menyimpan file dan keluar.
4. Akses IP publik CVM Anda di browser.
Jika hasil berikut muncul, artinya pengaturan LNMP Anda telah berhasil diinstal dan dikonfigurasi.
![](https://main.qcloudimg.com/raw/0adc6168e7407931c597228520b35413.png)

## Lihat Juga
Setelah lingkungan LNMP dibangun, Anda dapat menggunakannya untuk [menyiapkan situs web WordPress](https://intl.cloud.tencent.com/document/product/213/8044) untuk memahami CVM Anda dan fungsinya.

## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah:
Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).



