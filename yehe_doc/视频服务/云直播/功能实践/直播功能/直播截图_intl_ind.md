


Fitur pengambilan tangkapan layar langsung mengambil tangkapan layar streaming langsung secara real-time dengan interval yang teratur dan menghasilkan gambar. Anda dapat memperoleh informasi tangkapan layar melalui pemberitahuan panggilan balik. Tangkapan-tangkapan layar ini memiliki beragam penggunaan, seperti deteksi pornografi dan thumbnail.

## Proses Pengambilan Tangkapan Layar Langsung
![](https://qcloudimg.tencent-cloud.cn/raw/c0412cf3d639a0f9804a7fc08373a9de.png)

Detail lengkap proses:
1. Mengonfigurasi fitur pengambilan tangkapan layar langsung di konsol atau melalui API TencentCloud.
2. Memulai push langsung. 
3. Layanan pengambilan tangkapan layar membuat data tangkapan layar berdasarkan konfigurasi dan menyimpannya di COS.
4. Informasi tentang tangkapan layar yang dibuat ditampilkan di panggilan balik.

## Konfigurasi Pengambilan Tangkapan Layar Langsung

### Metode konfigurasi pengambilan tangkapan layar
- [API CSS](https://intl.cloud.tencent.com/document/product/267/30760#.E6.88.AA.E5.9B.BE.E9.89.B4.E9.BB.84.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3)
- **CSS console** > **Feature Configuration** > **[Live Screencapture and Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)** (konsol CSS > Konfigurasi Fitur > Pengambilan Tangkapan Layar dan Deteksi Pornografi Langsung)

### Konfigurasi interval pengambilan tangkapan layar

Anda dapat menetapkan frekuensi pengambilan tangkapan layar berdasarkan kebutuhan bisnis, dengan mengatur interval pengambilan tangkapan layar (SnapshotInterval). Tersedia rentang antara 5–300 detik dengan interval default 10 detik.

### Konfigurasi lebar dan tinggi tangkapan layar

Layanan pengambilan tangkapan layar mendukung pengambilan tangkapan layar berdasarkan lebar dan tinggi yang ditetapkan:

 ![](https://main.qcloudimg.com/raw/86e3ce12a58b5125cca87a2d19ff922f.png)

>! Jika lebar dan tinggi tidak perlu ditetapkan, lebar dan tinggi tangkapan layar default (diatur ke 0) akan menggunakan lebar dan tinggi streaming video yang di-push sehingga Anda dapat mengabaikan petunjuk konfigurasi di bawah ini dan melompat ke bagian berikutnya.

Pertama, perhatikan tiga konsep lebar dan tinggi berikut:

- Lebar dan tinggi push, yaitu lebar dan tinggi video streaming langsung, yang diatur ke (X, Y) dalam dokumen ini.
- Lebar dan tinggi terkonfigurasi, yaitu lebar dan tinggi yang dikonfigurasikan di konsol/melalui API TencentCloud, yang diatur ke (W, H) dalam dokumen ini.
- Lebar dan tinggi tangkapan layar, yaitu lebar dan tinggi tangkapan layar yang dibuat layanan pengambilan tangkapan layar, yang diatur ke (N, M) dalam dokumen ini.

Layanan pengambilan tangkapan layar mendukung konfigurasi berikut:

- Jika tidak ada lebar dan tinggi yang ditetapkan, (W, H) = (0, 0) digunakan secara default. Lebar dan tinggi tangkapan layar sama dengan lebar dan tinggi push, yaitu (N, M) = (X, Y).
- Jika hanya lebar W yang diatur, lebar tangkapan layar akan menjadi N = W, dan tinggi tangkapan layar akan menyesuaikan secara berbanding lurus, yaitu M = N/X \* Y.
- Jika hanya tinggi H yang diatur, tinggi tangkapan layar akan menjadi M = H, dan lebar tangkapan layar akan menyesuaikan secara berbanding lurus, yaitu N = M/Y \* X.
- Jika (W, H) diatur pada waktu bersamaan, lebar dan tinggi tangkapan layar sama dengan lebar dan tinggi terkonfigurasi, yaitu (N, M) = (W, H).

Pertukaran otomatis lebar dan tinggi terkonfigurasi sesuai untuk skenario berikut:

- Jika W diatur lebih kecil dari H, nilai W dan H lebih besar dari 0, dan jika X diatur lebih besar dari Y selama push, lebar terkonfigurasi lebih kecil dari tinggi, tetapi lebar push lebih besar dari tinggi.

Dalam kasus ini, jika tangkapan layar diambil secara langsung, hasilnya akan mengalami distorsi. Untuk mencegah distorsi, backend layanan pengambilan tangkapan layar langsung akan secara otomatis menukar nilai W dan H untuk memastikan rasio aspek konfigurasinya sesuai dengan rasio aspek konfigurasi streaming langsung.


## Pemberitahuan Pesan Peristiwa untuk Pengambilan Tangkapan Layar Langsung

Penjelasan seputar konfigurasi pemberitahuan pesan peristiwa dapat dipelajari di [Pemberitahuan Pesan Peristiwa](https://intl.cloud.tencent.com/document/product/267/31566). Pemberitahuan panggilan balik pengambilan tangkapan layar dikirim ke server penerima yang sudah dikonfigurasikan sebelumnya melalui protokol HTTP POST dalam format JSON.

### Bidang panggilan balik pengambilan tangkapan layar

| Nama Bidang | Jenis | Deskripsi |
| --- | --- | --- |
| event\_type | int | Jenis informasi panggilan balik, yaitu selalu 200 untuk panggilan balik pengambilan tangkapan layar |
| stream\_id | string | Nama streaming |
| channel\_id | string | Sama dengan nama streaming |
| create\_time | int64 | Stempel waktu Unix pengambilan tangkapan layar |
| file\_size | int | Ukuran file tangkapan layar dalam byte |
| width | int | Lebar tangkapan layar dalam piksel |
| height | int | Tinggi tangkapan layar dalam piksel |
| pic\_url | string | Jalur file tangkapan layar /path/name.jpg. Informasi selengkapnya dapat dilihat di [Detail bidang](#jump) di bawah |
| pic\_full\_url | string | URL tangkapan layar utuh. Informasi selengkapnya dapat dilihat di [Detail bidang](#jump) di bawah |
| sign | string | Tanda tangan panggilan balik. Informasi lebih lanjut dapat dilihat di [Pemberitahuan Pesan Peristiwa](https://intl.cloud.tencent.com/document/product/267/31566) |
| t | int64 | Stempel waktu UNIX yang menunjukkan waktu kedaluwarsa tanda tangan panggilan balik. Informasi lebih lanjut dapat dilihat di [Pemberitahuan Pesan Peristiwa](https://intl.cloud.tencent.com/document/product/267/31566) |

### <span id="jump">Detail bidang</span>
- Detail `pic_url`:
 - jalur: tahun-bulan-hari
 - nama: live stream name-screenshot-jam-menit-detik-lebarxtinggi.jpg
 Contoh:
```
 /2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg
```
Bidang ini dapat digunakan untuk menghimpun nama domain COS CDN kustom. Jika Anda tidak membutuhkan nama domain CDN, gunakan pic_full_url secara langsung.

- Detail `pic_full_url`:
 - http://COS domain name+pic_url
	Contoh:
```
	http://testbucket-1234567890.cos.region.myqcloud.com/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg
```


### Panggilan balik pengambilan tangkapan layar sampel

```
{

"event_type":200,

"stream_id":"stream_name",

"channel_id":"stream_name",

"create_time":1545030273,

"file_size":7520,

"width":640,

"height":352,

"pic_url":"/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"pic_full_url":"http://testbucket-1234567890.cos.region.myqcloud.com/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873

}
```
