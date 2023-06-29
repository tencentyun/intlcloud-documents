
## Fitur

Tencent Cloud CDN mendukung pengelolaan versi untuk satu nama domain.Anda dapat membuat satu konfigurasi untuk setiap versi nama domain, dan men-deploy-nya di lingkungan produksi dan lingkungan percobaan.

- Lingkungan produksi: lingkungan operasional tempat layanan akselerasi diterapkan.
- Lingkungan percobaan: lingkungan pengujian untuk menguji konfigurasi nama domain saja.Lingkungan ini dibuat dalam skala kecil dan hanya digunakan untuk pengujian konfigurasi nama domain pada konsol.Lingkungan ini tidak boleh digunakan untuk menjalankan bisnis yang sebenarnya atau untuk pengujian kinerja.

>!
>1.Wilayah akselerasi harus di Tiongkok daratan.Nama domain tidak boleh menggunakan sertifikat eksternal, dan fitur Optimisasi Gambar tidak boleh diaktifkan.
>2.Hanya satu versi yang dapat di-deploy dalam satu waktu di setiap lingkungan.
>3.Penyegaran URL didukung di lingkungan produksi dan lingkungan percobaan, sedangkan penyegaran direktori dan pramuat URL hanya diizinkan di lingkungan produksi.Untuk informasi selengkapnya, lihat [Pembersihan dan Pramuat](https://intl.cloud.tencent.com/document/product/228/6299).
>4.Fitur pemantauan data dan penggunaan, seperti [konfigurasi batas bandwidth](https://intl.cloud.tencent.com/document/product/228/7541), hanya tersedia di lingkungan produksi.


## Kasus Penggunaan

- Dapat diterapkan pada pengujian beta untuk konfigurasi nama domain



[](id:open)
## Mengaktifkan Pengelolaan Versi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan pilih **Domain Management** (Pengelolaan Domain) untuk melihat daftar nama domain.Klik nama domain sasaran untuk masuk ke halaman konfigurasi, dan centang **Enable Version Management** (Aktifkan Pengelolaan Versi) di pojok kanan atas.
![](https://main.qcloudimg.com/raw/52d05f1d49c1143e572d5bd2ff7cb88c.png)

Setelah pengelolaan versi diaktifkan, Ver.1 akan dibuat dengan konfigurasi nama domain saat itu dan di-deploy ke lingkungan produksi maupun lingkungan percobaan.

## Mengelola Versi

Setelah mengaktifkan pengelolaan versi, Anda dapat melihat dan mengelola versi di halaman **Version Management** (Pengelolaan Versi).Setiap versi diidentifikasi dengan nomor versi Ver.n (n=1,2,3,...).
Untuk mengakses halaman pengelolaan versi, Anda dapat memilih **More** > **Version Management** (Selengkapnya > Pengelolaan Versi) di bawah kolom operasi pada daftar nama domain.Anda juga bisa mengeklik nama domain untuk mencari **Version Management** (Pengelolaan Versi) di halaman konfigurasinya.
![](https://main.qcloudimg.com/raw/6d74d6b53b75ef97a63926718f50cda4.png)



### Menambahkan Versi
Klik **Add Version** (Tambahkan Versi).Suatu versi akan dibuat berdasarkan konfigurasi lingkungan produksi saat itu menurut pengaturan default.Anda dapat mengubah konfigurasi sesuai kebutuhan dan kemudian membuat versi baru.
![](https://main.qcloudimg.com/raw/7d6277fad76dd1391f9be965c4c99df0.png)

>! Jika Anda mendapat pesan kesalahan setelah mengirimkan versi baru tersebut, Anda tidak perlu membuat yang baru.Kembali ke halaman pengelolaan versi dan ubah versi yang Anda kirimkan.

### Mengedit versi

Versi terbaru dapat diedit sebelum dirilis ke lingkungan percobaan.Anda dapat memilih **More** > **Edit** (Selengkapnya > Edit) di bawah kolom operasi.
![](https://main.qcloudimg.com/raw/ccd2e75a24c5076c0a624b5cd8cbbecb.png)
Versi lama (semua versi sebelum versi terbaru), walaupun telah dirilis ke lingkungan percobaan, hanya dapat dilihat, tetapi tidak dapat diedit.

>!Sebelum menambahkan versi baru, pastikan semua versi yang ada sudah dirilis.Jika tidak, versi yang tidak dirilis akan menjadi versi lama yang tidak dapat diedit dan dirilis ke lingkungan percobaan.


### Merilis versi

Untuk nama domain yang pengelolaan versinya diaktifkan, rilis versi sebagai berikut:

1.Cari versi yang perlu dirilis ke lingkungan percobaan, pilih **More** > **Release to the staging environment** (Selengkapnya > Rilis ke lingkungan percobaan) di bawah kolom operasi.
![](https://main.qcloudimg.com/raw/13b8f5a168719c31c2c1b03b532933a9.png)
2.CDN akan memberikan IP IPv4 ke nama domain tersebut.Untuk menguji versi yang di-deploy di lingkungan percobaan, ubah HOSTS klien, dan arahkan nama domain ke IP tersebut.
3.Jika Anda ingin menyesuaikan konfigurasi dan melakukan pengujian lagi, Anda harus menambahkan dan mengirimkan versi baru, dan kemudian mengulangi langkah 1 dan 2.
4.Setelah pengujian, klik **Sync to Production Env.** (Sinkronkan ke Lingkungan Produksi) di sebelah nomor versi untuk menyinkronkannya dengan lingkungan produksi dan men-deploy konfigurasi tersebut ke situs operasional.
![](https://main.qcloudimg.com/raw/89b2d937dcba03f68c62a2aad60b9f6f.png)
5.Jika Anda perlu mengubah versi di lingkungan produksi, langkah 1 sampai 4.

>!
>- Anda hanya dapat merilis versi terbaru (versi dengan nomor versi terbesar) ke lingkungan percobaan.Versi lama hanya dapat dilihat.
>- Pembaruan khusus konfigurasi atau platform backend akan dirilis ke lingkungan produksi secara langsung.
>- Dalam pembaruan khusus konfigurasi atau platform backend, konflik bisa terjadi saat menyinkronkan lingkungan percobaan dengan lingkungan produksi, dan Anda akan menerima pesan kesalahan mengenai “konfigurasi backend khusus”.Dalam hal ini, Anda harus membuat versi lain yang akan dirilis.
>- IP lingkungan percobaan tidak boleh sering diubah.Namun, untuk menjamin akurasi, Anda sebaiknya mendapatkan IP baru dengan mengeklik tombol penyegaran setiap kali sebelum melakukan pengujian.



### Melihat Versi

Jika Anda ingin melihat perincian konfigurasi suatu versi, klik **View** (Lihat) di bawah kolom operasi.


### Mengaktifkan/Menonaktifkan Versi
Klik **Disable** (Nonaktifkan) pada bagian lingkungan produksi.Versi yang di-deploy di lingkungan produksi dan lingkungan percobaan akan dinonaktifkan pada saat yang sama sehingga nama domain akan dinonaktifkan dan layanan akselerasi akan ditutup.

Untuk mengaktifkan kembali versi tersebut, klik **Enable** (Aktifkan) pada bagian lingkungan produksi dan versi tersebut akan diaktifkan baik di lingkungan produksi maupun lingkungan percobaan.

## Menonaktifkan Pengelolaan Versi

Setelah Anda menonaktifkannya, versi yang di-deploy di lingkungan produksi akan ditampilkan sebagai konfigurasi operasional.Semua versi yang sudah ada lainnya akan dibuang dan tidak dapat dipulihkan.

Anda dapat mengeklik **Enable Version Management** (Aktifkan Pengelolaan Versi) untuk mengaktifkannya kembali sesuai keperluan.


## Catatan:

Untuk nama domain dengan pengelolaan versi diaktifkan:
- Mengonfigurasi fitur secara batch, seperti [menyalin konfigurasi](https://intl.cloud.tencent.com/document/product/228/38936) dan [mengubah konfigurasi secara batch](https://intl.cloud.tencent.com/document/product/228/39911), tidak didukung.
- Anda tidak bisa mengonfigurasi sertifikat untuk suatu nama domain di halaman pengelolaan sertifikat pada konsol.
- Jika Anda mengaktifkan atau menonaktifkan akselerasi untuk suatu nama domain, versi yang di-deploy di lingkungan produksi dan lingkungan percobaan juga akan diaktifkan atau dinonaktifkan.
- Tag dan proyek nama domain dapat diedit.
- Untuk mengubah wilayah akselerasi dan jenis layanan, Anda harus menonaktifkan pengelolaan versi terlebih dahulu.
