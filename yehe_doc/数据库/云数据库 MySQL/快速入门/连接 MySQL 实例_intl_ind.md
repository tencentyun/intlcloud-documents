Dokumen ini menjelaskan cara menghubungkan ke instans TencentDB for MySQL yang diinisialisasi melalui jaringan pribadi atau publik.

## Persiapan
- Anda telah menginisialisasi instans TencentDB for MySQL. Untuk informasi selengkapnya, lihat [Menginisialisasi Instans MySQL](https://intl.cloud.tencent.com/document/product/236/3128).
- Anda telah membuat akun database dan mengotorisasi IP atau rentang IP tertentu untuk mengakses instans TencentDB for MySQL. Untuk informasi selengkapnya, lihat [Membuat Akun](https://intl.cloud.tencent.com/document/product/236/31900) dan [Memodifikasi Alamat Host dengan Izin Akses](https://intl.cloud.tencent.com/document/product/236/31903). Atau, Anda dapat menggunakan akun root.
- Anda telah mengonfigurasi aturan grup keamanan untuk instans CVM dan instans TencentDB for MySQL untuk mengizinkan IP atau rentang IP tertentu mengakses instans TencentDB for MySQL. Untuk informasi selengkapnya, lihat [Manajemen Grup Keamanan TencentDB](https://intl.cloud.tencent.com/document/product/236/14470).

## Metode Koneksi
TencentDB for MySQL dapat dihubungkan dengan metode berikut:
- **Private network connection** (Koneksi jaringan pribadi): instans CVM dapat digunakan untuk terhubung ke alamat jaringan pribadi instans TencentDB. Metode ini menggunakan jaringan pribadi Tencent Cloud berkecepatan tinggi dan fitur penundaan yang rendah.
 - Kedua instans harus berada di bawah akun yang sama dan di [VPC](https://intl.cloud.tencent.com/document/product/215/535) yang sama di wilayah yang sama, atau keduanya di jaringan klasik.
 - Alamat jaringan pribadi disediakan oleh TencentDB secara default dan dapat dilihat di daftar instans atau di halaman detail instans di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb).
>?Instans CVM dan TencentDB di VPC yang berbeda (dalam akun yang sama atau berbeda di wilayah yang sama atau berbeda) dapat saling terhubung melalui jaringan pribadi melalui [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
>
- **Public network connection** (Koneksi jaringan publik): jika Anda tidak dapat mengakses jaringan pribadi, Anda dapat terhubung ke instans TencentDB for MySQL di alamat jaringan publiknya. Alamat jaringan publik harus [diaktifkan secara manual](#waiwang). Alamat tersebut dapat dilihat di halaman detail instans di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan dapat dinonaktifkan jika tidak lagi diperlukan.
 - Alamat jaringan publik dapat diaktifkan untuk instans sumber di wilayah Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Nanjing, Hong Kong (Tiongkok), Singapura, Seoul, Tokyo, Silicon Valley, dan Frankfurt. Informasi terbaru tentang wilayah tempat alamat jaringan publik dapat diaktifkan untuk instans baca saja dapat ditemukan di konsol.
 - Mengaktifkan alamat jaringan publik akan mengekspos layanan database Anda ke jaringan publik, yang dapat menyebabkan intrusi atau serangan database. Sebaiknya gunakan jaringan pribadi untuk menghubungkan ke database. 
 - Koneksi jaringan publik ke TencentDB cocok untuk pengembangan atau manajemen tambahan database tetapi tidak untuk akses bisnis di lingkungan produksi, karena faktor yang berpotensi tidak dapat dikontrol sehingga dapat menyebabkan tidak tersedianya koneksi jaringan publik, seperti serangan dan lonjakan DDoS akses lalu lintas tinggi.


Berikut ini menjelaskan cara menghubungkan ke instans TencentDB for MySQL dari instans CVM Windows dan Linux melalui jaringan pribadi dan publik.
## Menghubungkan dari Instans CVM Windows
1. Login ke instans CVM Windows. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/10516" target="_blank">Menyesuaikan Konfigurasi CVM Windows</a>.
2. Unduh klien SQL standar.
>?Sebaiknya unduh MySQL Workbench. Klik [di sini](https://dev.mysql.com/downloads/workbench/) dan unduh penginstal berdasarkan sistem operasi Anda.
>
![](https://main.qcloudimg.com/raw/851ab46468c554097a0cf742017157b7.png)
3. **Login** (Login), **Sign Up** (Daftar), dan **No thanks, just start my download.** (Tidak, terima kasih, mulai unduhan saya saja.) akan muncul di halaman. Pilih **No thanks, just start my download.** (Tidak, terima kasih, mulai unduhan saya saja.) untuk mengunduh dengan cepat.
![](https://main.qcloudimg.com/raw/47b195fb37ff584f21038ee54342d362.png)
4. Instal MySQL Workbench pada instans CVM ini.
>?
>- Microsoft .NET Framework 4.5 dan Visual C++ Redistributable untuk Visual Studio 2015 diperlukan untuk penginstalan.
>- Anda dapat mengklik **Download Prerequisites** (Unduh Prasyarat) di wizard penginstalan MySQL Workbench untuk masuk ke halaman terkait guna mengunduh dan menginstalnya. Kemudian, instal MySQL Workbench.
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. Buka MySQL Workbench, pilih **Database** (Database) > **Connect to Database** (Hubungkan ke Database), masukkan alamat jaringan pribadi (atau publik), nama pengguna, dan kata sandi instans TencentDB for MySQL Anda dan klik **OK** (OKE) untuk login.
 - **Hostname** (Nama host): masukkan alamat jaringan pribadi (atau publik), yang dapat dilihat dengan port pada halaman detail instans di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Untuk alamat jaringan publik, periksa apakah sudah diaktifkan seperti yang diinstruksikan di [Mengaktifkan Alamat Jaringan Publik](#waiwang).
 - **Port** (Port): port jaringan pribadi (atau publik)
 - **Username** (Nama Pengguna): nama pengguna adalah **root** (root) secara default. Untuk koneksi jaringan publik, sebaiknya [buat akun terpisah](https://intl.cloud.tencent.com/document/product/236/31900) untuk kontrol koneksi yang lebih mudah.
 - **Password** (Kata Sandi): kata sandi yang sesuai dengan **Username** (Nama Pengguna). Jika Anda lupa kata sandi, atur ulang seperti yang diinstruksikan di [Mengatur Ulang Kata Sandi](https://intl.cloud.tencent.com/document/product/236/31901).
![](https://main.qcloudimg.com/raw/946b50fb05de11d7c68c2262ac4fe933.png)
6. Setelah login berhasil, halaman berikut akan muncul, sehingga Anda dapat melihat mode dan objek database MySQL, membuat tabel, dan melakukan operasi seperti penyisipan data dan kueri.
![](https://main.qcloudimg.com/raw/33f081e99c384258bbc5ed3683ed4d7d.png)

## Menghubungkan dari Instans CVM Linux
1. Login ke instans CVM Linux. Untuk informasi selengkapnya, lihat [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).
2. Mengambil instans CVM pada CentOS 7.2 (64-bit) sebagai contoh, jalankan perintah berikut untuk menginstal klien MySQL.
```
yum install mysql
```
Jika `Complete!` ditampilkan, artinya klien MySQL berhasil diinstal.
![](https://main.qcloudimg.com/raw/16c77e28c40ae9be9a182b1c61843ecd.png)
3. Lakukan operasi yang sesuai berdasarkan metode koneksi:
 - **Private network connection:** (Koneksi jaringan pribadi:)
    1. Jalankan perintah berikut untuk login ke instans TencentDB for MySQL.
```
mysql -h hostname -u username -p
```
      - nama host: ganti dengan alamat jaringan pribadi target instans TencentDB for MySQL, yang dapat dilihat pada halaman detail instans di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb).
>?
>- Nomor port default MySQL adalah 3306.
>- Jika nomor port 3306, Anda hanya perlu mengganti `hostname` dengan alamat IP. Misalnya, jika alamat jaringan pribadi adalah 10.16.0.11:3306, atur `hostname` ke `10.16.0.11`.
>- Jika nomor port bukan 3306, Anda perlu menentukan port dalam perintah koneksi dalam format `mysql -h hostname -P port -u username -p`, seperti `mysql -h 10.16.0.11 -P 5308 -u username -p`.
>
		- nama host : ganti dengan `root` nama pengguna default.
    2. Masukkan kata sandi yang sesuai dengan akun `root` dari instans TencentDB for MySQL setelah `Enter password:` diminta. Jika lupa kata sandi, Anda dapat mengatur ulang seperti yang diinstruksikan di [Mengatur Ulang Kata Sandi](https://intl.cloud.tencent.com/document/product/236/31901).
    Jika `MySQL [(none)]>` ditampilkan, artinya Anda telah berhasil login ke MySQL.
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **Public network connection:** (Koneksi jaringan publik:)
    1. Jalankan perintah berikut untuk login ke instans TencentDB for MySQL.
```
mysql -h hostname -P port -u username -p
```
      - nama host: ganti dengan alamat jaringan publik target instans TencentDB for MySQL, yang dapat dilihat bersama dengan port pada halaman detail instans di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Jika alamat jaringan publik belum diaktifkan, aktifkan seperti yang diinstruksikan di [Mengaktifkan Alamat Jaringan Publik](#waiwang).
      - port: ganti dengan nomor port jaringan publik.
      - nama pengguna: ganti dengan nama pengguna akses jaringan publik. Sebaiknya [buat akun terpisah](https://intl.cloud.tencent.com/document/product/236/31900) untuk kontrol koneksi yang lebih mudah.
    2. Masukkan kata sandi yang sesuai dengan nama pengguna koneksi jaringan publik setelah `Enter password:` diminta. Jika Anda lupa kata sandi, atur ulang seperti yang diinstruksikan di [Mengatur Ulang Kata Sandi](https://intl.cloud.tencent.com/document/product/236/31901).
    Dalam contoh ini, `hostname` adalah 59281c4exxx.myqcloud.com dan port jaringan publik adalah 15311.
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. Di bawah prompt `MySQL [(none)]>`, Anda dapat mengirim pernyataan SQL ke server MySQL untuk dijalankan. Untuk baris perintah tertentu, lihat [mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).
Di bawah ini menggunakan `show databases;` sebagai contoh:
![](https://qcloudimg.tencent-cloud.cn/raw/faa7e8137e03b72f95d7a92faa971a42.png)

## Lampiran 1. Pemecahan Masalah Kesalahan Koneksi
Jika Anda mengalami kesalahan koneksi, sebaiknya gunakan [Pemeriksa Konektivitas Sekali Klik](https://intl.cloud.tencent.com/document/product/236/31927) untuk memecahkan masalah terlebih dahulu lalu menemukan solusi yang sesuai di [Kegagalan Koneksi Instans](https://intl.cloud.tencent.com/document/product/236/40333) sesuai dengan laporan pemeriksaan.

## Lampiran 2. Metode Verifikasi Konektivitas Jaringan
Kami merekomendasikan pemecahan masalah dan menemukan masalah konektivitas jaringan dengan cepat dengan perintah `telnet`.

Jika verifikasi dengan `telnet` menemukan bahwa akses jaringan instans TencentDB berjalan dengan baik, tetapi kesalahan dilaporkan saat Anda mencoba login melalui baris perintah di instans CVM, lihat [Pertanyaan Umum > Koneksi dan Login > Koneksi](https://intl.cloud.tencent.com/document/product/236/37783).

## [Lampiran 3. Mengaktifkan Alamat Jaringan Publik](id:waiwang)
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans.
2. Di bagian **Basic Info** (Info Dasar), klik **Enable** (Aktifkan) di samping **Public Network Address** (Alamat Jaringan Publik).
>?Jika bagian **Basic Info** (Info Dasar) menampilkan IP dan port publik, alamat jaringan publik telah diaktifkan.
>
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
3. Di jendela pop-up, klik **OK** (OKE).
>?
>- Setelah alamat jaringan publik berhasil diaktifkan, alamat tersebut dapat dilihat di informasi dasar.
>- Akses jaringan publik dapat dinonaktifkan menggunakan pengalihan. Ketika diaktifkan lagi, alamat jaringan publik yang sesuai dengan nama domain tetap sama.
