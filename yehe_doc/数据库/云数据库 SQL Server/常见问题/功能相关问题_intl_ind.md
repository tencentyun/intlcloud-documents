### Apa itu SQL Server?
SQL Server adalah database relasional dari Microsoft. SQL Server memiliki skalabilitas dan performa tinggi serta kemampuan untuk mengkueri, mencari, menyinkronkan, melaporkan, dan menganalisis data. Ada beberapa edisi SQL Server, dan setiap edisi memiliki fitur unik tersendiri.
Database mendukung SQL Server 2008 R2 SP3, 2012 SP3, dan 2016 SP1, yang memungkinkan aplikasi kustom yang dikembangkan oleh Microsoft .NET dan Visual Studio. Dengan banyak fitur baru dan peningkatan utama dalam penggunaan data dalam arsitektur berorientasi layanan (SOA) dan proses bisnis berbasis Microsoft BizTalk Server, 2016 SP1 telah menjadi versi SQL Server yang paling kuat dan inklusif. Anda dapat dengan mudah menyiapkan, mengoperasikan, dan meningkatkan deployment SQL Server di cloud untuk mengatasi perubahan bisnis yang cepat.

### Seperti apa arsitektur TencentDB for SQL Server?
TencentDB for SQL Server terdiri dari database master dan database cermin yang di-deploy di rak yang berbeda. Setiap database sesuai dengan sekelompok agen pemantau yang memantau database secara real time berdasarkan detak jantung. Pusat penjadwalan manajemen klaster terdiri dari dua set klaster pengambilan keputusan dan klaster konfigurasi yang di-deploy secara independen dan utamanya digunakan untuk mengelola operasi normal grup node database, klaster gateway akses, dan HDFS. Sistem file terdistribusi Hadoop (HDFS) menyediakan layanan pemulihan bencana data dengan cadangan cold. Klaster gateway diakses untuk memberikan IP unik, dan jika node data dialihkan, IP tidak akan berubah.

### Bagaimana cara membuat instans TencentDB for SQL Server dan terhubung ke database?
Anda dapat mengelola database di Konsol TencentDB for SQL Server.
Untuk petunjuk terperinci, lihat [Membuat Instans dan Menghubungkan ke Database].

### Bagaimana cara mengelola akun instans TencentDB for SQL Server?
TencentDB for SQL Server tidak mengizinkan pembuatan/penghapusan database dan membuat/menghapus/memodifikasi akun melalui Microsoft SQL Server Management. Anda dapat membuka **[TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver) > Instance Details page > Account Management** ([Konsol TencentDB for SQL Server] > halaman Detail Instans > Manajemen Akun) untuk membuat dan menghapus akun atau mengubah izin akun.
Saat ini, konsol hanya mengizinkan Anda untuk menggunakan izin "baca-tulis" dan "baca-saja". Jika Anda memerlukan izin di tingkat yang lebih tinggi, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk aplikasi (tidak ada akun sa yang disediakan).

### Bagaimana cara memantau instans TencentDB for SQL Server?
TencentDB for SQL Server mendukung 25 parameter umum SQL Server. Anda dapat mengumpulkan statistik parameter lain dengan mengonfigurasi penghitung SSMS. Untuk informasi selengkapnya, silakan lihat [Pemantauan dan Alarm](https://intl.cloud.tencent.com/document/product/238/7524).
Saat ini, alarm didukung untuk metrik berikut melalui Cloud Monitor. Anda dapat mengonfigurasi alarm di **[Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview)** (Konsol Cloud Monitor) > **Alarm Configuration** (Konfigurasi Alarm) > **Alarm Policy** (Kebijakan Alarm).
- Penggunaan CPU
- Jumlah Koneksi
- Lalu Lintas Masuk
- Lalu Lintas Keluar
- IOPS
- Kapasitas penyimpanan

### Bagaimana cara mengembalikan instans TencentDB for SQL Server?
Cadangan lengkap dan log di TencentDB for SQL Server disimpan selama tujuh hari; oleh karena itu, Anda dapat kembali ke titik waktu mana pun dalam tujuh hari terakhir.
Untuk petunjuk terperinci, lihat [Pengembalian Instans Database](https://intl.cloud.tencent.com/document/product/238/7522).

### Bagaimana cara mencadangkan instans TencentDB for SQL Server?
Di Konsol TencentDB for SQL Server, Anda dapat memulihkan database ke instans lain (seperti instans yang dibuat sendiri) menggunakan file cadangan yang diunduh.
Untuk petunjuk terperinci, lihat [Cadangan Instans Database](https://intl.cloud.tencent.com/document/product/238/7523).


### Bagaimana cara memigrasikan data ke TencentDB for SQL Server?
TencentDB for SQL Server mendukung migrasi data dari [instans SQL Server yang dibuat oleh CVM](https://intl.cloud.tencent.com/document/product/238/31421) atau [COS](https://intl.cloud.tencent.com/document/product/238/19103).

### Bagaimana cara meningkatkan instans TencentDB for SQL Server?
Peningkatan berarti meningkatkan instans TencentDB for SQL Server yang ada ke spesifikasi yang lebih tinggi.
1. Pilih instans di [Konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver) dan klik **Upgrade** (Peningkatan) di kolom **Operation** (Operasi).
2. Pada halaman peningkatan yang muncul, pilih spesifikasi yang diinginkan berdasarkan kebutuhan Anda dan lakukan pembayaran. Setelah pembayaran selesai, sistem akan meningkatkan spesifikasi instans secara otomatis.
Biaya peningkatan = (harga spesifikasi target - harga spesifikasi awal) x sisa masa berlaku


>- Anda hanya dapat meningkatkan instans ke spesifikasi yang lebih tinggi. Penurunan spesifikasi tidak didukung.
>- Anda tidak dapat membatalkan proses peningkatan setelah dimulai.

