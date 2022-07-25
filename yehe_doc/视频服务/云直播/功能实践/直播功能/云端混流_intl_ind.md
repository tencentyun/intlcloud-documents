CSS menyediakan fitur campuran streaming langsung. Fitur ini dapat mencampurkan secara bersamaan beberapa streaming sumber input menjadi satu streaming baru berdasarkan tata letak campuran streaming terkonfigurasi untuk streaming langsung interaktif. Selain itu, fitur campuran streaming telah terkoneksi dengan TencentCloud API 3.0. Informasi selengkapnya dapat dilihat di [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997). Dokumen ini menggunakan contoh untuk menjelaskan cara mengimplementasikan campuran streaming langsung dalam berbagai skenario.

## Catatan
- Penggunaan campuran streaming akan dikenai biaya transcoding. Penjelasan mendetail dapat dilihat di [Live Transcoding (Watermarking, Stream Mixing) (Transcoding Langsung (Pemberian Watermark, Pencampuran Streaming)](https://intl.cloud.tencent.com/document/product/267/39604).
- Untuk menggunakan fitur pencampuran dan pemotongan, nilai parameter pemotongan tidak boleh melebihi nilai parameter streaming input.


## Fitur yang Didukung
- Pencampuran dapat dilakukan pada maksimum **16** streaming bersamaan.
- Pencampuran dapat dilakukan pada maksimum **5** jenis sumber input (audio dan video, audio murni, video murni, gambar, dan kanvas).
- Streaming campuran dapat menjadi output sebagai streaming baru.
- Pemotongan dan pemberian watermark didukung.
- Konfigurasi templat didukung.
- Perekaman berdasarkan campuran streaming didukung.
- Campuran streaming otomatis didukung.
- Jenis dan posisi campuran streaming dapat diubah secara real-time.
- Campuran streaming dapat dimulai/dibatalkan dengan lancar.


## Templat Tata Letak Umum
Templat umum meliputi 10, 30, 40, 310, 390, 410, 510, dan 610. Ketika menggunakan templat umum, Anda tidak perlu memasukkan parameter posisi dan panjang/lebar streaming input, dan **skala gambar asli akan diatur secara otomatis.** Anda hanya perlu memasukkan ID templat.

**Gambar berbagai templat tata letak umum:**
<table>
<style>#m_img{width:90%;height:auto;display:block;margin-left:auto;margin-right:auto; }</style>
<thead><tr><th>Templat 10</th><th >Templat 30</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/a6b395f6fc7c1d07e4325836a3b725e6.jpg" id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/05fbe1c32bec1aed0624785d51b8a2ef.jpg"  id="m_img"></td>
</tr>
<thead><tr><th >Templat 40</th><th>Templat 310</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/06cd40976b29452fa297d52db0d3435c.jpg"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/e1f4aa6f198856c47d8175302c649448.jpg"  id="m_img"></td>
</tr>
<thead><tr><th>Templat 390</th><th >Templat 410</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/50157bb0b01d511c10b3637c13b1471a.png"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/6a420d03e7921453cbc461d1f1176f6c.jpg"  id="m_img"></td>

</tr>
<thead><tr><th>Templat 510</th><th>Templat 610</th></tr></thead>
<td><img src="https://main.qcloudimg.com/raw/c0e5bd29f275a6f055af9830ceea0a02.jpg"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/5ca8ba33cc08e80d6aeb403645e75aac.jpg"  id="m_img"></td>

</tr>
</tbody></table>	




## Membuat Sesi Campuran Streaming
### Parameter
Informasi selengkapnya dapat dilihat di [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997).



### Skenario 1. Mengajukan campuran streaming - menggunakan templat 20
Contoh ini menunjukkan cara menggunakan templat campuran streaming prasetel untuk mencampur streaming.

#### Contoh kode input
```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&MixStreamTemplateId=20
&OutputParams.OutputStreamName=test_stream1
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&<Common request parameters>
```

#### Kode output sampel
```
{
  "Response": {
    "RequestId": "e8fa8015-0892-40d5-95c4-12a4bc06ed31"
  }
}
```

#### Efek campuran streaming untuk koneksi mikrofon
![img](https://main.qcloudimg.com/raw/a9bdfd2622e3152e61d8cb15a1b21aa1.jpg)


### Skenario 2. Mengajukan campuran streaming - menggunakan templat 390
Contoh ini menunjukkan cara menggunakan templat campuran streaming prasetel untuk mencampur streaming.

#### Contoh kode input

```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&MixStreamTemplateId=390
&OutputParams.OutputStreamName=test_stream2
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.0.LayoutParams.InputType=3
&InputStreamList.0.LayoutParams.ImageWidth=1920 (lebar kanvas)
&InputStreamList.0.LayoutParams.ImageHeight=1080 (tinggi kanvas)
&InputStreamList.0.LayoutParams.Color=0x000000
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&InputStreamList.2.InputStreamName=test_stream3
&InputStreamList.2.LayoutParams.ImageLayer=3
&<Common request parameters>
```

#### Kode output sampel

```
{
  "Response": {
    "RequestId": "9d8d5837-2273-4936-8661-781aeab9bc9c"
  }
}
```

#### Efek campuran streaming untuk kompetisi host
![img](https://main.qcloudimg.com/raw/cad10f080a239725893e5221faa21c17.jpg)



### Skenario 3. Campuran streaming kustom
Gunakan tata letak kustom, dengan parameter posisi `LocationX` dan `LocationY` menunjukkan jarak piksel absolut antara sudut kiri atas citra kecil dan sudut kiri atas gambar latar belakang.
![](https://main.qcloudimg.com/raw/e1f81cd4a9b08af4ad7e4658fc643f0d.png)

#### Contoh kode input
```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&OutputParams.OutputStreamName=test_stream2
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.0.LayoutParams.InputType=3
&InputStreamList.0.LayoutParams.ImageWidth = 1920
&InputStreamList.0.LayoutParams.ImageHeight= 1080
&InputStreamList.0.LayoutParams.Color=0x000000
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&InputStreamList.1.LayoutParams.ImageWidth = 640
&InputStreamList.1.LayoutParams.ImageHeight= 360
&InputStreamList.1.LayoutParams.LocationX= 50
&InputStreamList.1.LayoutParams.LocationY= 720
&InputStreamList.2.InputStreamName=test_stream3
&InputStreamList.2.LayoutParams.ImageLayer=3
&InputStreamList.2.LayoutParams.ImageWidth = 640
&InputStreamList.2.LayoutParams.ImageHeight= 360
&InputStreamList.2.LayoutParams.LocationX= 740
&InputStreamList.2.LayoutParams.LocationY= 720
&<Common request parameters>
```


#### Kode output sampel
```
{
  "Response": {
    "RequestId": "8c443359-ba07-4b81-add8-a6ff54f9bf54"
  }
}
```


#### Efek campuran streaming kustom
![](https://main.qcloudimg.com/raw/db6a87baba1f1891f514d4bea9b38ee4.png)

## Membatalkan Campuran Streaming
### Parameter
Informasi selengkapnya dapat dilihat di [CancelCommonMixStream] (https://intl.cloud.tencent.com/document/product/267/35998).

### Contoh
Dalam contoh ini, Anda akan mempelajari cara membatalkan campuran streaming dengan ID sesi.
#### Contoh kode input
```
https://live.tencentcloudapi.com/?Action=CancelCommonMixStream
&MixStreamSessionId=test_room
```

#### Kode output sampel
```
{
  "Response": {
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```

>! 
>- Setelah mengajukan pembatalan campuran streaming, tunggu setidaknya selama 5 detik sebelum membatalkannya.
>- Setelah membatalkan campuran streaming, Anda dapat mengajukan campuran streaming menggunakan ID sesi yang sama setelah menunggu setidaknya selama setengah menit sebelum.

## Kode Kesalahan
Untuk campuran streaming API 3.0, kode-kode kesalahan paling umum telah ditransformasikan menjadi gaya [kode kesalahan API 3.0](https://intl.cloud.tencent.com/document/product/267/35997#6.-.E9.94.99.E8.AF.AF.E7.A0.81). Namun, beberapa kode kesalahan masih belum berubah, yang akan tersedia dalam format `err_code [ $code ],msg [ $message ]` di `Message` (Pesan) dan di-prompt sebagai kesalahan `InvalidParameter`. Penyebab ditampilkannya kode tertentu dijelaskan di bawah ini:

<table>
<thead><tr><th>Kode Kesalahan</th><th>Alasan</th><th>Pemecahan Masalah</th></tr></thead>
<tbody><tr>
<td>-1</td>
<td>Terjadi kesalahan ketika menguraikan parameter input</td>
<td><ul style="margin:0">
    <li>Periksa format JSON isi permintaan sudah benar atau belum.</li>
    <li>Periksa kemungkinan `InputStreamList` kosong.</li>
    </ul></td>
</tr><tr>
<td>-2</td>
<td>Parameter input salah</td>
<td>Periksa kemungkinan parameter gambar terlalu besar.</td>
</tr><tr>
<td>-3</td>
<td>Jumlah streaming salah</td>
<td>Periksa jumlah streaming input berada dalam rentang [1,16] atau tidak.</td>
</tr><tr>
<td>-4</td>
<td>Parameter streaming salah</td>
<td><ul style="margin:0">
    <li>Periksa panjang/lebar streaming input/output berada dalam rentang (0,3000) atau tidak.</li>
    <li>Periksa jumlah streaming input berada dalam rentang (0,16] atau tidak.</li>
    <li>Periksa streaming input membawa `LayoutParams` atau tidak.</li>
    <li>Periksa `InputType` didukung atau tidak (nilai valid: 0, 2, 3, 4, 5).</li>
    <li>Periksa panjang ID streaming berada dalam rentang (1,80) atau tidak.</li>
    </ul></td>
</tr><tr>
<td>-11</td>
<td>Kesalahan lapisan</td>
<td><ul style="margin:0">
    <li>Periksa jumlah lapisan sama dengan jumlah streaming input atau tidak.</li>
    <li>Periksa ID lapisan merupakan duplikat atau bukan.</li>
    <li>Periksa ID lapisan berada dalam rentang (0,16] atau tidak.</li>
    </ul></td>
</tr><tr>
<td>-20</td>
<td>Parameter input tidak sesuai dengan API</td>
<td><ul style="margin:0">
    <li>Periksa jumlah streaming input sesuai dengan ID templat atau tidak.</li>
    <li>Periksa parameter warna benar atau tidak.</li>
    </ul></td>
</tr><tr>
<td>-21</td>
<td>Jumlah streaming input untuk campuran streaming salah</td>
<td>Periksa ada sedikitnya dua streaming input atau tidak.</td>
</tr><tr>
<td>-28</td>
<td>Gagal mendapatkan panjang/lebar latar belakang</td>
<td><ul style="margin:0">
    <li>Periksa panjang dan lebar kanvas sudah diatur atau belum ketika mengatur kanvas.</li>
    <li>Periksa streaming latar belakang sudah ada atau belum (campuran streaming harus dimulai 5 detik setelah push dimulai).</li>
    </ul></td>
</tr><tr>
<td>-29</td>
<td>Parameter pemotongan salah</td>
<td>Periksa posisi pemotongan berada di luar rentang panjang/lebar streaming atau tidak.</td>
</tr><tr>
<td>-33</td>
<td>ID gambar watermark salah</td>
<td>Periksa ID gambar input sudah diatur atau belum.</td>
</tr><tr>
<td>-34</td>
<td>Gagal mendapatkan URL gambar watermark</td>
<td>Periksa gambar berhasil diunggah atau tidak dan URL sudah dibuat atau belum.</td>
</tr><tr>
<td>-111</td>
<td>Parameter `OutputStreamName` tidak sesuai dengan `OutputStreamType`</td>
<td><ul style="margin:0">
    <li>Jika `OutputStreamType` diatur ke `0`, `OutputStreamName` harus berada dalam `InputStreamList`.</li>
    <li>Jika `OutputStreamType` diatur ke `1`, `OutputStreamName` tidak boleh berada dalam `InputStreamList`.</li>
    </ul></td>
</tr><tr>
<td>-300</td>
<td>ID streaming output sudah digunakan</td>
<td>Periksa streaming output saat ini termasuk dalam tugas campuran streaming.lain atau tidak</td>
</tr><tr>
<td>-505</td>
<td>Gagal menemukan streaming input dalam `upload`</td>
<td>Periksa campuran streaming dimulai 5 detik setelah push atau tidak dan streaming dapat diputar ulang atau tidak.</td>
</tr><tr>
<td>-507</td>
<td>Gagal mengajukan kueri tentang parameter panjang/lebar streaming</td>
<td><ul style="margin:0">
    <li>Periksa panjang dan lebar kanvas sudah diatur atau tidak.</li>
    <li>Periksa push berhasil atau tidak. Anda sebaiknya memulai campuran streaming 5 detik setelah push dimulai.</li>
    </ul></td>
</tr><tr>
<td>-508</td>
<td>ID streaming output salah</td>
<td>Periksa kemungkinan ID streaming output yang berbeda digunakan oleh `MixStreamSessionId` yang sama.</td>
</tr><tr>
<td>-10031</td>
<td>Gagal memicu campuran streaming</td>
<td>Anda sebaiknya memulai campuran streaming 5 detik setelah push dimulai.</td>
</tr><tr>
<td>-30300<br>-31001<br>-31002</td>
<td>`Sessionid` tidak ada ketika campuran streaming dibatalkan</td>
<td>Periksa `MixStreamSessionId` ada atau tidak.</td>
</tr><tr>
<td>-31003</td>
<td>ID streaming output tidak sesuai dengan ID streaming di `session`</td>
<td>Periksa ID streaming output yang dimasukkan ketika campuran streaming dibatalkan.</td>
</tr><tr>
<td>-31004</td>
<td>Bitrate streaming output tidak valid</td>
<td>Periksa bitrate streaming output berada dalam rentang [1.50000] atau tidak.</td>
</tr><tr>
<td>Lainnya</td>
<td>Untuk kesalahan lainnya, silakan <a href="https://cloud.tencent.com/act/event/connect-service">hubungi layanan pelanggan</a> untuk mendapatkan bantuan.</td>
<td>-</td>
</tr>
</tbody></table>

## Pertanyaan Umum
- [Bagaimana cara memastikan bahwa skala streaming input dapat diatur secara otomatis tanpa bilah hitam di gambar video selama campuran streaming?](https://intl.cloud.tencent.com/document/product/267/38255)
- [Apa yang harus dilakukan jika kode kesalahan -505 ditampilkan untuk campuran streaming setelah push?](https://intl.cloud.tencent.com/document/product/267/38255)
- [Apa saja risiko yang akan terjadi jika campuran streaming tidak dibatalkan setelah diajukan?](https://intl.cloud.tencent.com/document/product/267/38255)
- [Mengapa gambar video host asisten dalam streaming campuran tidak berada di posisi yang diperkirakan?](https://intl.cloud.tencent.com/document/product/267/38255)

>? Pertanyaan Umum lebih lanjut tentang campuran streaming dapat dilihat di [On-cloud Stream Mix (Campuran Streaming di Cloud)](https://intl.cloud.tencent.com/document/product/267/38255).





