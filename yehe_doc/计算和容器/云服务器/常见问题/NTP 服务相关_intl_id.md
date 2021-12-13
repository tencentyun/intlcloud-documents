### Bagaimana cara menyesuaikan interval sinkronisasi layanan NTP yang dikonfigurasi?
Setelah [mengonfigurasi layanan NTP pada instans Linux](https://intl.cloud.tencent.com/document/product/213/32381), Anda dapat memulai ulang ntpd untuk mengatur ulang interval sinkronisasi. Untuk mengatur interval sinkronisasi ntpd secara manual, lakukan langkah-langkah berikut:
1. Jalankan perintah berikut untuk mengubah file konfigurasi NTP.
```
vi /etc/ntp.conf
```
2. Tekan **i** untuk masuk ke mode edit dan konfigurasikan sebagai berikut:
  1. Tambahkan tanda pound (`#`) di bagian awal `server time1.tencentyun.com iburst`, jika ada, untuk mengomentarinya.
  2. Tambahkan konfigurasi berikut. `minpoll 4` berarti interval minimum adalah 2<sup>4</sup>, dan `maxpoll 5` berarti interval maksimum adalah 2<sup>5</sup>.
```
server time1.tencentyun.com minpoll 4 maxpoll 5
```
Hasilnya akan terlihat sebagai berikut. Masukkan **:wq** untuk menyimpan perubahan dan menutup file.
![](https://main.qcloudimg.com/raw/02d6457d29b4c573605e3c79c5ccfc9f.png)
3. Mulai ulang ntpd dan jalankan `ntpd -p`. Nilai `poll` yang akan Anda lihat adalah 16 (yaitu, 2<sup>4</sup>), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/9fa0c72751de74d3b6e72cc1ca831952.png)

### Apa sumber waktu server ntpd Tencent Cloud?
Server NTP biasanya menggunakan jam satelit BeiDou.
 
### Apa yang harus dilakukan ketika konfigurasi NTP melaporkan kesalahan `localhost.localdomain timeout`?
Kesalahannya terjadi seperti yang terlihat pada gambar berikut.
![](https://main.qcloudimg.com/raw/1b3158135475e6cfbee28d2373685616.png)
Periksa dan konfirmasi apakah Anda menjalankan `POSTROUTING`. Jika demikian, ubah IP sumber di file konfigurasi `ntp.conf` ke alamat IP eth0.

### Dapatkah server di luar cloud berbagi NTP dengan Tencent Cloud CVM? Apa alamat sinkronisasi NTP?
Tencent Cloud menyediakan server NTP pribadi untuk sumber daya Tencent Cloud. Untuk perangkat lain, Anda dapat menggunakan server NTP publik yang disediakan oleh Tencent Cloud untuk sinkronisasi.
- Server NTP pribadi di:
```
time1.tencentyun.com
time2.tencentyun.com
time3.tencentyun.com
time4.tencentyun.com
time5.tencentyun.com
```
- Server NTP publik di:
```
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

### Mengapa waktu instans CVM yang dibuat dari citra kustom salah?
Periksa apakah layanan NTP sudah diaktifkan. Untuk menggunakan fitur sinkronisasi NTP nanti, lihat dokumen berikut berdasarkan sistem operasi untuk mengatur NTP. Kemudian, buat ulang citra kustom.
 - [Atur layanan NTP pada instans Linux](https://intl.cloud.tencent.com/document/product/213/32381)
 - [Atur layanan NTP pada instans Windows](https://intl.cloud.tencent.com/document/product/213/32380)

### Apakah sinkronisasi NTP akan terpengaruh jika CVM tidak dapat melakukan ping ke server NTP?
Tidak. Selama Anda dapat mengakses NTP, sinkronisasi akan tetap berfungsi. 

### Mengapa konten ntp.conf dari CVM yang dibuat dari citra kustom dipulihkan?
Hal ini mungkin disebabkan oleh inisialisasi Cloud-Init. Hapus konfigurasi terkait NTP di `/etc/cloud/cloud.cfg` sebelum membuat citra kustom. Untuk informasi selengkapnya, lihat [Cloud-Init & Cloudbase-Init](https://intl.cloud.tencent.com/document/product/213/19670).

### Apa dampak DNS jaringan pribadi yang dimodifikasi?
Semua layanan yang melibatkan resolusi nama domain pribadi Tencent Cloud akan terpengaruh. Misalnya,
- Repositori YUM menggunakan nama domain pribadi Tencent Cloud. Anda perlu memodifikasi repositori YUM setelah mengubah DNS.
- Pelaporan data pemantauan menggunakan nama domain pribadi dan akan terpengaruh.
- Fitur NTP tergantung pada nama domain pribadi untuk menyinkronkan waktu server, dan akan terpengaruh.

### Mengapa waktu lokal instans Windows diatur ulang dari EST yang dikonfigurasi ke waktu Beijing setelah dimulai ulang?
Periksa apakah layanan windowstime sudah diaktifkan pada instans. Anda mungkin perlu mengaktifkannya secara manual untuk menyinkronkan waktu sistem instans secara otomatis. Sebaiknya aktifkan layanan mulai otomatis.

### Mengapa saya tidak dapat menggunakan perintah `ntpq -np` untuk melihat waktu sinkronisasi?
Kesalahannya terjadi seperti yang terlihat pada gambar berikut.
![](https://main.qcloudimg.com/raw/88972a2aeda155c10000e8576d16bbe9.png)
Periksa apakah tidak ada IP atau IP yang salah dikonfigurasi untuk `listen` dalam file konfigurasi `/etc/ntp.conf`. Ubah ke IP pribadi utama instans dan mulai ulang ntpd.

### Bagaimana cara memperbaiki kesalahan yang terjadi saat menyinkronkan waktu menggunakan server NTP publik?
Kesalahan `tidak ada server yang cocok untuk sinkronisasi ditemukan` seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/1909910bc2a86a5f93e09f4601654327.png)
Hal ini mungkin disebabkan oleh kebijakan perlindungan NTP sebagai respons terhadap serangan DDoS ke alamat IP publik instans. Kebijakan ini memblokir semua lalu lintas masuk publik di titik sumber Tencent Cloud 123 dan menyebabkan pengecualian sinkronisasi. Sebaiknya coba gunakan server NTP pribadi untuk menyinkronkan waktu.
