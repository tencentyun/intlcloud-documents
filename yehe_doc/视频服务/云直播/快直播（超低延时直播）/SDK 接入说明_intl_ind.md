Sebagai versi LVB dengan latensi lebih rendah, LEB memberikan pengalaman **streaming langsung** yang sangat baik dengan latensi pemutaran ulang milidetik, jauh lebih rendah daripada latensi pemutaran ulang streaming langsung menggunakan protokol pada umumnya.
Sebelum Anda menggunakan LEB, silakan baca [LEB Billing Overview (Ikhtisar Penagihan LEB)](https://intl.cloud.tencent.com/document/product/267/39969) untuk mempelajari daftar item yang dapat dikenai tagihan dan harganya.

> ! LEB menggunakan protokol WebRTC untuk memastikan latensi rendah. LEB menerapkan codec Opus dan tidak mendukung B-frame. Jika streaming asli berisi B-frame atau codec yang digunakan bukan Opus, backend CSS akan menghapus B-frame dan melakukan transcoding pada streaming ke format Opus, dan transcoding ini akan dikenai [biaya transcoding standar](https://intl.cloud.tencent.com/document/product/267/39604).

[](id:app)
## Integrasi ke dalam Aplikasi
### Petunjuk
Anda dapat mengintegrasikan SDK MLVB ke dalam aplikasi iOS atau Android untuk menerapkan fitur push dan pemutaran ulang langsung.

- **Live push on apps** (Push langsung di aplikasi): Mendukung pengambilan tangkapan layar video kamera atau ponsel, dan kemudian melakukan push pada konten ke platform CSS menggunakan protokol RTMP. Untuk informasi lebih lanjut, pelajari [Publishing from Camera (Penerbitan dari Kamera)](https://intl.cloud.tencent.com/document/product/1071/38157) dan [Publishing from Screen (Penerbitan dari Layar)](https://intl.cloud.tencent.com/document/product/1071/41878).
- **Live playback on apps** (Pemutaran ulang langsung di aplikasi): Mendukung protokol pemutaran ulang WebRTC. Anda dapat menggunakan SDK MLVB, yang mengintegrasikan LEB, untuk mengaktifkan pemutaran ulang dengan latensi ultra-rendah secara cepat di aplikasi seluler. Untuk informasi selengkapnya, pelajari [Playback > LEB (Pemutaran Ulang > LEB)](https://intl.cloud.tencent.com/document/product/1071/41875).

>? SDK MLVB menggunakan CSS, IM, TRTC, dan layanan lainnya untuk komunikasi audiovisual latensi rendah untuk banyak pihak. Peserta dapat berinteraksi satu sama lain melalui koneksi mikrofon sementara peserta yang lain menonton. Untuk informasi selengkapnya, pelajari [Mic Connect (Koneksi Mikrofon)](https://intl.cloud.tencent.com/document/product/1071/42210).

### Demo gratis
TCToolkit adalah solusi audio/video komprehensif sumber terbuka yang dikembangkan oleh Tencent Cloud. Anda dapat menggunakannya untuk mencoba kemampuan LEB dalam memutar streaming langsung dengan latensi milidetik.
<table>
  <tr>
    <th><div align="center">Platform</div></th>
    <th><div align="center">Demo</div></th>
    <th><div align="center">Demonstrasi Push (Android)</div></th>
    <th><div align="center">Demonstrasi Pemutaran Ulang (Android)</div></th>
  </tr>
  <tr>
    <td>Android</td>
    <td style="text-align:center"><img width="150" src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png"> </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200" src="https://main.qcloudimg.com/raw/dca4b24bc363d25c9ea45e60859a2f6d.png"/>
      </div>
    </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200"  src="https://main.qcloudimg.com/raw/6dd7c02dc2381d84225c2f2f286e7358.png"/>
      </div>
    </td>
  </tr>
  <tr>
      <td>iOS</td>
    <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150"></td>
  </tr>
</table>




[](id:web)
## Integrasi ke dalam Halaman Web
### Petunjuk
Anda dapat menggunakan cara berikut untuk mencapai push dan pemutaran ulang langsung di situs web Anda:

- **Live push on web** (Push langsung di web): Komponen push dirancang dan dikemas sesuai dengan standar WebRTC, yang didukung oleh sebagian besar browser. Anda dapat mengaktifkan fitur push langsung cukup dengan mengimpor kode yang kami berikan. Informasi mendetail dapat dilihat di [WebRTC Push (Push WebRTC)](https://intl.cloud.tencent.com/document/product/267/41620).
> ! 
> - Push WebRTC menggunakan codec audio Opus. Jika Anda menggunakan protokol LVB (RTMP, HTTP-FLV, atau HLS) untuk pemutaran ulang, backend CSS akan secara otomatis mengonversi audio ke format AAC untuk memastikan pemutaran ulang berjalan normal, dan konversi otomatis ini akan dikenai biaya transcoding audio. Informasi selengkapnya dapat dilihat di [Live Transcoding > Audio Transcoding](https://intl.cloud.tencent.com/document/product/267/39604) (Transcoding Langsung > Transcoding Audio). Jika hanya LEB yang digunakan, backend CSS tidak akan melakukan transcoding pada audio.
> - Dengan WebRTC, setiap nama domain push dapat digunakan untuk maksimum **100 streaming bersamaan** secara default. Jika Anda ingin melakukan push pada lebih banyak streaming, silakan [kirimkan tiket](https://console.cloud.tencent.com/workorder/category).


### Demo gratis

- **Live push on web** (Push langsung di web): Anda dapat menguji fitur push web di **CSS console** > **[Web Push](https://console.cloud.tencent.com/live/tools/webpush)** (Konsol CSS > Push Web).

- **Live playback on web** (Pemutaran ulang langsung di web): Anda dapat menggunakan [Demo Langsung WebRTC](https://tcplayer.vcube.tencent.com/webrtc-demo/index.html) untuk menguji pemutaran ulang.
>?
>- Push dan pemutaran ulang langsung di web sama-sama menggunakan protokol WebRTC standar. Push web tidak menghasilkan B-frame, dan audio dikodekan dalam format Opus sehingga tidak ada biaya transcoding audio atau penghapusan B-frame.
>- Demo Langsung WebRTC mendukung pemutaran ulang multi-definisi. Anda dapat membuat templat transcoding untuk output HD dan SD di **Feature Configuration** > [**Live Transcoding**](https://console.cloud.tencent.com/live/config/transcode) (Konfigurasi Fitur > Transcoding Langsung) di konsol CSS, memasukkan URL streaming WebRTC yang berisi templat transcoding ke dalam demo, dan menguji pemutaran ulang. Jika Anda tidak perlu menguji transcoding, masukkan URL asli streaming WebRTC.
>- Untuk informasi selengkapnya tentang transcoding langsung dan penagihannya, pelajari [Live Transcoding (Transcoding Langsung)](https://intl.cloud.tencent.com/document/product/267/31071).

[](id:obs)
## Integrasi Push WebRTC via OBS
Push pada protokol WebRTC digunakan terutama untuk LEB (streaming langsung dengan latensi ultra-rendah). Push pada protokol WebRTC akan mendorong audio/video langsung atau file video ke server CSS melalui protokol WebRTC. Berikut adalah penjelasan cara menggunakan OBS untuk mengimplementasikan push WebRTC.

### Catatan
- Anda harus menggunakan versi OBS v26 atau yang lebih tinggi.
- Saat ini, kami hanya menawarkan plugin OBS untuk Windows. Jika Anda ingin menggunakan OBS untuk menerapkan fitur push WebRTC di macOS, pelajari [Integration into Webpage (Integrasi ke dalam Halaman Web)](https://intl.cloud.tencent.com/document/product/267/42131).

[](id:set)
### Mengonfigurasikan plugin OBS
1. **Configure the plugin data** (Konfigurasi data plugin)
Unduh [plugin OBS](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TOBSWebRTC/Release/tencent_webrtc_plugin_20210628.zip), salin file `services.json` dan `package.json` di direktori `data`, lalu gunakan untuk mengganti file terkait di **obs-studio** > **rtmp-service** > **data**. (`obs-studio` diinstal di `C:\Program Files\` secara default.)
![](https://main.qcloudimg.com/raw/967335d17284d931e3a01505d45b884a.png)  
2. **Configure the plugin's dynamic library** (Konfigurasi pustaka dinamis plugin)
Pindahkan file DLL dan PDB di `obs-plugins\64bit` ke **obs-studio** > **obs-plugins** > **64bit**. (`obs-studio` diinstal di `C:\Program Files\` secara default.)
![](https://main.qcloudimg.com/raw/ca9cc7d84071526009624978dc38e2c8.png)   

[](id:push)
### Mengonfigurasikan URL push
[](id:push)
1. **Generate a WebRTC push address** (Buat alamat push WebRTC).
  1. Masuk ke konsol CSS dan buka **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Toolkit CSS > Pembuat Alamat) untuk membuat URL push. Untuk informasi selengkapnya, pelajari [Address Generator (Pembuat Alamat)](https://intl.cloud.tencent.com/document/product/267/31084).
  2. Ubah awalan `rtmp` di URL yang dibuat menjadi `webrtc`. Untuk informasi selengkapnya, pelajari [Splicing Live Streaming URLs (Menyambungkan URL Streaming Langsung)](https://intl.cloud.tencent.com/document/product/267/38393).

    ![](https://qcloudimg.tencent-cloud.cn/raw/e4e8118922b8f4be309e33f740152006.png)    
2. **Configure push in OBS** (Konfigurasi push di OBS)[](id:set_obs)
  1. Buka OBS dan klik **Control** > **Settings** (Kontrol > Pengaturan) di bagian bawah untuk masuk ke halaman pengaturan.
  2. Klik **Stream** (Streaming), pilih `Tencent webrtc` untuk **Service** (Layanan) dan `Default` untuk **Server**, masukkan [URL push WebRTC](#push) yang telah dibuat ke bidang **Stream Key** (Kunci Streaming), lalu tambahkan `&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream` di belakangnya.

    **Contoh kunci streaming:**
```
webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx &stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream 
```
Seperti yang ditunjukkan di bawah ini:
![](https://qcloudimg.tencent-cloud.cn/raw/8035e95d3f62e62dcb3c33db2e5560d6.png)     

[](id:play)
### Pemutaran ulang LEB
Penjelasan seputar cara menggunakan SDK MLVB untuk pemutaran ulang LEB dapat dilihat di [Playback > LEB (Pemutaran Ulang > LEB)](https://intl.cloud.tencent.com/document/product/1071/41875).
