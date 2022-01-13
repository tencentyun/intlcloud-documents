Dalam skenario deployment cloud hibrida, Anda bisa langsung mengikat instance CLB ke IP di IDC lokal luar cloud untuk mengikatnya ke server asli di seluruh VPC dan IDC.
Fitur ini saat ini dalam versi beta.Jika Anda ingin menggunakannya, untuk pengikatan lintas wilayah di luar Tiongkok daratan, silakan [hubungi perwakilan Tencent Cloud Anda](https://intl.cloud.tencent.com/contact-sales).

## Keunggulan Solusi
- Cloud hibrida bisa dibangun dengan cepat untuk menghubungkan lingkungan di dalam dan luar cloud dengan lancar.CLB bisa meneruskan permintaan ke instance CVM di VPC in-cloud dan IDC off-cloud sekaligus.
- Kemampuan akses jaringan publik kualitas tinggi Tencent Cloud bisa digunakan kembali.
- Fitur CLB yang kaya seperti akses lapisan 4/7, pemeriksaan kesehatan, dan persistensi sesi bisa digunakan kembali.
- Jaringan pribadi bisa saling terhubung melalui [CCN](https://intl.cloud.tencent.com/document/product/1003/30049), mendukung perutean mendetail untuk menjamin kualitas, dan mendukung diversifikasi harga bertingkat untuk mengurangi biaya.
![](https://main.qcloudimg.com/raw/e09b0e4b6fcaedf44267f6ca1950ee54.png)

## Batas
- Saat ini tidak mendukung pengikatan instance CVM lintas jaringan untuk instance CLB klasik.
- Fitur ini hanya tersedia untuk akun tagihan per IP.Untuk memeriksa tipe akun Anda, silakan lihat [Memeriksa Tipe Akun](https://intl.cloud.tencent.com/document/product/684/15246).
- Pengikatan lintas wilayah 2.0 dan deployment cloud hibrida tidak mendukung [Izinkan Lalu Lintas secara Default di grup keamanan](https://intl.cloud.tencent.com/document/product/214/14733), yang mengharuskan Anda mengizinkan IP klien dan port layanan di server asli.
- Saat ini, fitur ini hanya didukung di Guangzhou, Shenzhen, Shanghai, Jinan, Hangzhou, Beijing, Tianjin, Chengdu, Chongqing, Hong Kong (Tiongkok), Singapore, dan Silicon Vally.
- Pendengar TCP dan TCP SSL harus menggunakan TOA di server asli untuk memperoleh IP sumber.Untuk informasi selengkapnya, silakan lihat [Metode Pemuatan Modul TOA](https://intl.cloud.tencent.com/document/product/608/18945).
- Pendengar HTTP dan HTTPS harus menggunakan `X-Forwarded-For` (XFF) untuk memperoleh IP sumber.
- Pendengar UDP tidak bisa memperoleh IP sumber.

## Prasyarat
1.Kirim permohonan untuk kelayakan pengujian beta.Untuk pengikatan lintas wilayah di Tiongkok daratan, silakan kirimkan tiket untuk mendaftar.Untuk pengikatan lintas wilayah di luar Tiongkok daratan, silakan [hubungi perwakilan Tencent Cloud Anda](https://intl.cloud.tencent.com/contact-sales).
2.Buat instance CLB.Untuk informasi selengkapnya, silakan lihat [Membuat Instance CLB](https://intl.cloud.tencent.com/document/product/214/6149).
3.Buat instance CCN.Untuk informasi selengkapnya, silakan lihat [Membuat Instance CCN](https://intl.cloud.tencent.com/document/product/1003/30062).
4.Asosiasikan Direct Connect gateway yang diasosiasikan dengan IDC dan VPC target dengan instance CCN yang dibuat.Untuk informasi selengkapnya, silakan lihat [Mengasosiasikan Instance Jaringan](https://intl.cloud.tencent.com/document/product/1003/30064).

## Petunjuk Operasi
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Di halaman **Instance Management** (Manajemen Instance), klik ID instance CLB target.
3.Pada bagian **Real Server** (Server Asli) di tab **Basic Info** (Info Dasar), klik **Configure** (Konfigurasikan) untuk mengikat IP pribadi VPC lainnya.
![](https://main.qcloudimg.com/raw/1214576094baa072eb1d3577a5f5781a.png)
4.Klik **Submit** (Kirim) di kotak pop-up.
![](https://main.qcloudimg.com/raw/4f7b99a8532afabe54440ca7819dcd72.png)
5.Pada bagian **Real Server** (Server Asli) di tab **Basic Info** (Info Dasar), klik **Add SNAT IP** (Tambahkan IP SNAT).
![](https://main.qcloudimg.com/raw/fc41b320241fa4de1d961e1a9c8d428f.png)
6.Pada kotak pop-up, pilih **Subnet**, klik **Add** (Tambahkan) untuk menetapkan IP, dan klik **Save** (Simpan).
<img src="https://main.qcloudimg.com/raw/6aad8ac7d4a38a8e74ea7b3b59e36cbb.png" width="50%"/>
7.Di halaman detail instance, buka tab **Listener Management** (Manajemen Pendengar), dan ikat server asli ke instance CLB di bagian konfigurasi pendengar.Untuk informasi selengkapnya, silakan lihat [Mengelola Server Asli](https://intl.cloud.tencent.com/document/product/214/6156).
8.Pada kotak pop-up, pilih **Other Private IP** (IP Pribadi Lain), klik **Add a private IP** (Tambahkan IP pribadi), masukkan IP pribadi IDC, port, dan bobot target, dan klik **Confirm** (Konfirmasi).Untuk informasi selengkapnya mengenai port, silakan lihat [Port Umum Server](https://intl.cloud.tencent.com/document/product/213/12451).

9.Kini Anda bisa menampilkan IP pribadi IDC yang terikat di bagian **Bound Real Servers** (Server Asli Terikat).<br/>



