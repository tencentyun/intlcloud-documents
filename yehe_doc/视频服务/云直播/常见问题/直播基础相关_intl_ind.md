<span id="Que1"></span>
### Apa yang dimaksud dengan push, streaming langsung, dan video sesuai permintaan?
- **Push**: proses push video dan audio lokal oleh host ke server Tencent Video Cloud. Push juga disebut sebagai "publikasi RTMP" di beberapa skenario.
- **Streaming langsung**: selama streaming langsung, streaming video dibuat secara real-time. Streaming langsung hanya berfungsi jika seseorang melakukan push. URL streaming langsung akan menjadi tidak valid begitu host menghentikan push. Karena streaming langsung diputar ulang secara real-time, pemirsa tidak dapat melihat bilah kemajuan selama streaming langsung.   
**Video sesuai permintaan (video on demand/VOD)**: VOD memungkinkan Anda memutar file di cloud. File dapat diputar setiap saat, kecuali jika file telah dihapus oleh penyedia (misalnya Tencent Video). Karena video sudah disimpan di server, pemirsa dapat melihat bilah kemajuan selama pemutaran ulang.

<span id="Que2"></span>
### Apa saja persyaratan untuk nama domain pemutaran ulang di CSS?	
Nama domain dapat berisi maksimum 45 karakter dan tidak boleh berisi huruf kapital. Informasi selengkapnya dapat dilihat di [Adding Domain Name (Menambahkan Nama Domain)](https://intl.cloud.tencent.com/document/product/267/35970).

<span id="Que3"></span>
### Apakah saya dapat menggunakan nama domain yang sama untuk pemutaran ulang dan push? Apakah saya dapat menggunakan nama domain tingkat kedua?
Anda harus menggunakan nama domain yang berbeda untuk pemutaran ulang dan push, tetapi Anda dapat menggunakan domain tingkat kedua yang sama untuk menunjukkan bahwa streaming tersebut sama.
Misalnya, Anda dapat menggunakan `123.abc.com` untuk push, dan `456.abc.com` untuk pemutaran ulang.

<span id="Que4"></span>

### Protokol push apa saja yang didukung?
RTMP mungkin bukan protokol yang umum digunakan untuk streaming langsung, tetapi ini adalah protokol yang paling umum digunakan untuk push streaming (push data dari host ke server). Sebagian besar layanan cloud video di Tiongkok Daratan menggunakan RTMP sebagai protokol push utama. SDK MLVB disebut juga dengan SDK RTMP karena modul fitur pertamanya adalah publikasi streaming.

<span id="Que5"></span>

### Protokol pemutaran ulang apa saja yang didukung?
Protokol streaming langsung yang umum digunakan meliputi RTMP, HTTP-FLV, HLS, dan WebRTC.
- **RTMP** dapat digunakan untuk push langsung dan pemutaran ulang langsung. Protokol ini bekerja dengan membagi potongan video dan audio berdurasi panjang menjadi fragmen pendek, lalu mentransfernya sebagai paket data berukuran kecil melalui internet. RTMP mendukung enkripsi sehingga menjamin privasi. Namun, proses pembagian dan penyambungan yang rumit menambah ketidakpastian pada stabilitas transmisi data dalam skenario konkurensi tinggi. 
- **HTTP-FLV** dikembangkan oleh Adobe Systems dan merupakan format video yang cukup sederhana. Protokol ini bekerja dengan menambahkan header ke potongan data video dan audio berukuran besar. Formatnya yang sederhana membuat protokol ini memiliki kontrol penundaan dan kinerja konkurensi tinggi yang sangat baik. Satu-satunya kekurangan HTTP-FLV adalah dukungan yang buruk di browser seluler. Namun, protokol ini merupakan opsi yang tepat untuk aplikasi seluler.  
- **HLS** dirilis oleh Apple. Protokol ini membagi streaming video menjadi segmen berdurasi 5‒10 detik dan mengelolanya menggunakan daftar putar M3U8. Protokol ini memastikan bahwa pemutaran ulang berjalan dengan lancar saat klien mengunduh potongan data berdurasi 5‒10 detik. Namun, HLS memiliki latensi yang tinggi, yaitu sekitar 10‒30 detik. Tidak seperti HTTP-FLV, HLS dapat digunakan dengan baik di browser iPhone dan sebagian besar browser Android sehingga sering kali digunakan untuk berbagi URL di QQ dan WeChat Moments.
- **WebRTC** adalah singkatan dari Web Real-Time Communication (Komunikasi Web Real-Time). WebRTC adalah API yang memungkinkan panggilan audio/video real-time di browser web. Spesifikasi WebRTC didukung oleh Google, Mozilla, dan Opera, dan diterbitkan oleh World Wide Web Consortium (W3C) pada 1 Juni 2011. WebRTC digunakan oleh LEB, yang merupakan versi LVB dengan latensi ultra- rendah dan menawarkan streaming dengan latensi milidetik. LEB cocok untuk skenario dengan persyaratan yang tinggi akan latensi, misalnya kegiatan pembelajaran online, streaming pertandingan olahraga, dan kuis online.

|Protokol|Kekuatan|Kelemahan|Latensi Pemutaran Ulang|
| --------- | ---------------------- | -------------------- | --------- |
| HTTP-FLV | Siap pakai, cocok untuk skenario dengan konkurensi tinggi | Memerlukan integrasi SDK. | 2‒3 detik |
|RTMP|Latensi relatif rendah|Kinerja buruk untuk skenario dengan konkurensi tinggi |1‒3 detik |
| HLS (M3U8) | Didukung dengan baik di browser seluler | Latensi tinggi |10‒30 detik|
|WebRTC |Latensi rendah |Memerlukan integrasi SDK. |< 1 detik |

[](id:Que6)
### Apa format yang digunakan URL pemutaran ulang?
URL pemutaran ulang Tencent Cloud terdiri dari awalan protokol pemutaran ulang, nama domain (`domain`), nama aplikasi (`AppName`), nama streaming (`StreamName`), akhiran protokol pemutaran ulang, kunci autentikasi, dan parameter kustom lainnya. Berikut adalah contohnya:
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```

- **Awalan**
RTMP: **rtmp://**
HTTP-FLV: **http://** atau **https://**
HLS: **http://** atau **https://**
WebRTC: **webrtc://**
- **Nama aplikasi (`AppName`)**
Nama aplikasi menentukan jalur penyimpanan file streaming langsung. Secara default, nama aplikasi adalah **live**.
- <span id="streamname">**nama streaming (`StreamName`)**</span>
Nama streaming (`StreamName`) mengidentifikasi streaming langsung secara unik.
- **Kunci autentikasi dan parameter kustom lainnya**
Kunci autentikasi: **txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)**.


<span id="Que7"></span>
### Apa saja metode yang umum digunakan untuk melakukan push?
- **Kamera di perangkat Android/iOS**: gunakan perangkat lunak pihak ketiga atau [SDK MLVB](https://intl.cloud.tencent.com/product/mlvb) untuk merekam video kamera dan melakukan push pada streaming video ke URL push.
- **Kamera atau perekam layar di PC**: gunakan perangkat lunak pihak ketiga untuk merekam video kamera atau merekam layar, lalu lakukan push pada data ke URL push. Perangkat lunak pihak ketiga tersebut meliputi [OBS (direkomendasikan)](https://intl.cloud.tencent.com/document/product/267/31569), XSplit, FMLE, dll.
- **Perangkat perekam video**: hubungkan kamera perekam HD dengan output HDMI atau SDI ke encoder, lalu lakukan push pada streaming RTMP ke aplikasi streaming langsung. Anda perlu mengatur alamat publikasi RTMP encoder ke URL push Anda.
Jika menggunakan webcam yang mendukung RTMP, Anda juga dapat mengatur alamat publikasi RTMP webcam ke URL push Anda.
- **Konversi file video ke streaming video**: baca file video, lalu lakukan push pada file sebagai streaming RTMP ke URL push RTMP. Cara ini dapat dilakukan menggunakan perintah `FFmpeg`, yang dapat digunakan di Windows, Linux, dan macOS.

<span id="Que8"></span>
### Apa perbedaan antara gangguan streaming dan penonaktifan streaming?
- **Gangguan streaming**: jika streaming terganggu, push akan berhenti dan pemirsa tidak akan dapat menonton streaming. Namun, host dapat memulai push kembali untuk melanjutkan streaming langsung.
- **Penonaktifan streaming**: jika streaming langsung dinonaktifkan, push akan berhenti dan pemirsa tidak akan dapat menonton streaming. Host tidak dapat memulai push kembali. Anda dapat menonaktifkan streaming di halaman manajemen streaming melalui konsol CSS. Streaming yang dinonaktifkan dapat ditemukan di daftar streaming yang dinonaktifkan. Klik **Enable** (Aktifkan) untuk mengaktifkan streaming yang dinonaktifkan.

[](id:Que10)
### Apakah saya dapat mengaktifkan obrolan teks untuk streaming langsung?
Ya. Anda dapat menggunakan komponen Instant Messaging (IM/Pesan Instan) untuk menampilkan obrolan teks selama streaming langsung. Selain itu, IM menyediakan komentar di layar, reaksi suka, hadiah, pemberitahuan berulang, dan berbagai fitur interaktif lainnya. Anda juga dapat menggunakan fitur manajemen ruang, misalnya untuk melakukan co-anchoring serta mengelola identitas pengguna dan izin untuk menonaktifkan suara anggota.

[](id:Que13)

### Apakah CSS adalah sebuah perangkat lunak?
 Bukan. CSS menyediakan berbagai API yang dapat Anda gunakan untuk mengembangkan aplikasi streaming langsung. 

[](id:Que16)
### Bagaimana cara mengetahui jumlah pemirsa streaming langsung?
Anda dapat memanggil API v3.0 CSS [DescribeStreamPlayInfoList](https://intl.cloud.tencent.com/document/product/267/37297) untuk mengetahui jumlah pemirsa online.
