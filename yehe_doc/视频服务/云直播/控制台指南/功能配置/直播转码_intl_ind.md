Transcoding langsung (termasuk transcoding video dan transcoding audio) merupakan proses konversi streaming asal yang di-push dari situs streaming langsung menjadi ke streaming dengan berbagai codec, resolusi, dan bitrate di dalam cloud sebelum streaming tersebut di-push kepada pemirsa. Transcoding langsung memenuhi kebutuhan pemutaran ulang di berbagai lingkungan jaringan di beragam perangkat. Dokumen ini menjelaskan cara membuat, mengikat, melepaskan ikatan, memodifikasi, dan menghapus templat transcoding melalui konsol CSS.

**Anda dapat membuat templat transcoding dengan dua cara:**

- Membuat templat transcoding di konsol CSS. Petunjuk mendetail dapat dilihat di [Membuat templat transcoding standar](#C_trans), [Membuat templat transcoding codec kecepatan tinggi](#C_topspeed), dan [Membuat templat transcoding audio saja](#C_audio).
- Membuat templat transcoding untuk saluran langsung dengan API. Detail tentang parameter dan sampel tertentu dapat dipelajari di [CreateLiveTranscodeTemplate](https://intl.cloud.tencent.com/document/product/267/30790).


## Catatan
- CSS mendukung transcoding standar, transcoding codec kecepatan tinggi, dan transcoding audio saja. Baca ikhtisar penagihan sebelum Anda menggunakan layanan ini.
   - [Live Transcoding > Standard Transcoding (Transcoding Langsung > Transcoding Standar)](https://intl.cloud.tencent.com/document/product/267/39604)
   - [Live Transcoding > Top Speed Codec Transcoding (Transcoding Langsung > Transcoding Codec Kecepatan Tinggi)](https://intl.cloud.tencent.com/document/product/267/39604)
- Dibandingkan dengan **transcoding standar**, **transcoding codec kecepatan tinggi** memberikan kualitas video yang lebih tinggi dengan bitrate yang lebih rendah. Dengan dukungan berbagai teknologi, termasuk pengenalan adegan cerdas, pengodean dinamis, dan kontrol bitrate level CTU/line/frame, transcoding codec kecepatan tinggi membantu Anda menyediakan layanan streaming dengan definisi lebih tinggi dan bitrate lebih rendah (rata-rata 30% lebih rendah). Transcoding codec kecepatan tinggi banyak digunakan untuk streaming game, pertunjukan, dan acara lainnya.
- Setelah membuat templat, Anda dapat mengikatnya dengan nama domain pemutaran ulang. Pengikatan akan diterapkan dalam waktu 5‒10 menit.
- Anda dapat menambahkan nama templat transcoding ke `StreamName` streaming langsung untuk membuat URL streaming yang di-transcoding. Jika Anda telah menentukan tinggi dan lebar atau sisi pendek dan panjang dari streaming yang di-transcoding, pertahankan resolusi asli sedekat mungkin dengan nilai yang ditetapkan guna mencegah distorsi gambar.
- Di halaman **Live Transcoding** (Transcoding Langsung) di konsol, Anda dapat melihat domain tempat templat diikat, serta pengikatan dengan perincian lebih halus yang dilakukan melalui API. Anda juga dapat [melepaskan ikatan](#untie) templat di sini.
- Anda dapat mengikat satu nama domain pemutaran ulang dengan **beberapa templat transcoding**, atau mengikat satu templat transcoding dengan **beberapa nama domain pemutaran ulang**.
- Anda dapat membuat hingga **50** templat transcoding.

[](id:create)
## Membuat Templat Transcoding
[](id:C_trans)
### Membuat templat transcoding standar

1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)** (Konfigurasi Fitur > Transcoding Langsung).
2. Klik **Create Transcoding Template** (Buat Templat Transcoding), pilih **Standard Transcoding** (Transcoding Standar) untuk jenis transcoding, dan selesaikan konfigurasi berikut:
  - Konfigurasi dasar: Nama templat, bitrate video, resolusi video, dan lainnya. Informasi selengkapnya dapat ditemukan di [Konfigurasi Dasar untuk Transcoding Standar](#C_trans_normal).
  - Konfigurasi lanjutan (opsional): Klik **Advanced Configuration** (Konfigurasi Lanjutan) untuk menampilkan pengaturan lanjutan. Informasi selengkapnya dapat ditemukan di [Konfigurasi Lanjutan untuk Transcoding Standar](#C_trans_high).
3. Klik **Save** (Simpan).

![](https://qcloudimg.tencent-cloud.cn/raw/a687312d5f0cb459a9684fe9f2de6459.png)

<table id="C_trans_normal">
<tr><th width="20%">Konfigurasi Dasar untuk Transcoding Standar</th><th>Diperlukan</th><th>Deskripsi</th></tr>
<tr>
<td>Transcoding Type (Jenis Transcoding)</td>
<td>Ya</td>
<td>Jenis transcoding, yang dapat berupa <b>transcoding standar</b>, transcoding codec kecepatan tinggi, atau transcoding audio saja.</td>
</tr><tr>
<td>Template Name (Nama Templat)</td>
<td>Ya</td>
<td>Nama templat transcoding langsung, yang harus terdiri dari 1‒10 karakter dan hanya boleh berisi huruf atau kombinasi angka dan huruf.</td>
</tr><tr>
<th>Template Description (Deskripsi Templat)</th>
<td>Tidak</td>
<td>Deskripsi templat transcoding langsung, yang hanya boleh berisi huruf, angka, garis bawah (_), dan tanda hubung (-).</td>
</tr><tr>
<td>Parameter yang Direkomendasikan</td>
<td>Tidak</td>
<td>Anda dapat memilih <b>Smooth (Halus), SD, atau HD</b>. Setelah Anda memilih nilai, sistem akan secara otomatis memasukkan bitrate dan tinggi video yang direkomendasikan, tetapi Anda dapat mengubahnya.</td>
</tr><tr>
<td>Bitrate Video<br>(dalam Kbps)</td>
<td>Ya</td>
<td>Rata-rata bitrate output. Rentang nilai: 100‒8000.<ul style="margin:0">
  <li>Nilai yang tidak melebihi 1.000 harus merupakan kelipatan 100.</li>
  <li>Nilai yang melebihi 1.000 harus merupakan kelipatan 500.</li></ul>
</td>
</tr><tr>
<td>Resolusi Video (px)</td>
<td>Ya</td>
<td>Default: <b>Set the height (Atur tinggi)</b>.<li>Nilai yang dimasukkan akan menjadi tinggi video yang di-transcoding. Anda juga dapat memilih <b>Set the short side length (Atur panjang sisi pendek)</b>, dan nilai yang dimasukkan akan menjadi sisi pendek video yang di-transcoding. <li>Rentang nilai: 0‒3000. Nilai harus merupakan kelipatan 2. Sisi lain akan disesuaikan secara otomatis.</td>
</tr></table>


<table id="C_trans_high">
<tr><th width="20%">Konfigurasi Lanjutan untuk Transcoding Standar</th><th>Diperlukan</th><th>Deskripsi</th></tr>
<tr>
<td>Codec</td>
<td>Tidak</td>
<td>Pengaturan default: Codec asli. Anda juga dapat memilih H.264 atau H.265.</td>
</tr><tr>
<td>Frame Rate Video (fps)</td>
<td>Tidak</td>
<td>Rentang nilai: 0‒60. Jika parameter ini dibiarkan kosong, `0` akan digunakan, yang artinya frame rate asli akan digunakan.</td>
</tr><tr>
<td>GOP<br>(dalam detik)</td>
<td>Tidak</td>
<td>Rentang nilai: 2‒6. Makin besar GOP, makin tinggi penundaan. Jika parameter ini dibiarkan kosong, nilai default akan digunakan.</td>
</tr><tr>
<td>Batas Parameter</td>
<td>Tidak</td>
<td>Dinonaktifkan secara default dan dapat diaktifkan secara manual.<br>Setelah batas diaktifkan, nilai asli streaming input akan digunakan jika Anda memasukkan nilai yang lebih besar dari nilai asli. Hal ini dapat mencegah masalah kualitas video akibat penggunaan pengaturan kualitas video yang tinggi untuk melakukan transcoding pada video berkualitas rendah.</td>
</tr></table>


   

[](id:C_topspeed)

### Membuat templat transcoding codec kecepatan tinggi
1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)** (Konfigurasi Fitur > Transcoding Langsung).
2. Klik **Create Transcoding Template** (Buat Templat Transcoding), pilih **Top Speed ​​Codec Transcoding** (Transcoding Codec Kecepatan Tinggi) untuk jenis transcoding, dan selesaikan konfigurasi berikut:
  - Konfigurasi dasar: Nama templat, bitrate video, resolusi video, dan lainnya. Informasi lebih lanjut dapat dipelajari di [Konfigurasi Dasar untuk Transcoding Codec Kecepatan Tinggi](#C_topspeed_normal).
  - Konfigurasi lanjutan (opsional): Klik **Advanced Configuration** (Konfigurasi Lanjutan) untuk menampilkan pengaturan lanjutan. Informasi lebih lanjut dapat dipelajari di [Konfigurasi Lanjutan untuk Transcoding Codec Kecepatan Tinggi](#C_topspeed_high).
3. Klik **Save** (Simpan).

![](https://qcloudimg.tencent-cloud.cn/raw/54a0334f1d24f7e0acb4e4f923b27d23.png)

<table  id="C_topspeed_normal">
<tr><th width="20%">Konfigurasi Dasar untuk Transcoding Codec Kecepatan Tinggi</th><th>Diperlukan</th><th>Deskripsi</th>
</tr><tr>
<td>Transcoding Type (Jenis Transcoding)</td>
<td>Ya</td>
<td>Jenis transcoding, yang dapat berupa transcoding standar, <b>transcoding codec kecepatan tinggi</b>, atau transcoding audio saja.</td>
</tr><tr>
<td>Template Name (Nama Templat)</td>
<td>Ya</td>
<td>Nama templat transcoding langsung, yang harus terdiri dari 2‒10 karakter dan hanya boleh berisi huruf atau kombinasi angka dan huruf.</td>
</tr><tr>
<th>Template Description (Deskripsi Templat)</th>
<td>Tidak</td>
<td>Deskripsi templat transcoding langsung, yang hanya boleh berisi huruf, angka, garis bawah (_), dan tanda hubung (-).</td>
</tr><tr>
<td>Parameter yang Direkomendasikan</td>
<td>Tidak</td>
<td>Anda dapat memilih <b>Smooth (Halus), SD, atau HD</b>. Setelah Anda memilih nilai, sistem akan secara otomatis memasukkan bitrate dan tinggi video yang direkomendasikan, tetapi Anda dapat mengubahnya.</td>
</tr><tr>
<td>Bitrate Video<br>(dalam Kbps)</td>
<td>Ya</td>
<td>Rata-rata bitrate output. Rentang nilai: 100‒8000. <li>Nilai yang tidak melebihi 1.000 harus merupakan kelipatan 100.</li><li>Nilai yang melebihi 1.000 harus merupakan kelipatan 500.</li></td>
</tr><tr>
<td>Resolusi Video</td>
<td>Ya</td>
<td>Default: <b>Set the height (Atur tinggi)</b>.<li>Nilai yang dimasukkan akan menjadi tinggi video yang di-transcoding. Anda juga dapat memilih <b>Set the short side length (Atur panjang sisi pendek)</b>, dan nilai yang dimasukkan akan menjadi sisi pendek video yang di-transcoding. </li><li>Rentang nilai: 0‒3000. Nilai harus merupakan kelipatan 2. Sisi lain akan disesuaikan secara otomatis.</li></td>
</tr>
</table>

<table  id="C_topspeed_high">
<tr><th width="20%">Konfigurasi Lanjutan untuk Transcoding Codec Kecepatan Tinggi</th><th>Diperlukan</th><th>Deskripsi</th>
</tr><tr>
<td>Codec</td>
<td>Tidak</td>
<td>Pengaturan default: Codec asli. Anda juga dapat memilih H.264 atau H.265.</td>
</tr><tr>
<td>Frame Rate Video (fps)</td>
<td>Tidak</td>
<td>Rentang nilai: 0‒60. Jika parameter ini dibiarkan kosong, `0` akan digunakan.</td>
</tr><tr>
<td>GOP<br>(dalam detik)</td>
<td>Tidak</td>
<td>Rentang nilai: 2‒6. Makin besar GOP, makin tinggi penundaan. Jika parameter ini dibiarkan kosong, nilai default akan digunakan.</td>
</tr><tr>
<td>Batas Parameter</td>
<td>Tidak</td>
<td><li/>Dinonaktifkan secara default dan dapat diaktifkan secara manual.<li/>Setelah batas diaktifkan, nilai asli streaming input akan digunakan jika Anda memasukkan nilai yang lebih besar dari nilai asli. Hal ini dapat mencegah masalah kualitas video akibat penggunaan pengaturan kualitas video yang tinggi untuk melakukan transcoding pada video berkualitas rendah.</td>
</tr></table>

[](id:C_audio)
### Membuat templat transcoding audio saja

1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)** (Konfigurasi Fitur > Transcoding Langsung).
2. Klik **Create Transcoding Template** (Buat Templat Transcoding), pilih **Audio-only Transcoding** (Transcoding Audio Saja) untuk jenis transcoding, selesaikan [konfigurasi](#C_audio_normal), lalu klik **Save** (Simpan).

![](https://qcloudimg.tencent-cloud.cn/raw/3cfe98bcc9f21c445e5db220a9ea0673.png)

<table id="C_audio_normal">
<tr><th width="20%">Konfigurasi Dasar untuk Transcoding Audio Saja</th><th>Diperlukan</th><th>Deskripsi</th></tr>
</tr><tr>
<td>Transcoding Type (Jenis Transcoding)</td>
<td>Ya</td>
<td>Jenis transcoding, yang dapat berupa transcoding standar, transcoding codec kecepatan tinggi, atau <strong>transcoding audio saja</strong>.</td>
</tr>
<tr>
<td>Template Name (Nama Templat)</td>
<td>Ya</td>
<td>Nama templat transcoding langsung, yang harus terdiri dari 1‒10 karakter dan hanya boleh berisi huruf atau kombinasi angka dan huruf.</td>
</tr>
<tr>
<th>Template Description (Deskripsi Templat)</th>
<td>Tidak</td>
<td>Deskripsi templat transcoding langsung, yang hanya boleh berisi huruf, angka, garis bawah (_), dan tanda hubung (-).</td>
</tr>
<tr>
<td>Audio Bitrate (Bitrate Audio) (Kbps)</td>
<td>Ya</td>
<td>Anda dapat <b>menggunakan bitrate audio asli</b> atau <b>mengatur bitrate kustom</b>. Rentang nilai: 101‒500.</td>
</tr>
</tbody></table>


[](id:related)
## Mengikat Nama Domain
1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)** (Konfigurasi Fitur > Transcoding Langsung).
2. Buka halaman pengikatan nama domain dengan salah satu cara berikut:
  - **Mengikat nama domain ke templat transcoding yang sudah ada**: Klik **Bind Domain Name** (Ikat Nama Domain) di kiri atas.
    ![](https://qcloudimg.tencent-cloud.cn/raw/7bcbc02fbc3ec3390ed16475b62482c5.png)
  - **Mengikat nama domain setelah membuat templat transcoding**: Setelah [membuat templat](#create), klik **Bind Domain Name** (Ikat Nama Domain) di jendela pop-up.
    ![](https://qcloudimg.tencent-cloud.cn/raw/2927d94d3e07f7344b6d740593265a0b.png)
3. Pilih templat transcoding dan nama domain pemutaran ulang di jendela pengikatan nama domain, lalu klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/1dc995d90d354e72613c699d59836f05.png)
>? Anda dapat mengeklik **Add** (Tambahkan) untuk mengikat beberapa nama domain pemutaran ulang ke satu templat.



[](id:untie)
## Melepaskan Ikatan Nama Domain
1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)** (Konfigurasi Fitur > Transcoding Langsung).
2. Pilih templat, temukan nama domain target, dan klik **Unbind** (Lepaskan Ikatan).
![](https://main.qcloudimg.com/raw/59ecf14bea1e5b3ffa7b1fe6da0d565b.png)
3. Di jendela pop-up, klik **Confirm** (Konfirmasi).
![](https://main.qcloudimg.com/raw/e335a8c597413b90dfabda9a1f7f3150.png)

[](id:modify)
## Memodifikasi Templat
1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)** (Konfigurasi Fitur > Transcoding Langsung).
2. Pilih templat transcoding target dan klik **Edit** di sebelah kanan untuk memodifikasinya.
3. Setelah modifikasi selesai, klik **Save** (Simpan).
![](https://main.qcloudimg.com/raw/202923ad5334c6ee3e5a879042aa0d5c.png)

[](id:delect)
## Menghapus Templat
>! Jika templat telah diikatkan ke nama domain tertentu, Anda perlu [melepaskan ikatan](#untie) sebelum menghapus templat. 

1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)** (Konfigurasi Fitur > Transcoding Langsung).
2. Pilih templat yang tidak terikat dengan nama domain pemutaran ulang mana pun, dan klik **Delete** (Hapus).
![](https://main.qcloudimg.com/raw/c3109628fcb4a5a4fabce8ad58c03db5.png)
3. Di jendela pop-up, klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/0e27dc5c0ebfc2915161894c3d6a337c.png)

## Operasi Terkait
Informasi lebih lanjut tentang **mengikat** dan **melepaskan ikatan** nama domain dapat dilihat di [Transcoding Configuration (Konfigurasi Transcoding)](https://intl.cloud.tencent.com/document/product/267/31062).


