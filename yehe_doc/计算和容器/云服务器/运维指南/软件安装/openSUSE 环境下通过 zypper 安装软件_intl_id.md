Pastikan Anda telah mengikuti langkah-langkah pada [Menginstal Perangkat Lunak melalui YAST di Lingkungan SUSE](https://intl.cloud.tencent.com/document/product/213/2047) menginstal perangkat lunak yang diperlukan.
## 1. Konfigurasi nginx
1) Mulai layanan nginx

Mulai nginx dengan perintah berikut:
```
 service nginx restart
```

2) Uji apakah layanan nginx berfungsi dengan baik

Uji dengan perintah berikut:
```
wget http://127.0.0.1
```
Jika hasilnya seperti gambar di bawah ini dan menampilkan "'index.html' saved" di bagian akhir, artinya layanan nginx berfungsi dengan baik.

```
--2013-02-20 17:07:26-- http://127.0.0.1/
Menghubungkan ke 127.0.0.1:80... terhubung.
Permintaan HTTP terkirim, menunggu respons... 200 OK
Panjang:  151 [teks/html]
Menyimpan ke:  'index.html'
100%[==========================================================================================>] 151 --.-K/s in 0s 
2013-02-20 17:07:26 (37.9 MB/s) - 'index.html' saved [151/151]
```

3) Di browser, buka IP Publik CentOS CVM untuk memeriksa apakah layanan nginx berfungsi dengan baik.

Munculnya halaman berikut menunjukkan bahwa nginx telah berhasil diinstal dan dikonfigurasi.

## 2. Konfigurasi PHP
1) Buat file konfigurasi baru php-fpm.conf dengan perintah berikut:

```
vim /etc/php5/fpm/php-fpm.conf
```
Tulis nilai berikut ini:

```
[global]
error_log = /var/log/php-fpm.log
[www]
user = nobody
group = nobody
listen = 127.0.0.1:9000
pm = dynamic
pm.max_children = 5
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3
```

## 3. Mulai layanan
Mulai semua layanan dengan perintah berikut:

```
/etc/init.d/mysql start; /etc/init.d/php-fpm start; /etc/init.d/nginx start
```

Contoh:

![](//mccdn.qcloud.com/img56b01d2fa2d5c.png)


## 4. Validasi konfigurasi lingkungan
Buat index.php di bawah direktori web menggunakan perintah berikut:

```
vim /usr/share/nginx/html/index.php
```
Tulis nilai berikut ini:

```
<?php
echo "<title>Test Page</title>";
echo "hello world";
?>
```

Di browser, buka IP Publik SUSE CVM untuk memeriksa apakah konfigurasi lingkungan berhasil. Jika halaman web menunjukkan "hello world", artinya konfigurasi berhasil.
