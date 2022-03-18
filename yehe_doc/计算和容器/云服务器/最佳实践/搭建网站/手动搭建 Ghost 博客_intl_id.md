## Skenario
Ghost adalah platform blog sumber terbuka dan gratis yang ditulis dalam JavaScript dan didistribusikan di bawah Lisensi MIT, yang dirancang untuk menyederhanakan proses penerbitan online untuk masing-masing blogger serta publikasi online. Artikel ini menjelaskan cara menyiapkan Ghost di CVM. 

Untuk menyiapkan Ghost, pahami Linux dan perintah umumnya, seperti [Instal Perangkat Lunak melalui Apt-get berdasarkan Lingkungan Ubuntu](https://intl.cloud.tencent.com/document/product/213/2123).

## Perangkat Lunak
Artikel ini menggunakan perangkat lunak berikut:
- Sistem operasi Linux. Artikel ini menggunakan Ubuntu 18.04.
- Nginx 1.14.0 digunakan untuk menyediakan layanan web.
- MySQL 5.7.27 digunakan untuk database.
- Node.js 10.17.0 adalah lingkungan waktu proses kami.
- Ghost 3.0.2


##  Prasyarat
Anda harus memiliki CVM Linux. Jika Anda belum membelinya, lihat [Memulai CVM Linux](http://intl.cloud.tencent.com/document/product/213/2936).
- Nama domain yang mengarah ke CVM Anda. Jika nama domain digunakan untuk layanan Tiongkok Daratan, pengisian ICP diperlukan.



## Petunjuk

### Langkah 1 Login ke instans Linux
- [Login ke instans Linux menggunakan WebShell (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang nyaman bagi Anda:
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke Instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Langkah 2 Buat pengguna baru
1. Setelah login, alihkan ke `root`. Lihat [artikel ini](https://intl.cloud.tencent.com/document/product/213/17278) untuk mengetahui detailnya.
2. Jalankan perintah berikut untuk membuat pengguna bernama `user`.
>Jangan gunakan `ghost` sebagai nama pengguna. Tindakan ini menyebabkan konflik dengan Ghost-CLI. 
>
```
adduser user
```
 1. Masukkan dan konfirmasi kata sandi seperti yang diminta. Kata sandi tidak ditampilkan secara default. Tekan **Enter** (Enter) untuk melanjutkan.
 2. Masukkan informasi pengguna. Atau tekan **Enter** (Enter) untuk melewatinya dan melanjutkan.
 3. Masukkan **Y** (Y) untuk konfirmasi dan tekan **Enter** (Enter) untuk menyelesaikan proses, seperti yang ditunjukkan di bawah ini:
 ![](https://main.qcloudimg.com/raw/66ca399607b89f2653668eb4b0cb71f5.png)
3. Jalankan perintah berikut untuk menambahkan hak istimewa pengguna.
```
usermod -aG sudo user
```
4. Jalankan perintah berikut untuk beralih ke pengguna `user`.
```
su user
```

### Langkah 3 Perbarui paket yang diinstal
Jalankan perintah berikut untuk memperbarui paket yang diinstal.
>Masukkan kata sandi untuk `user` seperti yang diminta dan tekan **Enter** (Enter) untuk memulai.
>
```
sudo apt-get update
```
```
sudo apt-get upgrade -y
```

### Langkah 4 Penyiapan lingkungan
#### Menginstal Nginx
Jalankan perintah berikut untuk menginstal Nginx.
```
sudo apt-get install -y nginx 
```

#### Menginstal dan mengonfigurasi MySQL
1. Jalankan perintah berikut untuk menginstal MySQL.
```
sudo apt-get install -y mysql-server 
```
2. Jalankan perintah berikut untuk terhubung ke MySQL.
```
sudo mysql
```
3. <span id="database"></span>Jalankan perintah berikut untuk membuat database untuk Ghost bernama `ghost_data`.
```
CREATE DATABASE ghost_data;
```
4. <span id="sercet"></span>Jalankan perintah berikut untuk mengatur kata sandi bagi pengguna database `root`.
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
```
5. Jalankan perintah berikut untuk keluar dari MySQL.
```
\q
```

#### Menginstal Node.js
1. Jalankan perintah berikut untuk mengatur versi Node.js default yang akan digunakan.
```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash
```
2. Jalankan perintah berikut untuk menginstal Node.js.
```
sudo apt-get install -y nodejs
```

#### Menginstal Ghost-CLI
Jalankan perintah berikut untuk menginstal Ghost-CLI yang membantu mengonfigurasi Ghost.
```
sudo npm install ghost-cli@latest -g
```

### Langkah 5 Instal dan konfigurasikan Ghost
1. Jalankan perintah berikut.
```
sudo mkdir -p /var/www/ghost
```
```
sudo chown user:user /var/www/ghost
```
```
sudo chmod 775 /var/www/ghost
```
```
cd /var/www/ghost
```
2. Jalankan perintah berikut untuk menginstal Ghost.
```
ghost install
```
3. Gunakan citra berikut untuk menyelesaikan proses penginstalan.
![](https://main.qcloudimg.com/raw/6c3a3b9d083dfb253285f47d81e928b5.png)
 1. **Enter your blog URL** (Masukkan URL blog Anda): masukkan nama domain Anda dalam format `http://your_domain_name`.
 2. **Enter your MySQL hostname** (Masukkan nama host MySQL Anda): masukkan alamat database Anda. Gunakan `localhost` dalam kasus ini, lalu tekan **Enter** (Enter).
 3. **Enter your MySQL username** (Masukkan nama pengguna MySQL Anda): masukkan nama pengguna yang Anda gunakan untuk terhubung ke MySQL. Gunakan `root` dalam kasus ini, lalu tekan **Enter** (Enter).
 4. **Enter your MySQL password** (Masukkan kata sandi MySQL Anda): masukkan kata sandi yang sesuai yang Anda atur [sebelumnya](#secret), lalu tekan **Enter** (Enter).
 5. **Enter your database name** (Masukkan nama database Anda): masukkan nama database yang Anda buat untuk Ghost [pada langkah sebelumnya](#database). Gunakan `ghost_data`, lalu tekan **Enter** (Enter).
 6. Masukkan **Y** (Y) atau **n** (n) untuk menyelesaikan konfigurasi.
 URL admin muncul di bagian bawah layar.
4. Buka jendela browser di komputer lokal Anda dan kunjungi URL admin untuk mulai mengonfigurasi blog Anda.
Klik **Create your account** (Buat akun Anda) untuk membuat akun admin.
![](https://main.qcloudimg.com/raw/e2eeacd71eec4c27660eeb4797f83f2a.png)
5. Masukkan informasi yang diinginkan dan klik **Last step** (Langkah terakhir), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/a7a81f16b811bdceeb429116ee23081c.png)
6. Anda dapat mengundang orang lain untuk membuat blog, atau lewati langkah ini.
7. Buka halaman administrasi untuk mengelola blog, seperti yang ditunjukkan di bawah ini: 
![](https://main.qcloudimg.com/raw/fd9071dba9748ce8125f8597be0d248a.png)
Setelah selesai, gunakan browser untuk membuka nama domain Anda `www.xxxxxxxxx.xx` untuk melihat blog Anda, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/055decab4524eb9f2f5602fbd0502c7c.png)

## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah berdasarkan situasi aktual Anda.
- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).
