### Apakah CVM dilengkapi dengan FTP?
Ya. Anda dapat menginstal dan mengonfirmasi FTP sesuai kebutuhan.
- Untuk membangun situs FTP menggunakan layanan FTP bawaan Windows, lihat [Membangun Layanan FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414).
- Untuk membangun situs FTP menggunakan perangkat lunak vsftpd, lihat [Membangun Layanan FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912).

### Bagaimana cara mengunggah file ke CVM Windows?
- Untuk Windows lokal, lihat [Mengunggah File dari Windows ke CVM Windows menggunakan MSTSC](https://intl.cloud.tencent.com/document/product/213/2761).
- Untuk Linux lokal, lihat [Mengunggah File dari Linux ke Windows CVM menggunakan RDP](https://intl.cloud.tencent.com/document/product/213/34822).
- Untuk MacOS lokal, lihat [Mengunggah File dari MacOS ke Windows CVM menggunakan MRD](https://intl.cloud.tencent.com/document/product/213/34820).

### Bagaimana cara host lokal mentransfer data ke dan dari Windows CVM?
### Untuk mentransfer data:
- Jika Anda menggunakan file RDP untuk masuk ke CVM Windows dari komputer Windows lokal, Anda dapat langsung menyeret dan mengunggah file lokal ke CVM.
- [Unggah File dari Windows ke Windows CVM menggunakan MSTSC](https://intl.cloud.tencent.com/document/product/213/2761)
- [Membangun Layanan FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912) di host lokal.

### Bagaimana cara mengunggah file ke CVM Linux menggunakan WinSCP?
Untuk informasi selengkapnya, lihat [Mengunggah File melalui WinSCP ke CVM Linux dari Windows](https://intl.cloud.tencent.com/document/product/213/2131).

### Bagaimana cara mengunggah file ke atau mengunduh file dari CVM Linux?
Untuk informasi selengkapnya, lihat [Mengunggah File melalui SCP ke CVM Linux dari Linux](https://intl.cloud.tencent.com/document/product/213/2133).

### Apa yang harus dilakukan jika waktu koneksi klien-server habis selama pengunggahan file FTP?
Firewall server atau grup keamanan mungkin telah memblokir koneksi. Ikuti langkah-langkah di bawah ini untuk memecahkan masalah ini:
1. Periksa pengaturan firewall server.
2. Nonaktifkan firewall atau tambahkan aturan.
