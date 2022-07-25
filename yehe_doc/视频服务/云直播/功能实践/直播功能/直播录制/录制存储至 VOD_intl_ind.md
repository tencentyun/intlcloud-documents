Perekaman langsung menyimpan file yang sudah dibuat dengan melakukan muxing pada streaming asal (tanpa memodifikasi informasi, seperti data audio dan video serta stempel waktu yang sesuai) di platform VOD.

## Catatan
- Anda dapat menggunakan salah satu metode berikut untuk merekam: [membuat tugas perekaman](https://intl.cloud.tencent.com/document/product/267/37309) atau [membuat templat perekaman](https://intl.cloud.tencent.com/document/product/267/34223). Jika Anda membuat templat perekaman serta tugas perekaman untuk satu streaming langsung yang sama, perekaman akan dilakukan secara berulang.
- Karena terjadi penundaan singkat dalam memulai tugas perekaman setelah push dilakukan pada streaming, push yang sangat singkat tidak dapat menghasilkan file rekaman. Karena itu, durasi setiap push untuk perekaman sebaiknya lebih dari 10 detik.

## Penyimpanan Perekaman
Karena file rekaman disimpan di platform VOD, Anda harus mengaktifkan [layanan VOD](https://intl.cloud.tencent.com/product/vod) terlebih dahulu.
>? Aturan penamaan file rekaman yang dihasilkan dapat dipelajari di [VodFileName](https://intl.cloud.tencent.com/document/product/267/30767#RecordParam).

## Format Perekaman

Format file rekaman yang didukung meliputi .aac (untuk perekaman audio), .flv, .hls, dan .mp4.

## Kasus Penggunaan Perekaman

<table>
<thead>
<tr>
<th width="20%">Kasus Penggunaan</th>
<th>Deskripsi</th>
</tr>
</thead>
<tbody><tr>
<th>Perekaman multilevel oleh nama domain push dan nama streaming</th>
<td>Anda dapat mengonfigurasikan perekaman streaming di level nama domain push dan nama streaming.</td>
</tr>
<tr>
<th>Perekaman dalam periode waktu yang ditentukan</th>
<td>Anda dapat memanggil API untuk mengatur waktu dimulainya dan waktu berakhirnya perekaman streaming dalam periode waktu yang ditentukan.</td>
</tr>
<tr>
<th>Perekaman real-time</th>
<td>Anda dapat memanggil API untuk merekam frame mana saja dalam suatu streaming secara real-time.</td>
</tr>
<tr>
<th>Perekaman audio murni</th>
<td>Anda dapat menggunakan format .aac untuk merekam streaming audio murni.</td>
</tr>
</tbody></table>

## Mengaktifkan Perekaman untuk Semua Streaming Langsung di Nama Domain Push yang Ditetapkan

Parameter perekaman dikelola berdasarkan templat. Anda dapat membuat templat perekaman untuk berbagai skenario dan mengelola konfigurasi perekaman secara fleksibel dengan mengikatkan templat ke berbagai nama domain push dan nama streaming.
Setelah mengaktifkan VOD, Anda dapat merekam streaming langsung di nama domain push tertentu dengan dua cara:

### Konsol CSS
1. Buka **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)** (Konfigurasi Fitur > Perekaman Langsung) untuk membuat templat perekaman.
2. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) untuk menambahkan nama domain dan klik **Manage** (Kelola) untuk mengikatnya dengan templat perekaman. Informasi selengkapnya dapat dipelajari di [Recording Configuration (Konfigurasi Perekaman)](https://intl.cloud.tencent.com/document/product/267/34224).

### API

1. Panggil API [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) untuk mengatur sedikitnya satu format perekaman, misalnya `FlvParam`.
2. Panggil API [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) dengan mengatur `DomainName` (nama domain push) dan `TemplateId` (kembali ke langkah 1). Anda dapat mengosongkan bidang `AppName` dan `StreamName` untuk merekam semua streaming di nama domain yang sama.

Anda juga dapat menentukan streaming tertentu yang akan direkam.

Sebuah templat dapat diikat dengan berbagai nama domain push, aplikasi, dan streaming, tetapi satu nama domain push, aplikasi, atau streaming tidak dapat diikat dengan banyak templat. Jika Anda mengikat streaming yang sama dengan beberapa templat (kasus ini jarang terjadi), hanya templat dengan prioritas tertinggi yang akan diterapkan. Prioritas templat ditentukan sebagai berikut.

| Prioritas | DomainName | AppName  | StreamName |
| ---- | ---------- | -------- | ---------- |
| 1    | &#10003;   | &#10003; | &#10003;   |
| 2    | &#10003;   | ×        | &#10003;   |
| 3    | &#10003;   | &#10003; | ×          |
| 4    | &#10003;   | ×        | ×          |

Tanda ✓ berarti nilai parameter tidak kosong dan tanda × berarti nilai parameter kosong.


## Menonaktifkan Perekaman untuk Streaming Spesifik di Suatu Nama Domain Push
Jika Anda sudah mengonfigurasikan perekaman untuk suatu nama domain push, tetapi tidak perlu merekam streaming tertentu di nama domain push tersebut:

1. Panggil API [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) tanpa menentukan format perekaman.
```
   https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate
   &TemplateName=norecord
   &Description=test
   &<Common request parameters>
```
2. Buka [konsol CSS](https://intl.cloud.tencent.com/document/product/267/34223#conect) atau gunakan API [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) untuk mengikat templat perekaman di atas dengan `DomainName` dan `StreamName` spesifik.

> ! Metode ini dapat diterapkan pada berbagai skenario yang tidak perlu melakukan perekaman pada beberapa streaming. Jika jumlah streaming terlalu banyak, Anda sebaiknya menggunakan nama domain push lain untuk mengelolanya karena:
> - Jumlah maksimum templat perekaman atau aturan perekaman yang diizinkan adalah 50.
> - Pengelolaan berdasarkan nama domain push memberikan fleksibilitas lebih besar karena templat perekaman dan aturan perekaman tidak akan terpengaruh meskipun bisnis Anda berubah.

## Perekaman dalam Periode Waktu yang Ditentukan

Anda dapat menggunakan API untuk menentukan waktu dimulainya, waktu berakhirnya, dan parameter lain perekaman untuk streaming tertentu. Cara ini tidak sama jika dibandingkan dengan penggunaan templat perekaman prasetel dengan parameter yang sudah ditetapkan. Biasanya, API digunakan ketika tidak ada templat perekaman yang dibuat.

### API
Panggil API [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309).


### Sampel perekaman
- Dalam skenario sederhana, Anda perlu menetapkan `StreamName`, `DomainName`, `AppName`, dan `EndTime` saja.
Contoh kode berikut membuat tugas perekaman video dalam format .flv untuk pukul 08.00 hingga 10.00, tanggal 10 Agustus 2020, dengan segmen 30 menit dan file rekaman akan disimpan secara permanen.
**Contoh kode input:**
```
https://live.tencentcloudapi.com/?Action=CreateRecordTask
&AppName=live
&DomainName=mytest.live.push.com
&StreamName=livetest
&StartTime=1597017600
&EndTime=1597024800
&TemplateId=0
&<Common request parameters>
```
- Anda juga dapat menentukan parameter format perekaman, jenis perekaman, dan penyimpanan.
Contoh kode berikut membuat tugas perekaman dalam format .mp4 untuk pukul 08.00 hingga 10.00, tanggal 10 Agustus 2020, dengan segmen 1 jam dan file rekaman akan disimpan secara permanen.
	1. Panggil API [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) untuk membuat templat perekaman.
**Contoh kode input:**
```
https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate
&TemplateName=templat
&Description=test
&Mp4Param.Enable=1
&Mp4Param.RecordInterval=3600
&Mp4Param.StorageTime=0
&<Common request parameters>
```
**Contoh kode output:**
```
{
  "Response": {
    "RequestId": "839d12da-95a9-43b2-a9a0-03366d01b532",
    "TemplateId": 17016
  }
}
```
	2. Panggil API [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) untuk membuat tugas perekaman.
**Contoh kode input:**
```
https://live.tencentcloudapi.com/?Action=CreateRecordTask
&StreamName=livetest
&AppName=live
&DomainName=mytest.live.push.com
&StartTime=1597017600
&EndTime=1597024800
&TemplateId=17016
&<Common request parameters>
```


> ?
>- Untuk streaming langsung yang sama, tidak ada benturan antara tugas-tugas terjadwal atau antara tugas terjadwal dan tugas perekaman jenis lain. Dengan kata lain, periode waktu dapat bertumpang-tindih jika terdapat beberapa tugas terjadwal, dan Anda dapat memanggil API untuk membuat tugas perekaman, selain untuk mengaktifkan konfigurasi perekaman.
>- Anda sebaiknya membuat tugas perekaman terlebih dahulu (sebagai contoh, 1 jam sebelumnya atau pada pagi hari jika acara Anda berlangsung pada siang hari) dan mengatur waktu dimulainya tugas sedikit lebih awal daripada waktu dimulainya acara.


## Perekaman Real-Time

Jika dalam proses streaming langsung Anda ingin merekam frame tertentu saat itu juga untuk membuat klip sorotan, Anda dapat memanggil API untuk mengaktifkan perekaman real-time.

```
https://live.tencentcloudapi.com/?Action=CreateRecordTask
&StreamName=test
&AppName=live
&DomainName=mytest.live.push.com
&EndTime=1597024800
&<Common request parameters>
```

Catatan seputar perekaman real-time:
- Pastikan push berjalan ketika Anda membuat tugas perekaman.
- Anda dapat memanggil API [StopRecordTask](https://intl.cloud.tencent.com/document/product/267/37307) untuk menghentikan tugas di awal.
- Cara ini juga dapat dilakukan untuk streaming di luar Tiongkok Daratan.

## Perekaman Streaming Campuran

Pertama, silakan pelajari dengan saksama [Mencampur Streaming Langsung](https://intl.cloud.tencent.com/document/product/267/37665).

Ada dua jenis campuran streaming yang ditunjukkan oleh parameter `OutputStreamType`:

- Jika `OutputStreamType` diatur ke `0`, streaming output berada di daftar streaming input. Artinya, tidak ada streaming baru yang akan dibuat.
- Jika `OutputStreamType` diatur ke `1`, streaming output tidak berada di daftar streaming input. Artinya, streaming baru akan dibuat.

Misalnya, streaming yang di-push adalah A dan B, sedangkan streaming campuran adalah streaming output C:

- Jika `OutputStreamType` diatur ke `0` dan nama streaming A digunakan sebagai nama streaming output C, setelah perekaman dimulai, file rekaman streaming A (streaming campuran) dan streaming B akan dibuat. Karena nama streaming A digunakan lagi, streaming asal A tidak akan membuat file rekaman.
- Jika `OutputStreamType` diatur ke `1`, file rekaman streaming A, streaming B, dan streaming C (streaming campuran) akan dibuat setelah perekaman dimulai.

Jika hanya ingin merekam streaming campuran, Anda dapat memanggil API [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309). Harap ingat bahwa jika `OutputStreamType` diatur ke `1`, parameter `StreamType` harus diatur ke `1` ketika pemanggilan API ini dilakukan.

>! Perekaman streaming campuran tidak mendukung streaming campuran di dalam dan di luar Tiongkok Daratan karena kesalahan file rekaman akan terjadi dan memengaruhi pemutaran ulang normal.


## Perekaman dengan Penyambungan Otomatis (Perekaman Multi-Push)

Jika beberapa file rekaman dihasilkan ketika push diinterupsi beberapa kali akibat jitter jaringan, hal tersebut akan memengaruhi kontinuitas pemutaran ulang streaming langsung. Untuk mengatasi masalah ini, perekaman langsung dapat menyambungkan secara otomatis beberapa file rekaman di antara interupsi streaming pendek menjadi satu file.

Fitur ini membagi data audio dan video dengan tag **`#EXT-X-DISCONTINUITY`** dalam perekaman HLS. Akibat interupsi streaming, stempel waktu data audio dan video, codec video, codec audio, dan tingkat sampel sebelum dan sesudah pemberian tag mungkin berbeda. Pemutar perlu memuat ulang decoder agar pemutaran ulang berjalan dengan lancar. Untuk menggunakan fitur ini, pemutar harus mendukung tag **`#EXT-X-DISCONTINUITY`**. Saat ini, tag ini didukung di pemutar asli dan Safari di iOS, ExoPlayer di Android, dan pemutar HLS.js di web, tetapi tidak didukung di pemutar VLC.

Setelah fitur ini diaktifkan, Anda harus mengatur periode waktu habis penyambungan otomatis. Periode ini berlangsung hingga 30 menit. Artinya, file-file rekaman antara interupsi dengan durasi hingga 30 menit dapat disambungkan menjadi satu file HLS setelah push terakhir berakhir.

Saat ini, perekaman dengan penyambungan otomatis hanya didukung untuk format HLS. Anda dapat mengatur periode waktu habis penyambungan otomatis di **[Live Recording](https://intl.cloud.tencent.com/document/product/267/34223)** (Perekaman Langsung).

> !
>- Mode ini tidak mendukung streaming langsung tanpa data audio.
>- API `ComposeMedia` VOD dapat digunakan untuk menggabungkan berbagai file video. Informasi selengkapnya dapat dilihat di [ComposeMedia](https://intl.cloud.tencent.com/document/product/266/34127).
>- Setelah pelanjutan perekaman HLS diaktifkan, panggilan balik akan terpicu hanya ketika file rekaman dihasilkan, bukan ketika streaming diinterupsi.

## Mendapatkan File Rekaman

File rekaman secara otomatis disimpan di sistem VOD setelah dibuat dan dapat ditemukan melalui:

### Konsol VOD

Login ke [konsol VOD](https://console.cloud.tencent.com/vod/media) dan pilih **Media Assets** > **Video Management** (Aset Media > Manajemen Video) di halaman **non-admin** (bukan admin) untuk melihat semua file rekaman yang dibuat.
![](https://main.qcloudimg.com/raw/66bde9882dab60099bed8013a3d8c521.png)

### Pemberitahuan peristiwa perekaman

Alamat panggilan balik perekaman dapat diatur di konsol atau melalui panggilan API. Pemberitahuan akan dikirim ke alamat panggilan balik setelah file rekaman dibuat. Setelah itu, Anda dapat mengacu ke [pemberitahuan pesan peristiwa panggilan balik](https://intl.cloud.tencent.com/document/product/267/38080) perekaman untuk mengambil langkah selanjutnya.

Panggilan balik pemberitahuan peristiwa efisien, andal, dan bersifat real-time, jadi Anda sebaiknya menggunakannya untuk mendapatkan informasi file rekaman.

### Kueri dengan API VOD

Anda dapat memanggil API [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) VOD untuk memfilter dan melakukan kueri file rekaman.
>! Ketika Anda memanggil API [CreateRecordTask](https://intl.cloud.tencent.com/zh/document/product/267/37309), parameter [stream_param](#message) yang terbawa dalam URL push tidak akan ditampilkan dalam panggilan balik perekaman. Namun, jika Anda menggunakan metode perekaman lain, parameter tersebut akan ditampilkan dalam panggilan balik perekaman.


## Catatan seputar Modifikasi Konfigurasi
Anda sebaiknya memulai ulang push dan memverifikasi konfigurasi perekaman jika melakukan modifikasi konfigurasi. Konfigurasi diterapkan dengan mengikuti aturan berikut:
- Secara default, konfigurasi diterapkan dalam 10 menit.
- Konfigurasi diterapkan setelah dimulainya push langsung dan tidak akan diperbarui selama proses perekaman.
- Dalam skenario dengan push berlangsung untuk waktu lama (misalnya perekaman untuk pengawasan), Anda harus menginterupsi dan memulai ulang push agar konfigurasi diterapkan.
