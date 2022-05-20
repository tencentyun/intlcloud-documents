
Pengambilan data perubahan (CDC) digunakan untuk menangkap penyisipan, pembaruan, dan penghapusan yang diterapkan ke tabel SQL Server dan memberikan detail perubahan ini dalam format relasional yang mudah digunakan.

Tabel perubahan yang digunakan untuk CDC berisi kolom struktur kolom dari tabel sumber yang dilacak oleh gambar, serta metadata yang diperlukan untuk memahami perubahan yang telah terjadi. Setelah CDC diaktifkan untuk tabel, semua operasi DML dan DDL di atasnya akan direkam, yang membantu melacak perubahannya.

## Mengaktifkan/Menonaktifkan CDC untuk Satu Database
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Database Management** (Manajemen Database), pilih baris database target, dan klik **Other** (Lainnya) > **Enable/Disable CDC** (Aktifkan/Nonaktifkan CDC) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/b527d8852328d14a7a375dc0ab693d76.png)
3. Jendela pop-up menampilkan nama dan status database CDC saat ini. Setelah mengaktifkan atau menonaktifkan CDC, klik **OK** (OKE).
![](https://main.qcloudimg.com/raw/ea3716dbfcbbd14eec5a84faa057137a.png)<br>
Anda dapat melihat kemajuan tugas mengaktifkan atau menonaktifkan CDC melalui **Current Task** (Tugas Saat Ini) di sudut kanan atas tab **Database Management** (Manajemen Database).
![](https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png)

## Mengaktifkan/Menonaktifkan CDC untuk Beberapa Database Secara Massal
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans untuk mengakses halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Database Management** (Manajemen Database), pilih baris database target, dan klik **Batch Management** (Manajemen Database) > **Batch Enable/Disable CDC** (Aktifkan/Nonaktifkan CDC Secara Massal) di bagian atas daftar.
![](https://main.qcloudimg.com/raw/492b21e192566c64c17917325160182b.png)
3. Jendela pop-up menampilkan nama dan status CDC saat ini dari database yang dipilih. Setelah mengaktifkan atau menonaktifkan CDC, klik **OK** (OKE).
![](https://main.qcloudimg.com/raw/ea3716dbfcbbd14eec5a84faa057137a.png)
Anda dapat melihat kemajuan tugas mengaktifkan atau menonaktifkan CDC melalui **Current Task** (Tugas Saat Ini) di sudut kanan atas tab **Database Management** (Manajemen Database).
![](https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png)
