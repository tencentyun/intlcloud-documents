Dokumen ini menjelaskan cara mendiagnosis dan memecahkan masalah kegagalan login jarak jauh yang disebabkan oleh masalah port.
>?Operasi berikut menggunakan instans CVM dengan sistem operasi CentOS 7.8 sebagai contoh.
>

## Alat
Anda dapat menggunakan alat berikut untuk memeriksa apakah masalah login terkait dengan konfigurasi port atau grup keamanan:
- [Diagnosis mandiri](https://console.cloud.tencent.com/workorder/check)
- [Verifikasi Port](https://console.cloud.tencent.com/vpc/helper)

Jika masalah memang disebabkan oleh konfigurasi grup keamanan, klik **Open all ports** (Buka semua port) di [Verifikasi Port](https://console.cloud.tencent.com/vpc/helper) dan coba login lagi. Jika Anda masih tidak dapat login setelah membuka port, lihat hal berikut untuk pemecahan masalah.

## Pemecahan Masalah
### Memeriksa konektivitas jaringan
Anda dapat menggunakan perintah `Ping` untuk menguji konektivitas jaringan dari PC Anda. Anda harus menjalankan pengujian dari komputer di lingkungan jaringan yang berbeda (seperti rentang IP atau ISP yang berbeda) untuk memeriksa apakah masalahnya adalah jaringan lokal atau masalah server.
1. Buka alat baris perintah di komputer lokal Anda.
	- **Windows** (Windows): klik **Start** (Mulai) > **Run** (Jalankan) dan masukkan `cmd`. Jendela Prompt Perintah muncul.
	- **MacOS** (MacOS): membuka jendela Terminal.
2. Jalankan perintah berikut untuk menguji koneksi jaringan.
```
ping [alamat IP publik instans CVM]
```
Anda harus terlebih dahulu [mendapatkan alamat IP publik](https://intl.cloud.tencent.com/document/product/213/17940) dari instans CVM. Misalnya, `ping 81.71.XXX.XXX`.
 - Jika hasil seperti berikut ditampilkan, koneksi jaringan Anda ke instans CVM adalah normal.
![](https://main.qcloudimg.com/raw/796dd285720755d7b5dc9e0bee492c83.png)
 - Jika **Request Timeout** (Waktu Permintaan Habis) muncul, koneksi jaringan Anda ke instans CVM tidak berfungsi dengan benar. Dalam hal ini, lihat [Kegagalan Ping Alamat IP Instans](https://intl.cloud.tencent.com/document/product/213/14639) untuk petunjuk pemecahan masalah.

### Memeriksa konektivitas port
1. [Login ke instans Linux melalui VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Jalankan perintah berikut dan tekan **Enter** (Enter) untuk memeriksa apakah port jarak jauh terbuka dan dapat diakses.
```
telnet [alamat IP publik instans CVM] [Nomor port]
```
Misalnya, jalankan perintah `telnet 119.XX.XXX.67 22` untuk memeriksa apakah port 22 terbuka.
 - Jika informasi yang mirip dengan apa yang ditampilkan di bawah ini dikembalikan, port 22 dapat diakses.
![](https://main.qcloudimg.com/raw/246134de6829323457dc1d51f85589b8.png)
 - Jika informasi yang mirip dengan yang ditampilkan di bawah ini dikembalikan, port 22 tidak dapat diakses. Periksa konfigurasi jaringan yang sesuai. Misalnya, periksa apakah port 22 terbuka di firewall atau grup keamanan instans.
 ![](https://main.qcloudimg.com/raw/d6eadfe7638046f0b0c1f15261ea74ab.png)


### Memeriksa layanan SSHD
Jika Anda tidak dapat [login ke instans Linux melalui kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501) karena kegagalan koneksi, mungkin karena port SSHD tidak didengarkan atau layanan SSHD tidak dimulai. Dalam hal ini, lihat [Tidak Dapat Login ke Instans Linux melalui SSH](https://intl.cloud.tencent.com/document/product/213/32486) untuk petunjuk pemecahan masalah.
