## Ikhtisar

Daemon Network Time Protocol (ntpd) adalah daemon dari sistem operasi Linux. Ini adalah implementasi lengkap dari NTP dan digunakan untuk memperbaiki perbedaan waktu antara sistem lokal dan server sumber jam. Tidak seperti ntpdate, yang memperbarui waktu secara berkala, ntpd mengoreksi waktu terus menerus tanpa jeda waktu. Dokumen ini menggunakan CentOS 7.5 sebagai contoh untuk menjelaskan cara menginstal dan mengonfigurasi ntpd.

## Catatan

- Beberapa sistem operasi menggunakan chrony sebagai layanan NTP default. Pastikan ntpd berjalan dan dikonfigurasi untuk diluncurkan secara otomatis saat startup.
 - Jalankan perintah `systemctl is-active ntpd.service` untuk melihat apakah ntpd sedang berjalan.
 - Jalankan perintah `systemctl is-enabled ntpd.service` untuk melihat apakah ntpd dikonfigurasi untuk diluncurkan secara otomatis saat startup.
- Port komunikasi layanan NTP adalah UDP 123. Pastikan Anda telah membuka port ke Internet sebelum mengonfigurasi layanan NTP.
Jika port tidak terbuka, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272) untuk membukanya ke Internet.

## Petunjuk

### Menginstal ntpd

Jalankan perintah berikut untuk memeriksa apakah ntpd telah diinstal.
```
rpm -qa | grep ntp
```
 - Jika hasil berikut ditampilkan, ntpd telah diinstal.
![Memeriksa apakah ntpd telah diinstal](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
 - Jika ntpd belum terinstal, jalankan perintah `yum install ntp` untuk menginstalnya. 
```
yum -y install ntp
```
ntpd menggunakan mode klien secara default.

### Mengonfigurasi NTP
1. Jalankan perintah berikut untuk membuka file konfigurasi layanan NTP.
```
vi /etc/ntp.conf
```
2. Tekan **i** (i) untuk beralih ke mode pengeditan dan menemukan konfigurasi `server`. Ubah nilai `server` ke server sumber jam NTP yang ingin Anda gunakan (seperti `time1.tencentyun.com`) dan hapus nilai yang tidak diinginkan, seperti yang ditunjukkan di bawah ini:
![Konfigurasi server](https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)
3. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.

### Meluncurkan ntpd

Jalankan perintah berikut untuk memulai ulang layanan ntpd.
```
systemctl restart ntpd.service
```

### Memeriksa status ntpd

Jalankan perintah berikut untuk memeriksa status ntpd sesuai kebutuhan. 
- Jalankan perintah berikut untuk memeriksa apakah NTP secara normal mendengarkan pada port layanan UDP 123.
```
netstat -nupl
```
Jika hasil berikut ditampilkan, operasi mendengarkan berjalan normal.
![netstat -nupl](https://main.qcloudimg.com/raw/d7da764d05135959154920b81fa9f1e4.png)
- Jalankan perintah berikut untuk memeriksa apakah status ntpd berjalan normal.
```
service ntpd status
```
Jika hasil berikut ditampilkan, status ntpd berjalan normal.
![status ntpd](https://main.qcloudimg.com/raw/321e56d0f7797f382d9f6903c0315f96.png)
- Jalankan perintah berikut untuk memeriksa apakah NTP telah dimulai secara normal dan dikonfigurasi ke server sumber jam NTP yang benar.
```
ntpstat
```
Alamat IP server sumber jam NTP saat ini yang dikonfigurasi sebelumnya harus ditampilkan, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/a99f5da438bafb1d148e9b033f48afad.png)
Anda juga bisa mendapatkan alamat IP yang sesuai dengan nama domain dengan menjalankan perintah `nslookup domain name`.
- Jalankan perintah berikut untuk mendapatkan informasi layanan NTP mendetail.
```
ntpq -p
```
Hasil berikut akan ditampilkan:
![](https://main.qcloudimg.com/raw/ca9ef4caf98b49ed2c9110198a66e7c3.png)
 - **remote** (jarak jauh): nama server NTP yang merespons permintaan ini.
 - **refid** (refid): server NTP satu strata di atasnya tempat server NTP pada strata ini disinkronkan.
 - **st** (st): strata server jarak jauh. Lapisan server dapat diatur ke 1 hingga 16 dari tinggi ke rendah. Untuk mengurangi beban dan kemacetan jaringan, Anda harus menghindari koneksi langsung ke server strata 1.
 - **when** (kapan): jumlah detik yang telah berlalu sejak permintaan terakhir yang berhasil.
 - **poll** (kumpulan): interval sinkronisasi (dalam detik) antara server lokal dan jauh. Pada awalnya, nilai `poll` akan lebih kecil, yang menunjukkan frekuensi sinkronisasi yang lebih tinggi, sehingga waktu dapat disesuaikan dengan rentang waktu yang tepat secepatnya. Nantinya, nilai `poll` akan meningkat secara bertahap, dan frekuensi sinkronisasi akan berkurang.
 - **reach** (jangkauan): nilai oktal yang digunakan untuk menguji apakah server dapat terhubung. Nilainya meningkat setiap kali server berhasil terhubung.
 - **delay** (penundaan): waktu bolak-balik pengiriman permintaan sinkronisasi dari mesin lokal ke server NTP.
 - **offset** (offset): perbedaan waktu dalam milidetik (md) antara host dan sumber waktu melalui NTP. Semakin dekat offset ke 0, semakin dekat waktu host dan server NTP.
 - **jitter** (jitter): nilai yang digunakan untuk statistik yang mencatat distribusi offset pada sejumlah koneksi berurutan tertentu. Semakin kecil nilai absolutnya, semakin akurat waktu hostnya.

### Mengatur peluncuran otomatis ntpd saat startup

1. Jalankan perintah berikut untuk meluncurkan ntpd secara otomatis saat startup.
```
systemctl enable ntpd.service
```
2. Jalankan perintah berikut untuk memeriksa apakah chrony diatur untuk diluncurkan saat startup.
```
systemctl is-enabled chronyd.service
```
Jika chrony diatur untuk diluncurkan saat startup, jalankan perintah berikut untuk menghapus chrony dari daftar mulai otomatis.
chrony tidak kompatibel dengan ntpd, yang dapat menyebabkan kegagalan mulai ntpd.
```
systemctl disable chronyd.service
```

### Meningkatkan keamanan ntpd

Jalankan perintah berikut secara berurutan untuk meningkatkan keamanan file konfigurasi `/etc/ntp.conf`.
```
interface ignore wildcard
```
```
interface listen eth0
```
