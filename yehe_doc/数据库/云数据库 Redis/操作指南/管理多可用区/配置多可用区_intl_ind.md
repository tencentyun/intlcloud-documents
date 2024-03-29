Dokumen ini menjelaskan cara mengonfigurasi beberapa zona ketersediaan untuk instans TencentDB for Redis Anda dan cara melihatnya di konsol.

## Ikhtisar
Anda dapat men-deploy node master TencentDB for Redis dan node replika di zona ketersediaan yang berbeda di wilayah yang sama. [Instans yang di-deploy multi-AZ](https://intl.cloud.tencent.com/document/product/239/39812) memiliki ketersediaan yang lebih tinggi dan kemampuan pemulihan bencana yang lebih baik daripada instans yang di-deploy AZ tunggal.
- Pemisahan baca/tulis dinonaktifkan (yaitu, replika dapat ditulis ke dan dibaca dari): permintaan tulis/baca di zona ketersediaan replika dirutekan oleh proksi ke node master, dan node master disinkronkan dengan node replika guna memastikan data yang konsisten di semua node. Dalam proses ini, hanya terjadi satu akses lintas-AZ.
- Pemisahan baca/tulis diaktifkan (yaitu, replika hanya dapat dibaca dari): permintaan tulis dirutekan oleh proksi ke node master, tetapi permintaan baca di zona ketersediaan replika dirutekan ke node replika di zona ketersediaan replika yang sama sehingga bahwa permintaan baca dapat ditanggapi oleh node terdekat.

Kami sarankan Anda men-deploy satu node master dan satu replika di zona ketersediaan master, dan node replika lainnya di zona ketersediaan yang berbeda. Jika node master gagal, node replika di zona ketersediaan master dapat dipromosikan dengan cepat guna menghindari peralihan replika master lintas-AZ. Solusi deployment seperti itu dapat memaksimalkan ketersediaan layanan dan mengurangi penundaan yang disebabkan oleh kegagalan node master.

>?Saat ini, instans TencentDB for Redis 4.0 dan 5.0 dalam arsitektur standar atau cluster mendukung deployment multi-AZ.


## Petunjuk
### Mengaktifkan deployment multi-AZ
1. Login ke [Halaman Pembelian Redis](https://buy.cloud.tencent.com/redis), tentukan informasi instans, termasuk wilayah, zona ketersediaan, dan replika, lalu klik **Beli Sekarang**.
 - Jumlah replika: jumlah maksimum zona ketersediaan = jumlah replika + 1.
 - Zona ketersediaan: deploy node Redis di zona ketersediaan yang berbeda. Hingga enam zona ketersediaan yang didukung.
![](https://main.qcloudimg.com/raw/d76a6c8cc996b58c8f5df1a17102111c.png)
2. Setelah selesai melakukan pembelian, Anda akan dialihkan ke daftar instans. Setelah status instans berubah menjadi **Berjalan**, instans dapat digunakan secara normal.

### Melihat deployment multi-AZ
- Login ke [Konsol TencentDB for Redis](https://console.cloud.tencent.com/redis). Di kolom **Zona Ketersediaan** dalam daftar instans, label **M** menunjukkan bahwa node instans ini di-deploy di beberapa zona ketersediaan. Arahkan mouse ke label tersebut untuk melihat detail.
![](https://main.qcloudimg.com/raw/5c553bf4c0817c0dbddb662405078fe7.png)
- Di [daftar instans](https://console.cloud.tencent.com/redis), klik ID/nama instans dan masuk ke halaman manajemen instans. Di bagian **Basic Info** (Info Dasar) pada tab **Instance Details** (Detail Instans), label **M** di dekat **Availability Zone** (Zona Ketersediaan) menunjukkan bahwa node instans ini di-deploy di beberapa zona ketersediaan. Arahkan mouse ke label tersebut untuk melihat detail.
![](https://main.qcloudimg.com/raw/d579e1ab309c754ef0ea56904ad5f194.png)
- Di [daftar instans](https://console.cloud.tencent.com/redis), klik ID/nama instans dan masuk ke halaman manajemen instans. Pada tab **Manage Node** (Kelola Node), Anda dapat melihat detail node dan menyesuaikan konfigurasi node.
![](https://main.qcloudimg.com/raw/aa0adb39b9bfb543051ca6bdfda78664.png)
