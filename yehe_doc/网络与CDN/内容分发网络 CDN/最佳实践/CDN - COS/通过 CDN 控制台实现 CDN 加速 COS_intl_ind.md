Dokumen ini menguraikan cara mempercepat akses ke sumber daya di COS melalui CDN.

## Prasyarat
1.Anda telah mendaftar akun Tencent Cloud dan memverifikasi identitas Anda.
2.Bucket COS telah dibuat.Untuk informasi selengkapnya, silakan lihat [Membuat Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Panduan Pengoperasian
### Menambahkan nama domain
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), klik **Domain Management** (Pengelolaan Domain) di bilah samping kiri untuk masuk ke halaman pengelolaan nama domain, dan klik **Create Distribution** (Buat Distribusi).<!
![](https://main.qcloudimg.com/raw/557bb679be9e43f75f3a9c399a11abde.png)

### Memilih COS sebagai server asal
![](https://main.qcloudimg.com/raw/ec7ea324171295b8fd0321e226d0e0a3.png)
1.Masukkan **domain name** (nama domain) yang akan dipercepat.
Nama domain kartubebas didukung, seperti `*.test.com`.Hingga 10 nama domain dapat dihubungkan secara batch dalam satu operasi.
Nama domain harus memenuhi syarat berikut:
- Izin ICP untuk layanan di Tiongkok Daratan telah diperoleh dari MIIT untuk nama domain
- Nama domain belum pernah dihubungkan ke Tencent Cloud CDN
2.Pilih **project** (proyek) nama domain.
Proyek dibagikan oleh semua produk Tencent Cloud.Anda dapat menambahkan proyek di [Pengelolaan Proyek](https://console.cloud.tencent.com/project).
3.Pilih **COS** (COS) dari daftar turun **Origin Type** (Jenis Asal) di bawah **Domain Configuration** (Konfigurasi Domain).
4.Pilih nama domain dari **bucket** (bucket) yang sesuai.
5.Aktifkan **Private Access Bucket** (Akses Bucket Pribadi).Anda harus mengizinkan layanan CDN terlebih dahulu.Setelah otorisasi layanan dikonfirmasi, Anda dapat mengaktifkan fitur ini secara manual.

>
>- COS V5 di-deploy sepenuhnya untuk menghubungkan nama domain server asal COS ke CDN.Jika Anda ingin menggunakan bucket COS V4 sebagai server asal, Anda harus membuka Konsol COS V4 dan mengaktifkan layanan akselerasi untuk bucket yang sesuai.
>- Jika bucket COS V5 Anda bersifat pribadi, Anda harus mengizinkan terlebih dahulu layanan CDN untuk mengakses bucket COS yang sesuai dan kemudian mengaktifkan akses tarik-asal.Sumber daya di semua bucket pribadi kemudian akan dikirimkan melalui jaringan publik CDN, yang melibatkan risiko keamanan relatif tinggi.

### Mengonfigurasi layanan akselerasi
Berdasarkan kebutuhan bisnis Anda, pilih **Business Type** (Jenis Bisnis), lalu atur **Basic Configuration** (Konfigurasi Dasar) dan **Cache Expiration Configuration** (Konfigurasi Kedaluwarsa Cache).
![](https://main.qcloudimg.com/raw/6264633c18801547e4aece61a94009cb.png)
1.**Business Type** (Jenis Bisnis)
Jenis bisnis menentukan platform sumber daya yang akan dijadwal menurut nama domain.Konfigurasi akselerasi bervariasi menurut platform sumber daya.Silakan pilih jenis bisnis berdasarkan kondisi bisnis Anda:
- Akselerasi statis:Cocok untuk skenario akselerasi sumber daya statis, seperti ecommerce, situs web, dan gambar game.
- Akselerasi unduhan:Cocok untuk skenario, seperti penginstalan game, unduhan audio/video, dan distribusi paket firmware telepon seluler.
- Akselerasi streaming VOD:Cocok untuk skenario akselerasi VOD.

2.**Basic Configuration** (Konfigurasi Dasar)
CDN menyediakan sakelar Ignore Query String (Abaikan String Kueri), yang memungkinkan Anda mengontrol apakah akan memfilter parameter setelah **"?"** pada URL permintaan pengguna akhir.Anda dapat menggunakan fitur ini untuk kontrol versi fleksibel atau autentikasi berbasis-token.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Abaikan string kueri](https://intl.cloud.tencent.com/doc/product/228/6291).

3.**Cache expiration configuration** (Konfigurasi kedaluwarsa cache)
Konfigurasi kedaluwarsa cache adalah serangkaian aturan kedaluwarsa yang harus dipatuhi simpul cache CDN saat meng-cache konten bisnis Anda.Untuk informasi selengkapnya, silakan lihat [Konfigurasi kedaluwarsa cache](https://intl.cloud.tencent.com/doc/product/228/6290).


### Menyelesaikan hubungan
Setelah memasukkan semua item konfigurasi di halaman **Create Distribution** (Buat Distribusi), klik **Submit** (Kirim) untuk menambahkan nama domain dan tunggu konfigurasi nama domain dikirimkan melalui seluruh jaringan, yang biasanya memerlukan waktu 5 hingga 10 menit.

### Mengonfigurasi CNAME
Setelah berhasil menambahkan nama domain, Anda dapat melihat CNAME akselerasi yang diberikan oleh CDN di halaman **Domain Management** (Pengelolaan Domain).Anda harus menambahkan rekaman CNAME untuk nama domain tersebut melalui penyedia layanan DNS Anda (seperti DNSPod).Layanan akselerasi akan tersedia setelah **the DNS configuration takes effect** (konfigurasi DNS berlaku).Untuk informasi selengkapnya, silakan lihat [Konfigurasi CNAME](https://intl.cloud.tencent.com/doc/product/228/3121).
