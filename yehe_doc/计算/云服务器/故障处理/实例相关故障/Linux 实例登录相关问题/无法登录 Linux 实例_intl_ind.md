Dokumen ini menjelaskan kemungkinan penyebab kegagalan login instans Linux dan metode pemecahan masalah, membantu Anda mendeteksi, menemukan, dan menyelesaikan masalah.

## Kemungkinan Penyebab
Penyebab utama kegagalan login instans Linux meliputi:
- [Masalah kunci SSH](#UseSSHLogin)
- [Masalah kata sandi](#CryptographicProblem)
- [Penggunaan bandwidth yang berlebihan](#BandwidthUtilization)
- [Beban server tinggi](#HighServerLoad)
- [Aturan grup keamanan salah](#SafetyGroupRule)


Jika Anda tidak dapat memeriksa masalah Anda dengan menggunakan alat diagnosis mandiri, kami sarankan Anda [login ke CVM melalui VNC](#VNC) dan memecahkan masalah langkah demi langkah.

## Pemecahan Masalah
### Login dengan menggunakan VNC
<span id="VNC"></span>
Jika Anda tidak dapat menggunakan metode standar (Orcaterm) atau perangkat lunak login jarak jauh untuk login ke instans Linux, Anda dapat menggunakan Tencent Cloud VNC untuk login dan menemukan penyebab masalah.
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, pilih intans yang akan diakses dan klik **Log In** (Login), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. Di jendela "Log in to Linux Instance" (Login ke Instans Linux) yang muncul, pilih **Alternative login methods (VNC)** (Metode login alternatif (VNC)) dan klik **Log In Now** (Login Sekarang).
> Saat login, jika Anda lupa kata sandi instans ini, Anda dapat mengaturnya ulang di konsol. Untuk informasi selengkapnya, lihat [Mengatur Ulang Kata Sandi Instans](http://intl.cloud.tencent.com/document/product/213/16566).
>
4. Masukkan nama pengguna dan kata sandi pada kotak dialog yang muncul untuk menyelesaikan proses login.

<span id="UseSSHLogin"></span>
### Masalah SSH
**Problem** (Masalah): selama [login ke instans Linux dengan menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501), sebuah pesan menunjukkan bahwa koneksi tidak tersedia atau gagal muncul.
**Steps** (Langkah-langkah): lihat [Tidak Dapat Login ke Instans Linux dengan Menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32486) untuk pemecahan masalah.

<span id="CryptographicProblem"></span>
### Masalah kata sandi
**Problem** (Masalah): tidak dapat login karena Anda lupa kata sandi, salah memasukkannya, atau gagal mengatur ulang.
**Solution** (Solusi): Atur ulang kata sandi instans ini di [Konsol Tencent Cloud](https://console.cloud.tencent.com/cvm/index), dan mulai ulang instans.
**Steps** (Langkah-langkah): untuk informasi tentang cara mengatur ulang kata sandi instans, lihat [Mengatur Ulang Kata Sandi Instans](http://intl.cloud.tencent.com/document/product/213/16566).

<span id="BandwidthUtilization"></span>
### Penggunaan bandwidth yang berlebihan
**Problem** (Masalah): alat diagnosis mandiri menunjukkan bahwa penggunaan bandwidth terlalu tinggi.
**Steps** (Langkah-langkah):
1. Login ke instans dengan menggunakan [VNC](#VNC).
2. Periksa penggunaan bandwidth instans dan atasi masalah yang sesuai. Untuk detailnya, lihat [Tidak Dapat Login Karena Penggunaan Bandwidth Tinggi](https://intl.cloud.tencent.com/document/product/213/32542).

<span id="HighServerLoad"></span>
### Beban server tinggi
**Problem** (Masalah): Tencent Cloud Observability Platform menunjukkan bahwa beban CPU server tinggi, dan sistem tidak dapat diakses dari jarak jauh atau aksesnya lambat.
**Possible Causes** (Kemungkinan Penyebab): virus, trojan, perangkat lunak anti-virus pihak ketiga, pengecualian aplikasi, pengecualian driver, dan pembaruan otomatis backend perangkat lunak dapat menyebabkan penggunaan CPU yang tinggi, menyebabkan kegagalan login CVM atau akses yang lambat.
**Steps** (Langkah-langkah):
1. Login ke instans dengan menggunakan [VNC](#VNC).
2. Di "Task manager" (Pengelola tugas), cari proses dengan beban tinggi. Untuk detailnya, lihat [Tidak Dapat Login Karena Penggunaan CPU dan Memori yang Tinggi](https://intl.cloud.tencent.com/document/product/213/32387).

<span id="SafetyGroupRule"></span>
### Aturan grup keamanan yang salah
**Problem** (Masalah): tidak dapat login karena aturan grup keamanan yang salah.
**Steps** (Langkah-langkah): pecahkan masalah dengan menggunakan [alat verifikasi port untuk grup keamanan](https://console.cloud.tencent.com/vpc/helper).
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
Jika masalah disebabkan oleh konfigurasi port grup keamanan yang salah, Anda dapat menggunakan **Open All Tools** (Buka Semua Alat) untuk membuka semua port.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
Jika Anda perlu menentukan aturan khusus bagi grup keamanan, lihat [Menambahkan Aturan ke Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272) untuk informasi tentang cara mengonfigurasi ulang aturan grup keamanan.



## Solusi Lain
Jika Anda masih tidak dapat login ke instans Linux setelah mencoba metode pemecahan masalah sebelumnya, simpan hasil diagnosis mandiri Anda dan [kirim tiket](https://console.cloud.tencent.com/workorder/category).
