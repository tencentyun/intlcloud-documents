## Ikhtisar

Manajemen daya kinerja tinggi diperlukan untuk sistem operasi (OS) Windows Server untuk mendukung soft shutdown instans CVM. Jika tidak, Anda hanya dapat mematikan paksa instans CVM di konsol CVM. Dokumen ini menggunakan Windows Server 2012 sebagai contoh untuk menjelaskan cara mengonfigurasi manajemen daya.

## Catatan

Untuk memodifikasi manajemen daya, mulai ulang komputer Anda.

## Petunjuk

1. Masuk ke instans Windows menggunakan [file RDP (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5435) atau [desktop jarak jauh](https://intl.cloud.tencent.com/document/product/213/32498).
2. Buka Internet Explorer di Windows CVM, akses jaringan pribadi Tencent Cloud, dan unduh alat konfigurasi dan modifikasi daya Tencent Cloud.
Alamat unduhan adalah `http://mirrors.tencentyun.com/install/windows/power-set-win.bat`.
Misalnya, unduh alat modifikasi dan konfigurasi daya Tencent Cloud (power-set-win.bat) ke drive C:.
3. Gunakan command line tool (CMD) sebagai administrator untuk membuka power-set-win.bat, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/22f81122e1188fc83ed4b1100a7469bc.png)
4. Jalankan perintah berikut untuk melihat rencana manajemen daya saat ini:
```
powercfg -L
```
Hasil yang ditampilkan adalah sebagai berikut:
 ![](https://main.qcloudimg.com/raw/54ceb4faddc8745b30556621268ac318.png)

4. Pada desktop sistem operasi, klik <img src = "https://main.qcloudimg.com/raw/87d894e564b7e83 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > **Control Panel** (Panel Kontrol) > **System and Security** (Sistem dan Keamanan) > **Power Options** (Opsi Daya).
5. Di jendela **Power Options** (Opsi Daya), klik **Change plan settings** (Ganti pengaturan paket), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/54183c1f9d914789b986781b8a4da6ec.png)
6. Di jendela **Edit Plan Settings** (Edit Pengaturan Paket), ubah waktu nonaktif monitor dan disk, seperti yang ditunjukkan di bawah ini:
 ![](https://main.qcloudimg.com/raw/f0b7f447d90fe50ef829a10dab0029c6.png)

