## Ikhtisar
Artikel ini menjelaskan cara menginstal MySQL 8.0 pada instans CVM dengan Windows Server 2012 R2 Datacenter Edisi 64bit. 
SQL Server kemungkinan adalah perangkat lunak database paling populer di Windows. Namun, SQL Server ini bersifat komersial dan mengharuskan Anda untuk mendapatkan lisensi Anda sendiri. Sebagai alternatif, Anda dapat membeli [instans CDB untuk database Tencent Cloud SQLServer](https://intl.cloud.tencent.com/product/sqlserver?from_cn_redirect=1).

## Prosedur

### Mengunduh MySQL
1. Login ke instans CVM Anda.
2. Buka jendela browser dan buka [situs resmi MySQL](https://www.mysql.com/) untuk mengunduh file penginstalan MySQL.

### Menginstal MySQL

1. Luncurkan penginstal MySQL dengan mengeklik dua kali file penginstalan. Jendela **Choose a Setup Type** (Pilih Jenis Pengaturan) muncul. Pilih **Developer Default** (Default Pengembang) dan klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/4077db7bfe9f7b97e1d7ddd649efa966.png)
2. Pada jendela **Check Requirements** (Periksa Persyaratan) yang muncul, klik **Execute** (Jalankan) dan selesaikan persyaratan yang tidak terpenuhi seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/16a5f7190d7720562681528072cf8129.png)
3. Klik **Next** (Selanjutnya).
4. Di jendela **Installation** (Penginstalan), klik **Execute** (Jalankan) untuk menginstal paket yang diperlukan, seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/1b4a3e338bb816e7c47b4603a7a1dbb4.png)
5. Klik **Next** (Selanjutnya) saat penginstalan paket selesai untuk membuka jendela **Product Configuration** (Konfigurasi Produk).


### Mengonfigurasi MySQL

#### Mengonfigurasi layanan MySQL

1. Di jendela **Product Configuration** (Konfigurasi Produk), klik **Next** (Selanjutnya) untuk membuka jendela **High Availability** (Ketersediaan Tinggi).
2. Pilih **Standalone MySQL Server/Classic MySQL Replication** (Server MySQL Mandiri/Replikasi MySQL Klasik) dan klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/5355f286598388f9e9846bf8122e6d98.png)
3. Di jendela **Type and Networking** (Jenis dan Jaringan), pertahankan konfigurasi default. Klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut:
> 
> - Jaringan TCP/IP diaktifkan secara default.
> - Port 3306 digunakan secara default.
> 
![](https://main.qcloudimg.com/raw/fbece2fafb34beb5825ae294a8e214fd.png)
4. Di jendela **Authentication Method** (Metode Autentikasi), pertahankan konfigurasi default. Klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/402624aaf02dce01ca2912d3548c03de.png)
5. Atur kata sandi root dan klik **Next** (Selanjutnya) seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/a0472f0b93c590997e78c2f590a0f901.png)
6. Di jendela **Windows Service** (Layanan Windows), pertahankan konfigurasi default dan klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/a85625c446218a275e743ff0ec599ece.png)
7. Di jendela **Apply Configuration** (Terapkan Konfigurasi), klik **Execute** (Jalankan).
![](https://main.qcloudimg.com/raw/2ee6000630d88774951ddf8aaea16fbb.png)
8. Klik **Finish** (Selesai) untuk menyelesaikan konfigurasi MySQL.

#### Mengonfigurasi Router MySQL

1. Di jendela **Product Configuration** (Konfigurasi Produk), klik **Next** (Selanjutnya).
2. Di jendela **MySQL Router Configuration** (Konfigurasi Router MySQL), pertahankan konfigurasi default dan klik **Finish** (Selesai), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/adece1334b6e1579eb2ace782cf47c59.png)

#### Mengonfigurasi sampel MySQL

1. Di jendela **Product Configuration** (Konfigurasi Produk), klik **Next** (Selanjutnya).
2. Di jendela **Connect to Server** (Hubungkan ke Server), masukkan kata sandi root. Klik **Check** (Periksa), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/ab8637391012a14ab2e5160c61675912.png)
3. Setelah kata sandi berhasil diautentikasi, klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/bff0aece8da11d15a52f4db91b4d7e69.png)
4. Di jendela **Apply Configuration** (Terapkan Konfigurasi), klik **Execute** (Jalankan).
![](https://main.qcloudimg.com/raw/8fe1f90eed50860e064044b314719cf6.png)
5. Klik **Finish** (Selesai) untuk menyelesaikan konfigurasi sampel MySQL.
6. Di jendela **Product Configuration** (Konfigurasi Produk), klik **Next** (Selanjutnya).
7. Di jendela **Installation Complete** (Penginstalan Selesai), pilih komponen lingkungan MySQL yang ingin Anda mulai dan klik **Finish** (Selesai), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/13f46296b85b00ce7e3bd08be13108c9.png)
 - Jika MySQL Workbench dimulai, MySQL berhasil diinstal, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/288f4cfbf1a9671b73dff64a940e0dc1.png)
 - Jika MySQL Shell dimulai, MySQL berhasil diinstal, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/90b788ffe3a8f92e0e5e70f35fb94356.png)


### Menambahkan Aturan Grup Keamanan

Tambahkan aturan masuk untuk mengizinkan lalu lintas pada port 3306 ke grup keamanan yang terikat ke instans CVM tempat MySQL diinstal.




