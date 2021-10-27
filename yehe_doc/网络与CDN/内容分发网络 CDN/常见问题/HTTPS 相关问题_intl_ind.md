[](id:q1)
### Apa itu HTTPS?
HTTPS adalah singkatan dari Hypertext Transfer Protocol Secure, yaitu protokol keamanan yang mengenkripsi dan mentransfer data berdasarkan protokol HTTP untuk menjamin keamanan transfer data. Saat mengonfigurasi HTTPS, Anda harus memberikan sertifikat untuk nama domain dan men-deploy-nya pada semua simpul CDN untuk mengimplementasikan transfer data terenkripsi ke seluruh jaringan.

[](id:q2)
### Apakah CDN mendukung konfigurasi HTTPS?
Ya. Tencent Cloud CDN mendukung sepenuhnya konfigurasi HTTPS. Anda dapat mengunggah sertifikat Anda sendiri untuk deployment atau buka [konsol Layanan Sertifikat SSL](https://console.cloud.tencent.com/ssl) untuk meminta sertifikat gratis pihak ketiga yang disediakan oleh TrustAsia.

[](id:q3)
### Bagaimana saya mengonfigurasi sertifikat HTTPS?
Anda dapat mengonfigurasi sertifikat HTTPS di [konsol CDN](https://console.cloud.tencent.com/cdn). Untuk mendapatkan petunjuk terperinci, silakan lihat [Panduan Konfigurasi HTTPS](https://intl.cloud.tencent.com/document/product/228/35213).

[](id:q4)
### Apakah sertifikat HTTPS pada simpul CDN harus disinkronkan dengan pembaruan sertifikat HTTPS pada server awal?
Tidak. Pembaruan sertifikat HTTPS pada server awal Anda tidak memengaruhi sertifikat yang dikonfigurasi pada CDN. Anda hanya perlu memperbarui sertifikat HTTPS pada CDN jika sertifikat tersebut sudah tidak berlaku atau hampir habis masa berlakunya.


[](id:q5)
### Bisakah saya menolak akses HTTP dan mengizinkan akses HTTPS saja?
Ya. Setelah berhasil mengonfigurasi sertifikat HTTPS, Anda dapat menggunakan fitur [Pengalihan Paksa](https://intl.cloud.tencent.com/document/product/228/35214). Permintaan HTTP dari pengguna akan dialihkan secara paksa ke permintaan HTTPS.
![](https://main.qcloudimg.com/raw/c562127135d558445481ab97973b1ebe.png)


[](id:q6)
### Mengapa akses HTTPS tidak berhasil setelah CDN dikonfigurasi?

Untuk akses HTTPS, silakan lakukan konfigurasi sesuai petunjuk:
1. Masuk ke [konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah sisi kiri, dan klik **Manage** (Kelola) di kanan nama domain untuk memasuki halaman pengelolaannya.
![](https://main.qcloudimg.com/raw/33ea31c11bfac2022ea5753b6d849042.png)
2. Buka tab **Advanced Configuration** (Konfigurasi Lanjutan) untuk menemukan bagian **HTTPS Configuration** (Konfigurasi HTTPS), lalu klik **Configure Now** (Konfigurasikan Sekarang) untuk masuk ke halaman **Certificate Management** (Pengelolaan Sertifikat). Untuk mendapatkan petunjuk konfigurasi, silakan lihat [Panduan Konfigurasi HTTPS](https://intl.cloud.tencent.com/document/product/228/35213#.E8.AF.81.E4.B9.A6.E9.85.8D.E7.BD.AE).
![](https://main.qcloudimg.com/raw/67be1f3b42a411613c0500afa97e06b5.png)
Akses HTTPS dapat diaktifkan setelah sertifikat berhasil dikonfigurasi.



