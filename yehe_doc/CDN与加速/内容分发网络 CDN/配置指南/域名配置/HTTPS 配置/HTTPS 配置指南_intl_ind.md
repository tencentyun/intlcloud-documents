## Ikhtisar Konfigurasi
CDN Tencent Cloud mendukung layanan akselerasi HTTPS. Anda dapat mengunggah sertifikat untuk men-deploy-nya atau langsung men-deploy sertifikat yang di-hosting di Layanan Sertifikat SSL Tencent Cloud ke platform CDN. Dengan cara ini, Anda dapat mengaktifkan layanan akselerasi HTTPS untuk menerapkan transfer data terenkripsi melalui seluruh jaringan.

## Panduan Konfigurasi
### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan buka tab **HTTPS Configuration** (Konfigurasi HTTPS).
![](https://main.qcloudimg.com/raw/df6c4966cfee58661251f88550214576.png)
Anda dapat memilih **Certificate Management** (Pengelolaan Sertifikat) di bilah samping kiri untuk melihat semua nama domain yang dikonfigurasi dengan akselerasi HTTPS di bawah akun Anda.
![](https://main.qcloudimg.com/raw/91335ed0a426118b76ad6b27a53d5197.png)

### Mengonfigurasi sertifikat
#### 1. Pilih nama domain
Di halaman **Certificate Management** (Pengelolaan Sertifikat), klik **Configure Certificate** (Konfigurasikan Sertifikat) dan pilih nama domain akselerasi yang akan dikonfigurasi dengan sertifikat:
+ Status nama domain akselerasi harus "Deploying" (Sedang Di-Deploy) atau "Enabled" (Diaktifkan). Nama domain yang dinonaktifkan tidak dapat dikonfigurasi dengan akselerasi HTTPS.
+ Nama domain yang diakhiri dengan `.file.myqcloud.com` adalah nama domain akselerasi default dari COS Tencent Cloud dan dapat menggunakan akselerasi HTTPS tanpa mengonfigurasi sertifikat apa pun.
+ Nama domain yang diakhiri dengan `.image.myqcloud.com` adalah nama domain akselerasi default CI Tencent Cloud dan dapat menggunakan akselerasi HTTPS tanpa mengonfigurasi sertifikat apa pun.

![](https://main.qcloudimg.com/raw/13c71dc1fc13576620768f7ae61d6c9e.png)

#### 2. Pilih sertifikat
Jika ada sertifikat yang ada dalam format PEM, Anda dapat langsung menempelkan konten dan kunci privat-nya ke bidang yang sesuai:
+ CDN mendukung deployment sertifikat ECC.
+ Konten sertifikat harus dalam format PEM. Jika tidak, silakan lihat [Mengonversi format lain ke PEM](https://intl.cloud.tencent.com/document/product/228/35212).
+ Anda dapat memilih sertifikat yang di-hosting oleh Tencent Cloud untuk deployment cepat.

![](https://main.qcloudimg.com/raw/d847eb87f076b972808b8e680705f706.png)



### Mengonfigurasi dalam batch
Klik **Batch Configuration** (Konfigurasi Batch) di bagian atas. Anda dapat mengunggah sertifikat untuk mencocokkan nama domain secara otomatis untuk konfigurasi batch:
#### 1. Pilih sertifikat
Jika ada sertifikat yang ada dalam format PEM, Anda dapat langsung menempelkan konten dan kunci privat-nya ke bidang yang sesuai:
+ CDN mendukung deployment sertifikat ECC.
+ Konten sertifikat harus dalam format PEM. Jika tidak, silakan lihat [Mengonversi format lain ke PEM](https://intl.cloud.tencent.com/document/product/228/35212).
+ Anda dapat memilih sertifikat yang di-hosting oleh Tencent Cloud untuk deployment cepat.

![](https://main.qcloudimg.com/raw/fcadb92849ebd780acbbc5b35f343478.png)

#### 2. Pilih nama domain
Berdasarkan sertifikat yang diunggah atau dipilih, CDN akan mencocokkan nama domain yang memungkinkan konfigurasi secara otomatis. Anda dapat memilih nama domain untuk konfigurasi sesuai kebutuhan:
![](https://main.qcloudimg.com/raw/04a8ad1088655f24282201da7b5ebd74.png)



### Mengubah sertifikat
#### Memodifikasi sertifikat
Klik **Edit** di sebelah kanan sertifikat untuk memperbaruinya untuk nama domain yang ditentukan. Anda juga dapat mengonfigurasi sertifikat dalam batch lagi untuk mengganti konfigurasi sertifikat asli.
![](https://main.qcloudimg.com/raw/bb2ed5ec740aa67abf2750dc58baae0d.png)
Pembaruan sertifikat akan berjalan mulus pada simpul satu per satu di seluruh jaringan tanpa memengaruhi layanan HTTPS di lingkungan produksi. Anda juga dapat mengeklik **Delete** (Hapus) untuk membatalkan layanan akselerasi HTTPS.

#### Kedaluwarsa sertifikat
Tencent Cloud akan mengirimi Anda pengingat kedaluwarsa melalui SMS, email, dan Pusat Pesan 30, 15, dan 7 hari sebelum masa kedaluwarsa sertifikat Anda dan pada hari kedaluwarsa-nya. Saat ini, penerima pengingat untuk sertifikat SSL dapat dikustomisasi. Anda dapat mengakses halaman [Langganan Pesan](https://console.cloud.tencent.com/message/subscription) untuk melakukan konfigurasi.

### Konfigurasi khusus wilayah
Jika nama domain Anda dikonfigurasi untuk akselerasi global, sertifikat HTTPS yang dikonfigurasi akan diterapkan secara global. Saat ini, sertifikat yang dikonfigurasi untuk wilayah di dalam dan di luar Tiongkok Daratan harus sama.

Jika nama domain memiliki sertifikat yang berbeda di dalam/di luar Tiongkok Daratan, Anda akan melihat tag Tiongkok Daratan dan di luar Tiongkok Daratan pada halaman **Certificate Management** (Pengelolaan Sertifikat), yang menunjukkan bahwa nama domain dengan tag memiliki konfigurasi lama yang berbeda.

Di bawah tab **Advanced Configuration** (Konfigurasi Lanjutan) dari nama domain, Anda juga dapat melihat dua konfigurasi:


