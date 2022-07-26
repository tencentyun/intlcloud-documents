![](https://main.qcloudimg.com/raw/c38bbed25d2953aea75f76764522e25d.png)
Ada tiga penyebab utama terjadinya kemacetan pada pemutaran ulang.

- **Penyebab 1: frame rate upstream rendah**
Frame rate upstream yang rendah dapat disebabkan oleh kinerja buruk telepon seluler host atau aplikasi yang memerlukan CPU besar di backend. Umumnya, untuk memastikan pemutaran ulang berjalan dengan lancar, frame rate upstream harus sebesar 15 FPS atau lebih tinggi. Frame rate kurang dari 10 FPS dianggap **terlalu rendah** sehingga menyebabkan kemacetan pemutaran ulang untuk **semua pemirsa**. Jika layar streaming langsung menampilkan gambar statis, PowerPoint, atau gambar lain dengan sedikit perubahan, frame rate yang rendah tidak akan menyebabkan kemacetan.
- **Penyebab 2: kemacetan upstream**
Telepon seluler host terus melakukan push data audio dan video selama streaming langsung. Jika bandwidth upstream ponsel terlalu rendah, data yang mengantre push akan terakumulasi dan menyebabkan kemacetan pada transfer data sehingga terjadi kemacetan pemutaran ulang untuk **semua pemirsa**.

 Meskipun **ISP di Tiongkok Daratan** menawarkan paket broadband dengan kecepatan bandwidth downstream 10 Mbps, 20 Mbps, atau bahkan 100 Mbps atau 200 Mbps, bandwidth upstream akan tetap lambat. Di banyak kota kecil, bandwidth upstream maksimum yang ditawarkan hanya 512 Kbps, yang artinya data maksimum yang dapat diunggah per detik hanya sebesar 64 KB.
 **Wi-Fi** menggunakan strategi CSMA/CA (carrier-sense multiple access and collision avoidance), sebagaimana dijelaskan dalam IEEE 802.11. Sederhananya, hotspot Wi-Fi hanya dapat berkomunikasi dengan satu ponsel dalam satu waktu, dan ponsel lain harus memverifikasi atau membuat kueri tentang memungkinkan atau tidaknya komunikasi sebelum melakukan koneksi ke suatu hotspot. Oleh karena itu, makin banyak orang yang menggunakan suatu hotspot Wi-Fi, koneksinya akan makin lambat. Kekuatan sinyal Wi-Fi juga menurun secara drastis ketika melewati dinding atau penghalang. Sebagian besar keluarga jarang memperhatikan posisi router Wi-Fi dan kekuatan sinyal Wi-Fi antar-ruangan saat merancang dan mendekorasi rumah. Selain itu, ketika push dilakukan pada streaming video, jumlah dinding di antara lokasi host dan router mungkin tidak terlalu diperhatikan.
- **Penyebab 3: koneksi downstream buruk**
Koneksi downstream buruk berarti kecepatan pengunduhan lambat atau jaringan tidak stabil untuk audiens. Bitrate 2 Mbps dalam streaming langsung berarti data sebesar 2 Mb perlu diunduh setiap detik. Audiens akan mengalami kemacetan jika bandwidth jaringan rendah, tetapi pengguna dengan bandwidth yang cukup tidak akan mengalaminya.

## Memeriksa Metrik Kinerja SDK
SDK MLVB RT-Cube memiliki mekanisme umpan balik status yang melaporkan metrik status SDK setiap 1‒2 detik. Jika menggunakan SDK MLVB untuk menerbitkan streaming, Anda dapat mendaftar TXLivePushListener untuk mendapatkan metrik. Berikut adalah metrik yang dilaporkan:
![](https://main.qcloudimg.com/raw/533391ae5c188ed87b748f78d8168591.png)

| Metrik                | Deskripsi                    |
| :------------------------  |  :------------------------ |
| NET_STATUS_CPU_USAGE |  Penggunaan CPU oleh proses saat ini dan perangkat |
| NET_STATUS_VIDEO_FPS | Frame rate video saat ini, yaitu jumlah frame yang dihasilkan oleh encoder video per detik |
| NET_STATUS_NET_SPEED | Kecepatan transfer data saat ini dalam Kbps |
| NET_STATUS_VIDEO_BITRATE | Bitrate output encoder video, yaitu jumlah data video yang dihasilkan oleh encoder per detik, dalam Kbps |
| NET_STATUS_AUDIO_BITRATE | Bitrate output encoder audio, yaitu jumlah data audio yang dihasilkan oleh encoder per detik, dalam Kbps |
| NET_STATUS_CACHE_SIZE | Akumulasi ukuran data audio/video. Nilai ≥ 10 menunjukkan bahwa bandwidth upstream tidak mencukupi untuk menggunakan data audio/video yang dihasilkan.|
| NET_STATUS_CODEC_DROP_CNT | Jumlah penurunan paket secara global. Begitu akumulasi data melampaui ambang batas tertentu, SDK akan mulai menurunkan paket untuk mencegah akumulasi data terus bertambah. Makin besar penurunan paket yang dilakukan SDK, makin parah masalah jaringan.|
| NET_STATUS_SERVER_IP | Alamat IP server penerbit tersambung, yang biasanya memiliki lonjakan paling sedikit dari klien. |

## Mengatasi Frame Rate Rendah
### 1. Cara mencari tahu terlalu rendah atau tidaknya frame rate
Frame rate upstream ditunjukkan oleh parameter status **VIDEO_FPS** yang ditampilkan oleh SDK MLVB melalui TXLivePushListener. Umumnya, frame rate harus 15 FPS atau lebih tinggi untuk memastikan pemutaran ulang berjalan dengan lancar. Pemirsa akan mengalami kemacetan yang signifikan jika frame rate penerbitan kurang dari 10 FPS.

### 2. Cara mengatasi masalah
- **2.1 Melacak `CPU_USAGE`**
Anda dapat mengetahui **penggunaan CPU SDK penerbit streaming dan seluruh sistem** dari parameter status `CPU_USAGE` yang ditampilkan SDK MLVB melalui TXLivePushListener. Penggunaan CPU sistem lebih dari 80% akan memengaruhi perekaman dan pengodean data video; jika penggunaan CPU mencapai 100%, penerbitan oleh host akan macet sehingga pemirsa tidak dapat menonton dengan lancar.

- **2.2 Mengidentifikasi pengguna CPU**
SDK penerbit bukan satu-satunya pengguna CPU di aplikasi streaming langsung. Memberikan komentar di layar, mengirimkan tanda hati, dan mengirimkan pesan teks juga termasuk dalam aktivitas yang menggunakan CPU. Jika ingin mengevaluasi penggunaan CPU SDK push saja, Anda dapat menggunakan [Basic Edition Demo (Demo Edisi Dasar)](https://intl.cloud.tencent.com/document/product/1071/38147).

- **2.3 Memilih resolusi yang tepat**
Resolusi tinggi belum tentu menghasilkan video berkualitas tinggi. Pada dasarnya, resolusi tinggi akan menghasilkan video berkualitas lebih baik hanya jika bitrate juga tinggi. Bitrate rendah dan resolusi tinggi biasanya menghasilkan video berkualitas lebih rendah daripada kualitas video yang dihasilkan bitrate tinggi dan resolusi rendah. Selain itu, perbedaan jelas antara resolusi 1280 × 720 dan 960 × 540 dapat dirasakan pemirsa ketika video ditonton dengan layar penuh di PC. Namun, perbedaan resolusi tidak terlihat ketika video ditonton di telepon seluler, yang rata-rata memiliki layar dengan ukuran sekitar 5 inci saja. Resolusi tinggi meningkatkan penggunaan CPU oleh SDK secara signifikan. Oleh karena itu, kami merekomendasikan agar Anda menggunakan `setVideoQuality` di `TXLivePusher` SDK MLVB untuk mengatur kualitas video ke **HD**. Anda mungkin tidak akan mendapatkan video berkualitas tinggi yang diinginkan jika pengaturan resolusi terlalu tinggi.

- **2.4 Menggunakan perangkat keras untuk akselerasi jika diperlukan**
Sebagian besar ponsel pintar menggunakan encoder perangkat keras untuk mengurangi penggunaan CPU dalam pengodean video. Jika penggunaan CPU aplikasi terlalu tinggi, Anda dapat mengaktifkan pengodean perangkat keras. Jika `setVideoQuality` di `TXLivePusher` diatur ke **HD**, encoder perangkat lunak akan digunakan secara default (pengodean perangkat keras tidak berfungsi secara optimal di beberapa perangkat Android dan menghasilkan video yang buram). Anda dapat menggunakan `enableHWAcceleration` di `TXLivePushConfig` untuk mengaktifkan pengodean perangkat keras.

## Mengatasi Kemacetan Upstream
Statistik menunjukkan bahwa kemacetan upstream pada host menjadi penyebab lebih dari 80% kemacetan pemutaran ulang pada streaming langsung.

### 1. Cara mengetahui terjadi atau tidaknya kemacetan upstream
- **1.1: Hubungan antara `BITRATE` dan `NET_SPEED`**
 `BITRATE` (`VIDEO_BITRATE` dan `AUDIO_BITRATE`) adalah jumlah data audio/video yang dihasilkan oleh encoder per detik untuk diterbitkan, sedangkan `NET_SPEED` adalah jumlah data aktual yang diterbitkan per detik. Jika secara umum `BITRATE` == `NET_SPEED`, penerbitan akan memiliki kualitas baik. Namun, jika `BITRATE` >= `NET_SPEED` dalam jangka waktu lama, kualitas penerbitan tidak akan memuaskan.
  
- **1.2: `CACHE_SIZE` dan `DROP_CNT`**
Jika `BITRATE` >= `NET_SPEED`, data audio/video yang dihasilkan oleh encoder akan terakumulasi di ponsel host. `CACHE_SIZE` menunjukkan keparahan akumulasi data. Begitu akumulasi data melampaui ambang batas peringatan, SDK akan mulai menurunkan data sehingga `DROP_CNT` meningkat. Gambar berikut memperlihatkan contoh umum kemacetan upstream. Seperti yang dapat Anda lihat, `CACHE_SIZE` tetap berada di atas **ambang batas peringatan** (garis merah) sepanjang proses, yang menunjukkan bahwa jaringan upstream tidak dapat memenuhi permintaan transfer data sehingga menyebabkan kemacetan upstream yang parah.
![](https://main.qcloudimg.com/raw/c894db6a9745543a349683745c4ba491.png)


 >? Anda dapat melihat gambar di atas di **[CSS console](https://console.cloud.tencent.com/live/livestat)** > **Operation Analysis** (Konsol CSS > Analisis Operasi).

### 2. Cara mengatasi masalah
- **2.1 Memberi tahu host tentang kondisi jaringan yang buruk**
Dalam skenario yang mementingkan kualitas video, sebaiknya informasikan kondisi jaringan yang buruk kepada host melalui pemberitahuan UI. Misalnya, Anda dapat mengirimkan: **Bad network conditions. You’re advised to move closer to your router and not to make Wi-Fi signal pass through walls.** (Kondisi jaringan buruk. Sebaiknya Anda mendekat ke router dan mengatur agar sinyal Wi-Fi tidak terhalang dinding.)
Informasi selengkapnya tentang cara melakukannya dapat dilihat di **Mobile Live Video Broadcasting > Basic Features > Camera Push > Event Handling** (Mobile Live Video Broadcasting > Fitur Dasar > Push Kamera > Penanganan Peristiwa). Sebaiknya ingatkan host untuk memeriksa kondisi jaringan jika aplikasi Anda menerima peristiwa [**PUSH_WARNING_NET_BUSY**](https://intl.cloud.tencent.com/document/product/1071/41678) beberapa kali dalam jangka waktu singkat. Host sering kali baru menyadari adanya kemacetan upstream setelah mendapatkan pengingat dari pemirsa atau pesan aplikasi.

- **2.2 Mengatur nilai yang tepat untuk parameter pengodean**
Anda dapat mengatur kualitas video menggunakan API `setVideoQuality` di `TXLivePusher`. Kami merekomendasikan pengaturan pengodean berikut ini (untuk showroom langsung). Informasi selengkapnya tentang pemastian kualitas video dapat dilihat di [Video Quality (Kualitas Video)](https://intl.cloud.tencent.com/document/product/1071/41932).
<table>
<tr><th width="15%">Kualitas Video</th>
<th width="15%">Resolusi</th>
<th width="5%">FPS</th>
<th width="20%">Bitrate</th>
<th width="45%">Kasus Penggunaan</th>
</tr><tr>
<td><b>SD</td>
<td>360 × 640</td>
<td>15</td>
<td>400‒800 Kbps</td>
<td>Gunakan pengaturan ini untuk menghemat biaya bandwidth. Gambar mungkin kurang jelas, tetapi biaya bandwidth akan berkurang 60% dibandingkan dengan gambar definisi tinggi.</td>
</tr><tr>
<td><b>HD (direkomendasikan)</td>
<td>540 × 960</td>
<td>15</td>
<td>1200 Kbps</td>
<td>Gunakan pengaturan ini untuk meningkatkan kualitas video. Pengaturan ini memastikan gambar video jelas di sebagian besar telepon seluler yang umum digunakan.</td>
</tr><tr>
<td><b>FHD</td>
<td>720 × 1280</td>
<td>15</td>
<td>1800 Kbps</td>
<td>Gunakan pengaturan ini dengan hati-hati. Pengaturan ini direkomendasikan hanya jika pemirsa menonton streaming langsung di layar berukuran besar dan host memiliki koneksi jaringan yang sangat baik. Pengaturan ini tidak direkomendasikan untuk pemutaran ulang di layar berukuran kecil.<td>
</tr></table>


## Mengatasi Masalah Pemutar
![](https://main.qcloudimg.com/raw/1f221c3ecba79a706014154531a02bbd.png)

### 1. Kemacetan dan lag
Seperti yang ditunjukkan oleh gambar di atas, fluktuasi jaringan downstream dan kekurangan bandwidth downstream dapat mengakibatkan **unfed period** (yaitu periode saat aplikasi tidak dapat memperoleh data audio/video untuk pemutaran ulang) dalam proses pemutaran ulang. Untuk mencegah kemacetan pada pemutaran ulang, aplikasi perlu melakukan cache data video hingga cukup untuk digunakan saat terjadi unfed period. Namun, terlalu banyak cache data dapat menimbulkan masalah baru: **latensi tinggi**, yang tidak diinginkan untuk skenario interaktif. Latensi dapat **berakumulasi** seiring waktu jika tidak diatasi, artinya latensi akan bertambah seiring berlanjutnya pemutaran ulang. Kemampuan untuk mengatasi latensi adalah indikator kinerja penting untuk pemutar. **Latensi dan kelancaran pemutaran ulang dapat diibaratkan seperti dua ujung timbangan**. Untuk memastikan latensi rendah, Anda mungkin perlu menurunkan stabilitas jaringan, yang menyebabkan kemacetan pada pemutaran ulang, dan untuk memastikan pemutaran ulang berjalan dengan lancar, Anda harus mengatasi latensi yang tinggi. Contoh umum untuk masalah kedua adalah adanya penundaan 20‒30 detik pada pemutaran ulang streaming HLS (M3U8) untuk memastikan pemutaran ulang berjalan dengan lancar.

### 2. Cara mengatasi masalah
Melalui pengoptimalan di berbagai versi SDK MLVB, kami telah mengembangkan teknologi penyesuaian otomatis, serta menggunakannya untuk membuat tiga skema kontrol latensi yang membantu Anda memberikan layanan pemutaran ulang terbaik tanpa perlu mempelajari kontrol QoS.

- **Auto mode** (Mode otomatis): gunakan mode ini jika Anda tidak yakin tentang skenario streaming langsung mana yang akan diterapkan.
>?Anda dapat beralih ke mode ini dengan mengatur `setAutoAdjustCache` ke `true` di `TXLivePlayConfig`. Dalam mode ini, pemutar akan menyesuaikan lag secara otomatis berdasarkan kondisi jaringan untuk meminimalkan lag antara host dan pemirsa serta memastikan kualitas interaksi host-pemirsa sekaligus memberikan layanan pemutaran ulang yang andal. Secara default, pemutar menyesuaikan lag dengan rentang antara 1‒5 detik. Anda dapat menggunakan `setMinCacheTime` dan `setMaxCacheTime` untuk memodifikasi rentang default.

- **Speedy mode** (Mode cepat): cocok untuk **acara langsung** dan skenario lain yang memerlukan lag rendah.
>? Anda dapat beralih ke mode ini dengan **mengatur `SetMinCacheTime` dan `setMaxCacheTime` ke 1 detik**. Perbedaan antara mode otomatis dan mode cepat hanya terletak pada nilai `MaxCacheTime`, yang umumnya lebih rendah dalam mode cepat dan lebih tinggi dalam mode otomatis. Fleksibilitas ini dapat terwujud berkat teknologi kontrol otomatis SDK, yang dapat menyesuaikan lag secara otomatis tanpa menyebabkan kemacetan. `MaxCacheTime` berkaitan dengan kecepatan penyesuaian. Makin tinggi nilai `MaxCacheTime`, makin konservatif penyesuaiannya, dan makin kecil kemungkinan terjadinya kemacetan.

- **Smooth mode** (Mode lancar): cocok untuk **streaming game langsung** dan skenario lain yang memerlukan bitrate tinggi dan definisi tinggi.
>? 
>- Anda dapat beralih ke mode ini dengan mengatur `setAutoAdjustCache` pemutar ke `false`. Dalam mode ini, pemutar akan menerapkan strategi yang mirip dengan strategi buffering Adobe Flash Player untuk IE. Ketika kemacetan terjadi, pemutar akan beralih ke mode pemuatan, dan ketika data yang di-buffer sudah cukup; pemutar akan kembali ke mode pemutaran, hingga fluktuasi jaringan berikutnya. Secara default, buffer akan dilakukan pada data video selama 5 detik, tetapi Anda dapat mengubahnya melalui `setCacheTime`.
>- Mode yang tampak sederhana ini mengurangi kemacetan pada pemutaran ulang dengan melakukan peningkatan yang cukup pada lag sehingga menjadi opsi yang andal untuk skenario yang tidak memerlukan lag rendah.

