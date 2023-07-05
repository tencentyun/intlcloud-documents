Dokumen ini menguraikan cara mempercepat akses ke layanan CVM melalui CDN pada konsol.

## Prasyarat
1.Anda telah mendaftar akun Tencent Cloud dan memverifikasi identitas Anda.
2.Anda telah mengaktifkan layanan CVM.Untuk informasi selengkapnya, silakan lihat [Memulai CVM](https://intl.cloud.tencent.com/document/product/213/2936).


## Panduan Pengoperasian

### Menambahkan nama domain

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), klik **Domain Management** (Pengelolaan Domain) pada bilah samping kiri untuk masuk ke halaman pengelolaan nama domain, dan klik **Create Distribution** (Buat Distribusi).
![](https://main.qcloudimg.com/raw/0d7c11a53f663ac8554f59e777dc01e7.png)

### Mengonfigurasi nama domain
![](https://main.qcloudimg.com/raw/be5e2b251bbcbcc674242062684649c1.png)
1.Masukkan **domain name** (nama domain) yang akan dipercepat.
Nama domain kartubebas didukung, seperti `*.test.com`.Hingga 10 nama domain dapat dihubungkan secara batch dalam satu operasi.
Nama domain harus memenuhi syarat berikut:
- Izin ICP untuk layanan di Tiongkok Daratan telah diperoleh dari MIIT untuk nama domain
- Nama domain belum pernah dihubungkan ke Tencent Cloud CDN
2.Pilih **project** (proyek) nama domain.
Proyek dibagikan oleh semua produk Tencent Cloud.Anda dapat menambahkan proyek di [Pengelolaan Proyek](https://console.cloud.tencent.com/project).
3.Pilih **Origin Server Type** (Jenis Server Asal) dan masukkan **Origin Server Configuration** (Konfigurasi Server Asal).
Untuk informasi selengkapnya mengenai jenis server asal, silakan lihat [Menghubungkan nama domain ke CDN](https://intl.cloud.tencent.com/document/product/228/5734).
Masukkan **CVM public network address** (alamat jaringan publik CVM) pada pengaturan server asal.

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


>Menurut peraturan, jika server asal berada di nama domain Tencent Cloud CVM yang dipercepat, nama domain yang dikonfigurasikan untuk header host harus mendapat izin ICP untuk layanan di Tiongkok Daratan melalui Tencent Cloud.Untuk informasi selengkapnya, silakan lihat [Konfigurasi header host](https://intl.cloud.tencent.com/document/product/228/6293).
