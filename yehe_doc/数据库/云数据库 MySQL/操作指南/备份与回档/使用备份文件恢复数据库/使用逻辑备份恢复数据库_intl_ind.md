## Ikhtisar
>?Untuk menghemat kapasitas penyimpanan, cadangan fisik dan logis di TencentDB for MySQL akan dikompresi dengan qpress lalu dikemas dengan xbstream yang ditawarkan oleh Percona.

TencentDB for MySQL mendukung [pencadangan logis](https://intl.cloud.tencent.com/document/product/236/37796). Di konsol, Anda dapat membuat file cadangan logis secara manual dari seluruh instans atau database/tabel tertentu dan mengunduhnya. Dokumen ini menjelaskan cara memulihkan data secara manual dari file cadangan logis.

- Metode pemulihan yang dijelaskan dalam dokumen ini hanya berlaku untuk Linux.
- Untuk informasi selengkapnya tentang cara memulihkan data di Windows, harap lihat [Migrasi Data Offline > Migrasi Data dengan Alat Baris Perintah](https://intl.cloud.tencent.com/document/product/236/8464).
- Arsitektur instans yang didukung: MySQL dua node atau tiga node

## Petunjuk
### Langkah 1. Mengunduh file cadangan
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada tab **Backup and Restore** (Cadangkan dan Pulihkan) > **Data Backup List** (Daftar Cadangan Data), cari file cadangan yang akan diunduh dan klik **Download** (Unduh) di kolom **Operation** (Operasi).
3. Sebaiknya salin tautan unduhan di kotak dialog pop-up, login ke instans [(Linux) CVM di VPC yang sama dengan instans TencentDB](https://intl.cloud.tencent.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8), dan jalankan perintah `wget` untuk mengunduh melalui jaringan pribadi dengan kecepatan yang lebih tinggi.
>?
>- Anda juga dapat mengeklik **Download** (Unduh) untuk mengunduhnya secara langsung, yang mungkin membutuhkan waktu lebih lama.
>- Format perintah `wget`: wget -c 'alamat unduhan file cadangan' -O nama file kustom.xb
>
Contoh:
```
wget -c 'https://mysql-database-backup-bj-118.cos.ap-beijing.myqcloud.com/12427%2Fmysql%2F42d-11ea-b887-6c0b82b%2Fdata%2Fautomatic-delete%2F2019-11-28%2Fautomatic%2Fxtrabackup%2Fbk_204_10385%2Fcdb-1pe7bexs_backup_20191128044644.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3D1%26q-sign-time%3D1574269%3B1575417469%26q-key-time%3D1575374269%3B1517469%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dfb8fad13c4ed&response-content-disposition=attachment%3Bfilename%3D%2141731_backup_20191128044644.xb%22&response-content-type=application%2Foctet-stream' -O test0.xb
```

### Langkah 2. Buka paket file cadangan
Buka paket file cadangan dengan xbstream.
>?xbstream dapat diunduh di [situs web resmi Percona](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Harap pilih Percona XtraBackup v2.4.6 atau yang lebih baru. Untuk informasi selengkapnya tentang penginstalan, harap lihat [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
```
xbstream -x < test0.xb
```
>?Ganti `test0.xb` dengan file cadangan Anda.
>
Hasil file yang dibuka ditampilkan dalam gambar di bawah ini:
![](https://main.qcloudimg.com/raw/61b53f4f54ffd2fbe7c0d1b3423255b0.png)

### Langkah 3. Dekompresi file cadangan
1. Unduh qpress dengan menjalankan perintah berikut:
```
wget http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?Jika kesalahan ditampilkan selama pengunduhan `wget`, Anda dapat mengunjungi [situs web resmi QuickLZ](http://www.quicklz.com/) untuk mengunduh qpress secara lokal dan mengunggahnya ke instans CVM Linux. Untuk informasi selengkapnya, harap lihat [Mengunggah File melalui SCP ke CVM Linux dari Linux](https://intl.cloud.tencent.com/zh/document/product/213/2133).
2. Ekstrak file biner qpress dengan menjalankan perintah berikut:
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Dekompresi file cadangan dengan qpress.
```
qpress -d cdb-jp0zua5k_backup_20191202182218.sql.qp .
```
>?Temukan file cadangan dengan ekstensi `.sql.qp` dengan waktu dekompresi dan ganti `cdb-jp0zua5k_backup_20191202182218` dengan nama filenya.
>
Hasil dekompresi ditampilkan dalam gambar di bawah ini:
![](https://main.qcloudimg.com/raw/355557bc949fd86af8346d8a44dc4551.png)

### Langkah 4. Impor file cadangan ke database target
Impor file .sql ke database target dengan menjalankan perintah berikut:
```
mysql -uroot -P3306 -h127.0.0.1 -p < cdb-jp0zua5k_backup_20191202182218.sql
```
>?
>- Dokumen ini mengimpor ke instans MySQL lokal dengan port 3306 sebagai contoh. Anda dapat menggantinya sesuai kebutuhan.
>- Ganti `cdb-jp0zua5k_backup_20191202182218.sql` dengan file .sql yang diekstrak oleh qpress.
