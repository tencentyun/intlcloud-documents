## Pengantar
WordPress adalah platform blog yang ditulis dalam PHP. Artikel ini menjelaskan cara menginstal WordPress di Windows Server 2012.

## Perangkat Lunak
Meskipun PHP versi 5.6.20 dan versi yang lebih baru serta MySQL versi 5.0 dan versi yang lebih baru mendukung WordPress, sebaiknya gunakan PHP 7.3 dan MySQL 5.6 atau versi yang lebih baru untuk alasan keamanan.

Berikut adalah perangkat lunak yang digunakan:
- Sistem operasi: Windows Server 2012
- Server web: IIS 8.5
- Database: MySQL 5.6.46
- Penerjemah hypertext: PHP 7.3.12
- Platform blog: WordPress 5.3


## Prosedur

### Langkah 1: Login ke Windows CVM
- [Login ke CVM Windows Menggunakan File RDP (Direkomendasikan)](http://intl.cloud.tencent.com/document/product/213/5435)
- [Login ke CVM Windows Menggunakan Desktop Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32498)

### Langkah 2: Menyiapkan WIMP
1. Instal IIS.
2. Deploy PHP 5.6.20 atau versi yang lebih baru.
3. Instal MySQL 5.6 atau versi yang lebih baru.

### Langkah 3: Menginstal dan mengonfigurasi WordPress
> Anda dapat mengunduh WordPress versi terbaru dari situs web resmi WordPress.
>

1. Unduh WordPress dan dekompresi ke direktori di CVM.
Misalnya, Anda dapat mendekompresinya ke `C:\wordpress`.
2. Klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;">. Masukkan **cmd** (cmd) di **Run** (Jalankan), lalu tekan **Enter** (Enter) untuk membuka jendela baris perintah.
3. Jalankan perintah berikut di jendela baris perintah guna membuat database untuk WordPress.
Misalnya, buat database bernama `wordpress`.
```
create database wordpress;
```
4. Temukan `wp-config-sample.php` pada bagian `C:\wordpress` dan ganti namanya menjadi `wp-config.php`.
5. Gunakan editor teks untuk membuka `wp-config.php` dan edit informasi konfigurasi seperti yang dijelaskan di [Langkah 4: Menginstal MySQL](#Step04).
6. Simpan `wp-config.php`.
7. Klik <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> untuk membuka **Server Manager** (Pengelola Server).
8. Di panel navigasi di sebelah kiri, pilih **IIS** (IIS). Klik kanan nama server di kolom **Server** (Server) dan pilih **Internet Information Services (IIS) Manager** (Pengelola Layanan Informasi Internet (IIS)) untuk membuka jendela **Internet Information Services (IIS) Manager** (Pengelola Layanan Informasi Internet (IIS)).
9. Di jendela **Internet Information Service (IIS) Manager** (Pengelola Layanan Informasi Internet (IIS)), perluas server Anda di panel navigasi kiri dan pilih situs web Anda. Tindakan ini akan membuka halaman manajemen situs web.
10. Hapus situs web yang terikat ke port 80.
Anda dapat mengubah port ke port lain yang tidak digunakan, seperti 8080.
11. Klik **Add Website** (Tambahkan Situs Web).
12. Masukkan informasi yang diperlukan dan klik **OK** (OKE).
 - Nama situs web: nama situs web, seperti `wordpress`.
 - Kumpulan aplikasi: pilih **DefaultAppPool** (DefaultAppPool).
 - Jalur fisik: direktori yang berisi WordPress, seperti `C:\wordpress`.
13. Cari `php.ini` pada bagian direktori yang berisi PHP. Buka dengan editor teks dan lakukan perubahan berikut:
 1. Perubahan yang diperlukan berbeda untuk versi PHP yang berbeda.
     - Untuk PHP 5.x, cari `extension=php_mysql.dll` dan hapus `;` di bagian awal.
     - Untuk PHP 7.x, cari `extension=php_mysqli.dll` dan hapus `;` di bagian awal.
 2. Cari `extension_dir= “ext”` dan hapus `;` di bagian awal.
14 Simpan `php.ini`.

### Langkah 4: Memverifikasi Konfigurasi WordPress

1. Buka jendela browser di komputer lokal Anda dan kunjungi `http://localhost/wp-admin/install.php`. Halaman penginstalan WordPress akan muncul.
2. Masukkan informasi seperti yang diminta oleh wizard penginstalan. Klik **Install WordPress** (Instal WordPress) untuk menyelesaikan prosesnya.
<table>
	<tr><th>Informasi </th><th>Deskripsi</th></tr>
	<tr><td>Nama Situs Web</td><td>Nama situs WordPress.</td></tr>
	<tr><td>Nama pengguna</td><td>Nama akun administrator WordPress. Untuk alasan keamanan, gunakan nama selain `admin`.</td></tr>
	<tr><td>Kata sandi</td><td>Gunakan kata sandi yang kuat, yang berbeda dengan kata sandi Anda saat ini. Simpan di lokasi yang aman.</td></tr>
	<tr><td>Email</td><td>Alamat email yang digunakan untuk menerima notifikasi</td></tr>
</table>
Sekarang, Anda dapat login ke situs blog WordPress dan memublikasikan blog.

## Menggunakan Nama Domain

Gunakan nama domain yang membuat situs web Anda lebih mudah diingat. Sebaiknya dapatkan nama domain dan atur agar mengarah ke situs WordPress Anda. Jika Anda menginstal WordPress hanya untuk mempelajari prosesnya, Anda dapat melewati langkah ini.

## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen pemecahan masalah berikut berdasarkan situasi aktual Anda.
- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).

