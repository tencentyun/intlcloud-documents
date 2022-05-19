
## Ikhtisar
Konsol TencentDB for SQL Server menyediakan daftar file cadangan yang dapat diunduh melalui jaringan pribadi atau publik. File tersebut kemudian dapat digunakan untuk memulihkan data dari satu database ke database lain (seperti database yang dibuat secara mandiri).

## Petunjuk
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada tab **Backup Management** (Manajenen Cadangan), lihat daftar cadangan.
 - Untuk mengunduh file cadangan yang diarsipkan, cari catatan cadangan di daftar cadangan, klik **Download** (Unduh) di kolom **Operation** (Operasi), dan unduh file di halaman unduhan yang ditampilkan.
![](https://main.qcloudimg.com/raw/30fb714fc7a8751b2833f50a2c0de654.png)
 - Untuk mengunduh file cadangan yang tidak diarsipkan, klik catatan cadangan di daftar cadangan untuk memperluas daftar berlapis, klik **Download** (Unduh) di kolom **Operation** (Operasi), dan unduh file cadangan dari setiap database pada halaman unduhan yang ditampilkan.
3. Dapatkan alamat unduhan file cadangan di kotak dialog pop-up.
>?
>- Salin **alamat unduhan** jaringan pribadi, [login ke CVM Linux di VPC yang sama dengan instans TencentDB](https://intl.cloud.tencent.com/document/product/213/10517), dan jalankan `wget` untuk mengunduh file melalui jaringan pribadi berkecepatan tinggi.
>- Alamat unduhan berlaku selama 15 menit, setelah itu Anda harus masuk lagi ke halaman unduhan untuk mendapatkan alamat unduhan baru.
>
![](https://main.qcloudimg.com/raw/b7a7289733af5100008952ed1ba3b589.png)


