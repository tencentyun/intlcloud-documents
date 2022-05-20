## Ikhtisar
Dokumen ini menjelaskan cara menggunakan instans CVM Linux yang dilengkapi dengan IP publik untuk memetakan port, menghubungkan ke instans melalui Studio Manajemen Server SQL (SSMS), dan menjalankan kueri sederhana.
>?Instans CVM dan TencentDB harus berada di bawah akun yang sama dan di VPC yang sama di wilayah yang sama.

## Petunjuk
Untuk pertimbangan keamanan data, TencentDB for SQL Server saat ini tidak membuka IP publik untuk instans. Jika Anda memerlukan IP publik, Anda dapat menggunakan fungsi pemetaan port SSH2 untuk menghubungkan, mengonfigurasi, dan mengelola instans Anda dari internet.
1. Pada halaman detail instans [TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver), lihat IP pribadi dan nomor port instans, yang akan digunakan untuk mengonfigurasi pemetaan port.
![](https://main.qcloudimg.com/raw/343f649c398b60f859c4aa5b47d7d47f.png)
2. Siapkan instans CVM Linux **with a public IP** (dengan IP publik). Untuk informasi selengkapnya, silakan lihat [Menyesuaikan Konfigurasi CVM Linux](/doc/product/213/2936).
3. Login ke instans CVM Linux secara lokal dengan alat SSH seperti SecureCRT (seperti yang ditunjukkan dalam dokumen ini) atau PuTTY. Untuk metode login, silakan lihat [Login ke Instans Linux](/doc/product/213/5436).
4. Pilih **Options** (Opsi) > **Session Options** (Opsi Sesi) pada bilah menu SecureCRT untuk masuk ke halaman pengaturan properti sesi.
![](https://main.qcloudimg.com/raw/acbb1ad0a808ac59a0053063b75aab8b.png)
5. Pada halaman pengaturan properti sesi, pilih **Connection** (Koneksi) > **Port Forwarding** (Penerusan Port) > **Add** (Tambah) untuk masuk ke halaman konfigurasi pemetaan port.
![](https://main.qcloudimg.com/raw/05f0cadcda75c6f931f34eb296a5ab6f.png)
6. Pada halaman konfigurasi pemetaan port, konfigurasikan parameter yang sesuai.
![](https://main.qcloudimg.com/raw/e364bded7f3611ef9da1eae0c1d575bd.png)
7. Unduh dan instal [Studio Manajemen Server SQL](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) secara lokal. Untuk informasi selengkapnya tentang SSMS, silakan lihat [Menggunakan Studio Manajemen Server SQL](https://docs.microsoft.com/zh-cn/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
8. Mulai SSMS secara lokal. Pada halaman **Connect to Server** (Hubungkan ke Server), masukkan informasi yang relevan untuk terhubung ke TencentDB. Klik **Connect** (Hubungkan) dan tunggu beberapa menit sebelum SSMS terhubung ke instans database Anda.
 - **Server type** (Jenis server): pilih **Database Engine** (Mesin Database).
 - **Server name** (Nama server): masukkan alamat IP lokal dan nomor port dan pisahkan dengan koma, seperti `10.0.0.1,4000`. Nomor port harus sama dengan yang dikonfigurasi pada langkah 6.
 - **Authentication** (Autentikasi): pilih **SQL Server Authentication** (Autentikasi SQL Server).
 - **Login** (Login) dan **Password** (Kata sandi): masukkan nama akun dan kata sandi yang Anda konfigurasikan saat membuat akun instans di halaman **Account Management** (Manajemen Akun).
![](https://main.qcloudimg.com/raw/14d90aa2eda6c841680f0fdc74db8219.png)
9. Setelah terhubung ke database, Anda dapat melihat database sistem bawaan standar (master, model, msdb, dan tempdb) dari SQL Server.
![](https://main.qcloudimg.com/raw/c65c02197b506bd5b326128f1a3983a0.png)
10. Sekarang Anda dapat mulai membuat database Anda sendiri dan menjalankan kueri untuk database tersebut. Pilih **File** (File) > **New** (Baru) > **Query with Current Connection** (Kueri dengan Koneksi Saat Ini) dan ketikkan kueri SQL berikut:
```
pilih @@VERSI
```
Jalankan kueri. SSMS akan menampilkan instans TencentDB for SQL Server.
![](//mc.qcloudimg.com/static/img/fbf64c03c7addda9c80fdd3dac7bbebb/image.png)

