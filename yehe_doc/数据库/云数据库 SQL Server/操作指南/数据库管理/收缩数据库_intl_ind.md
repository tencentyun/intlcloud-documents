
TencentDB for SQL Server mendukung pengurangan ukuran database dengan menyusutkan semua file database untuk menghapus ruang yang tidak digunakan. Dokumen ini menjelaskan cara menyusutkan database di konsol TencentDB for SQL Server.

## Menyusutkan Satu Database
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada tab **Database Management** (Manajemen Database), cari baris database yang akan disusutkan dan klik **Other** (Lainnya) > **Shrink Database** (Susutkan Database) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/ffc76302b167d3a198ddcb3310125b07.png)
3. Jendela pop-up menampilkan nama database dan rasio ruang yang tersisa. Saat ini, hanya menyusut hingga 10% dari ruang kosong yang didukung.
>!Hanya 10% dari ruang kosong database yang akan tersisa setelah dikecilkan. Namun, jika 10% ruang kosong kurang dari 2 GB, ruang kosong akan menyusut menjadi 2 GB.
>
![](https://main.qcloudimg.com/raw/d778ec0f30dfd19ada706dbd2280a84d.png)
Anda dapat melihat kemajuan tugas penyusutan database melalui **Running Tasks** (Tugas yang Berjalan) di sudut kanan atas tab **Database Management** (Manajemen Database).
![](https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png)

## Menyusutkan Database Secara Massal
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada tab **Database Management** (Manajemen Database), pilih baris database yang akan disusutkan dan klik **Batch Management** (Manajemen Massal) > **Batch Shrink Databases** (Susutkan Database Secara Massal) di bagian atas daftar.
![](https://main.qcloudimg.com/raw/3f2cc7da03c47fdcee08cce3fd804822.png)
3. Jendela pop-up menampilkan nama database dan rasio ruang yang tersisa. Saat ini, hanya menyusut hingga 10% dari ruang kosong yang didukung.
>!Hanya 10% dari ruang kosong database yang akan tersisa setelah disusutkan. Namun, jika 10% ruang kosong kurang dari 2 GB, ruang kosong akan menyusut menjadi 2 GB.
>
<img src="https://main.qcloudimg.com/raw/38ddbb2395dd0f1b54dc5e63ca584180.png" style="zoom:70%;" /><br>
Anda dapat melihat kemajuan tugas penyusutan database melalui **Running Tasks** (Tugas yang Berjalan) di sudut kanan atas tab **Database Management** (Manajemen Database).
<img src="https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png" style="zoom:100%;" />

