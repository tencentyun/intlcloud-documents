Dokumen ini menggunakan CVM dengan CentOS 7.5 sebagai contoh untuk menunjukkan cara memecahkan masalah saat instans Linux tidak dapat login dengan menggunakan SSH.

## Masalah

Selama [login ke instans Linux dengan menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501), sebuah pesan menunjukkan bahwa koneksi tidak tersedia atau gagal muncul.

## Menemukan dan Memecahkan Masalah
### Langkah 1: Memeriksa konfigurasi aturan grup keamanan

Gunakan [alat verifikasi port untuk grup keamanan](https://console.cloud.tencent.com/vpc/helper) untuk memeriksa apakah aturan grup keamanan sudah benar.
- Jika masalah disebabkan oleh konfigurasi port grup keamanan, Anda dapat menggunakan fitur **Open All Ports** (Buka Semua Port) untuk membuka semua port. Anda juga dapat menyesuaikan aturan grup keamanan berdasarkan kebutuhan aktual Anda. Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).
- Jika konfigurasi port grup keamanan sudah benar, lanjutkan ke [langkah berikutnya](#langkah07).
 
### Langkah 2: Mengkueri port layanan SSHD
1. <span id="step07">[Login ke instans Linux dengan menggunakan VNC](https://intl.cloud.tencent.com/document/product/213/32494).</span>
>?Ketika login jarak jauh dan metode login lainnya gagal, Anda dapat menggunakan VNC untuk menghubungkan instans, memantau status instans, dan memecahkan masalah.
>
2. Pada antarmuka sistem operasi, jalankan perintah berikut untuk memeriksa apakah port didengarkan oleh layanan SSH daemon (SSHD):
```
netstat -tnlp | grep sshd
```
 - Jika hasil berikut ditampilkan, proses SSHD mendengarkan pada port 22. Dalam hal ini, [kirim tiket](https://console.cloud.tencent.com/workorder/category).
```
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1015/sshd  
```
 - Jika tidak ada hasil yang ditampilkan, layanan SSHD belum diluncurkan. Dalam hal ini, lanjutkan ke [langkah berikutnya](#langkah09).
 
### Langkah 3: Memeriksa apakah layanan SSHD telah diluncurkan
<span id="step09">Jalankan perintah berikut untuk memeriksa apakah layanan SSHD telah diluncurkan.</span>
```
systemctl status sshd.service
```
 - Jika ya, [kirim tiket](https://console.cloud.tencent.com/workorder/category).
 - Jika tidak, jalankan perintah berikut untuk meluncurkan layanan SSDH dan coba login ke instans Linux lagi dengan menggunakan SSH.
```
systemctl mulai sshd
```

Jika Anda masih tidak dapat login ke instans Anda setelah melakukan langkah-langkah ini, sebaiknya laporkan masalah ini dengan [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category).

