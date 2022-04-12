
## Ikhtisar
>?Untuk menghemat kapasitas penyimpanan, cadangan fisik dan logis di TencentDB for MySQL harus dikompresi dengan qpress lalu dikemas dengan xbstream yang ditawarkan oleh Percona.
>
Percona XtraBackup sumber terbuka dapat digunakan untuk mencadangkan dan memulihkan database. Dokumen ini menjelaskan cara menggunakan XtraBackup untuk memulihkan file cadangan fisik instans TencentDB for MySQL ke database yang dibuat sendiri di CVM.
- XtraBackup hanya mendukung sistem operasi Linux.
- Untuk informasi selengkapnya tentang cara memulihkan data di Windows, lihat [Migrasi Data Offline > Migrasi Data dengan Alat Baris Perintah](https://intl.cloud.tencent.com/document/product/236/8464).

## Prasyarat
- Unduh dan instal XtraBackup.
 - Untuk MySQL versi 5.6 dan 5.7, unduh Percona XtraBackup versi 2.4.6 atau yang lebih baru di [situs web resmi Percona](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Untuk informasi selengkapnya tentang penginstalan, lihat [dokumentasi Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
 - Untuk MySQL 8.0, unduh Percona XtraBackup versi 8.0.22-15 atau yang lebih baru di [situs web resmi Percona](https://www.percona.com/downloads/Percona-XtraBackup-LATEST/#). Untuk informasi selengkapnya tentang penginstalan, lihat [dokumentasi Percona XtraBackup 8.0](https://www.percona.com/doc/percona-xtrabackup/8.0/installation.html).
- Arsitektur instans yang didukung: MySQL dua node atau tiga node
- Instans dengan enkripsi data yang diaktifkan tidak dapat dipulihkan dari cadangan fisik.

## Petunjuk
>?Dokumen ini mengambil instans CVM yang menjalankan CentOS dan instans MySQL v5.7 sebagai contoh.
>
### Langkah 1. Mengunduh file cadangan
Anda dapat mengunduh pencadangan data dan pencadangan log instans TencentDB for MySQL di konsol.
>?Setiap IP dapat memiliki hingga 10 tautan unduhan secara default, dengan batas kecepatan unduh masing-masing 20-30 Mbps.
>
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Pada tab **Backup and Restore** (Cadangkan dan Pulihkan) > **Data Backup List** (Daftar Cadangan Data), cari file cadangan yang akan diunduh dan klik **Download** (Unduh) di kolom **Operation** (Operasi).
3. Salin alamat unduhan di kotak dialog pop-up, [login ke CVM Linux di VPC yang sama dengan instans TencentDB](https://intl.cloud.tencent.com/document/product/213/10517), dan jalankan `wget` untuk mengunduh file melalui jaringan pribadi berkecepatan tinggi .
>?
>- Anda juga dapat mengklik **Download** (Unduh) untuk mengunduhnya secara langsung. Namun, ini mungkin memakan waktu lebih lama.
>- Format perintah `wget`: wget -c 'alamat unduhan file cadangan' -O nama file kustom.xb 
>
Contohnya adalah sebagai berikut:
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O /data/test.xb
```

### Langkah 2. Memulihkan data
#### 2.1 Buka paket file cadangan
Jalankan perintah `xbstream` untuk membuka file cadangan ke direktori target.
```
xbstream -x --parallel=2  -C /data/mysql < /data/test.xb
```
>?
>- Direktori target `/data/mysql` digunakan sebagai contoh dalam dokumen ini. Anda dapat menggantinya dengan direktori yang sebenarnya Anda gunakan untuk menyimpan file cadangan.
>- Ganti `/data/test.xb` dengan file cadangan Anda.
>
Hasil file yang dibuka ditampilkan di bawah ini:
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

#### 2.2 Dekompresi file cadangan
1. Unduh qpress dengan menjalankan perintah berikut:
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10. http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?Jika kesalahan ditampilkan selama pengunduhan `wget`, Anda dapat mengunjungi [situs web resmi QuickLZ](http://www.quicklz.com/) untuk mengunduh qpress secara lokal dan mengunggahnya ke instans CVM Linux. Untuk informasi selengkapnya, lihat [Mengunggah File dari Linux atau MacOS ke CVM Linux melalui SCP](https://intl.cloud.tencent.com/document/product/213/2133).
>
2. Ekstrak file biner qpress dengan menjalankan perintah berikut.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Dekompresi semua file `.qp` di direktori tujuan dengan menjalankan perintah qpress berikut:
```
xtrabackup --decompress --target-dir=/data/mysql
```
>?
>- `/data/mysql` adalah direktori target tempat file cadangan disimpan sebelumnya. Anda dapat menggantinya dengan direktori yang sebenarnya Anda gunakan.
>- Opsi `--remove-original` hanya didukung di Percona Xtrabackup v2.4.6 dan yang lebih baru.
>- `xtrabackup` tidak akan menghapus file asli selama dekompresi secara default. Jika Anda ingin menghapusnya setelah dekompresi selesai, tambahkan parameter `--remove-original` ke perintah di atas.
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

#### 2.3 Siapkan file cadangan
Setelah file cadangan didekompresi, Anda perlu menjalankan operasi "apply log" dengan menjalankan perintah berikut.
```
xtrabackup --prepare  --target-dir=/data/mysql
```
Jika hasil eksekusi berisi output berikut, berarti persiapan berhasil.
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
		
#### 2.4 Modifikasi file konfigurasi
1. Jalankan perintah berikut untuk membuka file `backup-my.cnf`.
```
vi /data/mysql/backup-my.cnf
```
>?Direktori target `/data/mysql` digunakan sebagai contoh dalam dokumen ini. Anda dapat menggantinya dengan direktori yang sebenarnya Anda gunakan.
>
2. Mengingat masalah versi yang ada, parameter berikut perlu diberi komentar dari file yang diekstrak `backup-my.cnf`.
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 

 ![](https://qcloudimg.tencent-cloud.cn/raw/6d56154cb19d16b56520199290a0c574.png)

#### 2.5 Modifikasi atribut file
Modifikasi atribut file dan periksa apakah file dimiliki oleh pengguna `mysql`.
```
chown -R mysql:mysql /data/mysql
```
![](https://qcloudimg.tencent-cloud.cn/raw/12fbe7f70fefa19fd7af5ac2f95bfdb8.png)

### Langkah 3. Memulai proses mysqld dan login untuk verifikasi
1. Mulai proses mysqld.
```
mysqld_safe --defaults-file=/data/mysql/backup-my.cnf --user=mysql --datadir=/data/mysql &
```
2. Login ke klien untuk verifikasi.
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

## Pertanyaan Umum terkait Cadangan
Lihat [Masalah Umum](https://intl.cloud.tencent.com/document/product/236/9036) dan [Alasan Kegagalan](https://intl.cloud.tencent.com/document/product/236/34394).
