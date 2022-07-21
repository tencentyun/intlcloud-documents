CSS menyediakan layanan [transcoding standar](#n_trans), [transcoding codec kecepatan puncak](#s_trans), dan [transcoding audio](#a_trans), yang dikenai tagihan berdasarkan codec, (ukuran) resolusi gambar streaming langsung, dan durasi transcoding. Pengaktifan **pemberian watermark** atau **pencampuran streaming** juga dapat dikenai biaya transcoding, yang ditagih berdasarkan resolusi streaming langsung output.

## Catatan

- Mode penagihan: bayar sesuai pemakaian.
- Siklus penagihan: siklus penagihan harian. Biaya untuk satu hari akan dipotong pada pukul 10.00 hari berikutnya. Untuk pengguna dengan siklus penagihan bulanan, tagihan transcoding bulan berjalan akan dibuat antara tanggal 1 dan 5 bulan berikutnya.
- Transcoding dinonaktifkan secara default dan dapat diaktifkan serta dikonfigurasi melalui [konsol CSS](https://intl.cloud.tencent.com/document/product/267/31071) atau melalui [API TencentCloud](https://intl.cloud.tencent.com/document/product/267/30790).
- Untuk penagihan, durasi transcoding akan dibulatkan ke atas hingga 1 menit terdekat.
- Jika layanan transcoding tidak digunakan, tidak ada biaya yang dikenakan.



<span id="n_trans1"></span>

## Transcoding Standar

### Harga

<table>
<tr>
<th >Codec</th>
<th >Bitrate yang Direkomendasikan (Kbps)</th>
<th >Resolusi</th>
<th >Harga (USD/mnt)</th>
<th >Catatan (sisi lebar dan tinggi yang lebih panjang dianggap sebagai sisi panjang dari gambar streaming langsung)</th>
</tr>
<tr>
<td rowspan="5"><b>H.264</td>
<td >500</td>
<td>480p</td>
<td>0,0028</td>
<td>Sisi panjang gambar ≤ 640 dan sisi pendek gambar ≤ 480</td>
</tr>
<tr>
<td >1000</td>
<td>720p</td>
<td>0,0057</td>
<td>Sisi panjang gambar ≤ 1280 dan sisi pendek gambar ≤ 720</td>
</tr>
<tr>
<td rowspan="2">2000</td>
<td>1080p</td>
<td>0,0111</td>
<td>Sisi panjang gambar ≤ 1936 dan sisi pendek gambar ≤ 1088</td>
</tr>
<tr>
<td>2K</td>
<td>0,024</td>
<td>Sisi panjang gambar ≤ 2560 dan sisi pendek gambar ≤ 1440</td>
</tr>
<tr>
<td >4000</td>
<td>4K</td>
<td>0,0491</td>
<td>Sisi panjang gambar > 2560 dan sisi pendek gambar > 1440</td>
</tr>
<tr>
<td rowspan="5"><b>H.265</td>
<td >500</td>
<td>480p</td>
<td>0,0141</td>
<td>Sisi panjang gambar ≤ 640 dan sisi pendek gambar ≤ 480</td>
</tr>
<tr>
<td >1000</td>
<td>720p</td>
<td>0,0275</td>
<td>Sisi panjang gambar ≤ 1280 dan sisi pendek gambar ≤ 720</td>
</tr>
<tr>
<td rowspan="2">2000</td>
<td>1080p</td>
<td>0,0549</td>
<td>Sisi panjang gambar ≤ 1936 dan sisi pendek gambar ≤ 1088</td>
</tr>
<tr>
<td>2K</td>
<td>0,1183</td>
<td>Sisi panjang gambar ≤ 2560 dan sisi pendek gambar ≤ 1440</td>
</tr>
<tr>
<td >4000</td>
<td>4K</td>
<td>0,2366</td>
<td>Sisi panjang gambar > 2560 atau sisi pendek gambar > 1440</td>
</tr>
</table>

>!Sebagai contoh, jika sisi panjang gambar adalah 1280 dan sisi pendek gambar adalah 480, resolusi video akan dihitung sebagai 720p. Sisi gambar dengan nilai lebih besar dianggap sebagai sisi panjang gambar.


### Ikhtisar penagihan

- Item yang dapat dikenai tagihan: durasi transcoding langsung (atau durasi pencampuran streaming atau streaming langsung yang diberi watermark jika fitur pencampuran streaming atau pemberian watermark diaktifkan).
- Aturan penagihan:
  - Biaya dihitung dengan mengalikan durasi transcoding dengan codec dan resolusi dalam suatu hari dan harga unit yang sesuai.
  - Transcoding langsung dipicu oleh pulling streaming, dan pemutaran ulang akan dikenai biaya transcoding standar. Pemberian watermark langsung dipicu oleh pushing, dan pencampuran streaming langsung dipicu oleh pemberian sinyal. Penggunaan pemberian watermark dan pencampuran streaming langsung akan dikenai biaya transcoding standar, meskipun streaming tidak diputar ulang.

### Rumus penagihan

Biaya transcoding standar = Durasi transcoding x Harga codec dan resolusi yang sesuai. 

### Contoh penagihan

Jika Anda menggunakan layanan transcoding dan pemberian watermark langsung pada 1 Januari 2021 yang melakukan transcoding streaming langsung A menjadi `H.264_720P` selama 1 jam dan streaming langsung B diberi watermark pada 480p selama 30 menit, biaya transcoding langsung yang harus Anda bayar pada 2 Januari 2021 adalah sebagai berikut:
Biaya transcoding langsung harian = 0,0057 (USD/mnt) × 60 (mnt) + 0,0028 (USD/mnt) × 30 (mnt) = 0,426 USD.
		
<span id="s_trans"></span>

## Transcoding Codec Kecepatan Puncak

### Harga

<table>
<tr>
<th>Codec</th>
<th>Resolusi</th>
<th>Harga (USD/mnt)</th>
</tr><tr>
<td rowspan="5"><b>H.264</td>
<td>480p</td>
<td>0,0116</td>
</tr><tr>
<td>720p</td>
<td>0,0222</td>
</tr><tr>
<td>1080p</td>
<td>0,0443</td>
</tr><tr>
<td>2K</td>
<td>0,0886</td>
</tr><tr>
<td>4K</td>
<td>0,1772</td>
</tr><tr>
<td rowspan="5"><b>H.265</td>
<td>480p</td>
<td>0,0349</td>
</tr><tr>
<td>720p</td>
<td>0,0665</td>
</tr><tr>
<td>1080p</td>
<td>0,1329</td>
</tr><tr>
<td>2K</td>
<td>0,2659</td>
</tr><tr>
<td>4K</td>
<td>0,5317</td>
</tr>
</table>

### Ikhtisar penagihan

- Aturan penagihan: biaya dihitung dengan mengalikan durasi transcoding codec kecepatan puncak dalam suatu hari dan harga unit yang sesuai.


### Rumus penagihan

Biaya transcoding codec kecepatan puncak = Durasi transcoding x Harga codec dan resolusi yang sesuai. 

### Contoh penagihan

Jika Anda menggunakan layanan transcoding codec kecepatan puncak pada 1 Januari 2021, yang melakukan transcoding streaming langsung A ke output codec kecepatan puncak pada 720p selama 1 jam dan transcoding streaming langsung B ke output codec kecepatan puncak pada 480p selama 30 menit, biaya transcoding codec kecepatan puncak yang harus Anda bayar pada 2 Januari 2021 adalah sebagai berikut:
Biaya transcoding codec kecepatan puncak harian = 0,0222 (USD/mnt) × 60 (mnt) + 0,0116 (USD/mnt) × 30 (mnt) = 1,68 USD.

>? Jika Anda memiliki bisnis streaming langsung skala besar, mode penagihan harian mungkin tidak memenuhi kebutuhan Anda. Silakan hubungi tim penjualan Tencent Cloud atau [kirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk mengetahui mode penagihan yang paling tepat untuk Anda.

<span id="a_trans"></span>	

## Transcoding Audio

CSS menawarkan layanan transcoding audio. Layanan ini menawarkan fitur transcoding audio berkualitas tinggi yang dapat melakukan transcoding konten audio dan video ke berbagai formats sehingga membantu mengurangi biaya penyesuaian, tenaga kerja, dan perangkat keras serta memberikan output yang lebih efektif dan andal bagi industri audiovisual, dan mampu beradaptasi secara optimal dengan kebutuhan spesifik Anda.

### Harga

| Item yang Dapat Dikenai Tagihan  | Mode Penagihan           | Harga            |
| -------- | ------------------ | ------------- |
| Transcoding audio | Ditagih berdasarkan durasi transcoding audio | 0,00099 USD/mnt |

### Ikhtisar penagihan

- Item yang dapat dikenai tagihan: durasi transcoding audio.
- Aturan penagihan: biaya dihitung dengan mengalikan durasi transcoding audio dalam suatu hari dan harga unit yang sesuai.

### Rumus penagihan

Biaya transcoding audio = Harga unit × Durasi transcoding.

### Contoh penagihan

Jika Anda menggunakan layanan transcoding audio selama 5 jam pada 1 Februari 2021, biaya transcoding audio langsung yang harus Anda bayar pada 2 Februari 2021 adalah sebagai berikut:
Biaya transcoding audio harian = 0,00099 (USD/mnt) x 300 (mnt) = 0,297 USD.

> !
> - **Aturan penagihan baru untuk fitur transcoding audio berlaku efektif pada 1 Februari 2021. Semua tagihan sejak 2 Februari 2021 telah dibuat menurut aturan penagihan yang baru.**
> - [Web push (Push web)](https://intl.cloud.tencent.com/document/product/267/35968) menggunakan protokol WebRTC dan codec audio Opus. Jika LVB digunakan untuk memutar ulang push web dalam format RTMP, FLV, atau HLS, transcoding akan secara otomatis dimulai untuk melakukan transcoding audio ke dalam format AAC sehingga biaya transcoding audio akan dikenakan.
