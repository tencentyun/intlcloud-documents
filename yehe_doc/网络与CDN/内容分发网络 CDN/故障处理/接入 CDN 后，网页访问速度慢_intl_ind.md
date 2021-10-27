
## Deskripsi Masalah

Situs web saya masih lambat setelah dihubungkan ke Tencent Cloud CDN.

## Kemungkinan Penyebab

- 1.Anda belum mengonfigurasi rekaman CNAME untuk nama domain yang terhubung di penyedia layanan DNS sehingga layanan akselerasi CDN untuk nama domain tersebut tidak berlaku.Silakan [periksa DNS](#step1).
- 2.Validitas cache simpul tidak dikonfigurasikan dengan benar.Silakan [periksa konfigurasi validitas cache simpul](#step2).
- 3.URL sumber daya diakses untuk pertama kali setelah CDN diaktifkan, dan belum dipramuat sebelumnya.Silakan [pramuat URL](#step3).
- 4.Arsitektur situs web mengalami cacat.Silakan [optimalkan arsitektur situs web](#step4).



## Solusi

[](id:step1)
### Memeriksa DNS
Contoh ini menunjukkan cara menjalankan `nslookup` untuk memeriksa rekaman DNS pada nama domain akselerasi CDN:
```
Jalankan perintah `nslookup` untuk nama domain akselerasi
```
![](https://main.qcloudimg.com/raw/e60f03d058f29134524166c211791568.png)
Jika nama domain yang dihasilkan tidak berakhiran `dnsv1.com` seperti ditunjukkan di atas, berarti layanan akselerasi CDN untuk nama domain Anda belum berlaku.Silakan periksa rekaman CNAME nama domain di penyedia layanan DNS sesuai petunjuk [Konfigurasi CNAME](https://intl.cloud.tencent.com/document/product/228/3121).

[](id:step2)
###  Memeriksa konfigurasi validitas cache simpul
Masuk ke [konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di kanan nama domain untuk masuk ke halaman konfigurasinya, dan pindah ke tab **Cache Configuration** (Konfigurasi Cache) untuk menemukan bagian **Node Cache Validity Configuration** (Konfigurasi Validitas Cache Simpul).
![](https://main.qcloudimg.com/raw/7722e07d356878b4e031984df0328759.png)

- Periksa aturan cache simpul sumber daya: apakah validitasnya "0", terlalu singkat, atau dikonfigurasikan sebagai "No Cache" (Tanpa Cache).
Permintaan akses akan diteruskan ke server asal jika sumber daya yang diminta tidak di-cache di simpul sehingga akselerasinya tidak berlaku.Silakan konfigurasikan validitas cache sesuai keperluan bisnis Anda.
- Periksa apakah header `Cache-Control` diatur menjadi `no-store/no-cache/private` untuk server asal Anda.
- Jika ya, Anda harus mengaktifkan **Force Cache** (Cache Paksa) agar simpul CDN meng-cache sumber daya sesuai konfigurasi.
- Jika **Force Cache** (Cache Paksa) tidak diaktifkan dan header dikonfigurasi untuk meng-cache paksa, simpul CDN tidak akan meng-cache sumber daya walaupun validitas cache sudah dikonfigurasikan.

Untuk aturan konfigurasi selengkapnya, silakan lihat [Konfigurasi Validitas Cache Simpul (Baru)](https://intl.cloud.tencent.com/document/product/228/38424).

[](id:step3)
### Pramuat URL

Kecepatan yang lambat itu hal yang normal saat mengakses suatu sumber daya untuk pertama kali yang belum pernah dipramuat.Masuk ke [konsol CDN](https://console.cloud.tencent.com/cdn), klik **Purge and Prefetch** (Bersihkan dan Pramuat) di bilah samping kiri, kemudian kirimkan URL yang akan dipramuat.Untuk informasi selengkapnya, silakan lihat [Pramuat Cache](https://intl.cloud.tencent.com/document/product/228/39000).
![](https://main.qcloudimg.com/raw/83e7ceeb26fca38870fe020231542988.png)

[](id:step4)
### Mengoptimalkan arsitektur situs web

Permintaan sumber daya dinamis selalu diteruskan ke server asal untuk menarik sumber daya terbaru sehingga mengurangi kecepatan akses.Jika situs web Anda memiliki banyak sumber daya dinamis, kami sarankan untuk memisahkannya dari sumber daya statis dan menggunakan CDN untuk sumber daya statis Anda saja.
