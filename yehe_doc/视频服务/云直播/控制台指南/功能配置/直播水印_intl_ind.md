CSS mendukung fitur watermark. Watermark ditambahkan ke layar streaming langsung untuk melindungi konten video dari pencurian. Dokumen ini menjelaskan cara membuat, memodifikasi, mengikat, melepaskan ikatan, dan menghapus templat watermark di konsol.
**Anda dapat membuat templat watermark dengan cara berikut:**
- Membuat templat watermark di konsol CSS. Informasi lebih lanjut dapat dilihat di [Membuat Templat Watermark](#watermark).
- Membuat templat watermark dengan memanggil API. Informasi lebih lanjut dapat dilihat di [AddLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30826).


## Catatan
- Setelah membuat templat, Anda dapat mengikatnya ke nama domain push. Pengikatan akan diterapkan dalam waktu 5‒10 menit.
- Templat watermark dikelola di tingkat nama domain di konsol, dan untuk saat ini aturan yang dibuat oleh API di templat tidak dapat dibatalkan. Jika Anda telah mengikatkan konfigurasi watermark ke streaming tertentu melalui API pengelolaan watermark dan ingin melepaskan ikatan tersebut, Anda perlu memanggil API [DeleteLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30824).
- Mengikat, melepaskan ikatan, dan memodifikasi templat hanya memengaruhi streaming langsung baru setelah pembaruan, dan tidak memengaruhi streaming langsung yang sedang berjalan. Agar aturan baru diterapkan pada streaming langsung yang sedang berjalan, Anda perlu menghentikan sementara streaming langsung dan melakukan push lagi pada streaming tersebut.


## Prasyarat

Anda telah mengaktifkan layanan CSS dan menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970).

<span id="Watermark"></span>
## Membuat Templat Watermark

1. Login ke konsol CSS, lalu pilih **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark) (Konfigurasi Fitur > Pemberian Watermark Langsung).
2. Klik **Create Watermark Template** (Buat Templat Watermark).
3. Masukkan nama watermark, yang dapat berisi hingga 30 huruf, angka, garis bawah (_), dan tanda hubung (-).
4. Klik **Select image** (Pilih gambar) untuk mengunggah gambar sebagai watermark.
>! Agar efek visual optimal, watermark harus berupa gambar transparan dalam format .png dengan ukuran kurang dari 2 MB.
5. Tentukan lokasi watermark dengan cara berikut:
	- Seret gambar watermark di panel konfigurasi.
	- Sesuaikan koordinat sumbu X dan sumbu Y.
6. Klik **Save** (Simpan).
![](https://main.qcloudimg.com/raw/944534ffbf8625b36a8883087bdf29f6.png)

<span id="conect"></span>
## Mengikat Nama Domain

1. Login ke konsol CSS, lalu pilih **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark) (Konfigurasi Fitur > Pemberian Watermark Langsung).
2. Buka halaman pengikatan nama domain dengan salah satu cara berikut:
	- **Mengikat nama domain secara langsung**: klik **Bind Domain Name** (Ikat Nama Domain) di pojok kiri atas.
	- **Mengikat nama domain setelah membuat templat watermark**: setelah [templat watermark dibuat](#Watermark), klik **Bind Domain Name** (Ikat Nama Domain) di jendela pop-up.
3. Pilih **watermark template** (templat watermark) dan **push domain name** (nama domain push) di jendela pengikatan nama domain, lalu klik **Confirm** (Konfirmasi).
>? Anda dapat mengeklik **Add** (Tambahkan) untuk mengikat banyak nama domain push ke templat ini.

<span id="untie"></span>
## Melepaskan Ikatan
1. Login ke konsol CSS, lalu pilih **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark) (Konfigurasi Fitur > Pemberian Watermark Langsung).
2. Pilih nama domain yang terikat ke templat watermark dan klik **Unbind** (Lepaskan Ikatan).
3. Konfirmasi pelepasan ikatan nama domain, lalu klik **Confirm** (Konfirmasi) untuk melepaskan ikatan.

<span id="change"></span>
## Memodifikasi Templat
1. Buka **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark) (Konfigurasi Fitur > Pemberian Watermark Langsung).
2. Pilih templat watermark target, lalu klik **Edit** di sebelah kanan untuk mengubah informasi templat.
3. Klik **Save** (Simpan).

![](https://main.qcloudimg.com/raw/aceffbdffb9dd2b892500c97d8d1654f.png)

>? Anda dapat mengeklik **Preview** (Pratinjau) untuk melihat tampilan watermark di layar.

<span id="delete"></span>
## Menghapus Templat
Jika templat telah terikat ke nama domain tertentu, Anda harus melepaskan ikatan templat sebelum menghapusnya. Petunjuk mendetail dapat dilihat di [Melepaskan Ikatan](#untie).
1. Buka **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark) (Konfigurasi Fitur > Pemberian Watermark Langsung).
2. Temukan templat watermark target yang telah Anda buat, lalu klik ikon penghapusan ![img](https://main.qcloudimg.com/raw/220ada95a4b631349543cc8cde96226e.png) di bagian atas.
3. Di kotak dialog pop-up, klik **Confirm** (Konfirmasi) untuk mengonfirmasi penghapusan.

![](https://qcloudimg.tencent-cloud.cn/raw/7a405987e7494de1f4551b3e90d00408.png)

## Operasi Terkait
Informasi selengkapnya tentang cara **mengikat/melepaskan ikatan** **nama domain** ke/dari templat watermark dapat dilihat di [Watermark Configuration (Konfigurasi Watermark)](https://intl.cloud.tencent.com/document/product/267/31064).
