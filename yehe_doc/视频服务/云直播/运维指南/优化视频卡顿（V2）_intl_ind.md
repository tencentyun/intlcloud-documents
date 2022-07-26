![](https://main.qcloudimg.com/raw/db29f65a777b1e445b5c9c7e0e694457.png)
Ada tiga penyebab utama terjadinya kemacetan pada pemutaran ulang.

- **Penyebab 1: frame rate upstream rendah**
Frame rate upstream yang rendah dapat disebabkan oleh kinerja buruk telepon seluler host atau aplikasi yang memerlukan CPU besar di latar belakang. Umumnya, untuk memastikan pemutaran ulang berjalan dengan lancar, frame rate upstream harus sebesar 15 FPS atau lebih tinggi. Frame rate di bawah 10 FPS dianggap **terlalu rendah** dan akan menyebabkan **semua pemirsa** mengalami kemacetan. Namun, jika gambar video host mengalami sedikit perubahan, misalnya saat host menampilkan gambar statis atau PowerPoint, frame rate yang rendah tidak akan menyebabkan kemacetan.
- **Penyebab 2: kemacetan upstream**
Telepon seluler host terus melakukan push data audio dan video selama streaming langsung. Jika bandwidth upstream ponsel terlalu rendah, data yang mengantre push akan terakumulasi dan menyebabkan kemacetan pada transfer data sehingga menimbulkan kemacetan pemutaran ulang untuk **semua pemirsa**.

 Meskipun **ISP di Tiongkok Daratan** menawarkan paket broadband dengan kecepatan bandwidth downstream 10 Mbps, 20 Mbps, atau bahkan 100 Mbps atau 200 Mbps, bandwidth upstream akan tetap kecil. Di banyak kota kecil, bandwidth upstream maksimum yang ditawarkan hanya 512 Kbps, yang berarti bahwa data maksimum yang dapat diunggah per detik hanya sebesar 64 KB.
 **Wi-Fi** menggunakan strategi CSMA/CA (carrier-sense multiple access and collision avoidance) yang dijelaskan dalam IEEE 802.11. Sederhananya, hotspot Wi-Fi hanya dapat berkomunikasi dengan satu ponsel dalam satu waktu, dan ponsel lain harus membuat kueri tentang memungkinkan atau tidaknya komunikasi sebelum melakukan koneksi ke suatu hotspot. Oleh karena itu, makin banyak orang yang menggunakan suatu hotspot Wi-Fi, koneksinya akan makin lambat. Sinyal Wi-Fi juga melemah secara signifikan ketika melewati dinding. Di antara kebanyakan keluarga Tionghoa, hanya sedikit yang mempertimbangkan hal ini saat merancang dan mendekorasi rumah. Selain itu, jumlah dinding di antara lokasi host dan router mungkin tidak terlalu diperhatikan pada waktu streaming di rumah.

- **Penyebab 3: koneksi downstream buruk**
Koneksi downstream buruk berarti kecepatan pengunduhan lambat atau jaringan tidak stabil untuk pemirsa. Bitrate 2 Mbps dalam streaming langsung berarti data sebesar 2 Mb perlu diunduh setiap detik. Pemirsa akan mengalami kemacetan jika bandwidth jaringan rendah, tetapi pemirsa dengan bandwidth yang cukup tidak akan mengalaminya.

## Memeriksa Metrik Kinerja SDK
SDK MLVB memiliki mekanisme umpan balik yang melaporkan berbagai metrik kinerja setiap 2 detik. Jika menggunakan SDK MLVB untuk push, Anda dapat mendaftarkan pendengar [V2TXLivePusherObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html) dan mendapatkan statistik di panggilan balik `onStatisticsUpdate`. Tabel di bawah menampilkan berbagai metrik yang terdapat dalam `V2TXLivePusherStatistics` dan artinya.

| Metrik                | Deskripsi                    |
| :------------------------  |  :------------------------ |
| appCpu | Penggunaan CPU aplikasi (%) |
| systemCpu | Penggunaan CPU sistem (%) |
| width | Lebar video |
| height | Tinggi video |
| fps | Frame rate (FPS) |
| audioBitrate | Bitrate audio dalam Kbps |
| videoBitrate | Bitrate video dalam Kbps |

## Mengatasi Frame Rate Rendah
### 1. Cara mencari tahu terlalu rendah atau tidaknya frame rate
Bidang **V2TXLivePusherStatistics.fps** di panggilan balik [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#af01be7a0bf0ed619cce63f49959ea8be) `V2TXLivePusherObserver` menunjukkan frame rate untuk push. Umumnya, frame rate harus 15 FPS atau lebih tinggi untuk memastikan pemutaran ulang berjalan secara lancar. Pemirsa biasanya mengalami kemacetan yang signifikan jika frame rate push kurang dari 10 FPS.

### 2. Cara mengatasi masalah
- **2.1 Memantau `appCpu` dan `systemCpu`**
Anda dapat mengetahui **penggunaan CPU aplikasi dan sistem** dari bidang **V2TXLivePusherStatistics.appCpu** dan **V2TXLivePusherStatistics.systemCpu** di panggilan balik [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#af01be7a0bf0ed619cce63f49959ea8be) `V2TXLivePusherObserver`. Jika penggunaan CPU sistem melebihi 80%, perekaman dan pengodean video dapat terpengaruh; jika penggunaan CPU sistem mencapai 100%, baik kelancaran push maupun pemutaran ulang bagi pemirsa akan sulit dipastikan.

- **2.2 Mengidentifikasi pengguna CPU**
SDK MLVB bukan satu-satunya pengguna CPU di aplikasi streaming langsung. Memberikan komentar di layar, mengirimkan tanda hati, dan mengirimkan pesan teks juga termasuk dalam aktivitas yang menggunakan CPU. Untuk memantau penggunaan CPU SDK MLVB saja, Anda dapat menggunakan [demo](https://intl.cloud.tencent.com/document/product/1071/38147).

- **2.3 Memilih resolusi yang tepat**
Resolusi tinggi belum tentu menghasilkan video berkualitas tinggi. Pada dasarnya, resolusi tinggi akan menghasilkan video berkualitas lebih baik hanya jika bitrate juga tinggi. Bitrate rendah dan resolusi tinggi biasanya menghasilkan video berkualitas lebih rendah daripada kualitas video yang dihasilkan bitrate tinggi dan resolusi rendah. Selain itu, perbedaan jelas antara resolusi 1280 × 720 px dan 960 × 540 px dapat dirasakan pemirsa ketika video ditonton dengan layar penuh di PC. Namun, perbedaan resolusi tidak terlihat ketika video ditonton di telepon seluler, yang rata-rata memiliki layar dengan ukuran sekitar 5 inci saja. Resolusi tinggi meningkatkan penggunaan CPU oleh SDK secara signifikan. Oleh karena itu, Anda sebaiknya mengatur kualitas video ke **HD** menggunakan API [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a2695806cb6c74ccce4b378d306ef0a02) di `V2TXLivePusher` SDK MLVB. Video berkualitas tinggi yang diinginkan mungkin tidak akan didapatkan jika Anda mengatur resolusi terlalu tinggi.

## Mengatasi Kemacetan Upstream
Statistik menunjukkan bahwa kemacetan upstream di sisi host menjadi penyebab lebih dari 80% kemacetan pemutaran ulang pada streaming langsung.

###1. Menginformasikan kondisi jaringan yang buruk kepada host
Dalam skenario yang mementingkan kualitas video, sebaiknya informasikan kondisi jaringan yang buruk kepada host melalui pemberitahuan UI. Misalnya, Anda dapat mengirimkan pemberitahuan berikut kepada host: **Bad network conditions. Please move closer to your router or make sure that your Wi-Fi signal does not have to pass through walls.** (Kondisi jaringan buruk. Harap mendekat ke router atau pastikan sinyal Wi-Fi tidak terhalang dinding.)
Informasi selengkapnya tentang cara melakukannya dapat dilihat di **Mobile Live Video Broadcasting > Basic Features > Camera Push > Event Handling** (Mobile Live Video Broadcasting > Fitur Dasar > Push Kamera > Penanganan Peristiwa). Sebaiknya ingatkan host untuk memeriksa kondisi jaringan jika aplikasi Anda menerima peristiwa [V2TXLIVE_WARNING_NETWORK_BUSY](https://intl.cloud.tencent.com/zh/document/product/1071) beberapa kali dalam jangka waktu singkat. Host sering kali baru menyadari adanya kemacetan upstream setelah mendapatkan pengingat dari pemirsa atau pesan aplikasi.

### 2. Menggunakan pengaturan pengodean yang direkomendasikan
Kami merekomendasikan pengaturan pengodean berikut (informasi selengkapnya dapat dilihat di [Setting Video Quality (Mengatur Kualitas Video)](https://intl.cloud.tencent.com/zh/document/product/1071)). Anda dapat menggunakan API [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a2695806cb6c74ccce4b378d306ef0a02) di `V2TXLivePusher` untuk mengatur parameter.

|Skenario |`resolution` |`resolutionMode` |
| :------------------------  |  :------------------------ | :------------------------ |
|Showroom langsung|<li/>V2TXLiveVideoResolution960x540<li/>V2TXLiveVideoResolution1280x720 |Lanskap atau potret |
|Streaming game langsung |V2TXLiveVideoResolution1280x720 |Lanskap atau potret |
|Koneksi mikrofon (gambar utama) |V2TXLiveVideoResolution640x360 |Lanskap atau potret |
|Koneksi mikrofon (gambar kecil) |V2TXLiveVideoResolution480x360 |Lanskap atau potret |
|Streaming langsung blue-ray |V2TXLiveVideoResolution1920x1080 |Lanskap atau potret |

## Mengatasi Masalah di Bagian Pemutar
![](https://main.qcloudimg.com/raw/c2c88d9bbf8f72c77eb778d7f2d5e993.png)

### 1. Kemacetan dan latensi
Seperti yang ditunjukkan oleh gambar di atas, fluktuasi jaringan downstream dan kekurangan bandwidth downstream dapat mengakibatkan **unfed period** (yaitu periode saat aplikasi tidak dapat memperoleh data audio/video untuk pemutaran ulang) dalam proses pemutaran ulang. Untuk mencegah kemacetan pada pemutaran ulang, aplikasi perlu melakukan cache data video hingga cukup untuk digunakan saat terjadi unfed period. Namun, terlalu banyak cache data dapat menimbulkan masalah baru: **latensi tinggi**, yang tidak diinginkan untuk skenario interaktif. Latensi dapat **berakumulasi** seiring waktu jika tidak diatasi, artinya latensi akan bertambah seiring berlanjutnya pemutaran ulang. Kemampuan untuk mengatasi latensi adalah indikator kinerja penting untuk pemutar. **Latensi dan kelancaran pemutaran ulang dapat diibaratkan seperti dua ujung timbangan**. Untuk memastikan latensi rendah, Anda mungkin perlu menurunkan stabilitas jaringan, yang menyebabkan kemacetan pada pemutaran ulang, dan untuk memastikan pemutaran ulang berjalan dengan lancar, Anda harus mengatasi latensi yang tinggi. Contoh umum untuk masalah kedua adalah adanya penundaan 20‒30 detik pada pemutaran ulang streaming HLS (M3U8) untuk memastikan pemutaran ulang berjalan dengan lancar.

### 2. Cara mengatasi masalah
Agar Anda dapat memberikan layanan pemutaran ulang yang unggul tanpa perlu mempelajari kontrol QoS, kami telah mengembangkan teknologi kontrol latensi otomatis, yang dioptimalkan dari versi ke versi, dan meluncurkan tiga [skema kontrol latensi](https://intl.cloud.tencent.com/document/product/1071). Anda dapat menggunakan API [setCacheParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a8a4f8f8e220a6e4aa2a04ca3e866efcb) di `V2TXLivePlayer` untuk memilih salah satu skema.

-  **Auto mode** (Mode otomatis): gunakan mode ini jika Anda tidak yakin tentang skenario yang akan Anda hadapi.
>? Dalam mode ini, pemutar akan menyesuaikan latensi secara otomatis berdasarkan kondisi jaringan untuk meminimalkan latensi antara host dan pemirsa serta memastikan kualitas interaksi host-pemirsa sekaligus memberikan layanan pemutaran ulang yang lancar. Secara default, pemutar akan menyesuaikan latensi dengan rentang antara 1‒5 detik, yang dapat Anda sesuaikan menggunakan API `setCacheParams`.

-  **Speedy mode** (Mode cepat): cocok untuk **showroom langsung** dan skenario interaktif lain yang memerlukan latensi rendah.
>? Anda dapat beralih ke mode ini dengan **mengatur `minTime` dan `maxTime` ke 1 detik**. Perbedaan antara mode otomatis dan mode cepat hanya terletak pada nilai `maxTime`, yang umumnya lebih rendah dalam mode cepat. Fleksibilitas ini dapat terwujud berkat teknologi kontrol latensi otomatis SDK, yang dapat menyesuaikan latensi secara otomatis tanpa menyebabkan kemacetan. `maxTime` berkaitan dengan kecepatan penyesuaian. Makin tinggi nilai `maxTime`, makin konservatif penyesuaiannya, dan makin kecil kemungkinan terjadinya kemacetan.

- **Smooth mode** (Mode lancar): cocok untuk **streaming game langsung** dan skenario bitrate tinggi dan definisi tinggi lain.
>?
>- Dalam mode ini, pemutar akan menerapkan strategi yang mirip dengan kebijakan cache Adobe Flash Player. Ketika kemacetan terjadi, pemutar akan beralih ke mode pemuatan, dan ketika data yang di-cache sudah cukup; pemutar akan kembali ke mode pemutaran, hingga koneksi jaringan berfluktuasi lagi. Secara default, cache akan dilakukan pada data video selama 5 detik, tetapi Anda dapat mengubahnya menggunakan API `setCacheParams`.
>- Mode yang tampak sederhana ini mengurangi kemacetan pada pemutaran ulang dengan melakukan peningkatan yang cukup pada latensi sehingga menjadi opsi yang lebih andal untuk skenario yang tidak memerlukan latensi rendah.
