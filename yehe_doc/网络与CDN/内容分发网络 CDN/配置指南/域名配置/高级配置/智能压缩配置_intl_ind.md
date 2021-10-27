## Ikhtisar Konfigurasi
Dengan bantuan kompresi cerdas, CDN Tencent Cloud dapat mengompresi sumber daya yang dikembalikan dengan Gzip atau Brotli sesuai dengan aturan yang ditetapkan, yang secara efektif mengurangi ukuran konten dan biaya yang ditransfer.

> ! 
> - Kompresi cerdas saat ini hanya didukung untuk dua jenis layanan: akselerasi statis dan akselerasi unduhan.
> - Jika nama domain Anda dikonfigurasi untuk akselerasi global, konfigurasi kompresi cerdas akan diterapkan secara global. Konfigurasi ini tidak membedakan antara permintaan dari Tiongkok Daratan dan dari luar Tiongkok Daratan.
> - Kompresi Brotli saat ini tidak didukung di wilayah di luar Tiongkok Daratan.


## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **Advanced Configuration** (Konfigurasi Lanjutan) untuk menemukan bagian **Smart Compression** (Kompresi Cerdas). Konfigurasi ini diaktifkan secara default.
- Setelah nama domain akselerasi terhubung, sumber daya dengan ukuran mulai dari 256 byte hingga 2 MB dengan ekstensi file .js, .html, .css, .xml, .json, .shtml, dan .htm akan dikompresi dengan Gzip secara default.

![](https://main.qcloudimg.com/raw/db292e0fcc2a0d993b72117756c76b63.png)

### Memodifikasi konfigurasi
Klik **Modify** (Modifikasi) untuk mengubah aturan kompresi:
![](https://main.qcloudimg.com/raw/887c62b7a53f6193f061ffc14b372de2.png)

**Batasan konfigurasi**
- Jenis file memungkinkan hingga 200 karakter.
- Ukuran file harus dalam 30 MB.
- Kompresi Brotli saat ini tidak didukung pada beberapa platform yang sedang ditingkatkan.

>? 
> - Konfigurasi dapat dimodifikasi saat dinonaktifkan, tetapi tidak akan di-deploy secara resmi hingga diaktifkan.
> - Jika Gzip dan Brotli dipilih, file yang dikompresi akan dikembalikan sesuai dengan header kompresi permintaan.
> - Jika hanya Brotli yang dipilih dan header kompresi permintaan tidak mendukungnya, sumber daya asli akan dikembalikan tanpa dikompresi.


