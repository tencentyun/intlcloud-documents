

## Ikhtisar Konfigurasi
Dengan fitur Duplicate Configuration (Buat Duplikat Konfigurasi), Anda dapat membuat duplikat konfigurasi nama domain penerusan yang ada ke satu atau beberapa nama domain penerusan baru. 

>!
>- Fitur ini tidak tersedia untuk nama domain yang dinonaktifkan atau diblokir, memiliki lisensi ICP yang kedaluwarsa (hanya untuk nama domain Tiongkok), menggunakan sertifikat eksternal, atau dengan konfigurasi yang tidak didukung yang berbeda di seluruh wilayah.
>- Konfigurasi backend (yaitu konfigurasi yang tidak diatur di konsol) tidak dapat dibuat duplikatnya.


## Panduan Konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Duplicate Configuration** (Buat Duplikat Konfigurasi) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya.
![](https://main.qcloudimg.com/raw/c9acd7ed82a3c675ec4369e294b2f94b.png)
Tambahkan nama domain penerusan baru dan kirimkan. Konfigurasi nama domain saat ini akan dibuat duplikatnya ke nama domain yang baru.
![](https://main.qcloudimg.com/raw/4e8c4c4cf589118a97bd71c01f798890.png)

>?
>- Proses pengiriman tidak dapat diganggu. Anda dapat mengelola konfigurasi setelah nama domain baru berhasil ditambahkan.
>- Konfigurasi nama domain baru akan di-deploy ke simpul CDN di seluruh jaringan, tanpa memengaruhi bisnis Anda yang sedang berjalan. Jika Anda ingin mengaktifkan layanan akselerasi, Anda perlu mengonfigurasi CNAME. Untuk petunjuk konfigurasi, lihat [Konfigurasi CNAME](https://intl.cloud.tencent.com/document/product/228/3121).
