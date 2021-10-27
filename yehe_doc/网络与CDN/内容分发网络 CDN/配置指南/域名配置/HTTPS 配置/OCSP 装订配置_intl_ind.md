## Konfigurasi
Setelah OCSP stapling (ekstensi kueri status sertifikat TLS) diaktifkan, server akan mengirim respons Online Certificate Status Protocol (OCSP) yang telah disimpan sebelumnya selama handshake TLS untuk verifikasi pengguna sehingga pengguna tidak perlu mengirim permintaan kueri kepada penyelenggara sertifikat elektronik (certificate authority/CA). OCSP stapling sangat meningkatkan efisiensi handshake TLS dan mengurangi waktu verifikasi pengguna.

CDN Tencent Cloud memungkinkan Anda untuk mengaktifkan/menonaktifkan OCSP stapling.

## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk mengakses halaman konfigurasinya. Di bawah tab **Advanced Configuration** (Konfigurasi Lanjutan), temukan **OCSP Stapling Configuration** (Konfigurasi OSCP Stapling), yang dinonaktifkan secara default:
![](https://main.qcloudimg.com/raw/a0f84d254848ea7c28a0642b3ab1866a.png)

### Memodifikasi konfigurasi
Jika nama domain telah dikonfigurasi dengan akselerasi HTTPS, Anda dapat langsung mengaktifkan switch OCSP stapling untuk mengaktifkan/menonaktifkan fitur ini. Setelah konfigurasi sertifikat dihapus, OCSP stapling akan tidak lagi diterapkan secara otomatis:
![](https://main.qcloudimg.com/raw/af090e9a10a99f552c2a57378d0b46ff.png)

>Jika nama domain Anda dikonfigurasi untuk akselerasi global, konfigurasi OCSP stapling akan diterapkan secara global. Konfigurasi ini tidak membedakan antara permintaan dari dan di luar Tiongkok Daratan.
