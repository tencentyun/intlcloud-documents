Biasanya, nama domain streaming langsung menggunakan Hypertext Transfer Protocol (HTTP). HTTP dapat dikonversi menjadi Hyper Text Transfer Protocol melalui Secure Socket Layer (HTTPS) menggunakan protokol SSL/TLS untuk transmisi data terenkripsi. Anda dapat membuka **Certificate Management** (Manajemen Sertifikat) untuk melakukan kueri dan mengonfigurasi sertifikat SSL untuk nama domain.

## Cara Mengonfigurasi
Konfigurasi sertifikat SSL untuk nama domain bertujuan untuk mengenkripsi data pengguna utama agar transmisi aman. Sertifikat Secure Sockets Layer (SSL) memungkinkan suatu situs untuk beralih dari HTTP ke versi terenkripsi berbasis SSL, yaitu HTTPS. 

[](id:c_ssl)
### Mengonfigurasi Sertifikat
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) di konsol CSS, lalu klik **Certificate Management** (Manajemen Sertifikat) untuk membuka halaman manajemen sertifikat.
![](https://main.qcloudimg.com/raw/e39413b101a445ed747d78c8c9e7c8ac.png)
2. Klik **Configure Certificate** (Konfigurasi Sertifikat) untuk menambahkan konfigurasi sertifikat.
![](https://main.qcloudimg.com/raw/5aeee06ba8b978b823be16e9191bf705.png)
3. Di jendela pop-up konfigurasi sertifikat, pilih sumber sertifikat:
  - **Self-owned certificate** (Sertifikat milik sendiri): masukkan keterangan, konten, dan kunci sertifikat ini. Setelah konfigurasi disimpan, info sertifikat akan disinkronkan ke [Certificate Management (Manajemen Sertifikat)](https://console.cloud.tencent.com/ssl) di konsol Layanan Sertifikat SSL. Detail tentang cara mengatur konten dan kunci sertifikat dapat dilihat di [HTTPS Configuration (Konfigurasi HTTPS)](https://intl.cloud.tencent.com/document/product/267/31066).
![](https://main.qcloudimg.com/raw/998de2fdadf6ed9ab52e7fdcef288f51.png)
  - **Tencent Cloud-hosted certificate** (Sertifikat yang di-hosting oleh Tencent Cloud): pilih sertifikat yang Anda beli di konsol Layanan Sertifikat SSL.
![](https://main.qcloudimg.com/raw/4f36c491c7392798bc81410ecc65ae6e.png)
4. Setelah sertifikat dipastikan tersedia, klik **Next** (Selanjutnya) untuk membuka halaman konfigurasi nama domain.
5. Di **Bind Domain Names** (Ikat Nama Domain), pilih satu atau beberapa nama domain pemutaran ulang yang cocok dengan sertifikat. Jika nama domain yang dipilih sudah terikat dengan suatu sertifikat, sertifikat yang baru akan diterapkan.
6. Di bagian **Selected** (Dipilih), Anda dapat melihat nama domain yang dipilih dan diaktifkan atau tidaknya konfigurasi HTTPS.
![](https://main.qcloudimg.com/raw/bc1a0c51023d295120b8c94420b7b628.png)
7. Pilih diaktifkan atau tidaknya Konfigurasi HTTPS untuk nama domain yang dipilih:
  >? 
  >- Mengaktifkan **Enable HTTPS Configuration** (Aktifkan Konfigurasi HTTPS) akan mengaktifkan konfigurasi HTTPS untuk nama domain.
  >- **Enable HTTPS Configuration** (Aktifkan Konfigurasi HTTPS) diaktifkan secara default. Jika Anda menonaktifkan tombol ini, status konfigurasi HTTPS dari nama domain tidak akan berubah setelah pengikatan, dan pembaruan hanya dilakukan pada sertifikat.
6. Klik **Confirm** (Konfirmasi).


[](id:check)
## Melihat Konfigurasi Sertifikat
Setelah [mengonfigurasi sertifikat](#c_ssl), Anda dapat membuka **[Certificate Management](https://console.cloud.tencent.com/live/common/certificate)** (Manajemen Sertifikat) untuk melihat konfigurasinya, termasuk nama domain, keterangan, sumber, konfigurasi HTTPS, dan waktu kedaluwarsa.
![](https://main.qcloudimg.com/raw/e4012e075b695afc912840462e0c5694.png)

[](id:update)
## Memperbarui Konfigurasi Sertifikat
1. Buka **[Certificate Management](https://console.cloud.tencent.com/live/common/certificate)** (Manajemen Sertifikat), temukan konfigurasi sertifikat target di daftar, lalu klik **Update** (Perbarui) di sebelah kanan.
![](https://main.qcloudimg.com/raw/bfad71179c2ab41cd3c35e23e47e0224.png)
2. Di halaman konfigurasi sertifikat, [konfigurasi sertifikat](#c_ssl) lagi.
3. Klik **Confirm** (Konfirmasi).

[](id:delete)
## Menghapus Konfigurasi Sertifikat
1. Buka **[Certificate Management](https://console.cloud.tencent.com/live/common/certificate)** (Manajemen Sertifikat), temukan konfigurasi sertifikat target dalam daftar, lalu klik **Delete** (Hapus) di sebelah kanan.
![](https://main.qcloudimg.com/raw/a5d8f92c8aa7f2264c56e5ef6bf1f15b.png)
2. Di jendela pop-up konfirmasi, klik **Confirm** (Konfirmasi).
![](https://main.qcloudimg.com/raw/10305e0609cfcda523505cbcf8a099c8.png)
>! Setelah Anda melepaskan ikatan sertifikat, nama domain tidak dapat menggunakan konfigurasi HTTPS.


