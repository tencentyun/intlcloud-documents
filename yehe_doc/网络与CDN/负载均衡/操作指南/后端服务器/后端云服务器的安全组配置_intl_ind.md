## Ikhtisar Grup Keamanan CVM
[Grup keamanan](https://intl.cloud.tencent.com/document/product/213/12452) bisa digunakan untuk mengakses kendali untuk server asli instance CLB, yang berperan sebagai firewall.
Anda bisa mengasosiasikan satu grup keamanan atau lebih dengan satu server asli dan kemudian menambahkan satu aturan atau lebih pada setiap grup keamanan untuk mengendalikan izin akses lalu lintas dari berbagai server.Anda bisa memodifikasi aturan grup keamanan kapan pun, dan aturan baru akan berlaku secara otomatis pada semua instance yang berkaitan dengan grup keamanan.Untuk informasi selengkapnya, silakan lihat [Panduan Pengoperasian Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452).Di lingkungan [VPC](https://intl.cloud.tencent.com/document/product/215/535), Anda juga bisa menggunakan [ACL Jaringan](https://intl.cloud.tencent.com/document/product/215/31850) untuk mengakses kendali.

## Deskripsi Konfigurasi Grup Keamanan CVM
IP klien dan port keamanan harus dibuka ke internet di grup keamanan CVM.
Jika Anda ingin menggunakan CLB untuk meneruskan lalu lintas bisnis ke CVM, untuk memastikan pemeriksaan kesehatan yang efektif, grup keamanan CVM harus dikonfigurasikan sebagai berikut:
1.CLB jaringan publik: Anda harus membuka VIP CLB ke internet di grup keamanan CVM backend, agar CLB bisa menggunakan VIP untuk mendeteksi status kesehatan CVM backend.
2.CLB jaringan pribadi:
- Untuk CLB jaringan pribadi (sebelumnya "CLB Aplikasi jaringan pribadi"), jika instance CLB Anda dalam VPC, VIP CLB harus dibuka ke internet di grup keamanan CVM backend untuk pemeriksaan kesehatan; jika instance CLB Anda dalam jaringan dasar, konfigurasi tambahan tidak dibutuhkan karena IP pemeriksaan kesehatan dibuka ke internet secara default.
- Untuk CLB klasik jaringan pribadi, jika instance CLB Anda dibuat sebelum 5 Desember 2016 dan dalam VPC, VIP CLB harus dibuka ke internet (untuk pemeriksaan kesehatan) di grup keamanan CVM backend; jika tidak, konfigurasi tidak dibutuhkan.

## Sampel Konfigurasi Grup Keamanan CVM
Sampel berikut ini menunjukkan cara mengonfigurasi grup keamanan CVM saat mengakses CVM melalui CLB.Jika Anda juga sudah mengonfigurasi grup keamanan di CLB, silakan lihat [Mengonfigurasi Grup Keamanan CLB
](https://intl.cloud.tencent.com/document/product/214/14733) untuk informasi selengkapnya tentang cara mengonfigurasi aturan grup keamanan CLB.
- **Skenario aplikasi 1:**
Jika instance CLB jaringan publik dikonfigurasikan dengan pendengar TCP:80, port server aslinya adalah 8080, dan Anda hanya ingin IP Klien tertentu (IP ClientA dan IP ClientB) yang bisa mengakses instance CLB, konfigurasikan aturan masuk grup keamanan server asli seperti yang berikut ini:
```
IP ClientA + 8080 izinkan
IP ClientB + 8080 izinkan
VIP CLB    + 8080 izinkan
0.0.0.0/0  + 8080 turunkan
```
- **Skenario aplikasi 2:**
Jika instance CLB jaringan publik dikonfigurasikan dengan pendengar HTTP:80, port server aslinya adalah 8080, dan Anda ingin semua IP Klien bisa mengakses instance CLB, konfigurasikan aturan masuk grup keamanan server asli seperti yang berikut ini:
```
0.0.0.0/0 + 8080 izinkan
```
- **Skenario aplikasi 3:**
Untuk instance CLB jaringan pribadi (sebelumnya "CLB Aplikasi jaringan pribadi"), tipe jaringannya VPC, grup keamanan CVM perlu membuka IP VIP CLB ke internet untuk pemeriksaan kesehatan, instance CLB ini dikonfigurasikan dengan pendengar TCP:80, port server aslinya adalah 8080, dan Anda ingin IP Klien tertentu (IP ClientA dan IP ClientB) untuk mengakses VIP CLB dan ingin IP Klien untuk mengakses server asli yang terikat ke instance CLB saja, maka:
a.Konfigurasikan aturan masuk untuk grup keamanan server asli seperti yang berikut ini:
```
IP ClientA + 8080 izinkan
IP ClientB + 8080 izinkan
VIP CLB    + 8080 izinkan
0.0.0.0/0  + 8080 turunkan
```
b.Konfigurasikan aturan keluar untuk grup keamanan server klien seperti yang berikut ini:
```
VIP CLB    + 8080 izinkan
0.0.0.0/0  + 8080 turunkan
```
- **Skenario aplikasi 4:**
Untuk instance CLB jaringan pribadi (misalnya, instance CLB VPC yang dibeli setelah 5 Desember 2016), grup keamanan CVM hanya perlu membuka IP Klien ke internet (tidak perlu membuka VIP CLB, dan IP pemeriksaan kesehatan terbuka secara default), instance CLB ini dikonfigurasikan dengan pendengar TCP:80, port server aslinya adalah 8080, dan Anda ingin IP Klien tertentu (IP ClientA dan IP ClientB) untuk mengakses VIP CLB dan ingin IP Klien untuk mengakses server asli yang terikat ke instance CLB saja, maka:
a.Konfigurasikan aturan masuk untuk grup keamanan server asli seperti yang berikut ini:
```
IP ClientA + 8080 izinkan
IP ClientB + 8080 izinkan
0.0.0.0/0  + 8080 turunkan
```
b.Konfigurasikan aturan keluar untuk grup keamanan server klien seperti yang berikut ini:
```
VIP CLB    + 8080 izinkan
0.0.0.0/0  + 8080 turunkan
```
- **Skenario aplikasi 5: daftar hitam**
Jika Anda perlu mengonfigurasikan daftar hitam untuk beberapa IP klien untuk menolak permintaan akses mereka, Anda bisa mengonfigurasikan grup keamanan yang berkaitan dengan layanan Tencent Cloud.Aturan grup keamanan perlu dikonfigurasikan seperti yang berikut ini:
- Tambahkan IP klien dan port yang akan ditolak ke grup keamanan dan pilih opsi tersebut di kolom "Kebijakan" untuk menolak akses dari IP ini.
- Tambahkan aturan grup keamanan lainnya setelah menyelesaikan konfigurasi di atas untuk mengizinkan permintaan akses ke port dari semua IP secara default.
Setelah konfigurasi selesai, aturan grup keamanan adalah sebagai berikut:

```
IP clientA + port turunkan
IP clientB + port turunkan
0.0.0.0/0  + port terima
```

>?
>- Langkah-langkah konfigurasi di atas harus dilakukan **in a correct order** (sesuai urutan); jika tidak, konfigurasi daftar hitam tidak bisa berlaku.
>- Grup keamanan bersifat stateful; oleh karena itu, konfigurasi di atas digunakan untuk **inbound rules** (aturan masuk), sementara aturan keluar tidak membutuhkan konfigurasi khusus.

## Panduan Pengoperasian Grup Keamanan CVM
### Mengelola grup keamanan server asli di konsol
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance) dan klik ID instance CLB terkait untuk masuk ke halaman detail CLB.
2.Di halaman CVM, klik ID server asli terkait untuk masuk ke halaman detail instance CVM.
3.Klik tab **Security Group** (Grup Keamanan) untuk mengikat/melepas ikatan grup keamanan.

### Mengelola grup keamanan server asli melalui API TencentCloud
Untuk informasi selengkapnya, silakan lihat [AssociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33265) dan [DisassociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33253).
