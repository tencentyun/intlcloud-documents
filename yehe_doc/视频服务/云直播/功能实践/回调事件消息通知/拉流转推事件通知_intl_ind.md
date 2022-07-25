Panggilan balik relai digunakan untuk memanggil balik informasi status tugas relai. Anda harus mengonfigurasikan alamat panggilan balik di tugas relai dan selanjutnya backend CSS Tencent Cloud akan memanggil balik berbagai hasil ke server yang sudah ditentukan.

Dokumen ini menjelaskan berbagai parameter dalam pemberitahuan pesan panggilan balik yang dikirim oleh CSS Tencent Cloud setelah peristiwa panggilan balik push/interupsi streaming terpicu.

 

## Catatan

Anda harus memahami cara mengonfigurasikan panggilan balik dan cara menerima pesan melalui CSS Tencent Cloud sebelum membaca dokumen ini. Informasi selengkapnya dapat dilihat di [How to Receive Event Notification (Cara Menerima Pemberitahuan Peristiwa)](https://intl.cloud.tencent.com/document/product/267/38080).

 

## Parameter Peristiwa Relai

### Parameter jenis peristiwa

| Jenis Peristiwa | Nilai Parameter |
| :------- | :--------------- |
| Relay | event_type = 314 |


### Parameter panggilan balik umum

| Parameter    | Jenis   | Deskripsi                                                                                                                    |
| ---------------  | ----------- | ----------- |
| appId      | int    | `APPID` Pengguna                                  |
| callback_event  | string     | Jenis peristiwa panggilan balik           |
| source_urls     | string     | URL sumber pull            |
| to_url          | string     | URL tujuan push           |
| stream_id    | string | Nama streaming langsung                  |
| task_id | string | ID Tugas |
| [msg](#msg)     | string           | Detail panggilan balik berbagai jenis peristiwa |

[](id:msg)
#### Parameter dalam `msg`

| Parameter    | Jenis   | Deskripsi        |
| ---------------  | ----------- | ----------- |
| task_start_time  | int        | Stempel waktu dimulainya tugas, dalam milidetik   |
| url              | string     | URL sumber untuk tugas pull saat ini      |
| index            | string     | Indeks daftar untuk file sesuai permintaan     |
| duration         | int        | Durasi file sesuai permintaan, dalam detik        |
| task_exit_time   | int       | Stempel waktu berhentinya tugas, dalam milidetik |
| code             | string       | Kode kesalahan berhentinya tugas |
| message          | string     | Pesan kesalahan berhentinya tugas         |

### Pesan panggilan balik sampel

#### `TaskStart` - Panggilan balik peristiwa dimulainya tugas
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "TaskStart",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"task_start_time\":0}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_230753472*****21162358-upload-45eb/playlist.m3u8\"]\n",
    
    "stream_id": "testvod",
    
    "task_id": "118148",
    
    "to_url": "rtmp://5000.livepush.myqcloud.com/live/testvod"
}
:::
</dx-codeblock>

#### `VodSourceFileStart` - Panggilan balik mulai file sesuai permintaan
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "VodSourceFileStart",
    
    "callback_url": "http://you.callback.url",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"url\":\"http://remit-tx-ugcpub.douyucdn2.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\",\"index\":0,\"duration\":14920}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\"]\n",
    
    "stream_id": "testvod",
    
    "task_id": "118145",
    
    "to_url": "rtmp://5000.livepush.myqcloud.com/live/testvod"
}
:::
</dx-codeblock>


#### `VodSourceFileFinish` - Panggilan balik akhir file sesuai permintaan
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "VodSourceFileFinish",
    
    "callback_url": "http://you.callback.url",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"url\":\"http://yourURL.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\",\"index\":0,\"duration\":14920}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\"]\n",
    
    "stream_id": "testvod",
    
    "task_id": "118145",
    
    "to_url": "rtmp://5000.livepush.myqcloud.com/live/testvod"
}
:::
</dx-codeblock>

#### `TaskExit` - Panggilan balik peristiwa berhentinya tugas
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "TaskExit",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"message\":\"write packet error.\",\"code\":-22,\"task_exit_time\":0}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_230753472*****21162358-upload-4\"]\n"
}
:::
</dx-codeblock>

>!
>- Urutan panggilan balik untuk tugas relai dengan “Video sesuai permintaan” sebagai konten sumber: `TaskStart` - Panggilan balik peristiwa dimulainya tugas > `VodSourceFileStart` - Panggilan balik dimulainya file sesuai permintaan > `VodSourceFileFinish` - Panggilan balik berakhirnya file sesuai permintaan.
>- Ada interval **hingga 2 detik** antara panggilan balik `TaskStart` dan `VodSourceFileStart`.
>- Pengaturan panggilan balik tercantum dalam konfigurasi tugas relai. Petunjuk mendetail dapat dilihat di [Relai](https://intl.cloud.tencent.com/zh/document/product/267/2818).


