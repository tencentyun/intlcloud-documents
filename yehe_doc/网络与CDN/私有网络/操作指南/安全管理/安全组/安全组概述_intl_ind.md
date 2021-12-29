Grup keamanan adalah firewall virtual yang menampilkan pemfilteran paket data stateful. Ini digunakan untuk mengonfigurasi kontrol akses jaringan CVM, Cloud Load Balancer, TencentDB, dan instans lainnya sambil mengontrol lalu lintas keluar dan masuknya. Ini adalah sarana penting untuk isolasi keamanan jaringan.

Anda dapat mengonfigurasi aturan grup keamanan untuk mengizinkan atau menolak lalu lintas masuk dan keluar instans dalam grup keamanan.

## Fitur
- Grup keamanan adalah grup logis. Anda dapat menambahkan CVM, ENI, TencentDB, dan instans lainnya di wilayah yang sama dengan persyaratan isolasi keamanan jaringan yang sama ke grup keamanan yang sama.
- Secara default, instans dalam grup keamanan yang sama tidak saling berhubungan, kecuali Anda mengizinkannya dengan menetapkan aturan.
- Grup keamanan bersifat stateful. Lalu lintas masuk yang Anda izinkan dapat secara otomatis menjadi keluar dan sebaliknya.
- Anda dapat mengubah aturan grup keamanan kapan saja, dan aturan baru akan segera berlaku.

## Batasan Penggunaan
Untuk informasi selengkapnya tentang batasan dan kuota grup keamanan, lihat [Ikhtisar Batasan Penggunaan](https://intl.cloud.tencent.com/document/product/213/15379).

## Aturan Grup Keamanan

### Komponen

Aturan grup keamanan terdiri dari:
- Sumber atau tujuan: IP sumber untuk aturan masuk, atau IP tujuan untuk aturan keluar. Ini bisa berupa alamat IP, rentang IP, atau grup keamanan. Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35513).
- Jenis protokol dan port protokol: jenis protokol, seperti TCP, UDP, dll.
- Kebijakan: mengizinkan atau menolak permintaan akses.

### Prioritas aturan

- Aturan dalam grup keamanan diprioritaskan dari atas ke bawah. Aturan di bagian atas daftar memiliki prioritas tertinggi dan akan berlaku lebih dulu, sedangkan aturan di bagian bawah memiliki prioritas terendah dan akan berlaku terakhir.
- Jika ada konflik aturan, aturan dengan prioritas lebih tinggi akan berlaku secara default.
- Saat lalu lintas masuk atau keluar dari instans terikat ke grup keamanan, aturan grup keamanan akan dicocokkan secara berurutan dari atas ke bawah. Jika aturan berhasil dicocokkan dan berlaku, aturan berikutnya tidak akan cocok.

### Beberapa grup keamanan

Instans dapat diikat ke satu atau beberapa grup keamanan. Ketika terikat ke beberapa grup keamanan, aturan grup keamanan akan dicocokkan secara berurutan dari atas ke bawah. Anda dapat menyesuaikan prioritas grup keamanan kapan saja.

## Templat Grup Keamanan

Saat membuat grup keamanan, Anda dapat memilih salah satu dari dua templat grup keamanan yang disediakan oleh Tencent Cloud:

- Templat yang membuka semua port: semua lalu lintas masuk dan keluar akan diizinkan untuk diteruskan.
- Templat yang membuka port utama: port TCP 22 (untuk login SSH Linux), port 80 dan 443 (untuk layanan Web), port 3389 (untuk login jarak jauh Windows), protokol ICMP (untuk perintah Ping), dan jaringan pribadi (untuk rentang IP VPC) akan terbuka untuk internet.

> ?
> - Jika templat ini tidak dapat memenuhi kebutuhan aktual Anda, Anda dapat membuat grup keamanan kustom. Untuk informasi selengkapnya, lihat [Membuat Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35506) dan [Kasus Aplikasi Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35519).
> - Jika Anda perlu melindungi lapisan aplikasi (HTTP/HTTPS), harap aktifkan [Tencent Cloud Web Application Firewall (WAF)](https://intl.cloud.tencent.com/product/waf) yang memberikan keamanan web pada lapisan aplikasi untuk melindungi dari kerentanan web, perayap berbahaya, dan serangan CC, melindungi situs web dan keamanan aplikasi web Anda.

## Cara Menggunakan Grup Keamanan
Gambar berikut menunjukkan cara menggunakan grup keamanan:
![](https://main.qcloudimg.com/raw/2fccad4c688f66f28cfb3d41dbbb7134.png)

## Praktik Terbaik Grup Keamanan

### Membuat Grup Keamanan
- Sebaiknya tentukan grup keamanan saat membeli CVM melalui API. Jika tidak, grup keamanan default akan digunakan dan tidak dapat dihapus.
- Jika Anda perlu mengubah kebijakan perlindungan instans, sebaiknya ubah aturan yang ada daripada membuat grup keamanan baru.

### Mengelola Peran
- Ekspor dan cadangkan aturan grup keamanan sebelum Anda mengubahnya, sehingga Anda dapat mengimpor dan memulihkannya jika terjadi kesalahan.
- Untuk membuat beberapa aturan grup keamanan, harap gunakan [templat parameter](https://intl.cloud.tencent.com/document/product/215/31867).

### Mengaitkan grup keamanan
- Anda dapat menambahkan instans dengan persyaratan perlindungan yang sama ke grup keamanan yang sama, sebagai ganti mengonfigurasi grup keamanan terpisah untuk setiap instans.
- Sebaiknya jangan mengikat satu instans ke terlalu banyak grup keamanan, karena aturan dalam grup keamanan yang berbeda dapat bertentangan dan mengakibatkan pemutusan jaringan.


