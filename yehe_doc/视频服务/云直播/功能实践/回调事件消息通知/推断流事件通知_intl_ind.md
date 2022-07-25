Panggilan balik pushing streaming memberi tahu Anda apakah pushing streaming berhasil atau terganggu. Anda harus mengonfigurasikan alamat server untuk panggilan balik di templat panggilan balik dan mengikatkan templat tersebut dengan nama domain push Anda. Setelah push dimulai melalui URL yang dibuat berdasarkan domain tersebut, backend Tencent Cloud akan mengirimkan panggilan balik ke server yang Anda atur.

Dokumen ini menjelaskan berbagai parameter dalam pemberitahuan panggilan balik pushing streaming yang dikirim CSS kepada Anda.

## Catatan
Panduan ini menganggap Anda sudah mengetahui cara mengonfigurasi panggilan balik dan menerima pemberitahuan panggilan balik dari CSS. Informasi mendetail dapat dilihat di [How to Receive Event Notification (Cara Menerima Pemberitahuan Peristiwa)](https://intl.cloud.tencent.com/document/product/267/38080). 


## Parameter Peristiwa Pushing Streaming
### Jenis peristiwa

| Jenis Peristiwa | Nilai           |
|---------|---------|
| Push berhasil | event_type = 1 |
| Push terganggu | event_type = 0 |

### Parameter panggilan balik umum
<table>
<tr><th>Parameter</th><th>Jenis</th><th>Deskripsi</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>Waktu kedaluwarsa, yaitu stempel waktu Unix yang menunjukkan waktu kedaluwarsa tanda tangan pemberitahuan peristiwa. <ul style="margin:0"><li>Periode validitas default pemberitahuan panggilan balik dari Tencent Cloud adalah 10 menit. Jika waktu yang ditentukan oleh nilai `t` dalam pemberitahuan sudah berlalu, pemberitahuan ini akan dianggap tidak valid. Hal ini mencegah serangan pemutaran ulang jaringan. <li>Nilai `t` merupakan stempel waktu Unix desimal, yaitu jumlah detik yang telah berlalu sejak pukul 00.00.00 (waktu UTC/GMT) tanggal 1 Januari 1970.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>Tanda tangan keamanan = MD5(key + t). <br>Tencent Cloud menyambungkan enkripsi <a href="#key">kunci</a> dan `t`, menghasilkan hash MD5 untuk string yang disambung, dan menyematkannya di pesan panggilan balik. Server backend Anda dapat melakukan perhitungan yang sama ketika menerima pesan panggilan balik. Jika tanda tangan cocok, artinya pesan berasal dari Tencent Cloud.</td>
</tr></table>

>? [](id:key)Anda dapat mengatur kunci panggilan balik di **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)** (Pusat Peristiwa > Panggilan Balik Streaming Langsung), yang digunakan untuk autentikasi. Anda sebaiknya mengatur bidang ini untuk memastikan keamanan data.
![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### Parameter panggilan balik

| Parameter | Jenis   | Deskripsi           |
| :------------ | :----- | :----------------------------------------------------------- |
| appid        | int    | [APPID](https://console.cloud.tencent.com/developer) Pengguna      |
| app           | string | Nama domain push         |
| appname       | string | Jalur push           |
| stream_id     | string | Nama streaming langsung              |
| channel_id   | string | Sama dengan nama streaming langsung              |
| event_time    | int64  | Waktu stempel UNIX ketika pesan peristiwa dihasilkan               |
| sequence      | string | Jumlah urutan pesan, yang mengidentifikasi suatu push. Pemberitahuan untuk push, baik push yang berhasil maupun interupsi streaming, memiliki jumlah urutan yang sama. |
| node          | string |  IP titik akses streaming langsung                                              |
| user_ip       | string | IP push pengguna                                                  |
| stream_param  | string | Parameter URL push pengguna                                      |
| push_duration | string | Durasi push streaming yang terganggu dalam milidetik                               |
| errcode       | int    | Kode kesalahan pushing streaming                      |
| errmsg        | string | Pesan kesalahan pushing streaming                                               |
| set_id          | int  | Informasi bahwa push berasal dari Tiongkok Daratan atau tidak. 1‒6: ya; 7‒200: tidak.  |
|width       |  int   |Lebar video. Nilai parameter ini mungkin `0` jika informasi header video tidak ada di awal push.  |
|height       |  int   |Tinggi video. Nilai parameter ini mungkin `0` jika informasi header video tidak ada di awal push.  |

### Penyebab terganggunya streaming
Daftar penyebab terganggunya streaming dapat dilihat di [Stream Interruption Records (Rekaman Interupsi Streaming)](https://intl.cloud.tencent.com/document/product/267/31083).

### Panggilan balik sampel
```JSON
{
	"app":"test.domain.com",
	
	"appid":12345678,
	
	"appname":"live",
	
	"channel_id":"test_stream",
	
	"errcode":0,
	
	"errmsg":"ok",
	
	"event_time":1545115790,
	
	"event_type":1,
	
	"set_id":2,
	
	"node":"100.121.160.92",
	
	"sequence":"6674468118806626493",
	
	"stream_id":"test_stream",
	
	"stream_param":"stream_param=test",
	
	"user_ip":"119.29.94.245",
	
	"width": 0,
	
	"height": 0,
	
	"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",
	
	"t":1545030873
}
```
