- Jangan gunakan Microsoft SQL Server Management Studio (SSMS) untuk membuat atau menghapus database, atau membuat, menghapus, atau memodifikasi akun database, atau pesan "Pengecualian terjadi saat menjalankan pernyataan Transact-SQL atau pemrosesan batch" mungkin diminta. Anda dapat melakukan operasi ini di [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver).

- Untuk instans kluster atau ketersediaan tinggi server ganda, TencentDB for SQL Server melarang peran `sysadmin` secara default untuk menghindari risiko penyusupan. Jika bisnis Anda harus menggunakan peran ini, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).
Saat Anda mencoba mengelola database di SSMS, pesan "Anda harus menjadi anggota peran sysadmin untuk melakukan operasi ini" mungkin diminta.

- Untuk instans edisi dasar, TencentDB for SQL Server memungkinkan akun admin memberikan izin kepada pengguna untuk menggunakan peran `sysadmin`. 
