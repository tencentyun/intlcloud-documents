Dokumen ini menjelaskan cara membuat instance CLB Klasik jaringan publik bernama `clb-test` dan meneruskan permintaan dari klien ke dua server asli.

## Prasyarat
1.CLB hanya meneruskan lalu lintas tetapi tidak dapat memproses permintaan; oleh karena itu, Anda harus memiliki instance CVM yang memproses permintaan pengguna.
Dalam contoh ini, dua instance CVM sudah cukup, tetapi Anda juga dapat mengonfigurasi instance lebih banyak lagi.Instance CVM `rs-1` dan `rs-2` telah dibuat di wilayah Guangzhou dalam contoh ini.Untuk informasi selengkapnya tentang cara membuat instance CVM, lihat [Membeli dan Meluncurkan Instance CVM](https://intl.cloud.tencent.com/document/product/213/4855).
2.Dokumen ini mengambil penerusan HTTP sebagai contoh.Server web yang sesuai (seperti Apache, Nginx, atau IIS) harus di-deploy pada instance CVM.
Untuk memverifikasi hasil, dalam contoh ini, Apache di-deploy di `rs-1` dan juga `rs-2`.Apache mengembalikan "Halo Tomcat!Ini adalah rs-1!"di `rs-1` dan "Halo Tomcat!Ini adalah rs-2!"di `rs-2`.Untuk informasi selengkapnya tentang cara men-deploy komponen pada instance CVM, lihat [Men-deploy Web Java di Linux (CentOS)](https://intl.cloud.tencent.com/document/product/214/32391) dan [Menginstal dan Mengonfigurasi PHP di Windows](https://intl.cloud.tencent.com/document/product/213/10182).
3.Akses IP publik dan jalur instance CVM Anda.Jika halaman yang di-deploy ditampilkan, layanan telah berhasil di-deploy.
>!
> - Untuk akun tambahan, bandwidth jaringan publik harus dibeli untuk instance CVM karena bandwidth ditagih oleh CVM, bukan CLB.Anda dapat menentukan jenis akun sesuai petunjuk di [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/214/36999).
>- Dalam contoh, nilai yang dikembalikan oleh layanan yang di-deploy di dua server asli adalah berbeda.Dalam skenario aktual, layanan yang sama biasanya harus di-deploy di semua server asli untuk memastikan agar semua pengguna memiliki pengalaman yang seragam.

## Membeli Instance CLB Klasik
1.Masuk ke situs web resmi Tencent Cloud dan buka [halaman pembelian CLB](https://buy.cloud.tencent.com/lb).
2.Dalam contoh ini, pilih **Guangzhou** sebagai wilayah yang sama dengan wilayah di instance CVM.Pilih **Classic** (Klasik) sebagai jenis instance, **Public Network** (Jaringan Publik) sebagai atribut jaringan, dan **Default-VPC (Default)** sebagai jaringan dan masukkan "clb-test" sebagai nama instance.
3.Klik **Buy Now** (Beli Sekarang) dan lakukan pembayaran.Untuk informasi selengkapnya tentang instance CLB, silakan lihat [Pilihan Atribut Produk](https://intl.cloud.tencent.com/document/product/214/13629).
4.Di halaman "CLB Instance List" (Daftar Instance CLB), pilih wilayah yang sesuai untuk melihat instance yang baru saja dibuat.
![](https://main.qcloudimg.com/raw/183ac407a68c4aafe440aa2c111a154e.png)

## Membuat Pendengar CLB
Pendengar CLB meneruskan permintaan dengan menetapkan protokol dan port.Dokumen ini mengambil konfigurasi meneruskan permintaan klien HTTP menggunakan CLB sebagai contoh.
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2.Di "CLB Instance List" (Daftar Instance CLB), cari instance CLB Klasik `clb-test` yang dibuat dan klik ID-nya untuk masuk ke halaman detail.
3.Di bagian "Basic Info" (Info Dasar), Anda dapat mengeklik "Edit" (Edit) di samping nama instance untuk mengganti namanya.
4.Di **Listeners** (Pendengar) di "Manajemen Pendengar", klik **Create** (Buat) untuk membuat pendengar CLB.
![](https://main.qcloudimg.com/raw/df7de6ac8996718bc5176b14f25cd3cb.png)
5.Di jendela pop-up, konfigurasikan berikut ini:
- Atur nama ke "Listener1" (Pendengar1).
- Atur protokol dan port pendengar ke `HTTP:80`.
- Atur port backend ke `80`.
- Pilih "WRR" sebagai mode penyeimbang muatan.
- Jangan periksa persistensi sesi.
- Aktifkan pemeriksaan kesehatan.
![](https://main.qcloudimg.com/raw/41cbc18c096ed2f6c01a238dc426963e.png)
6.Klik **Complete** (Selesaikan) untuk membuat pendengar CLB.

Untuk informasi selengkapnya tentang pendengar CLB, lihat [Ikhtisar Pendengar CLB](https://intl.cloud.tencent.com/document/product/214/6151).

## Mengikat Server Asli
1.Di "CLB Instance List" (Daftar Instance CLB), cari `clb-test` yang dibuat dan klik ID-nya untuk masuk ke halaman detail.
2.Di modul "Bind Real Server" (Ikat Server Asli) di “Manajemen Pendengar", klik **Bind** (Ikat).
![](https://main.qcloudimg.com/raw/a1c1ba2fa1b95a27a534a2446c381fc3.png)
3.Di jendela pop-up, pilih instance CVM `rs-1` dan `rs-2` di wilayah yang sama dengan instance CLB dan pertahankan bobot default "10" untuk instance tersebut.
4.Klik **OK** (Oke) untuk menyelesaikan pengikatan.
![](https://main.qcloudimg.com/raw/0c9f911e40621ff3615ac47d94651329.png)
5.Perluas pendengar **Listener1** (Pendengar1).Anda dapat melihat status pemeriksaan kesehatan dari instance CVM backend.Status "Healthy" (Sehat) menunjukkan bahwa instance CVM dapat memproses dengan semestinya permintaan yang diteruskan oleh CLB.


## Mengonfigurasi Grup Keamanan
Setelah membuat instance CLB, Anda dapat mengonfigurasi grup keamanan CLB untuk mengisolasi lalu lintas jaringan publik.Untuk informasi selengkapnya, silakan lihat [Mengonfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).
Setelah mengonfigurasi grup keamanan, Anda dapat memilih mengaktifkan atau menonaktifkan "Allow Traffic by Default in Security Group" (Izinkan Lalu Lintas secara Default di Grup Keamanan) dengan konfigurasi yang berbeda sebagai berikut:

### Metode 1.Aktifkan "Allow Traffic by Default in Security Group" (Izinkan Lalu Lintas secara Default di Grup Keamanan)
>?Fitur ini sedang dalam pengujian beta.Untuk mencobanya, silakan kirim tiket permohonan.Fitur ini tidak didukung untuk CLB jaringan privat klasik.
>
Untuk mendapatkan petunjuk lengkap, silakan lihat [Mengonfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).


### Metode 2.Izinkan IP klien di dalam grup keamanan CVM
Untuk mendapatkan petunjuk lengkap, silakan lihat [Mengonfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).

## Memverifikasi Layanan CLB
1.Masukkan alamat layanan dan port CLB `http://vip:80` ke peramban untuk menguji layanan CLB.Jika pesan ditampilkan seperti di bawah ini, permintaan telah diteruskan ke instance CVM `rs-1` oleh CLB, dan instance CVM telah memproses permintaan dengan semestinya dan mengembalikan hasilnya.
![](https://main.qcloudimg.com/raw/5a7cb3e86d04149978b90050546a2983.png)
2.Algoritme round robin dari pendengar berupa "round robin tertimbang", dan bobot kedua instance CVM sama-sama "10".Jika Anda memuat ulang halaman web di peramban untuk mengirim permintaan baru, Anda dapat melihat bahwa permintaan tersebut diteruskan ke instance CVM `rs-2` oleh CLB.
![](https://main.qcloudimg.com/raw/8f9f5f667461a5d0efd3e6b2bbe859f3.png)
>!
>- Jika persistensi sesi dinonaktifkan dan metode round-robin digunakan untuk penjadwalan, permintaan akan ditetapkan ke server asli yang berbeda secara berurutan.
>- Jika persistensi sesi diaktifkan, atau dinonaktifkan tetapi penjadwalan ip_hash digunakan, permintaan akan selalu ditetapkan ke server asli yang sama.
