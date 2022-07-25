## Persiapan
1. Aktifkan [layanan CSS](https://console.cloud.tencent.com/live?from=product-banner-use-lvb).
2. Login ke [konsol CSS](https://console.cloud.tencent.com/live/livestat) untuk mendapatkan URL push langsung. Petunjuk mendetail dapat dilihat di [Live Push (Push Langsung)](https://intl.cloud.tencent.com/document/product/267/31558).
3. Pilih [Domain Management (Manajemen Domain)](https://console.cloud.tencent.com/live/domainmanage), klik **Add Domain** (Tambahkan Domain), masukkan nama domain Anda, pilih **Playback Domain** (Domain Pemutaran Ulang) sebagai jenis, lalu klik **Save** (Simpan).
4. Login ke [Tencent Cloud Domain Service Console (Konsol Layanan Domain Tencent Cloud)](https://console.cloud.tencent.com/domain) dan konfigurasikan CNAME untuk nama domain pemutaran ulang yang berhasil ditambahkan. Petunjuk mendetail dapat dilihat di [Konfigurasi CNAME Nama Domain](https://intl.cloud.tencent.com/document/product/267/31057).

## Mendapatkan URL Pemutaran Ulang
Pilih **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Toolkit CSS > Pembuat Alamat) untuk mendapatkan URL pemutaran ulang dan lakukan konfigurasi sebagai berikut:
- Pilih **Playback Domain** (Domain Pemutaran Ulang) sebagai jenis URL.
- Pilih nama domain pemutaran ulang yang telah Anda tambahkan di **Domain Management** (Manajemen Domain).
- Pilih `StreamName` yang sama dengan yang ada di URL push. `StreamName` URL pemutaran ulang harus sama dengan yang ada di URL push agar streaming yang sesuai dapat diputar.
- Pilih waktu kedaluwarsa URL, misalnya `2019-10-18 23:59:59`.
- Klik **Generate Address** (Buat Alamat).
![](https://main.qcloudimg.com/raw/a2f130098eb40df252956ffb3752d230.png)

>? Selain menggunakan metode di atas, Anda dapat memilih nama domain pemutaran ulang di **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) di konsol CSS dengan mengeklik **Manage** (Kelola), memilih **Playback Configuration** (Konfigurasi Pemutaran Ulang), memasukkan waktu kedaluwarsa untuk URL pemutaran ulang dan `StreamName` yang sama dengan yang ada di URL push, dan mengeklik **Generate Playback Address** (Buat Alamat Pemutaran Ulang).

## Pemutaran Ulang Langsung
[Live push (push langsung)](https://intl.cloud.tencent.com/document/product/267/31558) harus berhasil agar streaming dapat ditonton melalui URL pemutaran ulang. Anda dapat menggunakan metode berikut untuk menguji streaming langsung berdasarkan skenario bisnis Anda:

### Skenario 1. Pemutaran ulang di klien PC
Anda dapat menggunakan alat, seperti [VLC](https://intl.cloud.tencent.com/document/product/267/32483), FFmepg, dan [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/player/demo/player.html) untuk pemutaran ulang.
![](https://main.qcloudimg.com/raw/e47f8d4d9ca63e678439df3e8a17c9b4.png)
### Skenario 2. Pemutaran ulang di klien seluler
1. Unduh dan instal [Toolkit Tencent Cloud](https://intl.cloud.tencent.com/document/product/1016/30285).
2. Pilih **MLVB** > **LVB Playback** (Pemutaran Ulang LVB) atau **LEB Playback** (Pemutaran Ulang LEB).
3. Masukkan URL pemutaran ulang di kotak input atau pindai kode QR URL pemutaran ulang.
4. Ketuk tombol putar di sudut kiri bawah untuk memulai pemutaran ulang.

### Skenario 4. Pemutaran ulang di web
Anda sebaiknya memilih TCPlayerLite di SDK pemutar untuk pemutaran ulang. Berdasarkan fungsionalitas backend dan teknologi AI Tencent Cloud yang andal, TCPlayerLite memberikan kemampuan pemutaran ulang yang sangat baik untuk streaming langsung dan video sesuai permintaan. Integrasi yang kuat dengan layanan LVB dan VOD Tencent Cloud membuat Player+ mampu memberikan performa pemutaran ulang, penempatan iklan, dan pemantauan data yang lancar dan stabil.
>! Saat ini, sebagian besar browser seluler di pasaran tidak mendukung pemutaran ulang HTTP-FLV. Oleh karena itu, untuk pemutaran ulang berbasis web, Anda sebaiknya memilih protokol pemutaran ulang HTTP-FLV untuk browser PC dan HLS untuk browser seluler. 

## Pertanyaan Umum
- [Protokol pemutaran ulang apa saja yang didukung?](https://intl.cloud.tencent.com/document/product/267/7968)
- [Alamat pemutaran ulang terdiri dari bagian apa saja?](https://intl.cloud.tencent.com/document/product/267/7968)
- [Bagaimana cara menggunakan transcoding langsung?](https://intl.cloud.tencent.com/document/product/267/35598)
- [Bagaimana cara menggunakan pergeseran waktu untuk pemutaran ulang?](https://intl.cloud.tencent.com/document/product/267/35598)
- [Bagaimana cara menggunakan HTTPS untuk pemutaran ulang?](https://intl.cloud.tencent.com/document/product/267/35598)
- [Bagaimana cara menggunakan node cache global untuk pemutaran ulang?](https://intl.cloud.tencent.com/document/product/267/35598)
- [Bagaimana cara mengaktifkan perlindungan hotlink?](https://intl.cloud.tencent.com/document/product/267/35598#que2)

