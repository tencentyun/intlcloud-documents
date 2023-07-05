## Ikhtisar Fitur
CDN menawarkan alat untuk mengueri kepemilikan IP. Alat ini dapat digunakan untuk memverifikasi apakah IP tertentu adalah simpul cache global CDN, dan memeriksa wilayah, distrik, dan ISP layanan akselerasi IP.
## Ikhtisar
Alat ini dapat digunakan untuk penanggulangan masalah. Ketika ada pengecualian akses, Anda dapat mengueri IP yang diakses dengan cara berikut:
- Jika IP bukan dari simpul CDN Tencent Cloud, masalahnya mungkin disebabkan oleh pengecualian resolusi nama domain. Silakan buka penyedia layanan DNS Anda dan periksa apakah konfigurasi CNAME-nya sudah benar;
- Jika IP adalah dari simpul CDN Tencent Cloud, Anda dapat memeriksa status layanan simpul untuk melihat apakah permintaan terganggu oleh pengaktifan/penonaktifan simpul.

## Panduan Pengoperasian
### Metode Kueri
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan pilih **Inspect Tool** -> **Verify CDN Tencent Cloud IP** (Alat Periksa -> Verifikasi IP CDN Tencent Cloud) di bilah samping kiri.
![](https://main.qcloudimg.com/raw/7c72a39a1c0f33e633057d02af9c3a6f.png)
### Batas Penggunaan
- Masukkan alamat IP yang akan diverifikasi di kotak teks (satu alamat per baris).
- Hingga 20 alamat IP dapat diverifikasi sekaligus.
- Verifikasi alamat IPv4 dan IPv6 didukung.
- Verifikasi didukung untuk simpul cache global. Untuk simpul di Tiongkok Daratan, data ISP di distrik terkait akan dikembalikan; untuk simpul di luar Tiongkok Daratan, data negara/wilayah terkait akan dikembalikan.
- Anda dapat melihat status layanan simpul **untuk 3 jam terakhir**. Jika ada perubahan status pengaktifan/penonaktifan, waktu operasi yang sesuai akan ditampilkan.

## Kasus Penggunaan
### Simpul di Tiongkok Daratan
![](https://main.qcloudimg.com/raw/92a04bfdc0905c9be0465d3dc4825dd3.png)
### Simpul di luar Tiongkok Daratan
![](https://main.qcloudimg.com/raw/6a2e1b6f94362d5508ed98a52bd2d125.png)







