Dokumen ini menjelaskan langkah awal penggunaan LEB. Sebelum Anda menggunakan LEB, silakan baca [Pricing Overview (Ikhtisar Harga)](https://intl.cloud.tencent.com/document/product/267/2819) untuk mengetahui **daftar item yang dapat dikenai tagihan** dan **harganya**.

[](id:step0)
## Persiapan
1. Buat [akun Tencent Cloud](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb).
2. Buka [konsol CSS](https://console.cloud.tencent.com/live?from=product-banner-use-lvb), setujui **Perjanjian Layanan Tencent Cloud**, lalu klik **Apply for Activation** (Ajukan Permohonan Aktivasi) untuk mengaktifkan CSS.
>?  
>-  Setelah mengaktifkan CSS, Anda akan mendapatkan 20 GB lalu lintas pemutaran ulang untuk Tiongkok Daratan secara gratis.
>- Langkah-langkah konfigurasi nama domain untuk LEB sama dengan langkah-langkah konfigurasi nama domain untuk LVB. Jika sudah menggunakan LVB, Anda dapat melompat ke [Langkah 4. Dapatkan URL pemutaran ulang](#step4).

[](id:step1)
## Langkah 1. Tambahkan nama domain
Untuk menggunakan CSS, Anda harus memiliki setidaknya satu **nama domain push** dan satu **nama domain pemutaran ulang**. Anda tidak dapat menggunakan satu nama domain yang sama untuk push dan pemutaran ulang.
Anda dapat **[menambahkan nama domain Anda sendiri](https://intl.cloud.tencent.com/document/product/267/35970)** dengan nomor izin ICP.

1. Daftarkan nama domain Anda. Izin ICP diperlukan jika Anda ingin menggunakan domain di Tiongkok Daratan.

2. Masuk ke konsol CSS, lalu buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain).

3. Klik **Add Domain** (Tambahkan Domain).

   ![](https://main.qcloudimg.com/raw/771bbce97962dcd1cffdd94324941280.png)
>?
>- CSS menyediakan nama domain pengujian `xxxx.livepush.myqcloud.com`. Anda dapat menggunakannya untuk menguji push, tetapi Anda sebaiknya tidak menggunakannya untuk tujuan bisnis.
>- Setelah nama domain berhasil ditambahkan, Anda dapat melihat informasinya di daftar nama domain di **Domain Management** (Manajemen Domain). Informasi seputar cara mengelola domain dapat dibaca di [Domain Management (Manajemen Domain)](https://intl.cloud.tencent.com/document/product/267/31056).
>- Untuk informasi selengkapnya tentang nama domain untuk streaming langsung, baca [Live Streaming Basics (Penjelasan Dasar tentang Streaming Langsung)](https://intl.cloud.tencent.com/document/product/267/7968).
5. Setelah nama domain Anda ditambahkan, sistem akan menetapkan untuknya nama kanonis (diakhiri dengan `.tlivecdn.com` atau `.tlivepush.com`), yang tidak dapat diakses jika Anda belum menyelesaikan konfigurasi CNAME di penyedia layanan DNS Anda. Contoh berikut menjelaskan cara menambahkan rekaman CNAME jika Anda menggunakan layanan DNS Tencent Cloud:[](id:step1_1_1)
    1. Masuk ke [konsol DNS](https://console.cloud.tencent.com/domain).
    2. Temukan nama domain Anda, lalu klik **Resolve** (Selesaikan).
    3. Di halaman resolusi nama domain, klik **Add Record** (Tambahkan Rekaman).
    4. Masukkan awalan nama domain Anda untuk **Host Record** (Rekaman Host), pilih CNAME untuk **Record Type** (Jenis Rekaman), dan masukkan nama kanonis untuk **Record Value** (Nilai Rekaman).
    5. Klik **Save** (Simpan).
>!
>- Penerapan konfigurasi CNAME memerlukan waktu beberapa saat. Anda dapat menggunakan CSS jika konfigurasi berhasil diterapkan.
>- Setelah konfigurasi CNAME diterapkan, Anda akan melihat ikon ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png) di depan alamat CNAME di **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain).
>- Jika konfigurasi CNAME gagal diterapkan, silakan hubungi penyedia DNS Anda.
>- Informasi seputar cara menambahkan rekaman CNAME dengan penyedia layanan DNS lain dapat dibaca di [Configuring CNAME for Domain Name (Mengonfigurasikan CNAME untuk Nama Domain)](https://intl.cloud.tencent.com/document/product/267/31057).

## Langkah 2. Dapatkan URL push

1. Buka **CSS Toolkit** > **[Address Generator](https://console.intl.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Toolkit CSS > Pembuat Alamat).
2. Selesaikan pengaturan berikut:
   1. Pilih **Push Domain** (Domain Push) untuk **Domain Type** (Jenis Domain).
   2. Pilih nama domain push yang telah Anda tambahkan di **Domain Management** (Manajemen Domain).
   3. Masukkan `StreamName` kustom, misalnya `liveteststream`.
   4. Pilih waktu kedaluwarsa URL, misalnya `2021-05-25 23:59:59`.
   5. Klik **Generate Address** (Buat Alamat) untuk membuat alamat push.
![](https://main.qcloudimg.com/raw/5a377614d5da22c5193bef68f4a3a6e7.png)

>? 
>- Nilai default untuk `AppName` adalah `live`. `txSecret` adalah tanda tangan untuk pemutaran, dan `txTime` adalah waktu kedaluwarsa URL.
>- Berikut adalah cara lain untuk membuat URL push: Di **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), temukan nama domain yang ingin Anda gunakan untuk push, lalu klik **Manage** (Kelola). Di bagian **Push Configuration** (Konfigurasi Push), masukkan waktu kedaluwarsa untuk URL dan `StreamName` kustom, lalu klik **Generate Push Address** (Buat Alamat Push).
>- Berdasarkan kebutuhan Anda, sebelum membuat URL push, Anda dapat membuat [templat](https://intl.cloud.tencent.com/document/product/267/31069) dan mengikatnya ke domain push Anda. Informasi seputar harga layanan dengan nilai tambah CSS dapat dibaca di [Pricing Overview (Ikhtisar Harga)](https://intl.cloud.tencent.com/document/product/267/2819).

[](id:step3)
## Langkah 3. Mulai push


Untuk memulai push, masukkan URL push yang dibuat ke perangkat lunak yang Anda gunakan untuk melakukan push.
- Untuk push di PC, Anda sebaiknya menggunakan OBS. Anda perlu [mengonfigurasikan plugin OBS](https://intl.cloud.tencent.com/document/product/267/42131) terlebih dahulu. Untuk langkah-langkah selanjutnya, baca [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).
- Untuk push di web, Anda sebaiknya menggunakan **[Web Push](https://console.intl.cloud.tencent.com/live/tools/webpush)** (Push Web). Click **Generate** (Buat). Di jendela pop-up, pilih nama domain push, masukkan `StreamName` kustom, pilih waktu kedaluwarsa URL, lalu klik **Confirm** (Konfirmasi). Nyalakan kamera, lalu klik **Start Push** (Mulai Push).
- Untuk push di perangkat seluler, unduh dan instal [TCToolkit](https://intl.cloud.tencent.com/document/product/1071/38147). Setelah instalasi selesai, buka perangkat lunak, pilih **MLVB** > **Push (Camera)** (Push (Kamera)), masukkan URL push secara manual atau pindai kode QR, lalu ketuk **Start streaming** (Mulai streaming).

>? 
>- Anda juga dapat mengintegrasikan [SDK MLVB](https://intl.cloud.tencent.com/document/product/1071) ke dalam aplikasi Anda untuk mengimplementasikan fitur push.
>- Solusi LEB untuk web tidak mendukung decoding atau pemutaran B-frame. Informasi selengkapnya dapat dibaca di bagian [B-Frame](#b_frame).

[](id:step4)
## Langkah 4. Dapatkan URL pemutaran ulang

1. Setelah push berhasil, pilih **[Stream Management](https://console.cloud.tencent.com/live/streammanage)** > **Live Streams** (Manajemen Streaming > Streaming Langsung), lihat status URL push, dan klik **Preview** (Pratinjau) untuk memutar streaming.
2. Buka **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Toolkit CSS > Pembuat Alamat), lalu selesaikan pengaturan berikut:
   1. Pilih **Playback Domain** (Domain Pemutaran Ulang) untuk **Domain Type** (Jenis Domain).
   2. Pilih nama domain pemutaran ulang yang telah Anda tambahkan di **Domain Management** (Manajemen Domain).
   3. Untuk **StreamName**, masukkan `StreamName` di URL push.
   4. Pilih waktu kedaluwarsa URL, misalnya `2021-05-25 23:59:59`.
   5. Pilih templat transcoding jika Anda ingin melakukan transcoding pada streaming dan dapatkan URL pemutaran ulang streaming yang di-transcoding. Langkah ini tidak perlu dilakukan jika Anda memutar streaming asli.
   5. Klik **Generate Address** (Buat Alamat) untuk membuat URL pemutaran ulang LEB dengan format `webrtc://domain/path/stream_id`.
![](https://main.qcloudimg.com/raw/5025e22cd8c4c555d7de3e0360e13d11.png)
3. Anda dapat menggunakan metode berikut untuk menguji pemutaran ulang di berbagai skenario:
   - **Di web**: Gunakan [Demo Langsung WebRTC](https://tcplayer.vcube.tencent.com/webrtc-demo/index.html) untuk memutar streaming.
>?
>- Demo Langsung WebRTC mendukung pemutaran ulang multi-definisi. Anda dapat membuat templat transcoding untuk output HD dan SD di **Feature Configuration** > [**Live Transcoding**](https://console.cloud.tencent.com/live/config/transcode) (Konfigurasi Fitur > Transcoding Langsung) di konsol CSS, masukkan URL WebRTC yang berisi templat transcoding ke dalam demo, lalu putar. Jika Anda tidak perlu menguji fitur ini, masukkan URL WebRTC asli.
>- Untuk informasi selengkapnya tentang transcoding langsung dan penagihannya, pelajari [Live Transcoding (Transcoding Langsung)](https://intl.cloud.tencent.com/document/product/267/31071).

   - **Di perangkat seluler**: Unduh dan instal [TCToolkit](https://intl.cloud.tencent.com/document/product/1071/38147). Setelah instalasi selesai, buka perangkat lunak, buka **Live broadcast** > **LEB Player** (Siaran langsung > Pemutar LEB), masukkan URL pemutaran ulang secara manual atau pindai kode QR untuk mendapatkan URL, lalu ketuk **Start Playback** (Mulai Pemutaran Ulang).
>? Jika ingin memutar streaming di aplikasi Anda, Anda dapat mengintegrasikan SDK MLVB. Jika Anda memiliki pertanyaan, silakan baca bagian [Pertanyaan Umum](#que).

## Langkah 5. Gunakan LEB
**Solusi LEB untuk perangkat seluler**: Solusi ini mendukung decoding B-frame dan AAC serta telah terintegrasi dengan SDK MLVB. Untuk mengetahui cara menggunakannya, lihat [LEB](https://intl.cloud.tencent.com/document/product/1071/41875).

[](id:que)
## Pertanyaan Umum
[](id:play_url)
### Membuat URL pemutaran ulang
Format URL LEB sama dengan format URL LVB, tetapi URL LEB diawali dengan `webrtc` sedangkan URL LVB diawali dengan `rtmp`.

Format URL pemutaran ulang LEB: `webrtc://domain/path/stream_id` or `webrtc://domain/path/stream_id?txSecret=xxx&txTime=xxx` ([perlindungan hotlink](https://intl.cloud.tencent.com/document/product/267/31560) diaktifkan). Informasi seputar cara membuat URL pemutaran ulang dapat dibaca di bagian [Dapatkan URL pemutaran ulang](#step4).

>? Anda dapat menggunakan URL streaming yang di-transcoding untuk diputar dengan berbagai resolusi dan bitrate. Informasi seputar cara membuat URL pemutaran ulang untuk streaming yang di-transcoding dapat dipelajari di bagian [Live Remuxing and Transcoding (Remuxing dan Transcoding Langsung)](https://intl.cloud.tencent.com/document/product/267/31561).

[](id:b_frame)
### B-frame
Solusi LEB untuk web **tidak mendukung decoding atau pemutaran B-frame**. Jika streaming berisi B-frame, backend akan menghapusnya saat transcoding berlangsung sehingga latensi meningkat dan **biaya transcoding akan dikenakan**. Sebaiknya jangan melakukan push streaming dengan B-frame atau menggunakan perangkat lunak streaming, seperti OBS, untuk menghapusnya dengan menyesuaikan parameter pengodean video. Gambar di bawah menunjukkan cara menghapus B-frame menggunakan OBS:
![](https://main.qcloudimg.com/raw/b28d5919589364e6a1f78d62e0b58c47.png)

[](id:a_transcoding)
### Transcoding audio
Pemutaran ulang dengan browser hanya mendukung protokol WebRTC standar dan tidak mendukung AAC. Jika streaming yang di-push berisi audio dalam format AAC, sistem akan melakukan transcoding pada audio ke dalam format Opus sehingga biaya [transcoding audio](https://intl.cloud.tencent.com/document/product/267/39604) akan dikenakan.
