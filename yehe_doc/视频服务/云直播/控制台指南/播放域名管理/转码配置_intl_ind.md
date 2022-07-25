Pemutaran ulang CSS adalah output untuk bitrate asli secara default. Jika ingin membatasi atau mengatur bitrate pemutaran ulang, Anda dapat mengaitkan nama domain pemutaran ulang dengan templat transcoding. Dokumen ini menjelaskan cara mengaitkan/membatalkan kaitan nama domain pemutaran ulang dengan/dari templat transcoding.

## Catatan
- Konfigurasi templat diterapkan dalam waktu sekitar 5‒10 menit.
- Setelah Anda menentukan templat transcoding, backend akan membuat URL pemutaran ulang yang sesuai dengan berbagai bitrate. Resolusi asli streaming akan mengikuti rasio aspek video sumber sebanyak mungkin untuk menghindari distorsi gambar.
- Karena kompatibilitas H.265 tidak sama seperti H.264, jika pemutar tidak mendukung H.265 dan pemutaran ulang gagal dilakukan, Anda dapat mengonfigurasikan [templat transcoding](https://intl.cloud.tencent.com/document/product/267/31071) untuk melakukan transcoding pada video menjadi H.264 untuk pemutaran ulang.
- Pemuatan biasanya membutuhkan waktu lebih lama untuk pengguna akhir yang pertama kali memicu URL untuk bitrate baru.
- Satu nama domain dapat diikat ke beberapa templat transcoding. Setelah nama domain terikat, transcoding akan dilakukan pada bitrate pemutaran ulang sesuai dengan templat transcoding yang terikat.
- Anda dapat membuat hingga **50** templat transcoding.



## Prasyarat
- Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live) dan menambahkan [nama domain pemutaran ulang](https://intl.cloud.tencent.com/document/product/267/35970).
- Anda telah membuat [templat transcoding](https://intl.cloud.tencent.com/document/product/267/31071).

[](id:conect)
## Mengikat Templat Transcoding
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) dan klik nama domain pemutaran ulang yang akan dikonfigurasikan atau **Manage** (Kelola) di sebelah kanan untuk membuka halaman detail domain.
2. Pilih **Template Configuration** (Konfigurasi Templat), dan klik **Edit** di sudut kanan atas tab **Transcoding Configuration** (Konfigurasi Transcoding).
3. Pilih templat transcoding dengan codec dan bitrate yang diinginkan untuk URL pemutaran ulang di nama domain tersebut.
4. Klik **Confirm** (Konfirmasi).

![](https://qcloudimg.tencent-cloud.cn/raw/2d8cb5be76debfbd04d60329891c5830.png)

[](id:descript)
## Catatan tentang URL Pemutaran Ulang
Setelah konfigurasi templat transcoding selesai, tambahkan namanya di URL pemutaran ulang dalam format **playback URL_transcoding template name** (URL pemutaran ulang_nama templat transcoding). Jika penambahan tidak dilakukan, streaming langsung asli akan diputar ulang. Informasi selengkapnya tentang URL pemutaran ulang dapat dilihat di [Playback Configuration (Konfigurasi Pemutaran Ulang)](https://intl.cloud.tencent.com/document/product/267/31058).

Misalnya, nama templat transcoding yang terikat dengan nama domain pemutaran ulang adalah **hd**, dan URL pemutaran ulang aslinya adalah:
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
URL berikut perlu dibuat untuk memutar ulang video yang di-transcoding:
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>

[](id:Untie)
## Melepaskan Ikatan Templat Transcoding
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), klik nama domain pemutaran ulang yang akan dikonfigurasikan atau **Manage** (Kelola) di sebelah kanan untuk membuka halaman detail domain.
2. Pilih **Template Configuration** > **Transcoding Configuration** (Konfigurasi Templat > Konfigurasi Transcoding).
3. Klik **Edit** di sebelah kanan, lalu hapus tanda centang di templat yang sesuai.
4. Klik **Confirm** (Konfirmasi) untuk membatalkan kaitan templat dari nama domain.
![](https://qcloudimg.tencent-cloud.cn/raw/872b71589554e8d89abf50db40f75777.png)

>? Untuk menghapus templat, Anda harus membatalkan kaitan templat terlebih dahulu, lalu buka **Feature Template** > **[Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode)** (Templat Fitur > Konfigurasi Transcoding) untuk menghapus templat. Informasi selengkapnya dapat dilihat di [Transcoding Configuration (Konfigurasi Transcoding)](https://intl.cloud.tencent.com/document/product/267/31071#delect).
