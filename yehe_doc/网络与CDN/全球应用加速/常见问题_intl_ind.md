

### Masalah apa yang dapat diselesaikan dengan GAAP?
GAAP membantu vendor membuat koneksi jaringan berkecepatan tinggi antara pengguna akhir dan server bisnis untuk mengatasi latensi dan kelambatan akses lintas wilayah.

### Apa cakupan GAAP?
GAAP memiliki lebih dari 50 node global yang tersebar di Asia, Eropa, Amerika Selatan, Amerika Utara, dan Oseania. Ini menyediakan koneksi berkecepatan tinggi yang stabil dan efisien untuk bisnis di seluruh dunia yang memerlukan akses lintas wilayah atau berbagi server, menghindari kelambatan akses dan latensi tinggi.

### Bagaimana cara kerja GAAP?
Koneksi peering diatur antara wilayah akselerasi dan wilayah server asal sehingga pengguna dapat menghindari jaringan publik yang tidak stabil menggunakan jaringan pribadi global berkecepatan tinggi Tencent Cloud dan rute akses yang dioptimalkan. Akses bisnis langsung melalui koneksi berkecepatan tinggi memberikan pengalaman akses yang cepat dan stabil.

### Apa itu node akses dan node origin-pull?
- Akses node (sebelumnya wilayah akselerasi): sebuah node di wilayah pengguna atau wilayah dekat pengguna, yaitu, node entri dari koneksi akselerasi.
- Node Origin-Pull (sebelumnya wilayah server asal): sebuah node di wilayah server tujuan atau wilayah yang paling dekat dengan server tujuan, yaitu node origin-pull dari koneksi akselerasi. 

Misalnya, jika server Anda berlokasi di Hong Kong (Tiongkok), dan Anda ingin semua pengguna di beberapa wilayah seperti AS Barat, AS Timur, Jepang, dan Korea mengakses server melalui koneksi berkecepatan tinggi untuk akses yang cepat dan stabil pengalaman, node akses akan menjadi AS Barat, AS Timur, Jepang, dan Korea, sedangkan node origin-pull akan menjadi Hong Kong (Tiongkok).

### Protokol dan metode penerusan apa yang didukung GAAP?
GAAP mendukung protokol TCP/UDP/HTTP/HTTPS pada lapisan 4 dan 7 dan IP/penerusan nama domain.

### Apakah GAAP mendukung server asal untuk mendapatkan IP pengguna nyata?
GAAP mendukung server asal untuk mendapatkan IP pengguna nyata.

### Apa saja skenario aplikasi GAAP?
GAAP dapat digunakan untuk akses bisnis lintas wilayah, seperti e-commerce global dan server game terpadu secara global. Untuk informasi selengkapnya tentang skenario aplikasi dan konfigurasi, harap lihat [Skenario Aplikasi](https://intl.cloud.tencent.com/document/product/608/13760).

### Bagaimana jika akun kolaborator tidak memiliki izin untuk mengakses GAAP?
Harap hubungi administrator akun root atau akun lain yang memiliki izin `AdministratorAccess` untuk memberikan izin baca/tulis atau baca-saja dari GAAP kepada kolaborator, seperti yang diinstruksikan di [Mengonfigurasi Izin](https://intl.cloud.tencent.com/document/product/608/31510).


