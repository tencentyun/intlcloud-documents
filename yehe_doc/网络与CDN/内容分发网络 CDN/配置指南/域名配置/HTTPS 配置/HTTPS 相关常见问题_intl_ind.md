[](id:q1)
### Apa itu HTTPS?
HTTPS adalah singkatan dari Hypertext Transfer Protocol Secure, yaitu protokol keamanan yang mengenkripsi dan mentransfer data berdasarkan protokol HTTP untuk menjamin keamanan transfer data.Saat mengonfigurasi HTTPS, Anda perlu memberikan sertifikat untuk nama domain dan men-deploy-nya di semua simpul CDN untuk menerapkan transfer data terenkripsi di seluruh jaringan.

[](id:q2)
### Apakah CDN mendukung konfigurasi HTTPS?
Ya.CDN Tencent Cloud mendukung sepenuhnya konfigurasi HTTPS.Anda dapat mengunggah sertifikat Anda sendiri untuk deployment atau membuka [Konsol Layanan Sertifikat SSL](https://console.cloud.tencent.com/ssl) untuk mengajukan permohonan sertifikat pihak ketiga gratis yang disediakan oleh TrustAsia.

[](id:q3)
### Bagaimana cara mengonfigurasi sertifikat HTTPS?
Anda dapat mengonfigurasi sertifikat HTTPS di [Konsol CDN](https://console.cloud.tencent.com/cdn).Untuk petunjuk mendetail, silakan lihat [Panduan Konfigurasi HTTPS](https://intl.cloud.tencent.com/document/product/228/35213).

[](id:q4)
### Apakah sertifikat HTTPS pada simpul CDN perlu disinkronkan dengan pembaruan sertifikat HTTPS di server asal?
Tidak. Memperbarui sertifikat HTTPS dari server asal Anda tidak memengaruhi sertifikat yang dikonfigurasi di CDN.Anda hanya perlu memperbarui sertifikat HTTPS pada CDN saat sertifikat tersebut sudah atau akan kedaluwarsa.


[](id:q5)
### Dapatkah saya menolak akses HTTP dan hanya mengizinkan akses HTTPS?
Ya.Setelah berhasil mengonfigurasi sertifikat HTTPS, Anda dapat menggunakan fitur [Pengalihan Paksa](https://intl.cloud.tencent.com/document/product/228/35214).Permintaan HTTP dari pengguna akan dialihkan secara paksa ke permintaan HTTPS.
![](https://main.qcloudimg.com/raw/c562127135d558445481ab97973b1ebe.png)


[](id:q6)
### Mengapa akses HTTPS tidak berfungsi setelah CDN dikonfigurasi?

Untuk akses HTTPS, harap konfigurasikan seperti yang diinstruksikan:
1.Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman pengelolaannya.
![](https://main.qcloudimg.com/raw/33ea31c11bfac2022ea5753b6d849042.png)
2.Buka tab **Advanced Configuration** (Konfigurasi Lanjutan) untuk menemukan bagian **HTTPS Configuration** (Konfigurasi HTTPS), dan klik **Configure Now** (Konfigurasikan Sekarang) untuk membuka halaman **Certificate Management** (Pengelolaan Sertifikat).Untuk petunjuk konfigurasi, silakan lihat [Panduan Konfigurasi HTTPS](https://intl.cloud.tencent.com/document/product/228/35213#.E8.AF.81.E4.B9.A6.E9.85.8D.E7.BD.AE).
![](https://main.qcloudimg.com/raw/67be1f3b42a411613c0500afa97e06b5.png)
Akses HTTPS dapat diaktifkan setelah sertifikat berhasil dikonfigurasi.



