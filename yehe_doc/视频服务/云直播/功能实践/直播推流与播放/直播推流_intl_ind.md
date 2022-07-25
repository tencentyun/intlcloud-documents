Pada dasarnya CSS adalah proses streaming, sama dengan siaran langsung saluran TV yang ditayangkan kepada pemirsa melalui jaringan kabel. Agar dapat menyelesaikan proses ini, CSS harus memiliki perangkat untuk menangkap dan untuk melakukan push (mirip kamera), layanan streaming langsung cloud (mirip jaringan kabel), dan perangkat pemutaran ulang (mirip pesawat TV). Perangkat-perangkat tersebut bisa berupa perangkat cerdas, seperti telepon seluler, PC, dan tablet serta browser web. Kami menyediakan demo perangkat lunak lengkap untuk berbagai jenis perangkat.

[](id:step1)
## Persiapan
1. Aktifkan [layanan CSS](https://console.cloud.tencent.com/live?from=product-banner-use-lvb).
2. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **Add Domain** (Tambahkan Domain) untuk menambahkan nama domain push dengan nomor izin ICP. Informasi selengkapnya dapat dilihat di [Adding Domain Name (Menambahkan Nama Domain)](https://intl.cloud.tencent.com/document/product/267/35970).
>? CSS menyediakan nama domain push default dalam format `xxx.livepush.myqcloud.com`. Anda sebaiknya tidak menggunakannya sebagai nama domain push untuk bisnis real Anda.

[](id:push_add)
## Mendapatkan Alamat Push
Login ke konsol CSS, pilih **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Toolkit CSS < Pembuat Alamat) untuk membuat alamat push dan lakukan konfigurasi sebagai berikut:
- Pilih *Push Domain** (Domain Push) sebagai jenis domain.
- Pilih nama domain push yang telah Anda tambahkan di manajemen domain.
- Masukkan `AppName` (secara default diisi `live`). Ini digunakan untuk membedakan jalur berbagai aplikasi dengan nama domain yang sama.
- Masukkan `StreamName` kustom, misalnya `liveteststream`.
- Pilih waktu kedaluwarsa alamat, misalnya `2019-10-18 23:59:59`.
- Klik **Generate Address** (Buat Alamat). 

>!
>- Untuk memastikan keamanan streaming langsung Anda, sistem akan secara otomatis mengaktifkan autentikasi push. Anda juga dapat memilih nama domain push yang akan dimodifikasi di **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) dan dengan mengeklik **Manage** (Kelola) di bagian kanan untuk masuk ke halaman detail nama domain, kemudian menyesuaikan informasi autentikasi di **Push Configuration** (Konfigurasi Push). Alamat push menggunakan format berikut:
`rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
>- Selain menggunakan metode di atas, Anda juga dapat memilih nama domain push melalui **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) di konsol CSS dengan mengeklik **Manage** (Kelola), memilih **Push Configuration** (Konfigurasi Push), memasukkan waktu kedaluwarsa alamat push dan `StreamName` kustom, dan mengeklik **Generate Push Address** (Buat Alamat Push) untuk membuat alamat push.
>-Jika membutuhkan **alamat push yang persisten**, Anda dapat masuk ke **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), memilih nama domain push, mengeklik **Manage** (Kelola), dan memilih **Push Configuration** (Konfigurasi Push) untuk perhitungan dan pembuatan dengan mengacu pada kode sampel di **Push Address Sample Code** (Kode Sampel Alamat Push). Informasi selengkapnya dapat dilihat di [Bagaimana cara melihat kode sampel push?](https://intl.cloud.tencent.com/document/product/267/31059).

[](id:live_push)
## Push Langsung
Anda dapat menggunakan metode berikut untuk menerapkan push langsung berdasarkan skenario bisnis Anda:

[](id:pc)
### Skenario 1. Push PC
Untuk PC (Windows/macOS), Anda dapat memilih menginstal [OBS](https://obsproject.com/download) atau [XSplit](https://www.xsplit.com/zh-cn) untuk push. OBS merupakan program perekaman dan streaming video sumber terbuka gratis yang mendukung sistem operasi, seperti Windows, macOS, and Linux, sedangkan XSplit adalah program berbayar yang menawarkan penginstal mandiri untuk streaming game langsung. Untuk streaming langsung selain game, Anda sebaiknya menggunakan BroadCaster.
![](https://main.qcloudimg.com/raw/dcb203971ac99415258ea0b0ee1529a8.png)
Dokumen ini menggunakan push dengan OBS sebagai contoh untuk menjelaskan langkah-langkah. Misalnya, alamat push yang sudah disiapkan adalah:

```
rtmp://3891.livepush.myqcloud.com/live/3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F
```


1. Buka [situs web resmi OBS](https://obsproject.com/download) untuk mengunduh dan menginstal alat push.
2. Buka OBS dan klik **Control** > **Settings** (Kontrol > Pengaturan) di bagian bawah untuk masuk ke halaman pengaturan.
3. Klik **Stream** (Streaming) untuk masuk ke halaman konfigurasi push dan atur sebagai berikut:
  1. Pilih "Custom" (Kustom) sebagai jenis layanan.
  1. Masukkan separuh pertama alamat push sebagai server, misalnya `rtmp://3891.livepush.myqcloud.com/live/`.
  1. Masukkan separuh kedua alamat push sebagai kunci streaming, misalnya `3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F`.
  1. Klik **OK** (Oke) di sudut kanan bawah.
![](https://main.qcloudimg.com/raw/7b5365a0be590c3694fbb6d0ded8e5e3.png)
4. Klik **Controls** > **Start Streaming** (Kontrol > Mulai Streaming) untuk menguji streaming. Informasi selengkapnya tentang cara menggunakan OBS dapat dilihat di [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).

[](id:web)
### Skenario 2. Push web
1. Login ke konsol CSS.
2. Pilih **CSS Toolkit** > **[Web Push](https://console.cloud.tencent.com/live/tools/webpush)** (Toolkit CSS > Push Web).
3. Lakukan pengaturan berikut di halaman push web:
  1. Pilih nama domain push.
  2. Masukkan `AppName` (secara default diisi `live`). Ini digunakan untuk membedakan jalur berbagai aplikasi dengan nama domain yang sama.
  2. Masukkan `StreamName` kustom, misalnya `liveteststream`.
  3. Pilih waktu kedaluwarsa, misalnya `2019-10-30 23:59:59`.
  4. Klik **Start Push** (Mulai Push) dan berikan izin ke kamera untuk memulai push.

>! Fitur push web mengharuskan Anda menggunakan perangkat dengan kamera yang telah terinstal dan browser yang mendukung plugin Flash untuk memanggil izin kamera.

![](https://main.qcloudimg.com/raw/9da7489bb2387049859131e792364124.png)

[](id:mobile)
### Skenario 3. Push seluler
1. Pindai kode QR dengan telepon seluler untuk mengunduh dan menginstal [Toolkit Video Cloud](https://intl.cloud.tencent.com/document/product/1071/38147).
2. Buka toolkit dan pilih **MLVB** > **Camera Push** (Push Kamera).
3. Masukkan [alamat push](#step1) secara manual atau dengan memindai kode QR.
4. Ketuk **Start** (Mulai) di sudut kiri bawah untuk memulai push.

>? Jika belum menyiapkan alamat push, Anda dapat mengetuk **New** (Baru) di sebelah kanan bilah alamat push di halaman **Camera Push** (Push Kamera), dan sistem akan secara otomatis memasukkan alamat push dan memberikan alamat pemutaran ulang yang sesuai dan dapat digunakan untuk pemutaran ulang langsung.

[](id:sdk)
### Skenario 4. Push SDK langsung
Jika Anda perlu mengintegrasikan push langsung saja ke aplikasi yang sudah ada, ikuti langkah-langkah berikut:
1. Unduh [SDK MLVB](https://intl.cloud.tencent.com/document/product/1071/38150).
2. Selesaikan integrasi sesuai dengan petunjuk di dokumen integrasi [iOS](https://intl.cloud.tencent.com/document/product/1071/38157) atau [Android](https://intl.cloud.tencent.com/document/product/1071/38158).

SDK langsung merupakan kumpulan layanan streaming langsung seluler. Fitur ini memperlihatkan, dalam bentuk kode sumber gratis, cara menggunakan CSS, VOD, IM, dan COS Tencent Cloud untuk membangun solusi streaming langsung yang paling tepat untuk bisnis Anda. Informasi selengkapnya dapat dilihat di [MLVB](https://intl.cloud.tencent.com/product/mlvb). 


## Pertanyaan Umum
- [Bagaimana cara menerapkan pemutaran ulang langsung?](https://intl.cloud.tencent.com/document/product/267/31559)
- [Bagaimana cara menyambung URL push?](https://intl.cloud.tencent.com/document/product/267/38393)
- [Bagaimana cara menghitung URL perlindungan hotlink?](https://intl.cloud.tencent.com/document/product/267/31560)

