## Deskripsi Masalah
Saat Anda mengakses CVM dari mesin lokal atau mengakses sumber daya jaringan lain dari CVM, jaringan akan macet. Kehilangan paket atau latensi tinggi ditemukan saat Anda menjalankan perintah `ping`.

## Analisis Masalah
Kehilangan paket atau latensi tinggi dapat disebabkan oleh kemacetan jaringan backbone, kegagalan node jaringan, beban tinggi, atau konfigurasi sistem. Anda dapat menggunakan MTR untuk diagnosis lebih lanjut setelah mengesampingkan masalah CVM.
MTR adalah alat diagnostik jaringan dan menyediakan laporan yang membantu Anda menemukan masalah jaringan.

## Solusi
>? Dokumen ini menggunakan Linux dan Windows CVM sebagai contoh untuk menjelaskan cara menggunakan MTR dan menganalisis laporan.
>
Silakan lihat pengenalan MTR dan instruksi yang sesuai dengan sistem operasi host.
- [Pengenalan dan Petunjuk WinMTR (untuk Windows)](#MTRofWindows)
- [Pengenalan dan Petunjuk MTR (untuk Linux)](#MTRofLinux)

<span id="MTRofWindows"></span>
### Pengenalan dan Petunjuk WinMTR (untuk Windows)
**WinMTR** adalah alat diagnostik jaringan gratis untuk Windows yang terintegrasi dengan fitur Ping dan tracert. Antarmuka grafisnya memungkinkan Anda untuk secara intuitif melihat waktu respons dan kehilangan paket dari setiap node.

#### Menginstal WinMTR
1. Login ke Windows CVM.
2. Pada antarmuka sistem operasi, kunjungi situs web resmi (atau saluran resmi lainnya) melalui browser untuk mengunduh paket penginstal WinMTR yang sesuai dengan sistem operasi Anda.
3. Buka zip paket penginstal WinMRT.

#### Menggunakan WinMTR
1. Klik dua kali WinMTR.exe untuk membuka alat WinMRT.
2. Masukkan IP atau nama domain host di bidang Host. Kemudian klik **Start** (Mulai) seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/7aa2d2e76b86deabd6d0248ecf89de56.png)
3. Tunggu hingga WinMTR berjalan beberapa saat dan klik **Stop** (Hentikan) untuk menghentikan pengujian, seperti yang ditunjukkan pada gambar di bawah ini:
![](https://main.qcloudimg.com/raw/5d73f806c0252d26755d584e874c26f1.png)
Informasi kunci dari hasil uji adalah seperti yang ditunjukkan di bawah ini:
 - **Hostname** (Nama host): IP atau nama setiap host yang dilalui pada jalur ke server tujuan.
 - **Nr** (Nr): Jumlah node yang telah dilewati.
 - **Loss%** (Kehilangan%): Kehilangan paket dari setiap node.
 - **Sent** (Terkirim): Jumlah paket data yang dikirim.
 - **Recv** (Recv): Jumlah respons yang diterima.
 - **Best** (Terbaik): Waktu respons tercepat.
 - **Avrg** (Rata-rata): Waktu respons rata-rata.
 - **Worst** (Terburuk): Waktu respons terlama.
 - **Last** (Terakhir): Waktu respons paling terakhir.

<span id="MTRofLinux"></span>
### Pengenalan dan Petunjuk MTR (untuk Linux)
**MTR** adalah alat diagnostik jaringan untuk Linux yang terintegrasi dengan fitur Ping, traceroute, dan nslookup. Paket ICMP digunakan secara default untuk menguji koneksi jaringan antara dua node.

#### Menginstal Instalasi MTR
Saat ini, semua versi Linux yang dirilis telah terinstal MTR. Jika tidak, Anda dapat menginstal MTR menggunakan perintah berikut:
- Untuk CentOS 6/7:
```
yum install mtr
```
- Untuk Ubuntu:
```
sudo apt-get install mtr
```

## Parameter MTR
- **-h/--help**: Menampilkan menu bantuan.
- **-v/--version**: Menampilkan informasi versi MTR.
- **-r/--report**: Menampilkan hasil dalam laporan.
- **-p/--split**: Berbeda dari ** --report**, **-p/--split** menampilkan hasil setiap trace secara terpisah.
- **-c/--report-cycles**: Mengatur jumlah paket data yang dikirim per detik. Nilai default-nya adalah 10.
- **-s/--psize**: Mengatur ukuran setiap paket data.
- **-n/--no-dns**: Menonaktifkan resolusi nama domain untuk alamat IP.
- **-a/--address**: Mengatur alamat IP dari mana paket data dikirim. Ini terutama digunakan untuk skenario dengan satu host dan beberapa alamat IP.
- **-4**：IPv4
- **-6**：IPv6

#### Kasus Penggunaan
Bawa mesin lokal ke server (IP: 119.28.98.39) sebagai contoh.
Jalankan perintah berikut untuk menampilkan hasil diagnostik MTR dalam laporan.
```
mtr 119.28.98.39 -- report
```
Pesan yang mirip dengan yang di bawah ini ditampilkan:
```
[root@VM_103_80_centos ~]# mtr 119.28.98.39 -- report
Mulai: Senin, 5 Februari 11.33.34 2019
HOST:VM_103_80_centos            Loss%    Snt    Last    Avg    Best    Wrst    StDev
1.|-- 100.119.162.130             0.0%     10     6.5    8.4     4.6    13.7      2.9
2.|-- 100.119.170.58              0.0%     10     0.8    8.4     0.6     1.1      0.0
3.|-- 10.200.135.213              0.0%     10     0.4    8.4     0.4     2.5      0.6
4.|-- 10.200.16.173               0.0%     10     1.6    8.4     1.4     1.6      0.0
5.|-- 14.18.199.58                0.0%     10     1.0    8.4     1.0     4.1      0.9
6.|-- 14.18.199.25                0.0%     10     4.1    8.4     3.3    10.2      1.9
7.|-- 113.96.7.214                0.0%     10     5.8    8.4     3.1    10.1      2.1
8.|-- 113.96.0.106                0.0%     10     3.9    8.4     3.9    11.0      2.5
9.|-- 202.97.90.206               30.0%     10    2.4    8.4     2.4     2.5      0.0
10.|-- 202.97.94.77               0.0%     10     3.5    4.6     3.5     7.0      1.2
11.|-- 202.97.51.142              0.0%     10   164.7    8.4   161.3   165.3      1.2
12.|-- 202.97.49.106              0.0%     10   162.3    8.4   161.7   167.8      2.0
13.|-- ix-xe-10-2-6-0.tcore2.LVW 10.0%     10   168.4    8.4   161.5   168.9      2.3
14.|-- 180.87.15.25              10.0%     10   348.1    8.4   347.7   350.2      0.7
15.|-- 180.87.96.21               0.0%     10   345.0    8.4   343.4   345.0      0.3
16.|-- 180.87.96.142              0.0%     10   187.4    8.4   187.3   187.6      0.0
17.|-- ???                      100.0%     10     0.0    8.4     0.0     0.0      0.0
18.|-- 100.78.119.231             0.0%     10   187.7    8.4   187.3   194.0      2.5
19.|-- 119.28.98.39               0.0%     10   186.5    8.4   186.4   186.5      0.0
```
Informasi hasil utama adalah sebagai berikut:
- **Host:** (Host.) Alamat IP atau nama domain sebuah node.
- **Loss%:** (Kehilangan.) Kehilangan paket.
- **Snt:** (Terkirim.) Jumlah paket data yang dikirim per detik.
- **Last:** (Terakhir.) Waktu respons paling terakhir.
- **Avg:** (Rata-rata.) Waktu respons rata-rata.
- **Best:** (Terburuk.) Waktu respons tercepat.
- **Wrst:** (Terburuk.) Waktu respons terlama.
- **StDev:** (StDev:) Standar penyimpangan. Standar penyimpangan yang lebih tinggi menunjukkan perbedaan yang lebih besar dalam waktu respon paket data pada node ini.

### Analisis laporan dan pemecahan masalah
>? Karena asimetri jaringan, kami menyarankan Anda mengumpulkan data MTR dua arah (dari mesin lokal ke server tujuan dan dari server tujuan ke mesin lokal) jika terjadi kesalahan jaringan.
>
1. Menurut laporan tersebut, periksa apakah ada kehilangan paket pada IP tujuan.
 - Jika tidak ada kehilangan paket pada IP tujuan, berarti kondisi jaringannya normal.
 - Jika ada kehilangan paket pada IP tujuan, lakukan [Langkah 2](#langkah02).
2. <span id="step02">Periksa hasilnya untuk menemukan node di mana kehilangan paket pertama terjadi.</span>
 - Jika kehilangan paket terjadi di server tujuan, mungkin disebabkan oleh konfigurasi jaringan server tujuan yang salah. Harap periksa konfigurasi firewallnya.
 - Jika kehilangan paket terjadi pada tiga hop pertama, ini mungkin disebabkan oleh masalah jaringan ISP mesin lokal. Jika masalah juga terjadi saat Anda mengakses alamat lain, laporkan ke ISP Anda.
 - Jika kehilangan paket terjadi pada hop yang dekat dengan server tujuan, ini mungkin disebabkan oleh masalah jaringan ISP tujuan. [Kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk melaporkan masalah.
 Saat mengirimkan tiket, harap lampirkan tangkapan layar hasil uji MTR dari mesin lokal ke server tujuan dan dari server tujuan ke mesin lokal.
