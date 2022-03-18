## Ikhtisar

Digunakan oleh lebih dari 2 juta situs web, Discuz! adalah perangkat lunak forum paling canggih dan dominan di dunia. Dokumen ini menjelaskan cara membuat situs web menggunakan Discuz! pada instans CVM Tencent Cloud dan men-deploy lingkungan runtime LAMP (Linux, Apache, MariaDB, dan PHP) yang dibutuhkan.


Untuk mengatur Discuz! situs secara manual, pahami dengan baik perintah Linux umum (Lihat [Menginstal Perangkat Lunak melalui YUM di CentOS Environment](https://intl.cloud.tencent.com/document/product/213/2046), dan memahami penggunaan dan kompatibilitas versi perangkat lunak yang akan diinstal.
## Perangkat Lunak
Perangkat lunak berikut digunakan untuk membuat situs web Discuz!.
- Linux: Sistem operasi Linux. Dokumen ini menggunakan CentOS 7.6 sebagai contoh.
- Apache: Perangkat lunak server web. Dokumen ini menggunakan Apache 2.4.15 sebagai contoh.
- MariaDB: database. Dokumen ini menggunakan MariaDB 5.5.60 sebagai contoh.
- PHP: bahasa skrip. Dokumen ini menggunakan PHP 5.4.16 sebagai contoh.
- Discuz!: perangkat lunak forum. Dokumen ini menggunakan Discuz! X3.4 sebagai contoh.


## Petunjuk
### Langkah 1: login ke CVM
Lihat [Login ke Instans Linux Menggunakan Metode Login Standar](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang lebih nyaman bagi Anda:

- [Login ke Instans Linux melalui Alat Login Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke Instans Linux melalui Kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501)



### Langkah 2: atur lingkungan LAMP 

Tencent Cloud menghosting repositori perangkat lunak yang berisi rilis resmi CentOS, yang menyediakan versi terbaru dan stabil. Gunakan Yum untuk menginstal CentOS dengan cepat.

<span id="InstallNecessarySoftware"></span>
#### Menginstal dan mengonfigurasi perangkat lunak yang diperlukan
1. Jalankan perintah berikut untuk menginstal Apache, MariaDB, PHP dan Git:
```
yum install httpd php php-fpm php-mysql mariadb mariadb-server git -y
```
2. Jalankan perintah berikut secara berurutan untuk memulai layanan.
```
systemctl start httpd
```
```
systemctl start mariadb
```
```
systemctl start php-fpm
```
3. <span id="step3"></span>Jalankan perintah berikut untuk mengatur kata sandi bagi pengguna `root` dan menyelesaikan konfigurasi dasar lainnya, sehingga pengguna root dapat mengakses database.
>!
>- Jalankan perintah berikut untuk mengatur kata sandi sebelum login pertama Anda ke MariaDB.
>- Saat Anda melihat permintaan untuk memasukkan kata sandi root, tekan Enter untuk mengatur kata sandi. Kata sandi Anda tidak akan ditampilkan secara default. Selesaikan konfigurasi dasar lainnya seperti yang diminta.
> 
```
mysql_secure_installation
```
4. Jalankan perintah berikut untuk login ke MariaDB. Masukkan kata sandi yang Anda atur di [langkah 3](#step3) dan tekan **Enter** (Enter).
```
mysql -u root -p
```
Login yang berhasil ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/18c54971e141db38c3f483161fefe251.png)

5. Jalankan perintah berikut untuk keluar dari MariaDB.
```
\q
```

#### Memverifikasi konfigurasi lingkungan

Periksa apakah lingkungan sudah diatur dengan benar seperti yang diinstruksikan di bawah ini:
1. Jalankan perintah berikut untuk membuat file uji `test.php` di direktori root default `/var/www/html` Apache:
```
vim /var/www/html/test.php
```
2. Tekan **i** (i) untuk beralih ke mode edit dan masukkan konten berikut:
```
<?php
echo "<title>Test Page</title>";
phpinfo()
?>
```
3. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.
4. Masukkan URL berikut di browser untuk mengakses `test.php` untuk memeriksa apakah lingkungan dikonfigurasi dengan benar.
```
http://[Public IP address of the CVM]/test.php 
```
Jika semuanya berfungsi dengan baik, akan muncul hal-hal berikut.
![](https://main.qcloudimg.com/raw/f511b15ac3016d710c2b1f833e69448d.png)



<span id="InstallDiscuz"></span>
### Langkah 3: instal dan konfigurasikan Discuz!  

#### Mengunduh Discuz! 
Jalankan perintah berikut untuk mengunduh paket penginstalan.
```
git clone https://gitee.com/Discuz/DiscuzX.git
```

#### Mempersiapkan penginstalan
1. Jalankan perintah berikut untuk mengakses direktori penginstalan.
```
cd DiscuzX
```
2. Jalankan perintah berikut untuk menyalin semua file pada bagian "unggah" ke "/var/www/html/".
```
cp -r upload/* /var/www/html/
```
3. Jalankan perintah berikut untuk memberikan izin menulis kepada pengguna.
```
chmod -R 777 /var/www/html
```

#### Menginstal Discuz!
1. Masukkan alamat IP situs Discuz! (alamat IP publik instans CVM Anda) di kotak alamat, atau Anda dapat [mengikat nama domain yang tersedia](#ConfigureDomain) ke alamat IP Anda.
2. Klik **I agree** (Saya setuju) dan buka halaman pemeriksaan lingkungan.
3. Periksa item dan klik **Next Step** (Langkah Selanjutnya).
4. Pilih **Clean Install** (Hapus Penginstalan), dan klik **Next Step** (Langkah Selanjutnya).
5. Masukkan informasi saat diminta untuk membuat database baru untuk Discuz!.
>!  
>- Gunakan `root` dan kata sandi yang ditetapkan di [Menginstal dan mengonfigurasi perangkat lunak yang diperlukan](#InstallNecessarySoftware) untuk terhubung ke database dan menyiapkan alamat email sistem dan nama pengguna, kata sandi, dan alamat email administrator.
>- Ingat nama pengguna dan kata sandi administrator Anda.
>
6. Klik **Next Step** (Langkah Selanjutnya) untuk memulai penginstalan.
7. Setelah penginstalan, klik **Your forum has been installed successfully. Click here to access.** (Forum Anda telah berhasil diinstal. Klik di sini untuk mengakses.) untuk mengakses forum Anda.

<span id="ConfigureDomain"></span>
## Menggunakan Nama Domain
Menggunakan nama domain, bukan IP dapat membantu pengguna mengingat situs web Anda dengan lebih mudah.

## Pertanyaan Umum
Periksa dokumentasi berikut untuk masalah penggunaan CVM: 
- Login CVM: [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Login dan Akses Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278)
- Jaringan CVM: [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Port](https://intl.cloud.tencent.com/document/product/213/2502)
- Disk CVM: [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351)



