Dokumen ini menjelaskan cara menemukan dan memecahkan masalah yang menyebabkan kegagalan akses situs web.

## Kemungkinan Penyebab

Kegagalan akses situs web mungkin disebabkan oleh masalah jaringan, konfigurasi firewall, atau kelebihan beban CVM.

## Pemecahan Masalah
<span id="TroubleshootServer"></span>
### Memecahkan masalah CVM
Pematian CVM, kegagalan perangkat keras, dan penggunaan CPU/memori/bandwidth yang tinggi semuanya dapat menyebabkan kegagalan akses situs web. Dengan demikian, kami sarankan Anda memeriksa status berjalan CVM dan penggunaan CPU/memori/bandwidth.

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) dan verifikasi apakah status berjalan instans CVM normal pada halaman manajemen instans, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c8347dcc04834aa44ade7324b7012d73.png)
 - Jika ya, silakan jalankan [langkah 2](#Server_step02).
 - Jika tidak, silakan mulai ulang instans CVM.
2. <span id="Server_step02">Klik ID/nama instans untuk masuk ke halaman detailnya.</span>
3. Pilih tab **Monitoring** (Pemantauan) untuk melihat penggunaan sumber daya instans, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/b8396a4507dd6a9808f9907b90e881fa.png)
 - Jika penggunaan CPU/memori terlalu tinggi, silakan lihat [Gagal login ke CVM Windows karena penggunaan CPU dan memori yang tinggi](https://intl.cloud.tencent.com/document/product/213/32405) dan [Gagal login ke CVM Linux karena penggunaan CPU dan memori yang tinggi](https://intl.cloud.tencent.com/document/product/213/32387) untuk pemecahan masalah.
 - Jika penggunaan bandwidth terlalu tinggi, silakan lihat [Kegagalan Login Karena Penggunaan Bandwidth Tinggi](https://intl.cloud.tencent.com/document/product/213/32542) untuk pemecahan masalah.
 - Jika penggunaan CPU/memori/bandwidth normal, silakan jalankan [langkah 4](#Server_step04).
4. <span id="Server_step04">Jalankan perintah berikut untuk memeriksa apakah port layanan Web yang sesuai dipantau secara normal. </span>
> Operasi berikut mengambil port 80, yang biasa digunakan dalam layanan HTTP, sebagai contoh.
>
 - Untuk instans Linux: jalankan perintah `netstat -ntulp |grep 80`, seperti yang ditunjukkan di bawah ini:
 ![](https://mc.qcloudimg.com/static/img/ab5fa663197c3fa0738b2ceb3f559fd3/image.png)
 - Untuk instans Windows: buka alat baris perintah CMD untuk menjalankan perintah `netstat -ano|findstr :80`, seperti yang ditunjukkan di bawah ini:
 ![](https://mc.qcloudimg.com/static/img/c9c32a2e9f12235ad3d2a5aca313f298/image.png)
 - Jika port dipantau secara normal, silakan jalankan [langkah 5](#Server_step05).
 – Jika port tidak dipantau secara normal,  periksa apakah proses layanan Web diluncurkan atau dikonfigurasi dengan benar.
5. <span id="Server_step05">Periksa apakah port layanan Web yang sesuai dibuka di konfigurasi firewall.</span>
 - Untuk instans Linux: jalankan perintah `iptables -vnL` untuk memeriksa apakah iptables membuka port 80.
    - Jika port 80 terbuka, silakan [memecahkan masalah terkait jaringan](#TroubleshootNetwork).
    - Jika port 80 tidak terbuka, jalankan perintah `iptables -I INPUT 5 -p tcp --dport 80 -j ACCEPT` untuk membukanya.
 - Untuk instans Windows: klik **Start** (Mulai) > **Control Panel** (Panel Kontrol) > **Windows Firewall** (Windows Firewall) pada antarmuka OS untuk memeriksa apakah konfigurasi firewall Windows dinonaktifkan.
		- Jika ya, silakan [memecahkan masalah terkait jaringan](#TroubleshootNetwork).
		- Jika tidak, matikan konfigurasi firewall Windows.

<span id="TroubleshootNetwork"></span>
### Memecahkan masalah terkait jaringan
Masalah jaringan juga dapat menyebabkan kegagalan akses jaringan. Anda dapat menjalankan perintah berikut untuk memeriksa apakah jaringan mengalami kehilangan paket atau latensi tinggi.
```
ping IP publik server
```
- Jika hasil yang serupa dengan yang di bawah ini ditampilkan, ada kehilangan paket atau latensi tinggi. Silakan gunakan MTR untuk pemecahan masalah. Untuk informasi selengkapnya, silakan lihat [Latensi Jaringan CVM dan Kehilangan Paket](https://intl.cloud.tencent.com/document/product/213/14638).
![](https://mc.qcloudimg.com/static/img/30d9946522f43cfc1c6731b9035ae9e9/image.png)
- Jika tidak ada kehilangan paket atau latensi tinggi, silakan [memecahkan masalah grup keamanan] (#TroubleshootSecurityGroup).

<span id="TroubleshootSecurityGroup"></span>
### Memecahkan masalah grup keamanan
Grup keamanan adalah firewall virtual yang memungkinkan Anda mengontrol lalu lintas masuk dan keluar dari instans terkait. Anda dapat menentukan protokol, port, dan kebijakan untuk aturan grup keamanan. Jika Anda tidak membuka port yang terkait dengan proses Web, kegagalan akses situs web dapat terjadi.
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) dan klik ID/nama instans untuk masuk ke halaman detailnya.
2. Klik tab **Security Group** (Grup Keamanan) untuk melihat grup keamanan terikat dan aturan keluar dan masuknya. Konfirmasikan bahwa port yang terkait dengan proses Web terbuka, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/b5782326fcdd77a74ca1435b202ca97b.png)


