## Ikhtisar

Dokumen ini menjelaskan cara menggunakan layanan FTP untuk mengunggah file dari komputer Windows lokal ke CVM.

## Prasyarat

Anda telah membangun layanan FTP di CVM.
- Untuk menggunakan FTP untuk mengunggah file ke CVM Linux, lihat [Membangun Layanan FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912)
- Untuk menggunakan FTP untuk mengunggah file ke CVM Windows, lihat [Membangun Layanan FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)


## Petunjuk

### Menghubungkan ke CVM
1. Unduh dan instal FileZilla sumber terbuka secara lokal.
> Jika Anda menggunakan FileZilla versi 3.5.3 untuk mengunggah file melalui FTP, unggahan mungkin gagal. Sebaiknya unduh dan gunakan FileZilla versi 3.5.1 atau 3.5.2 dari situs resminya.
>
2. Buka FileZilla.
3. Di jendela FileZilla, masukkan informasi seperti host, nama pengguna, kata sandi, dan port, dan klik **Quickconnect** (Quickconnect).

**Configuration description:** (Deskripsi konfigurasi:)
 - Host: IP publik CVM. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm) untuk melihat IP publik CVM di halaman **Instance** (Instans).
 - Nama pengguna: akun pengguna FTP yang dikonfigurasi saat Anda [membangun layanan FTP](https://intl.cloud.tencent.com/document/product/213/10912). Gambar di bawah ini menggunakan "ftpuser1" sebagai contoh.
 - Kata Sandi: kata sandi yang sesuai dengan akun pengguna FTP yang dikonfigurasi saat Anda [membangun layanan FTP](https://intl.cloud.tencent.com/document/product/213/10912).
 - Port: port listening FTP, yang secara default adalah **21** (21).
Setelah koneksi berhasil, Anda dapat melihat file di situs CVM jarak jauh.

### Mengunggah file
Di jendela "Local site" (Situs lokal) kiri bawah, klik kanan file lokal yang akan diunggah dan pilih **Upload** (Unggah) untuk mengunggahnya ke CVM Linux, seperti yang ditunjukkan di bawah ini:
> 
>- Jalur FTP CVM tidak mendukung dekompresi otomatis atau penghapusan file tar terkompresi yang diunggah.
>- Jalur situs jarak jauh adalah jalur default untuk mengunggah file ke CVM Linux.
>

### Mengunduh file
Di jendela "Remote site" (Situs jarak jauh) pada kanan bawah, klik kanan file CVM yang akan diunduh dan pilih **Download** (Unduh) untuk mengunduhnya ke direktori lokal.


