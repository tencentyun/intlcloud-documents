## Ikhtisar
TencentDB for SQL Server mendukung pembuatan dan penghapusan akun serta modifikasi izin akun di halaman **Manage Account** (Kelola Akun) di konsol. Operasi tersebut tidak dapat dilakukan di Microsoft SQL Server Management.
>?Nama akun dan kata sandi yang dibuat akan digunakan saat menghubungkan ke TencentDB for SQL Server. Harap simpan dengan benar.
>

## Petunjuk
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver) dan klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Di halaman manajemen instans, pilih **Manage Account** (Kelola Akun) > **Create Account** (Buat Akun) dan masukkan informasi yang relevan di jendela pop-up. Setelah mengonfirmasi bahwa semua konfigurasi sudah benar, klik **OK** (OKE).
 - 	 Nama Akun: wajib diisi, dapat berisi 1–50 huruf, angka, atau garis bawah, dan harus dimulai dengan huruf.
 - 	Admin: ini bersifat opsional. Setiap instans TencentDB for SQL Server dapat memiliki satu akun admin, yang memiliki izin baca/tulis ke semua database secara default. Database yang baru ditambahkan akan diotorisasi secara otomatis untuk akun admin tanpa memerlukan otorisasi manual.
>?Ada tiga jenis izin akun di TencentDB for SQL Server:
>- Admin: secara default, ia memiliki izin baca/tulis ke semua database. Hanya satu akun admin yang dapat diatur untuk satu instans.
>- Baca/Tulis: akun admin ini memiliki izin baca/tulis ke database resmi dan dapat melakukan perubahan database.
>- Baca saja: akun admin ini memiliki izin baca saja hanya untuk database yang diotorisasi dan tidak dapat melakukan perubahan.
 - Database: ini bersifat opsional. Anda dapat mengatur izin (baca saja atau tulis saja) yang dimiliki akun ke database saat membuat akun. Anda juga dapat memberikan izin saat memodifikasi izin atau membuat database.
 - Kata sandi: wajib diisi dan terdiri dari 8–32 karakter yang terdiri dari setidaknya dua jenis berikut: huruf, angka, dan simbol khusus (_+-&=!@#$%^()[]) .
 - Keterangan Akun: ini bersifat opsional dan dapat berisi hingga 256 karakter.
![](https://main.qcloudimg.com/raw/df24976a6bb9af279508c49e4f09f227.png)
3. Setelah akun dibuat, Anda dapat melakukan operasi seperti **Hapus Admin**, **Modifikasi Izin**, **Atur Ulang Kata Sandi**, dan **Hapus Akun** dalam daftar akun.
![](https://main.qcloudimg.com/raw/9a4a6c88f4e4a5b391241eca8080b09d.png)
