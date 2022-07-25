## Remuxing Langsung

Remuxing langsung adalah proses mengonversi streaming asal yang di-push dari situs streaming langsung (umumnya menggunakan protokol RTMP) ke berbagai format kontainer di cloud sebelum di-push kepada pemirsa. 

 ### Format kontainer output yang didukung

-  RTMP
-  FLV
-  HLS
-  DASH
-  HDS
-  Stream TS


 ### Jenis output yang didukung

- Output audio-saja: menghapus file video dan membuat output audio-saja. Format kontainer seperti uraian di atas.
- Output video-saja: menghapus file audio dan membuat output video-saja. Format kontainer seperti uraian di atas.


 ### Skema enkripsi media yang didukung

- **FairPlay**
  Remuxing HLS mendukung solusi Apple FairPlay DRM.
- **Widevine**
  Remuxing DASH mendukung solusi Google Widevine DRM.
- **Enkripsi AES-128 universal untuk HLS**
  Remuxing HLS mendukung skema enkripsi AES-128 universal.


## Transcoding Langsung

Transcoding langsung (termasuk transcoding video dan transcoding audio) merupakan proses transcoding streaming asal yang di-push dari situs streaming langsung ke streaming dengan berbagai codec, resolusi, dan bitrate di cloud sebelum streaming di-push kepada pemirsa. Transcoding langsung membantu memenuhi kebutuhan pemutaran ulang di berbagai lingkungan jaringan dan di beragam perangkat.

 ### Kasus penggunaan standar

- Streaming video asal dapat di-transcode ke berbagai definisi streaming. Pemirsa dapat memilih streaming video dengan berbagai bitrate sesuai dengan kondisi jaringan untuk memastikan kelancaran pemutaran ulang.
- Anda dapat menambahkan watermark kustom ke streaming video asal untuk tujuan hak cipta dan pemasaran.
- Streaming video dapat di-transcode ke codec video dengan rasio kompresi yang lebih tinggi. Sebagai contoh, ketika jumlah pemirsa sangat besar, Anda dapat mengonversi streaming video H.264 ke streaming H.265 yang memiliki rasio kompresi lebih tinggi sehingga penggunaan bandwidth dan biaya berkurang.
- Streaming video asal dapat di-transcode ke berbagai codec yang sesuai untuk pemutaran ulang di perangkat khusus. Sebagai contoh, jika streaming video H.264 tidak dapat diputar ulang secara real-time karena masalah performa, Anda dapat melakukan transcoding pada streaming video tersebut ke format .mpeg untuk tujuan decoding dan pemutaran ulang real-time.

<span id="parameter"></span>

 ### Parameter transcoding video

<table>
    <tr><th width="20%">Jenis Parameter</th><th width="80%">Deskripsi</th></tr>
    <tr>
        <td>Codec video</td>
        <td>Codec video yang didukung:<ul style="margin:0px;">
            <li>H.264</li>
            <li>H.265</li>
            </ul>
        </td>
    </tr><tr>
        <td>Profil video</td>
        <td>Profil video yang didukung:<ul style="margin:0px;">
            <li>Garis dasar</li>
            <li>Utama</li>
            <li>Tinggi</li>
            </ul></td>
    </tr><tr>
        <td>Bitrate encoding video</td>
        <td><ul style="margin:0px;">
            <li>Rentang bitrate output video yang didukung: 50 Kbps‒10 Mbps.</li>
            <li>Bitrate asal akan menjadi bitrate output jika Anda menetapkan bitrate output yang lebih tinggi daripada bitrate asal. Sebagai contoh, jika bitrate output yang ditetapkan adalah 3.000 Kbps, tetapi bitrate asal streaming input hanya 2.000 Kbps, bitrate output akan menjadi 2.000 Kbps.</li>
            </ul></td>
    </tr><tr>
        <td>Frame rate encoding video</td>
        <td><ul style="margin:0px;">
            <li>Rentang frame rate output video yang didukung: 1‒60 fps.</li>
            <li>Frame rate asal akan menjadi frame rate output jika Anda menetapkan frame rate output yang lebih tinggi daripada frame rate asal. Sebagai contoh, jika frame rate output yang ditetapkan adalah 30 fps, tetapi frame rate asal streaming input hanya 20 fps, frame rate output akan menjadi 20 fps.</li>
            </ul></td>
    </tr><tr>
        <td>Resolusi video</td>
        <td><ul style="margin:0px;" >
            <li>Rentang lebar yang didukung: 0‒3000.</li>
            <li>Rentang tinggi yang didukung: 0‒3000.</li>
            <li>Anda hanya dapat menetapkan lebar. Tinggi akan menyesuaikan secara berbanding lurus.</li>
            <li>Anda hanya dapat menetapkan tinggi. Lebar akan menyesuaikan secara berbanding lurus.</li>
            </ul></td>
    </tr><tr>
        <td>Durasi GOP video </td>
        <td>Rentang durasi GOP video yang didukung: 1‒10 detik; rentang yang disarankan: 2‒4 detik.</td>
    </tr><tr>
        <td>Metode kontrol bitrate video</td>
        <td>Metode kontrol bitrate video yang didukung:<ul style="margin:0px;">
            <li>Bitrate tetap (CBR)</li>
            <li>Bitrate dinamis (VBR)</li>
            </ul></td>
    </tr><tr>
        <td>Rotasi gambar video</td>
        <td>Video asal dapat dirotasikan searah jarum jam sebesar:<ul style="margin:0px;">
            <li>90 derajat</li>
            <li>180 derajat</li>
            <li>270 derajat</li>
            </ul></td>
    </tr>
</table>


 ### Parameter transcoding audio


<table>
    <tr><th width="20%">Jenis Parameter</th><th width="80%">Deskripsi</th></tr>
    <tr>
        <td>Codec audio</td>
        <td>Codec yang didukung:<ul style="margin:0px">
						<li>AAC-LC</li>
						<li>AAC-HE</li>
						<li>AAC-HE v2</li>
			</ul></td>
    </tr>
    <tr>
        <td>Tingkat sampel audio</td>
        <td>Tingkat sampel yang didukung (48000 dan 44100 biasanya digunakan):
				<ul style="margin:0px">
					<li>96000</li>
					<li>64000</li>
					<li>48000</li>
					<li>44100</li>
					<li>32000</li>
					<li>24000</li>
					<li>16000</li>
					<li>12000</li>
					<li>8000</li>
				</ul>
				</td>
    </tr>
    <tr>
        <td>Bitrate encoding audio</td>
        <td>Rentang bitrate yang didukung: 20‒192 Kbps; bitrate yang umum digunakan meliputi:
				<ul style="margin:0px">
					<li>48 Kbps</li>
					<li>64 Kbps</li>
					<li>128 Kbps</li>
					</ul></td>
    </tr>
    <tr>
        <td>Saluran suara</td>
        <td>Mode saluran suara yang didukung:
				<ul style="margin:0px">
					<li>Mono</li>
					<li>Dual</li>
					</ul></td>
</tr></table>




 ### Templat prasetel umum untuk transcoding video

| Definisi Video| Nama Templat | Resolusi Video | Bitrate Video | Frame Rate Video | Codec Video |
| ------ | -------- | ----------------- | -------- | -------- | ------------ |
| Lancar | 550 | Sisi pendek gambar (dengan skala proporsional) x sisi panjang (540) | 500 Kbps | 23       | H.264         |
| SD | 900 | Sisi pendek gambar (dengan skala proporsional) x sisi panjang (720) | 1000 Kbps | 25 |  H.264 |
| HD | 2000 | Sisi pendek gambar (dengan skala proporsional) x sisi panjang (1080) | 2000 Kbps | 25 | H.264 |

## Transcoding Codec Kecepatan Tinggi

Dengan pengalaman selama bertahun-tahun di berbagai bidang teknologi, misalnya encoding audio/video, pengenalan skenario cerdas, encoding dinamis, dan model kontrol bitrate presisi tiga tingkat (CTU/lini/frame), Tencent Video Cloud menyediakan layanan streaming definisi lebih tinggi dengan bitrate lebih rendah (rata-rata 30% lebih rendah) untuk streaming langsung, konten sesuai permintaan, dll.

### Kasus penggunaan

Jika push langsung memiliki bitrate tinggi dan gambarnya kompleks, Anda dapat menggunakan teknologi encoding dinamis cerdas dan model kontrol bitrate presisi untuk mempertahankan definisi yang tinggi dengan bitrate yang rendah sehingga kualitas gambar video yang ditonton pemirsa tetap sama dengan kualitas gambar video asal.

## Keuntungan

Karena adanya peningkatan permintaan dari pengguna di berbagai platform video terhadap definisi sumber video yang tinggi dan pengalaman menonton yang lancar, di industri streaming langsung saat ini, resolusi 1080p dan bitrate 3‒10 Mbps perlahan menjadi konfigurasi yang paling banyak dipakai, dan biaya bandwidth menyumbang persentase yang besar terhadap total biaya platform video. Dalam contoh ini, pengurangan bitrate video dapat mengurangi biaya bandwidth secara efektif.
**Contoh:**
Misalnya, Anda mengadakan sesi siaran langsung dengan kecepatan 3 Mbps selama 4 jam dengan 200 pemirsa. Codec menggunakan H.264 dan transcoding codec kecepatan tinggi tidak digunakan. Bandwidth puncak sebesar 600 Mbps. Biaya bandwidth untuk sesi siaran langsung ini adalah 600 x 0,2118 = 127,08 USD.

- Jika transcoding codec kecepatan tinggi digunakan untuk mengurangi bitrate, biaya bandwidth yang dikenakan adalah sebesar 127,08 x (100% - 30%) = 88,956 USD.
- Biaya transcoding codec kecepatan tinggi: 0,0443 x 240 = 10,632 USD (harga tertera belum dikurangi diskon).
- Biaya total: 88,956 + 10,632 = 99,588 USD.

Oleh karena itu, transcoding codec kecepatan tinggi dapat mengurangi biaya bandwidth platform secara efektif sambil tetap menghadirkan pengalaman menonton yang lebih baik.

### Parameter utama

Cara mengonfigurasikan parameter transcoding codec kecepatan tinggi pada dasarnya sama dengan cara mengonfigurasikan parameter transcoding langsung standar. Informasi selengkapnya dapat dilihat di [Parameter transcoding video](#parameter).



## Pemberian Watermark Langsung

Anda dapat menggunakan pemberian watermark langsung untuk menambahkan gambar logo prasetel ke streaming video asal untuk tujuan hak cipta dan pemasaran.

### Parameter watermark
Parameter utama suatu watermark meliputi lokasi dan ukuran watermark, yang ditentukan oleh parameter `XPosition`, `YPosition`, `Width`, dan `Height` seperti diuraikan di bawah ini:
- **XPosition**: Offset sumbu X, yang menunjukkan jarak persentase dari ujung kiri watermark ke ujung kiri video.
- **YPosition**: Offset sumbu Y, yang menunjukkan jarak persentase dari ujung atas watermark ke ujung atas video.
- **Width** (Lebar): lebar watermark atau persentase lebar video streaming langsung.
- **Height** (Tinggi): tinggi watermark atau persentase tinggi video streaming langsung.

![](https://main.qcloudimg.com/raw/b7341cfb465aae7a59ff24ca6abeecb2.png)

>! Jika Anda mengaktifkan transcoding multibitrate untuk sebuah streaming (yaitu satu streaming sumber di-transcode ke streaming dengan berbagai resolusi) dan ingin menambahkan watermark, Anda dapat mengatur posisi persentasenya di sumbu X dan Y di [konsol CSS](#W_control) atau melalui [API](#W_api) yang sesuai, dan posisi watermark akan secara otomatis ditentukan oleh sistem.

### Contoh parameter watermark

Misalnya, resolusi gambar output adalah 1920 x 1080, resolusi watermark adalah 320 x 240, XPosition = 5, YPosition = 5, dan Lebar = 10 (unit: persen).
Posisi dan ukuran absolut watermark di video output dijelaskan sebagai berikut:
```
XPosition_pixel = 1920 x 5% = 96
YPosition_pixel = 1080 x 5% = 54
Width_pixel = 1920 x 10% = 192
Height_pixel = 192 x 240/320 = 144
```

Watermark berjarak 96 piksel dari ujung kiri gambar video output dan 54 piksel dari ujung atas gambar. Watermark berukuran 192 x 144.

### Cara penggunaan
Anda dapat menambahkan watermark di [konsol CSS](#W_control) atau melalui [server API](#W_api) sesuai dengan kebutuhan bisnis Anda.

<span id="W_control"></span>

#### Konsol CSS
1. Buka **Feature Configuration** > **[Live Watermarking](https://console.cloud.tencent.com/live/config/watermark)** (Konfigurasi Fitur > Pemberian Watermark Langsung) untuk menambahkan templat konfigurasi watermark, mengatur parameter watermark, dan membuat ID templat watermark yang sesuai. Langkah-langkah spesifiknya dapat dipelajari di [Konfigurasi Templat Watermark](https://intl.cloud.tencent.com/document/product/267/31073).
2. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) untuk menambahkan nama domain dan klik **Manage** > **Template Configuration** (Kelola > Konfigurasi Templat) untuk mengikatnya dengan templat watermark. Informasi selengkapnya dapat dilihat di [Watermark Configuration (Konfigurasi Watermark)](https://intl.cloud.tencent.com/document/product/267/31064).
<span id="W_api"></span>
#### Memanggil API
1. Panggil API [AddLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30826) untuk menambahkan watermark dengan mengatur nama watermark dan parameter lainnya.
2. Panggil API [CreateLiveWatermarkRule](https://intl.cloud.tencent.com/document/product/267/30825) untuk membuat aturan watermark. Atur `DomainName` (nama domain push) dan `WatermarkId` (kembali ke langkah 1). Gunakan `AppName` yang sama dengan `AppName` di alamat push dan pemutaran ulang, yang secara default diberi nama `live`.

Catatan: Penggunaan fitur watermark akan dikenai biaya transcoding standar.



## Mengonfigurasikan Parameter Transcoding

### Cara penggunaan

Anda dapat mengatur parameter transcoding melalui [konsol CSS](#T_control) atau [API server](#T_api). Kedua cara tersebut mengharuskan Anda menggunakan templat watermark, templat transcoding, dan aturan transcoding untuk konfigurasi.
<span id="T_control"></span>
#### Konsol CSS
1. Buka **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)** (Konfigurasi Fitur > Transcoding Langsung) untuk menambahkan templat konfigurasi transcoding. Anda dapat menambahkan templat [transcoding standar](https://intl.cloud.tencent.com/document/product/267/31071) atau [transcoding codec kecepatan tinggi](https://intl.cloud.tencent.com/document/product/267/31071).
2. Buat jenis transcoding yang sesuai dan atur parameter transcoding sesuai kebutuhan. Anda dapat menggunakan parameter default sistem, dan selanjutnya ID templat transcoding yang sesuai akan dibuat.
3. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) untuk menemukan nama domain pull target dan klik **Manage** > **Template Configuration** (Kelola > Konfigurasi Templat) untuk mengikatnya dengan templat transcoding. Informasi selengkapnya dapat dilihat di [Transcoding Configuration (Konfigurasi Transcoding)](https://intl.cloud.tencent.com/document/product/267/31062).

<span id="T_api"></span>
#### Memanggil API

1. Panggil API [CreateLiveTranscodeTemplate](https://intl.cloud.tencent.com/document/product/267/30790) untuk mengatur parameter jenis transcoding.

2. Panggil API [CreateLiveTranscodeRule](https://intl.cloud.tencent.com/document/product/267/30791) untuk mengatur parameter `DomainName` (nama domain pull) dan `TemplateId` (kembali ke langkah 1). Masukkan string kosong di `AppName` dan `StreamName` sebagai wildcard untuk mencocokkan semua streaming di nama domain tersebut. Anda juga dapat mengikatkan templat transcoding ke berbagai nama streaming guna mengaktifkan transcoding untuk streaming langsung ini.

3. Setiap templat transcoding memiliki **nama templat transcoding unik** yang digunakan sebagai ID unik untuk memutar ulang streaming output. Anda dapat menempatkan nama templat transcoding setelah ID streaming di alamat pemutaran ulang untuk melakukan pull pada streaming output yang sesuai dengan templat transcoding tersebut.

>! Aturan transcoding digunakan guna mengatur diaktifkan atau tidaknya templat transcoding tertentu untuk nama domain atau streaming tertentu. Nama domain pemutaran ulang dapat digunakan untuk melakukan pull pada templat transcoding hanya setelah aturan transcoding yang sesuai selesai dibuat. Jika tidak ada aturan transcoding yang telah dibuat, alamat pull yang disambung menggunakan nama templat transcoding menjadi tidak valid.



### Contoh

```
**Alamat pemutaran ulang = Nama domain pemutaran ulang + Jalur pemutaran ulang + Nama templat Stream ID_transcoding + String autentikasi**
```
Untuk push dengan ID streaming `1234_test`, streaming asal dan streaming ber-watermark dengan berbagai bitrate dapat diputar ulang melalui alamat berikut:

- **Streaming asal:** `http://liveplay.tcloud.com/live/1234_test.flv?authentication string`
- **Streaming transcoding standar (ber-watermark):** `http://liveplay.tcloud.com/live/1234_test_sd.flv?authentication string`
- **Streaming transcoding codec kecepatan tinggi (ber-watermark):** `http://liveplay.tcloud.com/live/1234_test_hd.flv?authentication string`

>! Untuk memutar ulang streaming ber-watermark, Anda harus mengikatkan nama domain push yang sesuai ke templat watermark yang sudah dibuat.

### Menggunakan API
1. **Mengelola templat transcoding di konsol**:
   Anda dapat melakukan kueri, menambahkan, memodifikasi, dan menghapus templat transcoding di konsol.
2. **Mengelola templat transcoding melalui API server**:
<table>
<tr><th>Modul Fitur</th><th>API</th>
</tr><tr>
<td rowspan=8>Transcoding Langsung</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30790">CreateLiveTranscodeTemplate</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30784">ModifyLiveTranscodeTemplate</a></td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30786">DescribeLiveTranscodeTemplate</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30785">DescribeLiveTranscodeTemplates</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30788">DeleteLiveTranscodeTemplate</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30791">CreateLiveTranscodeRule</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30787">DescribeLiveTranscodeRules</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30789">DeleteLiveTranscodeRule</a></td>
</tr><tr>
<td rowspan=4>Pemberian Watermark Langsung</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30826">AddLiveWatermark</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30818">UpdateLiveWatermark</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30824">DeleteLiveWatermark</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30820">DescribeLiveWatermarks</a></td>
</tr></table>








 
