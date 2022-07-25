Fitur perekaman langsung merekam gambar streaming langsung secara real-time sesuai dengan templat perekaman yang terikat dengan nama domain push, lalu menyimpan file rekaman tersebut dalam VOD. Panggilan balik perekaman digunakan untuk melakukan push pada informasi file rekaman, yang meliputi waktu mulai dan waktu berakhir perekaman, serta ID, ukuran, dan URL pengunduhan file rekaman. Anda harus mengonfigurasikan alamat server untuk menerima pesan panggilan balik perekaman di templat panggilan balik, lalu mengikatkan templat dengan nama domain push. Ketika peristiwa perekaman dipicu oleh streaming langsung, backend CSS Tencent Cloud akan memanggil balik informasi file rekaman tersebut ke server penerima yang sudah dikonfigurasikan.

Dokumen ini menjelaskan bidang-bidang di pemberitahuan pesan panggilan balik yang dikirim oleh CSS Tencent Cloud setelah peristiwa panggilan balik perekaman terpicu.

## Catatan

- Anda harus memahami cara mengonfigurasikan panggilan balik dan cara menerima pesan melalui CSS Tencent Cloud sebelum membaca dokumen ini. Informasi selengkapnya dapat dilihat di [How to Receive Event Notification (Cara Menerima Pemberitahuan Peristiwa)](https://intl.cloud.tencent.com/document/product/267/38080).
- File video rekaman disimpan di [konsol VOD](https://console.cloud.tencent.com/vod/overview) secara default. Anda harus mengaktifkan layanan VOD terlebih dahulu dan memastikan layanan VOD tidak menunggak pembayaran.
- Ketika Anda memanggil API [CreateRecordTask](https://intl.cloud.tencent.com/zh/document/product/267/37309), parameter [stream_param](#message) yang terbawa dalam URL push pengguna tidak akan ditampilkan dalam panggilan balik perekaman. Namun, jika Anda menggunakan metode perekaman lain, parameter tersebut akan ditampilkan dalam panggilan balik perekaman.
- Setelah pelanjutan perekaman HLS diaktifkan, panggilan balik tidak akan ditampilkan untuk interupsi push, tetapi panggilan balik untuk file yang dihasilkan terakhir akan ditampilkan.


## Parameter Peristiwa Perekaman
### Parameter jenis peristiwa

| Jenis Peristiwa | Nilai Parameter           |
| :------- | :------------- |
| Perekaman langsung | event_type = 100 |

[](id:public)
### Parameter panggilan balik umum
<table>
<tr><th>Parameter</th><th>Jenis</th><th>Deskripsi</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>Waktu kedaluwarsa, yaitu stempel waktu Unix yang menunjukkan waktu kedaluwarsa tanda tangan pemberitahuan peristiwa. <ul style="margin:0"><li>Periode validitas default pemberitahuan pesan dari Tencent Cloud adalah 10 menit. Jika waktu yang ditetapkan oleh nilai `t` dalam sebuah pemberitahuan pesan sudah berlalu, pemberitahuan ini dianggap tidak valid sehingga mencegah serangan pemutaran ulang jaringan. <li>Format `t` adalah stempel waktu Unix desimal, yaitu jumlah detik yang sudah berlalu sejak 00.00.00 (waktu UTC/GMT), 1 Januari 1970.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>Tanda tangan keamanan pemberitahuan peristiwa = MD5(key + t). <br>Catatan: Tencent Cloud menggabungkan enkripsi <a href="#key">kunci</a> dan `t`, menghitung nilai `sign` melalui MD5, dan menempatkannya di pesan pemberitahuan. Ketika menerima pesan pemberitahuan, server backend Anda dapat mengonfirmasi kebenaran `sign` berdasarkan algoritme yang sama dan kemudian mengetahui benar atau tidaknya pesan tersebut berasal dari backend Tencent Cloud.</td>
</tr></table>

>? [](id:key)Anda dapat mengatur kunci panggilan balik di **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)** (Pusat Peristiwa > Panggilan Balik Streaming Langsung), yang digunakan untuk autentikasi. Anda sebaiknya mengatur bidang ini untuk memastikan keamanan data.
![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

[](id:message)

### Parameter pesan panggilan balik

| Parameter | Jenis   | Deskripsi   |
| ----------- | ----------- | ----------- |
| appid        | int    | [APPID](https://console.cloud.tencent.com/developer) Pengguna                                           |
| app           | string | Nama domain push  |
| appname       | string | Jalur push |
| stream_id    | string | Nama streaming langsung               |
| channel_id   | string | Nilainya sama dengan nama streaming LVB                                         |
| file_id      | string | ID file VOD, yang mengidentifikasi secara unik file VOD di [platform VOD](https://intl.cloud.tencent.com/document/product/266/33895) |
| file_format  | string | Format file. Nilai yang valid: `flv`, `hls`, `mp4`, `aac` |
| task_id| string| ID tugas perekaman, yang hanya valid jika tugas dibuat menggunakan [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API |
| start_time   | int64  | Waktu ketika data mulai ditulis ke dalam file. Nilai tersebut tidak dapat disetarakan dengan waktu mulai konten yang direkam. Waktu mulai konten yang direkam = `end_time` − `duration` |
| end_time     | int64  | Waktu ketika data berhenti ditulis ke dalam file                                |
| duration     | int64  | Durasi file rekaman, dalam detik                                 |
| file_size    | uint64 | Ukuran file rekaman dalam piksel                               |
| stream_param  | string | Parameter URL push pengguna (kustom)                                      |
| video_url    | string | URL pengunduhan file rekaman                                 |



[](id:example)
### Pesan panggilan balik sampel
<dx-codeblock>
::: JSON JSON
{
"event_type":100,

"appid":12345678,

"app":yourapp,

"appname":yourappname,

"stream_id":"stream_test",

"channel_id":"stream_test",

"file_id":"1234567890",

"file_format":"hls",

"task_id":"UpTbk5RSVhRQ********************0xTSlNTQltlRVRLU1JAWW9EUb",

"start_time":1545047010,

"end_time":1545049971,

"duration":2962,

"file_size":277941079,

"stream_param":"stream_param=test",

"video_url":"http://12345678.vod2.myqcloud.com/xxxx/yyyy/zzzz.m3u8",

"sign":"ca3e25e**********09a9ae7281e300d",

"t":1545030873
}
:::
</dx-codeblock>



 

