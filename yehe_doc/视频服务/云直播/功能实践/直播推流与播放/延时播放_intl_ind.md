Pemutaran ulang tertunda adalah fitur yang memungkinkan Anda menunda pemutaran streaming. Fitur ini umumnya digunakan dalam acara streaming langsung penting untuk memberi waktu kepada penyelenggara guna mengatasi kondisi darurat. Anda dapat mengaktifkan fitur ini melalui pengaturan parameter.

## Catatan
Anda dapat mengaktifkan pemutaran ulang tertunda dengan dua metode:
- Panggil [API penunda pemutaran ulang](https://intl.cloud.tencent.com/document/product/267/30850).
- Tambahkan parameter `txDelayTime` di belakang **push URL** (URL push). Keterangan mendetail dapat dilihat di bagian [Konfigurasi Push](#push_delay).

>? Metode API tidak dianjurkan karena pemanggilan API meliputi pembuatan cache konfigurasi sehingga perkiraan waktu diterapkannya fitur sulit diketahui. Anda sebaiknya mengaktifkan fitur ini menggunakan metode kedua.

## Persiapan
1. Aktifkan [CSS](https://console.cloud.tencent.com/live?from=product-banner-use-lvb).
2. Login ke konsol CSS, pilih [**Domain Management**](https://console.cloud.tencent.com/live/domainmanage) (Manajemen Domain), lalu klik **Add Domain Name** (Tambahkan Nama Domain) untuk menambahkan nama domain push. Informasi selengkapnya dapat dilihat di [Adding Domain Name (Menambahkan Nama Domain)](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:push_delay)
## Konfigurasi Push
1. Login ke konsol CSS, buka **CSS Toolkit** > [**Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) (Toolkit CSS > Pembuat Alamat), pilih **Push Domain** (Domain Push) untuk **Domain Type** (Jenis Domain), lalu klik **Generate Address** (Buat Alamat).
![](https://main.qcloudimg.com/raw/025aeea991996ddc35e6b61341714282.png)
2. Tambahkan `txDelayTime` di belakang alamat push, lalu lakukan push pada streaming melalui OBS. Untuk mendapatkan petunjuk mendetail, lihat [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).
![](https://main.qcloudimg.com/raw/11cc2aee28d263e5740b1b6d0701652f.png)
>! Atur `txDelayTime` ke jumlah detik sesuai dengan durasi penundaan pemutaran ulang yang Anda inginkan. Nilai harus dalam bentuk integer dan tidak boleh melebihi 600.


## Pemutaran Ulang Tertunda
1. Login ke konsol CSS, buka **CSS Toolkit** > [**Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) (Toolkit CSS > Pembuat Alamat), pilih **Playback Domain** (Domain Pemutaran Ulang) untuk **Domain Type** (Jenis Domain), lalu klik **Generate Address** (Buat Alamat).
2. Gunakan [VLC](https://intl.cloud.tencent.com/document/product/267/32483), FFmpeg, atau alat lain untuk pemutaran ulang. Informasi selengkapnya dapat dilihat di [Pemutaran Ulang CSS](https://intl.cloud.tencent.com/document/product/267/31559).

 Dalam gambar di atas, waktu penundaan yang diatur untuk pemutaran ulang melalui parameter `txDelayTime` di alamat push adalah 30 detik, dan latensi pemutaran ulang aktual adalah 34 detik, yang menunjukkan bahwa fitur pemutaran ulang tertunda sudah diterapkan.
