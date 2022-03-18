## Skenario

Dokumen ini menggunakan CVM yang menjalankan Windows Server 2012 R2 sebagai contoh untuk menjelaskan cara mengonfigurasi PHP 5.3 dan versi yang lebih lama atau versi yang lebih baru dari 5.3 di CVM Windows.


## Prasyarat

- Anda sudah login ke Windows CVM dan menambahkan serta menginstal peran IIS di CVM. Untuk informasi selengkapnya, lihat [Langkah 1: Menginstal dan Mengonfigurasi IIS](https://intl.cloud.tencent.com/document/product/213/2755).
- Anda telah memperoleh alamat IP publik CVM Windows. Untuk informasi selengkapnya, lihat [Mendapatkan Alamat IP Publik sebuah Instans](https://intl.cloud.tencent.com/document/product/213/17940).

## Petunjuk

<span id="jump1"></span>
### Menginstal PHP 5.3 atau versi yang lebih lama

>! [Situs web resmi PHP](http://windows.php.net/download/) tidak lagi menyediakan paket penginstalan untuk versi lebih yang lebih lama dari PHP 5.2. Jika Anda memerlukan versi yang lebih lama dari PHP 5.2, cari dan unduh dari CVM. Atau, unduh secara lokal dan kemudian unggah paket penginstalan ke CVM. Untuk informasi selengkapnya tentang cara mengunggah file ke CVM Windows, lihat [Mengunggah File Melalui MSTSC ke CVM Windows dari Windows](https://intl.cloud.tencent.com/document/product/213/2761). Prosedur berikut menggunakan PHP 5.2.13 sebagai contoh.
> 
1. Buka paket penginstalan PHP di CVM.
2. Klik **Next** (Selanjutnya).
3. Pada halaman "Web Server Setup" (Penyiapan Server Web), pilih **IIS FastCGI** dan klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/c5fc89547b020e6ec943732d16186a7b.png).
4. Selesaikan penginstalan PHP seperti yang diminta.
5. Buat file PHP seperti `hello.php` di `C:/inetpub/wwwroot`.
6. Pada file `hello.php` yang dibuat, tambahkan kode berikut dan simpan file.
```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
```
7. Di desktop, buka browser dan kunjungi `http://<Public IP address of the Windows CVM>/hello.php` dan periksa apakah lingkungan berhasil dikonfigurasi.
Jika muncul halaman seperti di bawah ini, konfigurasi tersebut berhasil.
![](https://main.qcloudimg.com/raw/0cdefc8707c4402e9ae5f9e6fa523ae1.png)

<span id="jump"></span>
### Menginstal versi yang lebih baru dari PHP 5.3

Versi yang lebih baru dari PHP 5.3 tidak memiliki paket penginstalan dan diinstal dengan menggunakan file zip atau paket debug. Contoh berikut menunjukkan cara menginstal PHP di lingkungan Windows Server 2012 R2 menggunakan file zip.

#### Mengunduh perangkat lunak

1. Di CVM, buka [situs web resmi PHP](http://windows.php.net/download/) dan unduh paket penginstalan PHP terkompresi, seperti yang ditunjukkan pada gambar berikut:
>! Untuk menjalankan PHP di bawah IIS, Anda harus memilih paket penginstalan x86 untuk Non Thread Safe. Jika server Anda menjalankan Windows Server 32-bit (x86), ganti IIS dengan Apache dan pilih paket penginstalan x86 untuk Thread Safe.
>
![](https://main.qcloudimg.com/raw/b54dcb237ae24673cd592561ffc91bc0.png)
2. Berdasarkan nama paket penginstalan PHP yang diunduh, unduh dan instal paket penginstalan Visual C++ Redistributable.
Tabel berikut mencantumkan paket penginstalan Visual C++ Redistributable yang perlu diunduh dan diinstal untuk paket penginstalan PHP.
<table>
<tr><th>Nama Paket Penginstalan PHP</th><th>Alamat Unduhan Paket Penginstalan Visual C++ Redistributable</th></tr>
<tr><td>php-x.x.x-nts-Win32-VC16-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Microsoft Visual C++ Redistributable untuk Visual Studio 2019</a>(x86)</td></tr>
<tr><td>php-x.x.x-nts-Win32-VC15-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/">Microsoft Visual C++ Redistributable untuk Visual Studio 2017</a>(x86)</td></tr>
<tr><td>php-x.x.x-nts-Win32-VC14-x86.zip</td><td><a href="https://www.microsoft.com/zh-cn/download/details.aspx?id=48145">Microsoft Visual C++ Redistributable untuk Visual Studio 2015</a>(x86)</td></tr>
</table>
Misalnya, jika nama paket penginstalan PHP yang diunduh adalah <code>PHP-7.1.30-nts-Win32-VC14-x86.zip</code>, unduh dan instal paket penginstalan Microsoft Visual C++ Redistributable untuk Visual Studio 2015 (x86).

#### Penginstalan dan konfigurasi
1. Mendekompresi paket penginstalan PHP yang diunduh, misalnya, ke `C:\PHP`.
2. Salin file `php.ini-production` di `C:\PHP` dan ubah ekstensi file menjadi `.ini`, yaitu, ubah namanya menjadi `php.ini`, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/52d9a2098fe73c8ddb41366b9732a000.png)
3. Di desktop, klik <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> untuk membuka **Server Manager** (Pengelola Server), seperti yang ditunjukkan pada gambar berikut:
4. Di bilah sisi kiri, klik **IIS** (IIS).
5. Di jendela manajemen IIS kanan, klik kanan nama server di kolom **Server** (Server) dan pilih **Internet Information Services (IIS) Manager** (Pengelola Layanan Informasi Internet (IIS)), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/55e0b4c86de284050e5d810e92650337.png)
6. Di jendela "Internet Information Service (IIS) Manager" (Pengelola Layanan Informasi Internet (IIS)), klik nama server di bilah sisi kiri untuk masuk ke beranda server, seperti yang ditunjukkan pada gambar berikut:
Misalnya, klik nama server 10_141_9_72 untuk membuka beranda 10_141_9_72.
![](https://main.qcloudimg.com/raw/ab0f2306624452d4a3ab9fd5389d5b1d.png)
7. Di **10_141_9_72 homepage** (beranda 10_141_9_72), klik dua kali **Handler Mappings** (Pemetaan Penangan) untuk membuka halaman "Handler Mappings" (Pemetaan Penangan), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/916a9cc9ce1270dbbfe6ddbb58f937e7.png)
8. Di kolom **Actions** (Tindakan) di sebelah kanan, klik **Add Module Mapping** (Tambahkan Pemetaan Modul) untuk membuka jendela "Add Module Mapping" (Tambahkan Pemetaan Modul).
9. Di jendela "Add Module Mapping" (Tambahkan Pemetaan Modul), masukkan informasi berikut dan klik **OK** (Oke), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/a4d139682fc14204acd77ac3d1ea10eb.png)
Parameter utama meliputi:
 - Jalur permintaan: masukkan `*.php`.
 - Modul: pilih "FastCgiModule".
 - Dapat dieksekusi (opsional): pilih file php-cgi.exe dalam paket penginstalan PHP, yaitu `C:\PHP\php-cgi.exe`.
 - Nama: masukkan nama kustom, seperti FastCGI.
10. Di jendela yang muncul, klik **OK** (Oke). 
11. Klik nama server 10_141_9_72 di bilah sisi kiri untuk kembali ke beranda 10_141_9_72.
12. Pada **10_141_9_72 homepage** (beranda 10_141_9_72), klik dua kali **Default Document** (Dokumen Default) untuk membuka halaman manajemen dokumen default, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/6a896eeb929ae0104b1792e08bd895a6.png)
13. Di kolom **Actions** (Tindakan) di sebelah kanan, klik **Add** (Tambahkan) untuk membuka jendela "Add Default Document" (Tambahkan Dokumen Default).
14. Di jendela "Add Default Document" (Tambahkan Dokumen Default), atur **Name** (Nama) ke `index.php` dan klik **OK** (Oke), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/2d09af5d86755dd481b13efb0b3619a2.png)
15. Klik nama server 10_141_9_72 di bilah sisi kiri untuk kembali ke beranda 10_141_9_72.
16. Pada **10_141_9_72 homepage** (beranda 10_141_9_72), klik dua kali **FastCGI Settings** (Pengaturan FastCGI) untuk membuka halaman manajemen pengaturan FastCGI, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/2a0693d3b837804b546fc690b4fb5cee.png)
17. Pada halaman manajemen pengaturan FastCGI, pilih aplikasi FastCGI dan klik **Edit** (Edit), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/2038fa0df5c08820dc028fb3635fcda4.png)
18. Di jendela "Edit FastCGI Application" (Edit Aplikasi FastCGI), atur **Monitor changes to file** (Pantau perubahan pada file) ke jalur file `php.ini`, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/b1aa458607934a5331b51e22762d0dec.png)
19. Di `C:\inetpub\wwwroot`, buat file PHP, seperti `index.php`.
20. Pada file `index.php` yang dibuat, tambahkan kode berikut dan simpan file.
```
<?php
phpinfo();
?>
```
21. Di desktop, buka browser dan kunjungi `http://localhost/index.php` untuk memeriksa apakah lingkungan berhasil dikonfigurasi.
Jika muncul halaman seperti di bawah ini, konfigurasi tersebut berhasil.
![](https://main.qcloudimg.com/raw/ccd08fd9af6afe4ee2c3bf38f9e581b9.png)

