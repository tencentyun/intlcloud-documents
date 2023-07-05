### Bagaimana cara melihat CVM yang sedang digunakan?

Anda bisa login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) untuk melihat CVM yang sedang digunakan.

### Bisakah VM diinstal di CVM?

Tidak.

### Bagaimana cara mematikan instans?

Untuk informasi selengkapnya, lihat [Mematikan Instans](https://intl.cloud.tencent.com/document/product/213/4929).

### Bagaimana cara memulai ulang instans?

Untuk informasi selengkapnya, lihat [Memulai Ulang Instans](https://intl.cloud.tencent.com/document/product/213/4928).

### Bagaimana cara menghentikan instans?

Untuk informasi selengkapnya, lihat [Menghentikan Instans](https://intl.cloud.tencent.com/document/product/213/4930).

### Bagaimana cara menanyakan nama pengguna dan kata sandi instans Linux?
Setelah membuat instans CVM, nama pengguna dan kata sandinya akan dikirimkan ke akun Anda melalui [Pusat Pesan](https://console.cloud.tencent.com/message). Secara default, akun admin dari instans Linux adalah `root`.

### Bagaimana cara membuat pertanyaan, mempartisi, dan memformat disk instans Linux?

Anda bisa menjalankan perintah `df -h` untuk menanyakan kapasitas total dan kapasitas disk yang digunakan dan menjalankan perintah `fdisk -l` untuk melihat informasi disk. Untuk informasi tentang cara mempartisi dan memformat disk instans Linux, lihat [Menginisialisasi Disk Cloud (Kurang dari 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) dan [Menginisialisasi Disk Cloud (Lebih dari 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### Bagaimana cara mengunggah file ke instans Linux?
- Anda bisa [menggunakan SCP untuk mengunggah file ke instans Linux](https://intl.cloud.tencent.com/document/product/213/2133).
- Anda bisa [menggunakan FTP untuk mengunggah file ke instans Linux](https://intl.cloud.tencent.com/document/product/213/35307).

### Bagaimana cara mengubah pemilik dan grup pemilik direktori serta file pada instans Linux?
Jika izin file atau direktori salah dikonfigurasi di server Web, maka akan terjadi kesalahan 403 saat Anda mengakses situs web yang dihosting di instans. Oleh karena itu, sebelum Anda menyesuaikan file atau direktori, Anda harus mengonfirmasi identitas tempat pemrosesan file atau direktori sedang berjalan.
- Anda bisa menjalankan perintah `ps` dan `grep` untuk menanyakan identitas tempat pemrosesan file atau direktori sedang berjalan.
- Anda bisa menjalankan perintah `ls –l` untuk mengajukan pertanyaan kepada pemilik dan grup pemilik file dan direktori.
- Anda bisa menjalankan perintah `chown` untuk mengubah izin. Misalnya, Anda bisa menjalankan perintah `chown -R www.www /tencentcloud/www/user/` untuk mengubah pemilik dan grup pemilik semua file dan direktori di bawah direktori `/tencentcloud/www/user` menjadi akun “www”.

### Apakah instans Linux mendukung desktop visual?
Ya, asalkan Anda sudah membuat desktop visual pada instans Linux. Untuk informasi selengkapnya, lihat [Membangun Desktop Visual Ubuntu](https://intl.cloud.tencent.com/document/product/213/37500).

### Mengapa saya tidak bisa menambahkan kartu suara atau video ke instans CVM?
Tencent Cloud CVM tidak menyediakan server multimedia dan komponen kartu suara dan video secara default. Oleh karena itu, kartu suara dan video tidak bisa ditambahkan ke instans CVM.

### Bisakah saya mentransfer waktu yang tidak digunakan dari instans CVM ke instans CVM lain?
Tidak. Jika Anda menginginkan fleksibilitas dan efisiensi biaya yang lebih tinggi, sebaiknya membeli instans bayar sesuai pemakaian saja.

### Bagaimana cara menanyakan wilayah tempat alamat IP instans CVM berada?
Alamat IP instans CVM terletak di wilayah yang sama dengan tempat Anda membeli instans CVM.

### Apakah instans CVM menyediakan database secara default?
Tidak. Untuk menggunakan layanan database, Anda bisa:
- Men-deploy database Anda sendiri. Misalnya, Anda bisa [memasang dan membangun MySQL](https://intl.cloud.tencent.com/document/product/213/10190).
- Membeli [TencentDB untuk MySQL](https://intl.cloud.tencent.com/product/cdb) secara terpisah.

### Bisakah saya membangun database pada instans CVM?
Ya. Anda bisa menginstal perangkat lunak database dan mengonfigurasi lingkungan database di instans CVM sesuai kebutuhan. Anda juga bisa membeli [TencentDB untuk MySQL](https://intl.cloud.tencent.com/product/cdb) secara terpisah.

### Apakah instans CVM mendukung database Oracle?
Ya. Sebelum menginstal database Oracle, kami sarankan agar Anda melakukan uji tekanan performa di instans CVM target untuk memastikan bahwa instans bisa memenuhi persyaratan baca/tulis database.

### Kapan saya bisa menghentikan instans CVM secara paksa? Apa saja konsekuensi dari penghentian paksa instans CVM?
Anda bisa menghentikan instans CVM secara paksa bila penonaktifan normal gagal. Harap dicatat bahwa penghentian paksa sama dengan pemadaman listrik dan dapat mengakibatkan hilangnya data yang belum disimpan.
