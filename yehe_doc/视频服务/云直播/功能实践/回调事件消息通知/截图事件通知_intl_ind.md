Pengambilan tangkapan layar langsung mengambil tangkapan layar real-time dari streaming langsung dengan interval tertentu dan menyimpannya dalam COS. Panggilan balik pengambilan tangkapan layar menampilkan informasi tentang tangkapan layar yang disimpan, yang meliputi waktu pembuatan tangkapan layar, ukuran gambar, jalur file, dan tautan pengunduhan. Untuk menerima panggilan balik pengambilan tangkapan layar, Anda harus mengonfigurasikan alamat server di templat panggilan balik dan mengikat templat tersebut dengan domain push Anda. Ketika terjadi peristiwa pengambilan tangkapan layar langsung, backend CSS akan mengirimkan informasi tangkapan layar ke server yang telah dikonfigurasikan.

Dokumen ini menjelaskan bidang-bidang yang terdapat dalam pesan panggilan balik pengambilan tangkapan layar langsung.

## Catatan

- Dokumen ini menganggap Anda sudah mengetahui cara mengonfigurasikan dan [menerima](https://intl.cloud.tencent.com/document/product/267/38080) panggilan balik.
- Informasi yang ditampilkan oleh panggilan balik pengambilan tangkapan layar dapat digunakan untuk deteksi pornografi, pembuatan thumbnail video langsung, dan skenario lainnya.

## Parameter Peristiwa Pengambilan Tangkapan Layar
### Jenis peristiwa

| Jenis Peristiwa | Nilai           |
| :------- | :------------- |
| Pengambilan tangkapan layar langsung | event_type = 200 |

### Parameter panggilan balik umum
<table>
<tr><th>Parameter</th><th>Jenis</th><th>Deskripsi</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>Waktu kedaluwarsa, yaitu stempel waktu Unix yang menunjukkan waktu kedaluwarsa tanda tangan pemberitahuan peristiwa. <ul style="margin:0"><li>Periode validitas default pemberitahuan pesan dari Tencent Cloud adalah 10 menit. Jika waktu yang ditetapkan oleh nilai `t` dalam sebuah pemberitahuan pesan sudah berlalu, pemberitahuan ini dianggap tidak valid sehingga mencegah serangan pemutaran ulang jaringan. <li>Nilai `t` adalah stempel waktu Unix desimal, yaitu jumlah detik yang sudah berlalu sejak 00.00.00 (waktu UTC/GMT), 1 Januari 1970.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>Tanda tangan keamanan = MD5(key + t). <br>Tencent Cloud menyambungkan enkripsi <a href="#key">kunci</a> dan `t`, menghasilkan hash MD5 untuk string yang disambung, dan menyematkannya di pesan panggilan balik. Server backend Anda dapat melakukan perhitungan yang sama ketika menerima pesan panggilan balik. Jika tanda tangan cocok, artinya pesan berasal dari Tencent Cloud.</td>
</tr></table>

>? Kunci digunakan untuk autentikasi. Anda dapat mengatur kunci di **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)** (Pusat Peristiwa > Panggilan Balik Streaming Langsung). Anda sebaiknya mengatur kunci untuk memastikan keamanan data.

![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### Parameter pesan panggilan balik

| Parameter | Jenis   | Deskripsi           |
| :----------- | :----- | :-------------------------- |
| app           | string | Nama domain push         |
| appname       | string | Jalur push           |
| stream_param  | string | Parameter URL push                                        |
| stream_id    | string | Nama streaming langsung                  |
| channel_id   | string | Sama dengan nama streaming                |
| create_time | int64 | Stempel waktu Unix yang menunjukkan waktu pembuatan tangkapan layar |
| file_size    | int    | Ukuran file tangkapan layar dalam byte    |
| width        | int    | Lebar tangkapan layar dalam piksel           |
| height       | int    | Tinggi tangkapan layar dalam piksel        |
| pic_url      | string | Jalur file tangkapan layar (`/path/name.jpg`) |
| pic_full_url | string | URL pengunduhan tangkapan layar                 |

### Pesan panggilan balik sampel
<dx-codeblock>
::: json json
{
    "app":"test.app",
		
    "appname":"live",
    	
    "channel_id":"your_channelid",
    	
    "create_time":1622599925,
    	
    "event_type":200,
    	
    "file_size":30670,
    	
    "height":720,
    
    "pic_full_url":"http://your.cos.region.myqcloud.com/channelid/channelid-screenshot-10-12-05-1280x720.jpg",
    	
    "pic_url":"/channelid/channelid-screenshot-10-12-05-1280x720.jpg",
    	
    "sign":"ca3e25e5dc17a6f9909a9ae7281e300d",
    	
    "stream_id":"your_streamid",
    	
    "stream_param":"txSecret=ca3e25e5dc17a6f9909a9ae7281e300d&txTime=60B83800",
    	
    "t":1622600525,
    	
    "width":1280
}
:::
</dx-codeblock>










