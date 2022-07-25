Jika peristiwa yang dikonfigurasikan dalam templat memicu panggilan balik selama streaming langsung, Tencent Cloud akan mengirimkan permintaan ke server pelanggan yang bertanggung jawab atas respons tersebut. Setelah berhasil melewati verifikasi, server akan mendapatkan paket JSON panggilan balik.

Saat ini, peristiwa berikut dapat memicu pemberitahuan selama streaming langsung: push streaming, interupsi streaming, perekaman, pengambilan tangkapan layar, dan deteksi pornografi.

## Detail Lengkap Proses

<img src="https://main.qcloudimg.com/raw/252b7e06b322350c8520283e7826d5a3.png" data-nonescope="true">

**Deskripsi Proses:**
1. Host mengonfigurasikan URL pemberitahuan pesan peristiwa dan fitur, seperti perekaman dan pengambilan tangkapan layar, di konsol atau dengan memanggil API TencentCloud.
2. Host melakukan push dan menghentikan streaming.
3. Ketika suatu peristiwa terjadi, pesan akan dikirimkan ke backend pelanggan melalui layanan pemberitahuan pesan peristiwa.


[](id:protocol)
## Protokol Pemberitahuan Pesan Peristiwa

### Protokol jaringan
- Permintaan: Permintaan HTTP POST dengan paket JSON. Konten paket spesifik untuk setiap jenis pesan akan dijelaskan di bagian selanjutnya.
- Respons: Kode status HTTP = 200. Server mengabaikan konten spesifik di paket respons. Untuk memastikan kompatibilitas dengan protokol, Anda sebaiknya menambahkan `JSON: `{"code":0}`` ke respons.

### Keandalan pemberitahuan
Layanan pemberitahuan peristiwa memiliki mekanisme percobaan ulang. Untuk peristiwa pengambilan tangkapan layar, maksimum 5 percobaan ulang akan dilakukan dengan interval 2 menit. Untuk peristiwa push streaming, interupsi streaming, perekaman, dan deteksi pornografi, maksimum 12 percobaan ulang akan dilakukan dengan interval 1 menit.
Agar percobaan ulang dengan frekuensi sering tidak terlalu membebani server dan bandwidth Anda, pastikan paket respons ditampilkan sebagaimana diharapkan. Percobaan ulang akan terpicu dalam kasus-kasus berikut:
- Tidak ada paket respons yang ditampilkan dalam waktu lama (minimal 20 detik).
- Kode status HTTP di respons bukan `200`.

[](id:configuration)
## Cara Mengonfigurasi Panggilan Balik Peristiwa
Anda dapat mengonfigurasi panggilan balik melalui [konsol CSS](#c_callback) atau [API server](#api_callback).
>?CSS membantu Anda mengonfigurasikan URL panggilan balik secara terpisah untuk peristiwa push streaming, interupsi streaming, perekaman, pengambilan tangkapan layar, dan deteksi pornografi.



[](id:c_callback)
### Konsol CSS
1. Login ke konsol CSS dan klik **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)** (Pusat Peristiwa > Panggilan Balik Streaming Langsung) untuk membuat templat panggilan balik. Petunjuk mendetail dapat dilihat di [Creating a Callback Template (Membuat Templat Panggilan Balik)](https://intl.cloud.tencent.com/document/product/267/31074).
2. Klik **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) untuk menemukan nama domain push target, lalu klik **Manage** > **Template Configuration** (Kelola > Konfigurasi Templat) untuk mengikatkannya dengan templat panggilan balik. Petunjuk lengkapnya dapat dipelajari di [Callback Configuration (Konfigurasi Panggilan Balik)](https://intl.cloud.tencent.com/document/product/267/31065).

[](id:api_callback)
### API Server
1. Panggil API [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815) untuk membuat templat panggilan balik dan mengatur parameter panggilan balik.
2. Panggil API [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816) untuk mengatur parameter `DomainName` (nama domain push) dan `TemplateId` (kembali ke langkah 1). Masukkan `AppName` ke URL push dan pemutaran ulang untuk mengaktifkan panggilan balik untuk streaming langsung tertentu.

## Parameter Panggilan Balik
Setelah templat berhasil diikatkan dengan nama domain, jika peristiwa yang dikonfigurasikan di templat terpicu selama streaming langsung, Tencent Cloud akan mengirimkan paket JSON yang berisi informasi panggilan balik ke server pelanggan. Berikut adalah penjelasan terperinci seputar parameter panggilan balik:
- [Stream push event notification (Pemberitahuan peristiwa push streaming)](https://intl.cloud.tencent.com/document/product/267/38081)
- [Stream interruption event notification (Pemberitahuan peristiwa interupsi streaming)](https://intl.cloud.tencent.com/document/product/267/38081)
- [Recording event notification (Pemberitahuan peristiwa perekaman)](https://intl.cloud.tencent.com/document/product/267/38082)
- [Screencapture event notification (Pemberitahuan peristiwa pengambilan tangkapan layar)](https://intl.cloud.tencent.com/document/product/267/38083)
- [Porn detection event notification (Pemberitahuan peristiwa deteksi pornografi)](https://intl.cloud.tencent.com/document/product/267/38084)






