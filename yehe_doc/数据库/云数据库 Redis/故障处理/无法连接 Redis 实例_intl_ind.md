
## Deskripsi Kesalahan
- [Gejala 1](id:xz1): gagal terhubung ke atau login ke instans TencentDB for Redis dari instans CVM.
- [Gejala 2](id:xz2): gagal terhubung ke atau login ke instans TencentDB for Redis dari pusat manajemen database (DMC).
![](https://qcloudimg.tencent-cloud.cn/raw/8917bd64abc5a131884fa3b0c9df190d.png)

## Penyebab Umum
- Masalah jaringan
- Masalah grup keamanan.
- Masalah kata sandi.
- Jumlah maksimum koneksi telah tercapai.
- Memori atau shard terpakai habis.
- Instans tidak dapat diakses melalui jaringan publik.
- Terjadi peralihan ketersediaan tinggi (HA), layanan database menjadi tidak tersedia, peralihan replika baca saja terjadi, atau layanan replika baca saja menjadi tidak tersedia, dll.

## Solusi
1. [Jalankan `telnet` untuk menemukan tempat kesalahan terjadi (di TencentDB for Redis atau bisnis Anda)](#sytqr).
2. [Periksa apakah kesalahan disebabkan oleh masalah kata sandi](#qrsfwmmwt).
3. [Ubah jumlah koneksi maksimum yang diizinkan](#tzzdljs).
4. [Periksa apakah kesalahan disebabkan oleh kegagalan penulisan karena memori atau shard yang terpakai habis](#qrsfncxm).
5. [Aktifkan akses jaringan publik](#sxwwfw).
6. [Periksa apakah salah satu hal berikut terjadi: Peralihan HA, layanan basis data tidak tersedia, peralihan replika baca saja, atau layanan replika baca saja tidak tersedia](#qrsffsh).

## Prosedur Pemecahan Masalah
### [Menjalankan `telnet` untuk menemukan di mana kesalahan terjadi (di TencentDB for Redis atau bisnis Anda)](id:sytqr)
Jalankan `telnet` di alat baris perintah untuk mempersempit penyebab kesalahan:
```js
[root@VM-4-10-centos ~]# telnet 10.x.x.34 6379
Mencoba 10.x.x.34...
Terhubung ke 10.x.x.34.
Karakter escape adalah '^]'.
```
Seperti yang ditunjukkan di atas, jika hasilnya menunjukkan bahwa koneksi berhasil, instans TencentDB for Redis berjalan normal. Harap pecahkan masalah bisnis Anda:

#### 1. Memecahkan masalah jaringan
Untuk terhubung melalui jaringan pribadi, instans CVM dan TencentDB harus berada di bawah akun yang sama dan di VPC yang sama di wilayah yang sama, atau keduanya di jaringan klasik.
- Jika instans CVM berada di VPC, sedangkan instans Redis di jaringan klasik, sebaiknya Anda mengalihkan jenis jaringan instans Redis dari jaringan klasik ke VPC. Untuk informasi selengkapnya, lihat [Mengonfigurasi Jaringan](https://intl.cloud.tencent.com/document/product/239/31944).
- Jika instans Redis berada di VPC, sedangkan instans CVM di jaringan klasik, sebaiknya Anda mengalihkan jenis jaringan instans CVM dari jaringan klasik ke VPC. Untuk informasi selengkapnya, lihat [Beralih ke VPC](https://intl.cloud.tencent.com/document/product/213/20278).
- Jika instans CVM dan TencentDB for Redis berada di VPC yang berbeda di wilayah yang sama, sebaiknya Anda memigrasikan instans Redis ke VPC instans CVM. Untuk informasi selengkapnya, lihat [Mengonfigurasi Jaringan](https://intl.cloud.tencent.com/document/product/239/31944).
- Jika instans CVM dan TencentDB for Redis berada di VPC yang berbeda di wilayah yang berbeda, sebaiknya Anda membuat [CCN](https://intl.cloud.tencent.com/zh/document/product/1003) di antara kedua VPC.
- Jika instans CVM dan TencentDB for Redis berada di VPC yang berbeda di bawah akun yang berbeda, sebaiknya Anda membuat [CCN](https://intl.cloud.tencent.com/zh/document/product/1003) di antara kedua VPC.

#### 2. Memecahkan masalah grup keamanan
Instans CVM tidak dapat terhubung ke instans TencentDB for Redis jika grup keamanannya salah.
- [Konfigurasi grup keamanan CVM salah](id:caqzpzyw)
Untuk menggunakan instans CVM guna mengakses instans Redis, Anda perlu mengonfigurasi aturan keluar di grup keamanan instans CVM. **Jika target aturan keluar bukan "0.0.0.0/0" dan port protokol bukan "ALL"**, IP dan port instans Redis harus ditambahkan ke aturan.
 1. Masuk ke halaman(https://console.cloud.tencent.com/cvm/securitygroup) [Grup Keamanan] di konsol CVM dan klik nama grup keamanan yang terikat dengan CVM untuk masuk ke halaman detailnya.
 2. Pada tab **Outbound rule** (Aturan outbound), klik **Add Rule** (Tambahkan Aturan).
Atur **Type** (Jenis) ke **Custom** (Kustom), **Target** (Target) ke IP/rentang IP instans Redis, dan **Policy** (Kebijakan) ke **Allow** (Izinkan).

- [Konfigurasi grup keamanan Redis salah](id:maqzpzyw)
Untuk menggunakan instans CVM guna mengakses instans Redis, Anda perlu mengonfigurasi aturan masuk di grup keamanan instans Redis. **Jika sumber aturan masuk bukan "0.0.0.0/0" dan port protokol bukan "ALL"**, IP dan port instans CVM harus ditambahkan ke aturan. 
 1. Masuk ke halaman(https://console.cloud.tencent.com/cvm/securitygroup) [Grup Keamanan] di konsol CVM dan klik nama grup keamanan yang terikat dengan CVM untuk masuk ke halaman detailnya.
 2. Pada tab **Inbound rule** (Aturan inbound), klik **Add Rule** (Tambahkan Aturan).
Harap perhatikan bahwa Anda juga perlu membuka IP dan port instans Redis dalam aturan masuk.
Atur **Type** (Jenis) ke **Custom** (Kustom), **Source** (Sumber) ke IP/rentang IP instans CVM, dan **Policy** (Kebijakan) ke **Allow** (Izinkan).
>!  
>- Instans Redis menggunakan port jaringan pribadi 6379 secara default dan mendukung penyesuaian port-nya. Jika port default diubah, port baru harus dibuka di aturan masuk grup keamanan Redis.
>- Jika port default 6379 dari instans Redis digunakan, port tersebut harus dibuka dalam aturan masuk grup keamanan Redis.

### [Memecahkan masalah kata sandi](id:qrsfwmmwt)
Jalankan perintah `info`. Jika informasi berikut ditampilkan, kata sandi instans TencentDB for Redis sudah benar.
```js
[root@SNG-Qcloud /data/home/rickyu]# redis-cli -h 10.x.x.34 -p 6379 -a kata sandi
10.x.x.2:6379> info cpu
# CPU
used_cpu_sys:1623.176000
used_cpu_user:4649.572000
used_cpu_sys_children:0,000000
used_cpu_user_children: 0,000000
```
Jika `NOAUTH Authentication required.` ditampilkan, kata sandi salah.
```js 
10.0.4.31:6379> memori info
NOAUTH Authentication required.
10.0.4.31:6379> 
```
#### Solusi
Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans untuk masuk ke halaman detail instans, tempat Anda dapat mengatur ulang kata sandi. Untuk informasi selengkapnya, lihat [Mengelola Akun](https://intl.cloud.tencent.com/document/product/239/34590).
![](https://qcloudimg.tencent-cloud.cn/raw/fe7308090ce478150a0b1c5706bc1aef.png)

### [Menyesuaikan jumlah maksimum koneksi](id:tzzdljs)
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan masuk ke halaman detail instans.
2. Klik **Adjust** (Sesuaikan) di sebelah **Max Connections** (Koneksi Maks) di **Network Info** (Info Jaringan).
>?Anda dapat mengubah jumlah maksimum koneksi proksi di konsol. Untuk mengubah jumlah maksimum koneksi Redis, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).
>
![](https://qcloudimg.tencent-cloud.cn/raw/40d1e79d20b29d4f381f53d79ecd9144.png)
3. Pada tab **System Monitoring** (Pemantauan System)  > **Monitoring Metrics** (Metrik Pemantauan), pilih metrik **Connection Utilization** (Penggunaan Koneksi) untuk melihat nilainya.
Data pemantauan proksi:
![](https://qcloudimg.tencent-cloud.cn/raw/ba5071d61ba24b97e1bc69b2d28e48d3.png)
Data pemantauan Redis:
![](https://qcloudimg.tencent-cloud.cn/raw/38dc0b1facdff97aec660e4c54e0b9d5.png)

### [Memeriksa apakah memori atau shard terpakai habis](id:qrsfncxm)
Jika Anda menerima pesan kesalahan berikut:
```js
"-READONLY You can't write against a read only slave.\r\n"
```
Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan pilih tab **System Monitoring** (Pemantauan Sistem) untuk melihat penggunaan memori.
![](https://qcloudimg.tencent-cloud.cn/raw/7a63fbc80e9cb39c317b842d458866cf.png)
Jika memori terpakai habis, penulisan akan gagal. Harap segera [perluas kapasitas](https://intl.cloud.tencent.com/document/product/239/31934) atau adopsi kebijakan penghapusan `allkeys-lru` atau `volatile-lru`.

>?Data instans mungkin hilang jika kebijakan penghapusan `allkeys-lru` diadopsi. Harap menilai dampaknya sebelum melakukannya.

### [Mengaktifkan akses jaringan publik](id:sxwwfw)
TencentDB for Redis sekarang memungkinkan Anda untuk secara manual mengaktifkan akses jaringan publik di konsol, sehingga instans dapat diakses melalui jaringan publik. Untuk informasi selengkapnya, lihat [Mengonfigurasi Alamat Jaringan Publik](https://intl.cloud.tencent.com/document/product/239/43452).

### [Memeriksa apakah salah satu hal berikut terjadi: Peralihan HA, layanan database tidak tersedia, peralihan replika baca saja, atau layanan replika baca saja yang tidak tersedia](id:qrsffsh)
Jika Anda menemukan bahwa koneksi tergolong tidak biasa, ada banyak kesalahan akses dan kueri lambat, dan Anda menerima alarm peristiwa dari CM pada titik waktu tertentu, maka peristiwa tidak biasa telah terjadi. Dalam hal ini, [hubungi kami](https://intl.cloud.tencent.com/contact-us) untuk mendapatkan bantuan.

**Konfigurasikan alarm peristiwa di konsol [Cloud Monitor](https://console.cloud.tencent.com/monitor/alarm2/policy) **:
![](https://qcloudimg.tencent-cloud.cn/raw/f7de41a133dd54b2c82574f2bbbc1dde.png)

## Lampiran
### [Melihat jenis jaringan dan informasi VPC](id:wllxvpdff)
Untuk mengaktifkan koneksi antara instans CVM dan TencentDB for Redis melalui jaringan pribadi, instans tersebut harus berada di bawah akun yang sama dan di VPC yang sama di wilayah yang sama, atau keduanya di jaringan klasik.
>?
>- Jika daftar instans menunjukkan **Classic Network** (Jaringan Klasik) atau **VPC** (VPC), itu berarti jaringan instans CVM dan TencentDB for Redis memiliki jenis yang sama.
>- Jika daftar instans menunjukkan **VPC** (VPC) yang sama (di wilayah yang sama), itu berarti instans CVM dan TencentDB for Redis berada di VPC yang sama.
>
- **View the network type/VPC of CVM** (Melihat jenis jaringan/VPC CVM): login ke [konsol CVM](https://console.cloud.tencent.com/cvm/instance) dan lihat informasi jaringan dalam daftar instans.
![](https://qcloudimg.tencent-cloud.cn/raw/ad8661c3906fa96962618e51b731fc4d.png)
- **View the network type/VPC of TencentDB for Redis** (Melihat tipe jaringan/VPC TencentDB for Redis): login ke [konsole TencentDB for Redis](https://console.cloud.tencent.com/redis) dan lihat **Network** (Jaringan) dalam daftar instans.
![](https://qcloudimg.tencent-cloud.cn/raw/920e151463fc3f6087c671294b05ee46.png)
