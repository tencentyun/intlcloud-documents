Alat migrasi online mendukung migrasi data Tencent Cloud CVM di seluruh akun. Anda dapat menggunakan migrasi data lintas-akun untuk memindahkan data antara CVM di bawah dua akun yang berbeda.

## 1. Mendapatkan Alat Migrasi  
 [Klik di sini](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) untuk mendapatkan paket alat migrasi terkompresi.

## 2. Memilih Mode Migrasi Berdasarkan Lingkungan Jaringan
Pilih mode migrasi yang sesuai dengan lingkungan jaringan server sumber dan CVM tujuan Anda.
Saat ini, alat migrasi mendukung mode default dan mode jaringan pribadi. Mode jaringan pribadi berlaku untuk tiga skenario. Setiap mode atau skenario migrasi memiliki persyaratan jaringan yang berbeda untuk server sumber dan CVM tujuan. Jika server sumber dan CVM tujuan dapat mengakses jaringan publik, Anda dapat menggunakan mode default untuk migrasi. Jika server sumber atau CVM tujuan tidak dapat mengakses jaringan publik secara langsung, Anda perlu membuat koneksi antara mereka melalui [koneksi peering VPC](https://intl.cloud.tencent.com/document/product/553), [koneksi VPN](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), atau [Direct Connect](https://intl.cloud.tencent.com/document/product/216) sebelum menggunakan mode jaringan pribadi untuk migrasi.

## 3. Mencadangkan Data
Anda dapat [membuat snapshot](https://intl.cloud.tencent.com/document/product/362/5755) atau menggunakan metode lain untuk mencadangkan data.

## 4. Memeriksa Sebelum Migrasi
Sebelum migrasi, periksa item berikut dari server sumber dan CVM tujuan:
<table>
	<tr><th style="width: 15%;">CVM Tujuan</th><td><ol style="margin: 0;"><li>Penyimpanan: disk cloud (termasuk disk sistem dan disk data) dari CVM tujuan harus memiliki kapasitas penyimpanan yang cukup untuk menyimpan data dari server sumber.</li><li>Grup keamanan: Port 443 dan 80 harus terbuka ke Internet dalam grup keamanan.</li><li>Bandwidth: sebaiknya Anda meningkatkan bandwidth masuk dan keluar untuk migrasi yang lebih cepat. Lalu lintas yang terpakai selama migrasi kira-kira sama dengan volume data. Jika perlu, ubah metode penagihan jaringan Anda terlebih dahulu.</li><li>Sistem operasi: sebaiknya gunakan sistem operasi yang sama pada server sumber dan CVM tujuan. Sistem operasi yang berbeda akan mengakibatkan inkonsistensi antara citra yang akan dibuat dan sistem operasi aktual. Misalnya, saat memigrasi server sumber dengan sistem CentOS 7 yang diinstal, pilih CVM dengan sistem CentOS 7 yang diinstal sebagai tujuan.</li></ol></td></tr>
	<tr><th>Server sumber Linux</th><td><ol  style="margin: 0;"><li>Periksa dan instal Virtio. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/9929">Memeriksa Driver Virtio di Linux</a>.</li><li>Periksa apakah rsync diinstal dengan menjalankan <code>rsync</code> untuk verifikasi.</li><li>Periksa apakah SELinux sudah diaktifkan. Nonaktifkan jika statusnya diaktifkan.</li><li>Pastikan waktu sistem saat ini sudah benar, karena Tencent Cloud API akan menggunakan stempel waktu UNIX untuk memeriksa token yang dihasilkan setelah menerima permintaan migrasi.</li></ol></td> </tr>
</table>

>? 
> - Anda dapat menggunakan perintah alat untuk memeriksa server sumber secara otomatis, misalnya, `sudo ./go2tencentcloud_x64 --check`.
> - Secara default, alat migrasi go2tencentcloud secara otomatis melakukan pemeriksaan saat diluncurkan. Untuk melewati pemeriksaan dan melakukan migrasi paksa, konfigurasikan `Client.Extra.IgnoreCheck` ke `true` di file client.json.
> - Untuk informasi selengkapnya tentang alat migrasi go2tencentcloud, lihat [Alat Migrasi](https://intl.cloud.tencent.com/document/product/213/35640).

## 5. Memulai Migrasi

1. (Opsional) Buat koneksi antara server sumber dan CVM tujuan. 
 - Jika Anda menggunakan mode jaringan pribadi, buat koneksi antara server sumber dan CVM tujuan melalui [koneksi peering VPC](https://intl.cloud.tencent.com/document/product/553), [koneksi VPN](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003), atau [Direct Connect](https://intl.cloud.tencent.com/document/product/216).
 - Lewati ke langkah berikutnya jika Anda menggunakan mode default.
2. Konfigurasikan file "user.json".
File “user.json” digunakan untuk mengonfigurasi server sumber dan CVM tujuan. File ini berisi item konfigurasi berikut:
 - Kunci API akun Anda, yaitu `SecretId` dan `SecretKey`. Untuk informasi selengkapnya, lihat [Kunci Akses](https://intl.cloud.tencent.com/document/product/598/32675).
 - Wilayah CVM tujuan. Untuk informasi selengkapnya tentang wilayah yang didukung, lihat [Wilayah dan Zona Ketersediaan](https://intl.cloud.tencent.com/document/product/213/6091).
 - ID instans CVM tujuan, yang dapat diperiksa di halaman [Instans](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
 - (Opsional) Konfigurasi disk data dari server sumber.  
3. Konfigurasikan file “client.json”.
File “client.json” digunakan untuk mengonfigurasi skenario migrasi dan parameter lainnya. Anda perlu mengonfigurasi parameter `Client.Net.Mode` di file “client.json”, apa pun mode migrasi atau skenario yang Anda pilih.
4. (Opsional) Kecualikan file dan direktori di server sumber yang tidak perlu dimigrasikan.  
 Edit file “rsync\_excludes\_linux.txt” di server sumber Linux untuk menghapus file dan direktori yang tidak perlu dimigrasikan.
5. Jalankan alat.
Lakukan migrasi lintas-akun dalam [mode jaringan pribadi: skenario 1](https://intl.cloud.tencent.com/document/product/213/35640#Scenario1) sebagai contoh:  
 1. Pada CVM yang memiliki akses ke jaringan publik, jalankan perintah berikut untuk menjalankan alat untuk migrasi tahap 1.
```
sudo ./go2tencentcloud_x64
```
Jika `Tahap 1 selesai dan jalankan tahap selanjutnya di mesin sumber.` diminta, artinya tahap 1 telah selesai. 
 ![](https://main.qcloudimg.com/raw/afeceabbdaad10f348cd0805b209e5cb.png)
 2. Setelah langkah sebelumnya (tahap 1) selesai, salin seluruh direktori alat di tahap 1 ke server sumber yang akan dimigrasikan, lalu jalankan alat untuk migrasi tahap 2.
 Jalankan perintah berikut untuk menjalankan alat untuk migrasi tahap 2.
```
sudo ./go2tencentcloud_x64
```
Jika `Tahap 2 selesai dan jalankan tahap selanjutnya di mesin gateway.` diminta, artinya tahap 2 telah selesai.
 ![](https://main.qcloudimg.com/raw/be35753f3f8f3a30b8d6364a1052991f.png)
 3. Setelah langkah sebelumnya (tahap 2) selesai, salin seluruh direktori alat di tahap 2 ke server sumber di tahap 1, lalu jalankan alat untuk migrasi tahap 3.
 Jalankan perintah berikut untuk menjalankan alat untuk migrasi tahap 3.
```
sudo ./go2tencentcloud_x64
```
Jika `Migrate berhasil.` diminta, artinya seluruh tugas migrasi telah berhasil diselesaikan.
 ![](https://main.qcloudimg.com/raw/1cf4ef72cebab8b42440608643cedade.png)

 
