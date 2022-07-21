Dokumen ini menjelaskan langkah awal penggunaan CSS. Sebelum mencoba CSS, Anda disarankan untuk membaca [Pricing Overview (Ikhtisar Harga)](https://intl.cloud.tencent.com/document/product/267/2819) CSS untuk memahami **daftar item yang dapat dikenai tagihan** dan **harganya**.



[](id:step0)

## Persiapan

1. Buat [akun Tencent Cloud](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb) dan selesaikan [verifikasi identitas](https://intl.cloud.tencent.com/document/product/378/3629). Pengguna yang belum diverifikasi tidak dapat membeli instans CSS di Tiongkok Daratan.
2. Buka [halaman aktivasi layanan CSS](https://console.cloud.tencent.com/live?from=product-banner-use-lvb), nyatakan persetujuan Anda terhadap "Ketentuan Layanan Tencent Cloud", lalu klik **Apply for Activation** (Ajukan Permohonan Aktivasi) untuk mengaktifkan layanan CSS.


[](id:step1)
## Langkah 1. Tambahkan nama domain
Untuk menggunakan CSS, Anda harus memiliki setidaknya satu **nama domain push** dan satu **nama domain pemutaran ulang**. Anda tidak dapat menggunakan satu nama domain yang sama untuk push dan pemutaran ulang.

<span id="step1_1"></span>
1. Siapkan nama domain Anda. Untuk nama domain di wilayah Tiongkok Daratan, diperlukan izin ICP.
2. Masuk ke konsol CSS, buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **Add Domain** (Tambahkan Domain).
![](https://main.qcloudimg.com/raw/771bbce97962dcd1cffdd94324941280.png)
>?
>- CSS menyediakan nama domain pengujian `xxxx.livepush.myqcloud.com`. Anda dapat menggunakannya untuk menguji push langsung, tetapi Anda sebaiknya tidak menggunakannya sebagai nama domain push untuk tujuan bisnis.
>- Setelah nama domain berhasil ditambahkan, Anda dapat melihat informasinya di daftar nama domain di **Domain Management** (Manajemen Domain). Informasi seputar cara mengelola domain dapat dilihat di [Domain Management (Manajemen Domain)](https://intl.cloud.tencent.com/document/product/267/31056).
>- Untuk informasi selengkapnya tentang nama domain streaming langsung, silakan baca [Basic CSS Features (Fitur CSS Dasar)](https://intl.cloud.tencent.com/document/product/267/7968).

[](id:step1_1_1)
4. Setelah nama domain Anda ditambahkan, sistem akan menetapkan untuknya nama domain CNAME (diakhiri dengan `.tlivecdn.com` atau `.tlivepush.com`), yang tidak dapat diakses jika Anda belum menyelesaikan konfigurasi CNAME di penyedia layanan DNS Anda. Setelah konfigurasi CNAME diterapkan, Anda dapat menggunakan CSS. Contoh berikut menjelaskan cara menambahkan rekaman CNAME dengan menganggap Tencent Cloud sebagai penyedia layanan DNS Anda:
  1. Login ke [konsol Layanan Nama Domain Tencent Cloud](https://console.cloud.tencent.com/domain).
  2. Temukan nama domain target, lalu klik **Resolve** (Selesaikan).
  3. Di halaman resolusi nama domain, klik **Add Record** (Tambahkan Rekaman).
  4. Di baris baru, masukkan awalan nama domain sebagai rekaman host, pilih CNAME sebagai jenis rekaman, dan masukkan nama domain CNAME sebagai nilai rekaman.
  5. Klik **Save** (Simpan).
>!
>- Setelah rekaman CNAME berhasil ditambahkan, diperlukan beberapa waktu untuk menerapkan konfigurasi CNAME. Jika konfigurasi gagal, Anda tidak dapat menggunakan CSS.
>- Setelah konfigurasi CNAME berhasil, Anda dapat melihat bahwa simbol status alamat CNAME di **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) di konsol CSS telah berubah menjadi ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png).
>- Jika konfigurasi CNAME masih gagal, hubungi penyedia layanan DNS Anda.
>- Untuk informasi selengkapnya tentang cara melakukan konfigurasi dengan penyedia layanan DNS lainnya, silakan pelajari [Configuring CNAME for Domain Name (Mengonfigurasikan CNAME untuk Nama Domain)](https://intl.cloud.tencent.com/document/product/267/31057).


[](id:step2)
## Langkah 2. Dapatkan URL push
1. Pilih **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Toolkit CSS > Pembuat Alamat).
2. Di halaman **Address Generator** (Pembuat Alamat), lakukan konfigurasi sebagai berikut:
   1. Pilih **Push Domain** (Domain Push) untuk **Domain Type** (Jenis Domain).
   2. Pilih nama domain push yang telah Anda tambahkan di **Domain Management** (Manajemen Domain).
   3. Masukkan **AppName**. Nama yang diberikan secara default adalah `live`.
   4. Masukkan `StreamName` kustom, misalnya `liveteststream`.
   5. Pilih waktu kedaluwarsa URL, misalnya `2021-05-31 23:59:59`.
   6. Klik **Generate Address** (Buat Alamat) untuk membuat alamat push.
![](https://main.qcloudimg.com/raw/5a377614d5da22c5193bef68f4a3a6e7.png)

>? 
>- Di URL push, `live` adalah `AppName` default, `txSecret` adalah tanda tangan untuk memutar ulang streaming, dan `txTime` adalah waktu kedaluwarsa URL.
>- Berikut adalah cara lain untuk membuat URL push: Di **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), temukan nama domain push yang ingin Anda gunakan untuk membuat URL push, klik **Manage** (Kelola), pilih **Push Configuration** (Konfigurasi Push), masukkan waktu kedaluwarsa untuk URL dan `StreamName` kustom, lalu klik **Generate Push Address** (Buat Alamat Push).
>- Anda dapat membuat dan mengonfigurasikan [templat fitur](intl.cloud.tencent.com/document/product/267/34223) sesuai keinginan sebelum membuat URL push berdasarkan kebutuhan bisnis Anda dan mengikatnya ke nama domain push. Untuk informasi seputar harga fitur dengan nilai tambah CSS, lihat [Pricing Overview (Ikhtisar Harga)](https://intl.cloud.tencent.com/document/product/267/2819).

[](id:step3)
## Langkah 3. Lakukan push pada streaming langsung

Anda dapat memasukkan URL push yang dibuat ke perangkat lunak push yang sesuai untuk kasus penggunaan Anda.
- Untuk push di PC, Anda sebaiknya menggunakan OBS. Untuk mendapatkan petunjuk mendetail, pelajari [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).
- Untuk push di web, Anda sebaiknya menggunakan **[Web Push](https://console.cloud.tencent.com/live/tools/webpush)** (Push Web): pilih nama domain push, masukkan `StreamName` kustom, pilih waktu kedaluwarsa URL, nyalakan kamera, lalu klik **Start Push** (Mulai Push).

- Untuk push di perangkat seluler, unduh dan instal [Demo Tencent Video Cloud](https://intl.cloud.tencent.com/document/product/1071/38147), buka, pilih **Mobile Live Video Broadcasting** > **Push (Camera)** (Siaran Video Langsung Seluler > Push (Kamera)), masukkan URL push ke kotak alamat secara manual atau dengan memindai kode QR, lalu ketuk ikon mulai di sudut kiri bawah untuk melakukan push pada streaming.

>? Anda dapat mengintegrasikan [SDK MLVB](https://intl.cloud.tencent.com/document/product/1071) Tencent Cloud ke dalam berbagai aplikasi khusus untuk push langsung.

[](id:step4)
## Langkah 4. Dapatkan URL pemutaran ulang
1. Setelah push berhasil, pilih **[Stream Management](https://console.cloud.tencent.com/live/streammanage)** > **Live Streams** (Manajemen Streaming > Streaming Langsung), lihat status URL push, lalu klik **Test** (Uji) untuk memutar ulang streaming secara online.
2. Pilih **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Toolkit CSS > Pembuat Alamat) untuk mendapatkan alamat pemutaran ulang dan lakukan konfigurasi sebagai berikut:
   1. Pilih **Playback Domain** (Domain Pemutaran Ulang) untuk **Domain Type** (Jenis Domain).
   2. Pilih nama domain pemutaran ulang yang telah Anda tambahkan di **Domain Management** (Manajemen Domain).
   3. Masukkan **AppName**. Nama yang diberikan secara default adalah `live`.
   4. Masukkan `StreamName` di URL push untuk memutar ulang streaming yang sesuai.
   5. Pilih waktu kedaluwarsa URL, misalnya `2021-05-31 23:59:59`.
   6. Untuk membuat URL pemutaran ulang untuk streaming yang di-transcoding, pilih templat transcoding yang harus diikatkan ke nama domain di URL pemutaran ulang. Langkah-langkah untuk mengikat templat transcoding dapat dipelajari di [Live Transcoding > Binding Domain Name (Transcoding Langsung > Mengikat Nama Domain)](https://intl.cloud.tencent.com/document/product/267/31071).
   7. Klik **Generate Address** (Buat Alamat) untuk membuat alamat pemutaran ulang.
![](https://main.qcloudimg.com/raw/5025e22cd8c4c555d7de3e0360e13d11.png)
[](id:step4_1)
3. Anda dapat menggunakan metode berikut untuk menguji bisa atau tidaknya suatu streaming langsung diputar ulang secara normal dalam kasus penggunaan yang berbeda:
   1. Untuk pengujian pemutaran ulang di PC, Anda sebaiknya menggunakan alat, seperti [VLC](https://intl.cloud.tencent.com/document/product/267/32483). Untuk informasi selengkapnya, silakan pelajari [Live Playback (Pemutaran Ulang Langsung)](https://intl.cloud.tencent.com/document/product/267/31559).

   2. - Untuk pengujian pemutaran ulang di perangkat seluler, Anda sebaiknya mengunduh dan menginstal [Aplikasi Toolkit Tencent Video Cloud](https://intl.cloud.tencent.com/document/product/1071/38147), pilih **Mobile Live Video Broadcasting** > **LVB Playback** (Siaran Video Langsung Seluler > Pemutaran Ulang LVB), masukkan URL pemutaran ulang ke kotak alamat secara manual atau dengan memindai kode QR, lalu ketuk ikon putar di sudut kiri bawah.

>? Untuk melakukan push/memutar ulang streaming di aplikasi, Anda dapat mengintegrasikan [SDK MLVB](https://cloud.tencent.com/product/mlvb) ke dalam aplikasi untuk melengkapi layanan CSS. Jika Anda mengalami masalah selama masa uji coba, silakan pelajari bagian [FAQ (Pertanyaan Umum)](https://intl.cloud.tencent.com/document/product/267/7968).

## Operasi
- Untuk mengaktifkan **live recording** (perekaman langsung), buat templat rekaman dan ikat templat ke nama domain terlebih dahulu. Untuk informasi selengkapnya, silakan pelajari bagian [Creating Recording Template (Membuat Templat Rekaman)](https://intl.cloud.tencent.com/document/product/267/34223).
- Untuk mengaktifkan **live transcoding** (transcoding langsung), buat templat transcoding dan ikat templat ke nama domain terlebih dahulu. Untuk informasi selengkapnya, silakan pelajari bagian [Creating Transcoding Template (Membuat Templat Transcoding)](https://intl.cloud.tencent.com/document/product/267/31071).
- Untuk mengaktifkan **live watermarking** (pemberian watermark langsung), buat templat watermark dan ikat templat ke nama domain terlebih dahulu. Untuk informasi selengkapnya, silakan pelajari bagian [Creating Recording Template (Membuat Templat Rekaman)](https://intl.cloud.tencent.com/document/product/267/31073).
- Untuk mengaktifkan **live screencapture and porn detection** (pengambilan tangkapan layar dan deteksi pornografi langsung), buat templat pengambilan tangkapan layar dan deteksi pornografi, dan ikat templat ke nama domain terlebih dahulu. Untuk informasi selengkapnya, silakan pelajari bagian [Creating Screencapture and Porn Detection Template (Membuat Templat Pengambilan Tangkapan Layar dan Deteksi Pornografi](https://intl.cloud.tencent.com/document/product/267/31072).
- Untuk mengaktifkan **live stream mixing** (pencampuran streaming langsung), panggil API campuran streaming [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997).




## Pertanyaan Umum
- [Apa perbedaan antara push, streaming langsung, dan video on demand?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.8E.A8.E6.B5.81.E3.80.81.E7.9B.B4.E6.92.AD.E5.92.8C.E7.82.B9.E6.92.AD.E5.88.86.E5.88.AB.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
- [Protokol push apa yang didukung?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.8E.A8.E6.B5.81.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [Protokol pemutaran ulang apa yang didukung?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.92.AD.E6.94.BE.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [Apa saja bagian penyusun sebuah URL pemutaran ulang?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.92.AD.E6.94.BE.E5.9C.B0.E5.9D.80.E7.94.B1.E4.BB.80.E4.B9.88.E7.BB.84.E6.88.90.EF.BC.9F)
- [Bagaimana cara menyambungkan beberapa URL streaming langsung?](https://intl.cloud.tencent.com/document/product/267/38393)

