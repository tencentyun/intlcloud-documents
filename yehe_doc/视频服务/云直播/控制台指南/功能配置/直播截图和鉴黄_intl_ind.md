CSS menyediakan fitur pengambilan tangkapan layar dan deteksi pornografi. Setelah Anda mengonfigurasi templat pengambilan tangkapan layar dan deteksi pornografi di konsol serta mengikatnya dengan nama domain push, CSS akan mengambil tangkapan layar streaming langsung dan menyimpannya atau data deteksi pornografi ke Cloud Object Storage (COS). Setelah nama domain push diikat dengan templat panggilan balik, jika peristiwa panggilan balik terpicu selama streaming langsung, Tencent Cloud akan mengirimkan permintaan ke server klien yang bertanggung jawab atas respons tersebut. Setelah lulus verifikasi, server akan mendapatkan paket JSON yang berisi panggilan balik deteksi pornografi.
Dokumen ini menjelaskan cara membuat, mengikat, melepaskan ikatan, memodifikasi, dan menghapus templat pengambilan tangkapan layar dan deteksi pornografi di konsol.

Anda dapat membuat templat pengambilan tangkapan layar dan deteksi pornografi dengan cara berikut:

- Membuat templat di konsol CSS. Penjelasan mendetail dapat dilihat di [Membuat Templat Pengambilan Tangkapan Layar dan Deteksi Pornografi](#Screenshot).
- Membuat templat dengan API. Detail tentang parameter dan sampel tertentu dapat dipelajari di [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834).



## Catatan

- Anda dapat mengaktifkan pengambilan tangkapan layar secara langsung. Untuk mengaktifkan deteksi pornografi, Anda harus mengaktifkan pengambilan tangkapan layar terlebih dahulu.
- Penggunaan fitur pengambilan tangkapan layar dan deteksi pornografi akan dikenai biaya. Harga unit untuk pengambilan tangkapan layar adalah 0,0176 USD per seribu tangkapan layar dan harga satuan untuk deteksi pornografi adalah 0,2294 USD per seribu tangkapan layar. Informasi lebih lanjut dapat dilihat di [Intelligent Porn Detection (Deteksi Pornografi Cerdas)](https://intl.cloud.tencent.com/document/product/267/39607).  
- Tangkapan layar yang dihasilkan akan disimpan di bucket COS Anda dan akan dikenai biaya penyimpanan COS. Informasi selengkapnya dapat dilihat di [COS Pricing (Harga COS)](https://intl.cloud.tencent.com/pricing/cos).
- Untuk mengaktifkan fitur pengambilan tangkapan layar, Anda harus memberikan izin terlebih dahulu kepada CSS untuk menulis ke bucket COS Anda. Informasi selengkapnya dapat dilihat di [Authorizing CSS to Store Screenshots in a COS Bucket (Mengizinkan CSS Menyimpan Tangkapan Layar di Bucket COS)](https://intl.cloud.tencent.com/document/product/267/33384).
- Setelah membuat templat, Anda dapat mengikatnya dengan nama domain push. Informasi selengkapnya dapat dilihat di [Screencapture and Porn Detection Configuration (Konfigurasi Pengambilan Tangkapan Layar dan Deteksi Pornografi)](https://intl.cloud.tencent.com/document/product/267/31063). Pengikatan akan diterapkan dalam waktu sekitar 5‒10 menit. 
- Di konsol, Anda dapat mengelola templat pengambilan tangkapan layar dan deteksi pornografi berdasarkan nama domain, tetapi Anda tidak dapat membatalkan aturan yang dibuat oleh API. Jika Anda telah mengikat templat dengan streaming tertentu melalui API pengambilan tangkapan layar dan deteksi pornografi serta ingin melepaskan ikatan tersebut, Anda perlu memanggil API [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833).
- Mengikat, melepaskan ikatan, atau memodifikasi templat hanya memengaruhi streaming langsung baru setelah pembaruan, dan tidak memengaruhi streaming langsung yang sedang berjalan. Agar aturan baru diterapkan pada streaming langsung yang sedang berjalan, Anda perlu menghentikan sementara streaming langsung dan melakukan push lagi pada streaming tersebut.



## Prasyarat

- Anda telah mengaktifkan CSS dan menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970).
- Anda telah membuat bucket COS dan memberikan izin kepada CSS untuk menyimpan tangkapan layar di bucket COS. Informasi selengkapnya dapat dilihat di [How to Authorize CSS to Store Screenshots in a COS Bucket (Cara Memberikan Izin kepada CSS untuk Menyimpan Tangkapan Layar di Bucket COS)](https://intl.cloud.tencent.com/document/product/267/33384).



<span id="Screenshot"></span>
## Membuat Templat Pengambilan Tangkapan Layar dan Deteksi Pornografi

1. Login ke konsol CSS, lalu pilih **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)** (Konfigurasi Fitur > Pengambilan Tangkapan Layar & Deteksi Pornografi Langsung).
2. Klik **Create Screencapture and Porn Detection Template** (Buat Templat Pengambilan Tangkapan Layar dan Deteksi Pornografi), konfigurasikan pengaturan, lalu klik **Save** (Simpan).
![](https://main.qcloudimg.com/raw/544c2127f7870add334eaf760f1da089.png)
<table>
<thead><tr><th width="15%">Item Konfigurasi</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>Template Name (Nama Templat)</td>
<td>Nama templat pengambilan tangkapan layar dan deteksi pornografi, yang dapat berisi hingga 30 huruf, angka, garis bawah (_), dan tanda hubung (-).</td>
</tr><tr>
<th>Template Description (Deskripsi Templat)</th>
<td>Deskripsi templat pengambilan tangkapan layar dan deteksi pornografi, yang dapat berisi hingga 100 huruf, angka, garis bawah (_), dan tanda hubung (-).</td>
</tr><tr>
<td>Screencapture Interval (Interval Pengambilan Tangkapan Layar)</td>
<td>Interval pengambilan tangkapan layar otomatis selama push, dalam hitungan detik. Rentang nilai: 2 (default)‒300
</tr><tr>    
<td>Intelligent Porn Detection (Deteksi Pornografi Cerdas)</td>
<td>Opsi untuk mengaktifkan deteksi pornografi cerdas atau tidak. Jika deteksi pornografi cerdas diaktifkan, Anda perlu mengonfigurasikan templat panggilan balik terlebih dahulu agar dapat menerima hasil deteksi pornografi.</td>
</tr><tr>
<td>Storage Account (Akun Penyimpanan)</td>
<td>Anda dapat memilih <b>Current Account (Akun Saat Ini)</b> atau <b>Other Account (Akun Lainnya)</b>.</td>
</tr><tr>
<td>CosAppId</td>
<td>Diperlukan hanya jika akun penyimpanan (akun tempat layanan COS berada) diatur ke <b>Other Account (Akun Lainnya)</b>. Nilai `AppId` bisa Anda dapatkan di <a href="https://console.cloud.tencent.com/developer"><b>Account Information (Informasi Akun)</b></a> akun penyimpanan.</td>
</tr><tr>
<td>Bucket</td>
<td>Pilih bucket <b>COS</b> yang telah Anda buat dan beri izin.</td>
</tr><tr>
<td>Region (Wilayah)</td>
<td>Wilayah tempat bucket berada. Wilayah tidak dapat dimodifikasi.</td>
</tr><tr>
<td>Folder</td>
<td>Klik kotak untuk memilih folder COS. Nama folder menggunakan format <code>{Year}-{Month}-{Day}/</code> secara default.<br>Catatan: nama folder COS hanya boleh berisi huruf, angka, placeholder, dan simbol <code>-, !, _, ., *</code>.</td>
</tr><tr>
<td>File Name (Nama File)</td>
<td>Format nama file tangkapan layar. Format default: <code>{StreamID}-screenshot-{Hour}-{Minute}-{Second}-{Width}x{Height}{Ext}</code>. Nama file dapat disesuaikan dengan menyambungkan parameter berikut:
    <ul style="margin:0">
        <li>{AppName}: `AppName` push</li>
        <li>{PushDomain}: nama domain push</li>
        <li>{StreamID}: ID streaming</li>
        <li>{Year}: waktu tangkapan layar (tahun)</li>
        <li>{Month}: waktu tangkapan layar (bulan)</li>
        <li>{Day}: waktu tangkapan layar (hari)</li>
        <li>{Hour}: waktu tangkapan layar (jam)</li>
        <li>{Minute}: waktu tangkapan layar (menit)</li>
        <li>{Second}: waktu tangkapan layar (detik)</li>
        <li>{Width}: lebar tangkapan layar</li>
        <li>{Height}: tinggi tangkapan layar</li><li>{Ext}: ekstensi (.jpg)</li>
    </ul>Catatan: parameter hanya boleh berisi huruf, angka, placeholder, dan simbol (-, !, _, ., *).
    <br>Contoh: jika format nama file adalah <code> {Year}-{Month}-{Day}- {Hour}-{Ext}</code>, tangkapan layar yang secara otomatis diambil selama streaming langsung pada pukul 14.00.00 tanggal 1 Januari 2020 akan disimpan dan diberi nama "2020010114.jpg" di COS.</td>
</tr>
</tbody></table>


<span id="conect"></span>
## Mengikat Templat dengan Nama Domain

1. Login ke konsol CSS, lalu pilih **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)** (Konfigurasi Fitur > Pengambilan Tangkapan Layar & Deteksi Pornografi Langsung).
2. Buka halaman pengikatan nama domain dengan salah satu cara berikut:
    - **Mengikat nama domain secara langsung**: klik **Bind Domain Name** (Ikat Nama Domain) di kiri atas.
    ![](https://qcloudimg.tencent-cloud.cn/raw/92b7542783d6d5ac59ef5faedbf53746.png)
    - **Mengikat nama domain setelah membuat templat pengambilan tangkapan layar dan deteksi pornografi:** setelah berhasil [membuat templat pengambilan tangkapan layar dan deteksi pornografi](#Screenshot), klik **Bind Domain Name** (Ikat Nama Domain) di jendela pop-up.
    ![](https://qcloudimg.tencent-cloud.cn/raw/61c40816a357ce0f79677e238a1a31ba.png)
1. Pilih **screencapture and porn detection template** (templat pengambilan tangkapan layar dan deteksi pornografi) dan **push domain name** (nama domain push) di jendela pengikatan nama domain, lalu klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/5e632f4a7712256fdd3f3a282e09a9c7.png)
>? Anda dapat mengeklik **Add** (Tambahkan) untuk mengikat banyak nama domain push dengan templat ini.


<span id="unite"></span>
## Melepaskan Ikatan Templat dari Nama Domain

1. Login ke konsol CSS, lalu pilih **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)** (Konfigurasi Fitur > Pengambilan Tangkapan Layar & Deteksi Pornografi Langsung).
2. Pilih templat pengambilan tangkapan layar dan deteksi pornografi dengan nama domain terikat, temukan nama domain target, lalu klik **Unbind** (Lepaskan Ikatan).
   ![](https://qcloudimg.tencent-cloud.cn/raw/e8a52af13916db8d50bc4395cfc5cc8d.png)
3. Di jendela pop-up, klik **Confirm** (Konfirmasi).
   ![](https://main.qcloudimg.com/raw/9182f6589885ecba5fafcea075c9184e.png)


<span id="change"></span>
## Memodifikasi Templat

1. Login ke konsol CSS, lalu pilih **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)** (Konfigurasi Fitur > Pengambilan Tangkapan Layar & Deteksi Pornografi Langsung).
2. Temukan templat pengambilan tangkapan layar dan deteksi pornografi yang telah Anda buat, lalu klik **Edit** di sebelah kanan untuk memodifikasi informasi templat.
3. Klik **Save** (Simpan).

![](https://qcloudimg.tencent-cloud.cn/raw/786b4fd9630a178a0aebb65cda16a49c.png)


<span id="delete"></span>
## Menghapus Templat

>! Jika templat telah terikat dengan nama domain tertentu, Anda perlu [melepaskan ikatan](#unite) sebelum menghapus templat.

1. Login ke konsol CSS, lalu pilih **Feature Configuration** > **[Live Screencapture & Porn Detection](https://console.cloud.tencent.com/live/config/jtjh)** (Konfigurasi Fitur > Pengambilan Tangkapan Layar & Deteksi Pornografi Langsung).
2. Temukan templat pengambilan tangkapan layar dan deteksi pornografi yang telah Anda buat, lalu klik **Delete** (Hapus) di bagian atas.
3. Di jendela pop-up, klik **Confirm** (Konfirmasi).

![](https://main.qcloudimg.com/raw/6ae7a299517803a92776d8077ccda1d3.png)



## Operasi
Informasi selengkapnya tentang **mengikat** dan **melepaskan ikatan nama domain** dengan atau dari templat pengambilan tangkapan layar dan deteksi pornografi dapat dilihat di [Screencapture and Porn Detection Configuration (Konfigurasi Pengambilan Tangkapan Layar dan Deteksi Pornografi)](https://intl.cloud.tencent.com/document/product/267/31063).
