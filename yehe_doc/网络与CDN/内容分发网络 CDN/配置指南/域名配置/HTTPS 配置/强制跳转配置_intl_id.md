## Ikhtisar Konfigurasi

CDN Tencent Cloud mendukung pengalihan paksa HTTPS/HTTP.

- Jika nama domain dikonfigurasi dengan sertifikat untuk akselerasi HTTPS, Anda dapat menentukan metode pengalihan 301/302 untuk memaksa semua permintaan HTTP di simpul CDN menjadi permintaan HTTPS.
- Anda juga dapat menentukan metode pengalihan 301/302 untuk memaksa semua permintaan HTTPS di simpul CDN menjadi permintaan HTTP.

## Panduan Konfigurasi

### Batasan konfigurasi

Akselerasi HTTPS harus diaktifkan untuk mengonfigurasi pengalihan paksa HTTPS.

### Petunjuk konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan buka tab **HTTPS Configuration** (Konfigurasi HTTPS) untuk menemukan bagian **Forced Redirection** (Pengalihan Paksa). Fitur ini dinonaktifkan secara default.
<img src="https://main.qcloudimg.com/raw/b11157d848d39d4e4bba540598f35eba.png" style="width:700px"/>
Aktifkan, dan konfigurasikan jenis pengalihan, metode:
<img src="https://main.qcloudimg.com/raw/731d7bcb51286683d259691178bf2b39.png" style="width:450px"/>
Terakhir, klik **Confirm** (Konfirmasikan) untuk men-deploy konfigurasi:
<img src="https://main.qcloudimg.com/raw/2dcfbacf16b47fe600935f57aadd2e77.png" style="width:700px"/>

