## Kasus Penggunaan
WordPress adalah platform blog yang ditulis dalam PHP. Artikel ini menjelaskan cara menginstal WordPress di CentOS 7.6.

Untuk menyiapkan WordPress, pahami perintah umum Linux, seperti [Menginstal Perangkat Lunak melalui YUM di CentOS](https://intl.cloud.tencent.com/document/product/213/2046) dan ketahui cara menggunakan perangkat lunak yang digunakan dan kompatibilitas versinya.

## Perangkat Lunak
Berikut adalah perangkat lunak yang digunakan:
- Sistem operasi: CentOS 7.6, distribusi Linux
- Server web: Nginx 1.17.5
- Database: MariaDB 10.4.8
- Prosesor hypertext: PHP 7.2.22
- Platform blog: WordPress 5.0.4

## Prosedur 
### Langkah 1: Login ke Linux CVM
[Login ke instans Linux menggunakan WebShell (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang nyaman bagi Anda.
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke Instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501)



### Langkah 2: Menyiapkan LNMP secara manual
LNMP adalah arsitektur layanan web yang umum. Nama adalah akronim dari komponennya: Linux, Nginx, MariaDB, dan PHP. Lihat [Membangun Lingkungan LNMP Secara Manual (CentOS 7)](https://intl.cloud.tencent.com/document/product/213/32733) untuk melihat petunjuknya.


### Langkah 3: Membuat database untuk WordPress<span id="database"></span>
>Metode autentikasi pengguna dapat berbeda-beda tergantung pada versi MariaDB yang berbeda. Untuk informasi selengkapnya, lihat situs resmi MariaDB.
>
1. Jalankan perintah berikut untuk masuk ke MariaDB.
```
mysql
```
2. Jalankan perintah berikut untuk membuat database bernama `wordpress`.
```
create database wordpress;
```
3. Jalankan perintah berikut untuk membuat pengguna baru bernama `user` dan atur kata sandinya ke `123456`.
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. Jalankan perintah berikut untuk memberikan `user` semua izin ke `wordpress`.
```
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. Jalankan perintah berikut untuk menerapkan semua konfigurasi.
```
FLUSH PRIVILEGES;
```
6. Jalankan perintah berikut untuk keluar dari MariaDB.
```
\q
```

### Langkah 4: Siapkan akun `root`
1. Jalankan perintah berikut untuk masuk ke MariaDB.
```
mysql
```
2. Jalankan perintah berikut untuk mengatur kata sandi untuk `root`.
>MariaDB 10.4 untuk CentOS sekarang memungkinkan `root` untuk login tanpa kata sandi. Jalankan perintah berikut untuk menetapkan kata sandi untuk `root` dan mencatatnya di lokasi yang aman.
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('your_pasword');
```
3. Jalankan perintah berikut untuk keluar dari MariaDB.
```
\q
```


### Langkah 5: Menginstal dan mengonfigurasi WordPress
#### Mengunduh WordPress
> Anda dapat mengunduh WordPress versi terbaru dari situs web resmi WordPress.
>
1. Jalankan perintah berikut untuk menghapus `index.php`. Perintah ini digunakan untuk menguji penyiapan PHP-Nginx.
```
rm -rf /usr/share/nginx/html/index.php
```
2. Jalankan perintah berikut untuk membuka `/usr/share/nginx/html/` serta unduh dan dekompresi paket penginstalan.
```
cd /usr/share/nginx/html
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```


#### Memodifikasi file konfigurasi WordPress
1. Jalankan perintah berikut untuk membuka direktori penginstalan WordPress, lalu salin dan ganti nama `wp-config-sample.php` menjadi `wp-config.php`. Simpan file asli untuk cadangan.
```
cd /usr/share/nginx/html/wordpress
cp wp-config-sample.php wp-config.php
```
2. Jalankan perintah berikut untuk membuka file konfigurasi baru.
```
vim wp-config.php
```
3. Tekan **i** (i) untuk masuk ke mode edit. Cari konten berikut dan lakukan perubahan yang diperlukan sesuai dengan [Mengonfigurasi database WordPress](#database).
```
	// ** MySQL settings - You can get this info from your web host ** //
	/** The name of the database for WordPress */
	define('DB_NAME', 'wordpress');
	
	/** MySQL database username */
	define('DB_USER', 'user');
	
	/** MySQL database password */
	define('DB_PASSWORD', '123456');
	
	/** MySQL hostname */
	define('DB_HOST', 'localhost');
```
4. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file dan keluar dari Vim.

### Langkah 6: Memverifikasi Konfigurasi WordPress
1. Buka jendela browser dan masukkan konten berikut untuk memulai proses.
```
http://your_CVM_public_IP/wordpress
```
Anda diarahkan ke halaman penginstalan.
2. Masukkan informasi seperti yang diminta. Klik **Install WordPress** (Instal WordPress) untuk menyelesaikan prosesnya.
<table>
	<th style="width: 18%;">Item</th>
	<th style="width: 100px;">Deskripsi</th>
					<tr>
					<td>
							Judul situs
					</td>
					<td>
							Nama situs WordPress Anda.
					</td>
			</tr>
				<tr>
					<td>
							Nama pengguna
					</td>
					<td>
							Nama akun administrator WordPress. Untuk alasan keamanan, gunakan nama selain `admin`.</td></tr>
					</td>
			</tr>
			<tr>
					<td>
							Kata sandi
					</td>
					<td>
							Gunakan kata sandi default atau atur kata sandi yang baru. Gunakan kata sandi yang kuat dan jangan gunakan kembali kata sandi yang sudah ada. Simpan kata sandi Anda dengan aman.
					</td>
			</tr>
				<tr>
					<td>
							Alamat email anda
					</td>
					<td>
							Alamat email yang digunakan untuk menerima notifikasi.
					</td>
			</tr>
	</table>
Sekarang, Anda dapat login ke WordPress dan memublikasikan blog.

## Menggunakan Nama Domain
Gunakan nama domain yang membuat situs web Anda lebih mudah diingat. Sebaiknya dapatkan nama domain dan atur agar mengarah ke situs WordPress Anda. Jika Anda menginstal WordPress hanya untuk mempelajari prosesnya, Anda dapat melewati langkah ini.

## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah.
- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).

