## Ikhtisar
Dokumen ini menjelaskan cara menghubungkan ke instans TencentDB for SQL Server melalui Studio Manajemen Server SQL (SSMS) pada instans CVM Windows dan menjalankan kueri sederhana.
>?
>- Instans CVM dan TencentDB lebih baik dikelola pada akun yang sama dan di VPC yang sama di wilayah yang sama.
>- Instans CVM dan TencentDB di VPC yang sama di AZ yang berbeda di wilayah yang sama dapat langsung terhubung melalui IP pribadi.
>- Instans CVM dan TencentDB di wilayah atau VPC yang berbeda atau pada akun yang berbeda dapat saling terhubung melalui [Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553/18836) atau [CCN](https://intl.cloud.tencent.com/zh/document/product/1003/31985).

## Petunjuk
1. Login ke konsol [TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver), klik nama instans untuk masuk ke halaman detail instans, dan lihat IP pribadi dan nomor port instans, yang akan digunakan untuk menghubungkan ke instans TencentDB.
![](https://main.qcloudimg.com/raw/343f649c398b60f859c4aa5b47d7d47f.png)
2. Login ke instans CVM Windows. Untuk informasi selengkapnya, silakan lihat [Menyesuaikan Konfigurasi CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516). Dokumen ini menggunakan Windows Server 2012 R2 Standard Edition (64-bit) sebagai contoh.
3. Unduh dan instal [Studio Manajemen Server SQL](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) pada instans CVM Windows. Untuk informasi selengkapnya tentang SSMS, silakan lihat [Menggunakan Studio Manajemen Server SQL](https://docs.microsoft.com/en-us/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
4. Mulai SSMS pada instans CVM Windows. Pada halaman **Connect to Server** (Hubungkan ke Server), masukkan informasi yang relevan untuk terhubung ke TencentDB. Klik **Connect** (Hubungkan) dan tunggu beberapa menit sebelum SSMS terhubung ke instans database Anda.
 - **Server type** (Jenis server): pilih **Database Engine** (Mesin Database).
 - **Server name** (Nama server): masukkan IP pribadi dan nomor port instans dan pisahkan dengan koma. Misalnya, jika IP pribadi instans adalah `10.10.10.10` dan nomor port adalah `1433`, masukkan `10.10.10.10,1433` di sini.
 - **Authentication** (Autentikasi): pilih **SQL Server Authentication** (Autentikasi SQL Server).
 - **Login** (Login) dan **Password** (Kata sandi): masukkan nama akun dan kata sandi yang Anda konfigurasikan saat membuat akun instans di halaman **Account Management** (Manajemen Akun).
![](https://main.qcloudimg.com/raw/31be70916eda52a393d97dcca5be90f8.png)
5. Setelah terhubung ke database, Anda dapat melihat database sistem bawaan standar (master, model, msdb, dan tempdb) dari SQL Server.
![](https://main.qcloudimg.com/raw/a25241cf8000e10bcf748abe99773a77.png)
6. Sekarang Anda dapat mulai membuat database Anda sendiri dan menjalankan kueri untuk database tersebut. Pilih **File** (File) > **New** (Baru) > **Query with Current Connection** (Kueri dengan Koneksi Saat Ini) dan ketikkan kueri SQL berikut:
```
pilih @@VERSI
```
Jalankan kueri. SSMS akan menampilkan instans TencentDB for SQL Server.
![](https://main.qcloudimg.com/raw/71c5d9603eae4484c84b2e12a3d721ce.png)

