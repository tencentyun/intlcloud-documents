
Pelacakan perubahan (CT) dapat diterapkan untuk melacak tabel atau bahkan kolom tertentu dalam database. Saat Anda melakukan operasi penambahan, modifikasi, atau penghapusan dalam tabel dengan CT diaktifkan, sistem akan menghasilkan nomor versi secara otomatis untuk operasi dan merekam informasi operasi, termasuk stempel waktu operasi, jenis operasi, dan kunci utama dari data yang terpengaruh.

CT hanya mencatat apakah baris dalam tabel telah diubah tetapi bukan data yang diubah, sehingga berdampak kecil pada performa operasi data. Informasi tersebut akan dicatat dalam tabel sistem SQL Server dan dihapus dan dipelihara oleh sistem secara otomatis.

## Mengaktifkan/Menonaktifkan CT untuk Satu Database
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Database Management** (Manajemen Database), pilih baris database target, dan klik **Other** (Lainnya) > **Enable/Disable CT** (Aktifkan/Nonaktifkan CT) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/521e8a6f5d36f2b2d29ca4cf0fa72ef2.png)
3. Jendela pop-up menampilkan nama dan status CT database saat ini. Setelah mengaktifkan atau menonaktifkan CT, klik **OK** (OKE). Jika Anda mengaktifkan CT, Anda dapat mengatur periode penyimpanan data.
![](https://main.qcloudimg.com/raw/bf32e15a168c9d43a69655f0df209558.png)
Anda dapat melihat kemajuan tugas mengaktifkan atau menonaktifkan CT melalui **Current Task** (Tugas Saat Ini) di sudut kanan atas tab **Database Management** (Manajemen Database).
![](https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png)

## Mengaktifkan/Menonaktifkan CT untuk Beberapa Database Secara Massal
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans untuk mengakses halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Database Management** (Manajemen Database), pilih baris database target, dan klik **Batch Management** (Manajemen Database) > **Batch Enable/Disable CDC** (Aktifkan/Nonaktifkan CT Secara Massal) di bagian atas daftar.
![](https://main.qcloudimg.com/raw/90ee38dc0216b446a52ea238819a31e4.png)
3. Jendela pop-up menampilkan nama dan status CT database saat ini. Setelah mengaktifkan atau menonaktifkan CT, klik **OK** (OKE). Jika Anda mengaktifkan CT, Anda dapat mengatur periode penyimpanan data.
![](https://main.qcloudimg.com/raw/bf32e15a168c9d43a69655f0df209558.png)
Anda dapat melihat kemajuan tugas mengaktifkan atau menonaktifkan CT melalui **Current Task** (Tugas Saat Ini) di sudut kanan atas tab **Database Management** (Manajemen Database).
![](https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png)
