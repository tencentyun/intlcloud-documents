CSS mendukung perekaman streaming langsung dan penyimpanan file rekaman dalam VOD agar dapat diunduh dan ditampilkan sebagai pratinjau. Dokumen ini menjelaskan cara membuat, mengikat, melepaskan ikatan, memodifikasi, dan menghapus templat perekaman.
Anda dapat membuat templat perekaman dengan dua cara:

- Di konsol CSS: Petunjuk mendetail dapat dilihat di [Membuat Templat Perekaman](#C_record).
- Melalui API: Parameter API dan contohnya dapat dilihat di [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845).

## Catatan
- File video yang direkam disimpan di [konsol VOD](https://console.cloud.tencent.com/vod/overview) secara default. Kami menyarankan Anda mengaktifkan layanan VOD terlebih dahulu. Informasi selengkapnya dapat dilihat di [Getting Started with VOD (Langkah Awal Memulai Penggunaan VOD)](https://intl.cloud.tencent.com/document/product/266/8757).
- Setelah fitur perekaman diaktifkan, pastikan layanan VOD Anda dalam status normal. Jika fitur perekaman tidak diaktifkan atau ditangguhkan karena keterlambatan pembayaran, perekaman langsung tidak akan tersedia, file rekaman tidak akan dibuat, dan biaya perekaman tidak akan dikenakan.
- File rekaman tersedia dalam waktu sekitar 5 menit setelah perekaman berakhir. Misalnya, jika Anda mulai merekam streaming langsung pada pukul 12:00 dan berhenti pada pukul 12.30, Anda akan mendapatkan video rekaman sekitar pukul 12.35.
- Karena format video yang didukung hanya .flv, .mp4, dan .hls, codec video hanya dapat menggunakan H.264 dan codec audio hanya dapat menggunakan AAC.
- Setelah membuat templat perekaman, Anda dapat mengikatnya dengan nama domain push. Petunjuk mendetail dapat dilihat di [Recording Configuration (Konfigurasi Perekaman)](https://intl.cloud.tencent.com/document/product/267/34224). Pengikatan akan diterapkan dalam waktu sekitar 5‒10 menit.
- Aturan penamaan file rekaman yang dihasilkan dapat dilihat di [VodFileName](https://intl.cloud.tencent.com/document/product/267/30767#RecordParam).
- Mengikat, melepaskan ikatan, atau memodifikasi templat hanya memengaruhi streaming langsung baru dan tidak memengaruhi streaming langsung yang sedang berjalan. Agar perubahan diterapkan pada streaming langsung yang sedang berjalan, Anda harus menghentikan streaming langsung dan melakukan push lagi pada streaming tersebut.
- Perekaman streaming campuran tidak mendukung pencampuran streaming di dalam Tiongkok Daratan dengan streaming di luar Tiongkok Daratan. Akibatnya, akan terjadi kesalahan dan pemutaran ulang tidak dapat dilakukan.



## Prasyarat
- Anda telah mengaktifkan layanan CSS dan menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970).
- Anda telah mengaktifkan [Layanan VOD](https://intl.cloud.tencent.com/document/product/266/8757#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5 .BC.80.E9.80.9A.E4.BA.91.E7.82.B9.E6.92.AD).

[](id:C_record)
## Membuat Templat Perekaman
1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)** (Konfigurasi Fitur > Perekaman Langsung).
2. Klik **Create Recording Template** (Buat Templat Perekaman) dan atur informasi templat sebagai berikut:
![](https://qcloudimg.tencent-cloud.cn/raw/ca30bd94a2f81ecead5c1684b8007744.png)

<table>
   <thead><tr><th width="20%" colspan=2>Item</th><th>Deskripsi</th></tr></thead>
   <tbody><tr>
   <tr>
   <td colspan=2>Template Name (Nama Templat)</td>
   <td>Nama templat perekaman langsung kustom, yang dapat berisi huruf, angka, garis bawah (_), dan tanda hubung (-).</td>
   </tr><tr>
   <td colspan=2>Template Description (Deskripsi Templat)</td>
   <td>Deskripsi templat perekaman langsung kustom, yang dapat berisi huruf, angka, garis bawah (_), dan tanda hubung (-).</td>
   </tr><tr>   
   <td rowspan=3 width="10%">Recording Content (Konten Perekaman)</td>
   <td width="30%">Original stream (Streaming asli)</td> 
   <td>Merekam video sebelum transcoding, pemberian watermark, dan pencampuran streaming.</ul></td>
   </tr><tr>
   <td>Watermarked stream (Streaming yang diberi watermark)</td>
   <td>Merekam video setelah video diberi watermark sesuai dengan templat watermark yang ditentukan.</td>
   </tr><tr>
   <td>Transcoded stream (Streaming yang di-transcoding)</td>
   <td> Merekam streaming yang di-transcoding. Anda dapat memilih templat transcoding yang ada atau mengeklik nama templat tertentu untuk mengubah konfigurasinya. Jika Anda memilih ini, streaming akan diberi watermark dan di-transcoding sebagaimana ditentukan dalam templat yang dipilih sebelum perekaman. Jika templat dihapus, streaming akan direkam setelah diberi watermark.</td>
   </tr><tr>
   <td colspan=2>Recording Format (Format Perekaman)</td>
   <td>Output video dapat menggunakan format .hls, .mp4, .flv, dan .aac (untuk perekaman audio saja).</td>
   </tr>
   </tbody></table>

>! 
>- Jika memilih **Original stream** (Streaming asli), Anda tidak dapat merekam audio streaming WebRTC.
>- Anda tidak dapat merekam streaming yang di-transcoding jika Anda menggunakan fitur pergeseran waktu. Jika pergeseran waktu dikonfigurasikan di templat perekaman, streaming asli akan direkam.
>- Jika dipilih templat transcoding audio saja, format perekaman juga harus dalam format audio.
>- Untuk merekam streaming yang di-transcoding, sistem akan memulai tugas transcoding sehingga Anda akan dikenai biaya. Jika Anda menggunakan templat transcoding yang sama untuk pemutaran ulang, transcoding hanya akan dikenai biaya satu kali.
3. Pilih konten dan format perekaman dan, di bagian opsi yang diperluas, selesaikan konfigurasi berikut:
![](https://qcloudimg.tencent-cloud.cn/raw/0a835b00a6864bc29411da9d8088a626.png)

<table>
   <thead><tr><th width="27%" colspan=2>Item</th><th>Deskripsi</th></tr></thead>
   <tbody><tr>
      <tr>
      <td colspan=2>Max Recording Time Per File (Waktu Perekaman Maks. Per File)</td>
      <td><ul style="margin-bottom:0px">
          <li>Tidak ada batasan atas untuk waktu perekaman file dalam format .hls. Jika streaming langsung terganggu dan periode waktu habis untuk melanjutkan kembali telah berlalu, file rekaman baru akan dibuat untuk melanjutkan perekaman.</li>
          <li>Durasi satu file yang direkam dalam format .mp4, .flv, atau .aac berkisar antara 1 sampai dengan 120 menit.</li>
          </ul></td>
      </tr><tr>
      <td colspan=2>Resumption Timeout (Waktu Habis Melanjutkan Kembali)</td>
      <td>Hanya format .hls yang mendukung melanjutkan kembali perekaman setelah gangguan push, dan periode waktu habis untuk melanjutkan kembali dapat diatur dari 1 sampai dengan 1.800 detik.</td>
      </tr><tr>
      <td colspan=2>Storage Period (Periode Penyimpanan) (hari)</td>
      <td>Anda dapat memilih <b>Permanent (Permanen)</b> untuk menyimpan file rekaman secara permanen atau <b>Custom (Kustom)</b> untuk menentukan periode penyimpanan (hingga 1.500 hari). Mengatur periode ke `0` berarti menyimpan file rekaman secara permanen.</td>
      </tr><tr>
      <td colspan=2>VOD Subapplication/Category (Subaplikasi/Kategori VOD)</td>
      <td>Secara default, streaming direkam ke aplikasi utama dalam VOD, tetapi Anda juga dapat merekamnya ke kategori tertentu <a href="https://console.cloud.tencent.com/vod/app-manage">subaplikasi</a> yang dapat ditulis yang ditentukan.</td>
      </tr><tr>
      <td rowspan=2 width="12%">Konfigurasi Lanjutan</td>
      <td>Storage Policy (Kebijakan Penyimpanan)</td> 
      <td><ul style=margin:0><li>Pilih STANDARD (default) jika file rekaman perlu diputar ulang untuk tujuan bisnis. </li><li>Pilih STANDARD_IA (penyimpanan dingin) jika file rekaman tidak akan sering diakses atau akan disimpan dalam jangka waktu yang lama.</li></ul></td>
      </tr><tr>
      <td>Alur Tugas VOD</td>
      <td>Klik <b>Select (Pilih)</b> untuk mengikat alur tugas yang dibuat di subaplikasi VOD. Anda juga dapat mengeklik alur tugas untuk membuka konsol VOD, tempat Anda dapat mengubah alur tugas atau membuat alur tugas baru. Alur tugas terikat akan dijalankan di file rekaman setelah dibuat, dan Anda akan dikenai <a href="https://tcloud-doc.isd.com/document/product/266/2838">biaya VOD</a>.</td>
      </tr>
      </tbody></table>
>! Untuk **Storage Policy** (Kebijakan Penyimpanan):
>- Jika Anda memilih **STANDARD** (STANDAR) dan penyimpanan dingin diaktifkan untuk aplikasi/kategori yang dipilih, streaming akan direkam ke penyimpanan STANDAR terlebih dahulu sebelum kebijakan penyimpanan dingin yang telah dikonfigurasikan dijalankan pada file rekaman. Anda dapat membuka [Cold Storage (Penyimpanan Dingin)](https://console.cloud.tencent.com/vod/inactivation) untuk melihat kebijakan penyimpanan dingin Anda.
>- Jika Anda memilih **STANDARD_IA** dan penyimpanan dingin diaktifkan untuk aplikasi/kategori yang dipilih, streaming akan direkam ke penyimpanan STANDARD_IA terlebih dahulu, dan sistem kemudian akan menentukan dijalankan atau tidaknya kebijakan penyimpanan dingin.
4. Klik **Save** (Simpan).

[](id:conect)
## Mengikat Nama Domain
1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)** (Konfigurasi Fitur > Perekaman Langsung).
    - **Mengikat nama domain ke templat transcoding yang sudah ada**: Klik **Bind Domain Name** (Ikat Nama Domain) di kiri atas.
    ![](https://main.qcloudimg.com/raw/bcb6c5da46a3455f94d441134e49825a.png)
    - Anda juga dapat mengeklik **Bind Domain Name** (Ikat Nama Domain) di kotak dialog yang muncul **setelah berhasil [membuat templat](#C_record)**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/b45ec9863fe4c6f16fe5551605ce46d9.png)
2. Di jendela pop-up, pilih **recording template** (templat perekaman) dan **push domain name** (nama domain push), lalu klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/9abc1af79841e877d4e194d0d5741efc.png)

>? Anda dapat mengeklik **Add** (Tambahkan) untuk mengikat beberapa nama domain push ke satu templat.

[](id:unite)
## Melepaskan Ikatan Nama Domain
1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)** (Konfigurasi Fitur > Perekaman Langsung).
2. Pilih templat perekaman dengan nama domain terikat, temukan nama domain target, lalu klik **Unbind** (Lepaskan Ikatan).
   ![](https://main.qcloudimg.com/raw/f7071a4b4f9297124b460ffebcba64d3.png)
3. Di jendela pop-up, klik **Confirm** (Konfirmasi).
    ![](https://main.qcloudimg.com/raw/a666387f882584860eaf2c229c2b4769.png)

>? 
>- Melepaskan ikatan templat perekaman tidak akan memengaruhi streaming langsung yang sedang berjalan.
>- Agar pelepasan ikatan diterapkan pada streaming yang sedang berjalan, hentikan streaming dan lakukan push lagi pada streaming tersebut, setelah itu tidak ada file rekaman yang akan dibuat.


[](id:change)
## Memodifikasi Templat
1. Buka **Feature Configuration** > **[Live Recording] (https://console.cloud.tencent.com/live/config/record)** (Konfigurasi Fitur > Perekaman Langsung).
2. Pilih templat perekaman target, klik **Edit** di sebelah kanan, modifikasi pengaturan, lalu klik **Save** (Simpan).
![](![img](https://main.qcloudimg.com/raw/68f4dd1a6452a3e97e7ff4dea6493d7b.png)

[](id:delete)
## Menghapus Templat
1. Login ke konsol CSS dan pilih **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)** (Konfigurasi Fitur > Perekaman Langsung).
2. Pilih templat perekaman target, lalu klik **Delete** (Hapus) di kanan atas.
3. Di jendela pop-up, klik **Confirm** (Konfirmasi).
![](https://main.qcloudimg.com/raw/c7c3e300488ba332b84bfd61da0fb999.png)

>! 
>- Jika nama domain telah terikat ke templat tertentu, Anda perlu [melepaskan ikatan](#unite) terlebih dahulu agar dapat menghapus templat.
>- Di konsol, templat perekaman dikelola di tingkat domain, dan Anda tidak dapat melepaskan ikatan aturan yang dibuat dan diikat oleh API. Anda perlu memanggil [DeleteLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30843) untuk melepaskan ikatan tersebut. 


## Operasi Terkait
Informasi selengkapnya tentang **mengikat nama domain dengan** dan **melepaskan ikatan nama domain dari** templat perekaman dapat dilihat di [Recording Configuration (Konfigurasi Perekaman)](https://intl.cloud.tencent.com/document/product/267/34224).


## Pertanyaan Umum
[](id:que1)
#### Bagaimana ketentuan pemberian nama untuk file rekaman?
Jika templat perekaman dibuat di konsol, file rekaman yang dibuat diberi nama (nama yang ditampilkan oleh panggilan balik perekaman) dalam format berikut secara default:
`{StreamID}*{StartYear}-{StartMonth}-{StartDay}-{StartHour}-{StartMinute}-{StartSecond}*{EndYear}-{EndMonth}-{EndDay}-{EndHour}-{EndMinute}-{EndSecond} `

**Bidang:**

| Placeholder             | Deskripsi          |
| ------------------ | ------------- |
| {StreamID}         | ID Streaming          |
| {StartYear}        | Waktu mulai - tahun   |
| {StartMonth}       | Waktu mulai - bulan   |
| {StartDay}         | Waktu mulai - hari   |
| {StartHour}        | Waktu mulai - jam |
| {StartMinute}      | Waktu mulai - menit |
| {StartSecond}      | Waktu mulai - detik   |
| {EndYear}          | Waktu berakhir - tahun   |
| {EndMonth}         | Waktu berakhir - bulan   |
| {EndDay}           | Waktu berakhir - hari   |
| {EndHour}          | Waktu berakhir - jam |
| {EndMinute}        | Waktu berakhir - menit |
| {EndSecond}        | Waktu berakhir - detik   |
