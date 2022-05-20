
### Apakah ada batas atas jumlah database di TencentDB for SQL Server?
Tidak; namun, demi performa, Anda disarankan untuk menjaga jumlah database yang dibuat dalam satu instans TencentDB for SQL Server di bawah 70. Jika Anda membutuhkan lebih banyak database, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meminta bantuan.

### Setelah database SQL Server dibuat, tidak ada atau hanya ada sejumlah kecil data yang ditulis, tetapi mengapa monitor kapasitas penyimpanan menunjukkan bahwa kapasitas sebesar 500 MB telah digunakan?
Ketika Tencent Cloud membuat setiap database SQL Server, Tencent Cloud secara otomatis akan mengalokasikan kapasitas awal sebesar 500 MB, dan data akan ditulis terlebih dahulu ke kapasitas awal tersebut ketika ada data yang dituliskan.
Oleh karena itu, bahkan jika Anda tidak menulis atau hanya menuliskan sejumlah kecil data, monitor kapasitas penyimpanan akan tetap menampilkan 500 MB.

### Setelah saya menghapus data yang ditulis ke instans TencentDB for SQL Server saya, monitor kapasitas penyimpanan masih menunjukkan bahwa kapasitas yang digunakan cukup besar. Bukankah kapasitas yang digunakan akan dilepaskan?
Setelah data dihapus dari SQL Server, file data yang diperluas tidak menyusut, dan kapasitas yang bebas di dalam file dapat mendukung operasi selanjutnya seperti penyisipan dan pembaruan.
Misalnya, jika Anda mengajukan instans 50 GB dan menulis data sebesar 50 GB ke database lalu menghapus semua data, monitor sistem akan menunjukkan bahwa Anda telah menggunakan kapasitas sebesar 50 GB. Namun, Anda masih dapat terus menulis banyak file.

### Saat mengelola database dengan Microsoft SQL Server Management, sistem menampilkan pesan "Login gagal. Login berasal dari domain yang tidak tepercaya dan tidak dapat digunakan dengan autentikasi Windows." Apa sebabnya?
Silakan ubah metode autentikasi menjadi "SQL Server Authentication".

### Bagaimana cara menggunakan pemetaan port SSH untuk manajemen instans TencentDB for SQL Server dari internet?
Untuk pertimbangan keamanan data, saat ini TencentDB for SQL Server tidak mendukung IP publik. Jika Anda perlu menggunakan IP publik, Anda dapat menggunakan fitur pemetaan port SSH2 untuk menghubungkan, mengonfigurasi, dan mengelola instans dari internet. Untuk petunjuk lebih rinci, silakan lihat [Menghubungkan ke Instans](https://cloud.tencent.com/document/product/238/11627).














