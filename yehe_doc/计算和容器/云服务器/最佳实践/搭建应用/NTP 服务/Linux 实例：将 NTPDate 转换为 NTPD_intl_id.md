## Ikhtisar

ntpdate adalah pembaruan titik perubahan untuk sinkronisasi waktu instans baru Anda. Ntpd adalah daemon bertahap untuk sinkronisasi waktu dari instans yang sedang berjalan. Dokumen ini menggunakan sistem operasi CentOS 7.5 sebagai contoh untuk memperkenalkan cara transisi dari ntpdate ke ntpd pada CVM.

## Prasyarat
Layanan NTP berkomunikasi pada port UDP 123. Pastikan Anda telah membuka port ke Internet sebelum beralih ke layanan NTP.
Jika port belum dibuka, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272) untuk membukanya ke Internet.

## Petunjuk
Anda dapat memilih untuk beralih dari ntpdate ke ntpd [manual](#manual) atau [otomatis](#automatic).
<span id="manual"></span>
### Melakukan transisi dari ntpdate ke ntpd secara manual
#### Mematikan ntpdate
1. Jalankan perintah berikut untuk mengekspor konfigurasi `crontab` dan memfilter ntpdate.
```
crontab -l |grep -v ntpupdate > /tmp/cronfile
```
2. Jalankan perintah berikut untuk memperbarui konfigurasi ntpdate.
```
crontab /tmp/cronfile
```
3. Jalankan perintah berikut untuk memodifikasi file `rc.local`.
```
vim /etc/rc.local
```
4. Tekan **i** (i) untuk beralih ke mode edit dan menghapus baris konfigurasi `ntpupdate`.
5. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.

#### Mengonfigurasi ntpd
1. Jalankan perintah berikut untuk membuka file konfigurasi layanan NTP.
```
vi /etc/ntp.conf
```
2. Tekan **i** (i) untuk beralih ke mode edit dan menemukan konfigurasi `server`. Ubah nilai `server` ke server sumber jam NTP yang ingin Anda gunakan (seperti `time1.tencentyun.com`) dan hapus nilai yang tidak diinginkan, seperti yang ditunjukkan di bawah ini:
![Konfigurasi server](https://main.qcloudimg.com/raw/643dc5bbd2a42307ec10b5d38f756dda.png)
3. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.

<span id="automatic"></span>
### Melakukan transisi dari ntpdate ke ntpd secara otomatis
1. Unduh skrip `ntpd_enable.sh`.
```
wget https://image-10023284.cos.ap-shanghai.myqcloud.com/ntpd_enable.sh
```
2. Jalankan perintah berikut untuk transisi dari ntpdate ke ntpd menggunakan skrip `ntpd_enable.sh`.
```
sh ntpd_enable.sh
```

## Operasi yang Relevan
### Memeriksa status ntpd
Jalankan perintah berikut untuk memeriksa status ntpd sesuai kebutuhan.
- Jalankan perintah berikut untuk memeriksa apakah NTP mendengarkan secara normal pada port layanan UDP 123.
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

- Jalankan perintah berikut untuk mendapatkan informasi layanan NTP mendetail.
```
ntpq -p
```
Hasil berikut akan ditampilkan:
![](https://main.qcloudimg.com/raw/ca9ef4caf98b49ed2c9110198a66e7c3.png)
 - **\***: server NTP sedang digunakan saat ini.
 - **remote** (jarak jauh): nama server NTP yang merespons permintaan ini.
 - **refid** (refid): server NTP satu strata di atasnya tempat server NTP pada strata ini disinkronkan.
 - **st** (st): strata server jarak jauh. Lapisan server dapat diatur ke 1 hingga 16 dari tinggi ke rendah. Untuk mengurangi beban dan kemacetan jaringan, Anda harus menghindari koneksi langsung ke server strata 1.
 - **when** (kapan): jumlah detik yang telah berlalu sejak permintaan terakhir yang berhasil.
 - **poll** (kumpulan): interval sinkronisasi (dalam detik) antara server lokal dan jauh. Pada awalnya, nilai `poll` akan lebih kecil, yang menunjukkan frekuensi sinkronisasi yang lebih tinggi, sehingga waktu dapat disesuaikan dengan rentang waktu yang tepat secepatnya. Nantinya, nilai `poll` akan meningkat secara bertahap, dan frekuensi sinkronisasi akan berkurang.
 - **reach** (jangkauan): nilai oktal yang digunakan untuk menguji apakah server dapat terhubung. Nilainya meningkat setiap kali server berhasil terhubung.
 - **delay** (penundaan): waktu bolak-balik pengiriman permintaan sinkronisasi dari mesin lokal ke server NTP.
 - **offset** (offset): perbedaan waktu dalam milidetik (md) antara host dan sumber waktu melalui NTP. Semakin dekat offset ke 0, semakin dekat waktu host dan server NTP.
 - **jitter** (jitter): nilai yang digunakan untuk statistik yang mencatat distribusi offset pada sejumlah koneksi berurutan tertentu. Semakin kecil nilai absolutnya, semakin akurat waktu hostnya.
