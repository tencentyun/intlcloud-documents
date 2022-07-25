CSS mendukung panggilan balik. Untuk menggunakan fitur ini, Anda perlu membuat templat panggilan balik di konsol, mengonfigurasikan alamat untuk menerima panggilan balik untuk suatu peristiwa, kemudian mengikat templat dengan nama domain push Anda. Jika peristiwa yang dikonfigurasikan dalam templat memicu panggilan balik selama streaming langsung, Tencent Cloud akan mengirimkan permintaan ke server Anda, yang bertanggung jawab untuk merespons permintaan tersebut. Setelah verifikasi berhasil, server akan mendapatkan paket JSON panggilan balik melalui alamat yang dikonfigurasikan untuk peristiwa tersebut.
Dokumen ini menjelaskan cara membuat, memodifikasi, dan menghapus templat panggilan balik di konsol. 

**Anda dapat membuat templat panggilan balik dengan cara berikut:**
- Membuat templat di konsol CSS. Penjelasan lebih lanjut dapat dilihat di [Membuat Templat Panggilan Balik](#Callback).
- Membuat templat dengan API. Detail tentang parameter dan sampel tertentu dapat dipelajari di [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815).


## Catatan

- Setelah membuat templat, Anda perlu [mengikatnya dengan nama domain push](https://intl.cloud.tencent.com/document/product/267/31065). Pengikatan akan diterapkan dalam waktu sekitar 5‒10 menit.
- Server HTTP atau HTTPS, yang alamatnya dikonfigurasikan sebagai alamat panggilan balik di templat untuk menerima panggilan balik, harus dapat menerima permintaan dan merespons secara normal.
- Di konsol, Anda dapat mengelola templat panggilan balik berdasarkan nama domain, tetapi tidak dapat membatalkan aturan yang dibuat oleh API. Jika Anda mengikat templat dengan streaming tertentu melalui API panggilan balik dan ingin melepaskan ikatan tersebut, Anda perlu memanggil API [DeleteLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30814).
- Informasi selengkapnya tentang protokol panggilan balik streaming langsung dapat dilihat di [Event Message Notification Protocol (Protokol Pemberitahuan Pesan Peristiwa)](https://intl.cloud.tencent.com/document/product/267/38080).
- Informasi selengkapnya tentang parameter pemberitahuan panggilan balik streaming langsung dapat dilihat di referensi berikut:
 - [Push event notification (Pemberitahuan peristiwa push)](https://intl.cloud.tencent.com/document/product/267/38081)
 - [Stream interruption event notification (Pemberitahuan peristiwa interupsi streaming)](https://intl.cloud.tencent.com/document/product/267/38081)
 - [Recording event notification (Pemberitahuan peristiwa perekaman)](https://intl.cloud.tencent.com/document/product/267/38082)
 - [Screencapture event notification (Pemberitahuan peristiwa pengambilan tangkapan layar)](https://intl.cloud.tencent.com/document/product/267/38083)
 - [Porn detection event notification (Pemberitahuan peristiwa deteksi pornografi)](https://intl.cloud.tencent.com/document/product/267/38084)




## Membuat Templat Panggilan Balik[](id:Callback)
1. Login ke [konsol CSS](https://console.cloud.tencent.com/live).
2. Pilih **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)** (Pusat Peristiwa > Panggilan Balik Streaming Langsung) di bilah sisi kiri.
3. Klik **Create Callback Template** (Buat Templat Panggilan Balik), isi informasi, pilih jenis panggilan balik yang ingin Anda terima, masukkan URL panggilan balik, dan klik **Save** (Simpan).
![](https://qcloudimg.tencent-cloud.cn/raw/f8418ac2c646c3461d95d7fab157f2f3.png)
<table>
<thead><tr><th width="17%">Item Konfigurasi</th><th>Deskripsi</th></tr></thead><tbody><tr>
<td>Template Name (Nama Templat)</td>
<td>Nama templat panggilan balik, yang dapat berisi hingga 30 huruf, angka, garis bawah (_), dan tanda hubung (-).</td>
</tr><tr>
<th>Template Description (Deskripsi Templat)</th>
<td>Deskripsi templat panggilan balik, yang dapat berisi hingga 100 huruf, angka, garis bawah (_), dan tanda hubung (-).</td>
</tr><tr>
<td>Callback Key (Kunci Panggilan Balik)</td>
<td>Kunci panggilan balik kustom. <br>Kunci ini dapat berisi hingga 32 huruf, angka, garis bawah (_), dan tanda hubung (-). Informasi lebih lanjut dapat dilihat di <a href="https://intl.cloud.tencent.com/document/product/267/38081#.E5.9B.9E.E8.B0.83.E5.85.AC.E5.85.B1.E5.8F.82.E6.95.B0">Parameter Umum Pemberitahuan Pesan Peristiwa</a>.</td>
</tr><tr>
<td>Push Callback (Panggilan Balik Push)</td>
<td>Masukkan alamat yang diawali dengan `http`, `https`, dll. untuk menerima panggilan balik push.</td>
</tr><tr>
<td>Interruption Callback (Panggilan Balik Gangguan)</td>
<td>Masukkan alamat yang diawali dengan `http`, `https`, dll. untuk menerima panggilan balik gangguan streaming.</td>
</tr><tr>
<td>Recording Callback (Panggilan Balik Perekaman)</td>
<td>Masukkan alamat yang diawali dengan `http`, `https`, dll. untuk menerima panggilan balik perekaman.</td>
</tr><tr>
<td>Screencapture Callback (Panggilan Balik Pengambilan Tangkapan Layar)</td>
<td>Masukkan alamat yang diawali dengan `http`, `https`, dll. untuk menerima panggilan balik pengambilan tangkapan layar.</td>
</tr><tr>
<td>Porn Detection Callback (Panggilan Balik Deteksi Pornografi)</td>
<td>Masukkan alamat yang diawali dengan `http`, `https`, dll. untuk menerima panggilan balik deteksi pornografi.</td>
</tr>
</tbody></table>



## Memodifikasi Templat Panggilan Balik[](id:change)

1. Pilih **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)** (Pusat Peristiwa > Panggilan Balik Streaming Langsung).
2. Pilih templat panggilan balik target, lalu klik **Edit** untuk memodifikasi informasi templat.
3. Setelah modifikasi selesai, klik **Save** (Simpan).

![](https://qcloudimg.tencent-cloud.cn/raw/6350e65d695ece9c075dd3e053c1aeca.png)


## Menghapus Templat Panggilan Balik[](id:delete)

Jika suatu templat sudah terikat ke nama domain tertentu, Anda harus melepaskan ikatan templat terlebih dahulu agar dapat menghapus templat. Petunjuk mendetail dapat dilihat di [Unbinding Callback Template (Melepaskan Ikatan Templat Panggilan Balik)](https://intl.cloud.tencent.com/document/product/267/31065#untie).

1. Pilih **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)** (Pusat Peristiwa > Panggilan Balik Streaming Langsung).
2. Temukan templat panggilan balik target, lalu klik **Delete** (Hapus).
3. Di jendela pop-up, klik **Confirm** (Konfirmasi).

![](https://qcloudimg.tencent-cloud.cn/raw/9cc8d3a6c82a8b54ae904ddcc9ca01f6.png)

