Dengan dukungan kemampuan perekaman CSS, fitur pergeseran waktu memungkinkan pemirsa untuk memutar balik dan memutar ulang streaming video dari titik waktu sebelumnya. Ketika pergeseran waktu diaktifkan untuk domain pemutaran ulang VOD, URL segmen TS dan file TS untuk video akan disimpan dalam VOD sehingga pengguna dapat memutar ulang konten video sebelumnya dengan melewati parameter waktu di URL permintaan untuk domain pemutaran ulang terkait.



## Cara Kerja
Dalam streaming HLS, streaming video dibagi menjadi beberapa segmen TS. Pemirsa menggunakan file M3U8 untuk mengakses URL segmen TS, mendapatkan file TS, dan memutar konten video yang dimulai dari segmen TS tersebut.
>! File TS tidak disimpan secara permanen sehingga ada batas terkait seberapa jauh waktu ke belakang pemutaran balik dapat dimulai.


## Catatan
Sejauh ini, fitur pergeseran waktu masih dalam pengujian beta. Namun, kami akan mulai mengenakan biaya untuk penggunaan fitur ini mulai pukul **0.:00 pada tanggal 1 Juni 2022**. Keterangan terperinci dapat dilihat di [Notice: Time Shifting to Become Paid Feature (Pemberitahuan: Pergeseran Waktu Akan Menjadi Fitur Berbayar)](https://intl.cloud.tencent.com/document/product/267/46847). Pergeseran waktu mengandalkan perekaman sehingga Anda juga akan dikenai [biaya perekaman langsung](https://intl.cloud.tencent.com/document/product/267/39605) oleh CSS dan [biaya penyimpanan dan pemutaran ulang](https://intl.cloud.tencent.com/document/product/266/2838) oleh VOD.

## Cara Menggunakan Pergeseran Waktu

### Prasyarat

- Anda sudah [membuat akun Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985). 
- Anda sudah mengaktifkan CSS dan menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970). 

[](id:step1)
### Langkah 1. Mengaktifkan VOD

1. Login ke [konsol VOD](https://console.cloud.tencent.com/vod/overview) dan klik **Activate Now** (Aktifkan Sekarang).
2. Pilih kotak centang untuk menyetujui perjanjian layanan, lalu klik **OK** (Oke) untuk mengaktifkan VOD.

[](id:step2)
### Langkah 2. Menambahkan nama domain

Ikuti langkah-langkah berikut untuk menambahkan nama domain VOD untuk pergeseran waktu:

1. Buka konsol VOD dan pilih **Distribution and Playback > Domain Name** (Distribusi dan Pemutaran Ulang > Nama Domain) di bilah sisi kiri.
2. Klik **Add Domain** (Tambahkan Domain) dan masukkan nama domain VOD yang sudah terdaftar dengan nomor izin ICP. Informasi selengkapnya dapat dilihat di [Distribution and Playback Settings (Pengaturan Distribusi dan Pemutaran Ulang)](https://intl.cloud.tencent.com/document/product/266/35572).
3. Tambahkan rekaman CNAME untuk domain tersebut.

[](id:step3)
### Langkah 3. Mengikat templat perekaman

1. Buka konsol CSS dan pilih **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)** (Konfigurasi Fitur > Perekaman Langsung).
2. Klik **Create Recording Template** (Buat Templat Perekaman). Petunjuk mendetail seputar pembuatan templat perekaman dapat dilihat di [Live Recording (Perekaman Langsung)](https://intl.cloud.tencent.com/document/product/267/34223).
> ! 
> - Pilih **HLS** sebagai format perekaman.
> - Masukkan periode penyimpanan kustom, yang tidak boleh lebih singkat dari [durasi pergeseran waktu](#step4).
3. Ikat templat perekaman dengan domain push yang ingin Anda gunakan. Petunjuk mendetail dapat dilihat di [Recording Configuration (Konfigurasi Perekaman)](https://intl.cloud.tencent.com/document/product/267/34224).

[](id:step4)
### Langkah 4. Mengaktifkan pergeseran waktu

[Kirim tiket](https://console.cloud.tencent.com/workorder/category?step=0&source=0) untuk mengaktifkan fitur pergeseran waktu. Anda harus memilih **CSS** sebagai produk dan memberikan informasi berikut:

- **VOD domain name** (nama domain VOD) yang ditambahkan di [Langkah 2](#step2).
- ID templat perekaman yang ditambahkan di [Langkah 3](#step3).
- Nilai kustom (detik) untuk `timeshift_dur` (durasi pergeseran waktu).
> ? 
> - Durasi pergeseran waktu menunjukkan seberapa jauh ke belakang dari waktu saat ini streaming video dapat Anda putar ulang. Saat ini, durasi pergeseran waktu terlama yang diizinkan adalah 7 hari.
>- Karena durasi pergeseran waktu yang Anda konfigurasikan mungkin tidak sama persis dengan durasi pergeseran waktu aktual, Anda sebaiknya mengatur durasi sedikit lebih lama dari durasi aktual yang Anda butuhkan.
>- Sebagai contoh, jika parameter diatur ke `7200` (2 jam), Anda dapat meminta konten yang dihasilkan dalam periode maksimum 2 jam lalu, dan rentang nilai untuk parameter penundaan pemutaran ulang `delay` adalah 90 detik hingga 2 jam. Jika `delay` diatur ke nilai lebih dari 2 jam, `HTTP 404` akan ditampilkan meskipun ada konten streaming langsung pada titik waktu tersebut. 



## Permintaan Pemutaran Ulang

### Format URL permintaan

```
http://[Domain]/timeshift/[AppName]/[StreamName]/timeshift.m3u8?delay=xxx
```

### Deskripsi parameter

| Parameter           | Deskripsi                                                         |
| -------------- | ------------------------------------------------------------ |
| [Domain]       | Nama domain VOD yang ditambahkan di [Step 2](#step2) untuk pergeseran waktu.     |
| timeshift      | Parameter tidak dapat dikustomisasi.                                           |
| [AppName]      | Nama aplikasi. Sebagai contoh, jika nama aplikasi Anda adalah `live`, masukkan `live` untuk parameter ini.           |
| [StreamName]   | Nama streaming. Atur parameter ini ke nama streaming yang pergeseran waktunya ingin Anda aktifkan.                                 |
| timeshift.m3u8 | Parameter tidak dapat dikustomisasi.                                           |
| delay          | Waktu penundaan pemutaran ulang (detik). Jika Anda memasukkan nilai lebih kecil dari `90`, `90` akan digunakan.|

### Contoh

Misalnya, nama domain pergeseran waktu adalah `testtimeshift.com`, nama aplikasi adalah `live`, dan nama streaming adalah `SLPUrIFzGPE`. Untuk memutar ulang konten video dari 5 menit lalu, Anda sebaiknya menggunakan URL permintaan berikut:

```
http://testtimeshift.com/timeshift/live/SLPUrIFzGPE/timeshift.m3u8?delay=300
```
