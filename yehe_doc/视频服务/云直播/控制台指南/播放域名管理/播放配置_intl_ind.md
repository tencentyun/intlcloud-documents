Setelah push melalui nama domain berhasil, Anda dapat membuka konsol CSS. Selanjutnya, salin `StreamName` di URL push, lalu masukkan ke pembuat alamat pemutaran ulang untuk membuat URL pemutaran ulang untuk streaming tersebut.

## Prasyarat
 Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live).
 - Anda telah menambahkan **nama domain pemutaran ulang**. Informasi selengkapnya dapat dilihat di [Adding Domain Name (Menambahkan Nama Domain)](https://intl.cloud.tencent.com/document/product/267/35970).

## Petunjuk
1. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **playback domain** (domain pemutaran ulang) target atau klik **Manage** (Kelola) di sebelah kanan untuk masuk ke halaman manajemen domain.
2. Pilih **Playback Configuration** (Konfigurasi Pemutaran Ulang) dan, di **Playback Address Generator** (Pembuat Alamat Pemutaran Ulang), selesaikan pengaturan berikut:
	1. Pilih putar **original stream** (streaming asli) atau **transcoded stream** (streaming yang di-transcoding). Jika Anda memilih opsi kedua, streaming akan di-transcoding sesuai dengan templat transcoding yang dipilih sebelum pemutaran ulang.
	2. Masukkan `StreamName` kustom, misalnya `liveteststream`. Untuk memutar ulang streaming yang sesuai dengan URL push, Anda harus memasukkan `StreamName` di URL push.
	3. Pilih waktu kedaluwarsa, misalnya `2021-06-30 19:00:44`.
	4. Klik **Generate Address** (Buat Alamat).
![](https://qcloudimg.tencent-cloud.cn/raw/ae67aa5386d9f47d7bd20d7cce7c7603.png)
3. Jika belum mengaktifkan autentikasi untuk domain pemutaran ulang, Anda dapat menemukan empat URL pemutaran ulang di bagian **Playback URL** (URL Pemutaran Ulang), yaitu URL RTMP, FLV, HLS, dan UDP. Ganti `StreamName` dengan nama streaming Anda agar Anda dapat menggunakan URL untuk memutar streaming.
![](https://qcloudimg.tencent-cloud.cn/raw/16a192a0090e8f4f470ace2b78cac52e.png)
>?Informasi selengkapnya dapat dilihat di [Live Playback (Pemutaran Ulang Langsung)](https://intl.cloud.tencent.com/document/product/267/31559).




## URL Pemutaran Ulang
### Format URL Pemutaran Ulang
```
Format RTMP: `rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
Format FLV: `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
Format M3U8: `http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
Format UDP: webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- `domain`: domain pemutaran ulang Anda dengan lisensi ICP
- `AppName`: nama aplikasi streaming langsung, yang secara default diberi nama `live`, tetapi dapat diubah
- `StreamName`: nama streaming kustom yang digunakan untuk mengidentifikasi streaming langsung
- `txSecret`: string autentikasi yang dibuat setelah autentikasi pemutaran ulang diaktifkan
- `txTime`: stempel waktu di URL pemutaran ulang yang ditambahkan di konsol. Ini menunjukkan waktu kedaluwarsa URL.

>!
>- Jika Anda telah mengaktifkan autentikasi, waktu kedaluwarsa aktual URL adalah `txTime` ditambah masa berlaku kunci.
>- Demi kenyamanan, waktu yang Anda atur di konsol adalah waktu kedaluwarsa aktual. Jika Anda telah mengaktifkan autentikasi, sistem akan menghitung `txTime` saat membuat URL pemutaran ulang.
>- Push atau pemutaran ulang dapat tetap dilanjutkan bahkan setelah URL kedaluwarsa asalkan Anda memulai push atau pemutaran ulang sebelum waktu kedaluwarsa dan streaming tidak terputus.

### URL pemutaran ulang streaming yang di-transcoding
Jika templat transcoding dikonfigurasikan untuk nama domain pemutaran ulang, `_transcoding template name` (`_nama templat transcoding`) akan ditambahkan setelah `StreamName` di URL pemutaran ulang asli untuk streaming yang di-transcoding.

Misalnya, jika URL pemutaran ulang asli adalah `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)` dan nama templat transcoding yang diikat dengan nama domain adalah `hd`, URL pemutaran ulang streaming yang di-transcoding seharusnya adalah `http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.

### URL pemutaran ulang streaming H.265
CSS mendukung push dan pemutaran ulang streaming H.265. Jika streaming asli adalah streaming H.264, Anda dapat menggunakan templat transcoding untuk melakukan transcoding pada streaming menjadi H.265. Penjelasan mendetail seputar transcoding melalui konsol dan melalui API dapat dilihat di [Transcoding melalui konsol CSS](https://intl.cloud.tencent.com/document/product/267/31561) dan [Transcoding melalui API](https: //intl.cloud.tencent.com/document/product/267/31561).
