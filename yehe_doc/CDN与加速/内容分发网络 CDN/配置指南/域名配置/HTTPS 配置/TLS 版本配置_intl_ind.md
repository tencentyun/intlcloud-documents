## Ikhtisar Fitur

CDN Tencent Cloud mengaktifkan TLS 1.0/1.1/1.2 dan menonaktifkan TLS 1.3 secara default. Anda dapat mengaktifkan dan menonaktifkan versi TLS sesuai kebutuhan.

>!
>- Pastikan sertifikat HTTPS dikonfigurasi dengan benar.
>- Konfigurasi versi TLS sekarang hanya tersedia di wilayah Tiongkok Daratan. Jika wilayah akselerasi nama domain adalah "Global", perubahan konfigurasi hanya akan diterapkan di Tiongkok Daratan.
>- Fitur ini mungkin tidak tersedia di beberapa platform. Kami akan menyelesaikan peningkatan server sesegera mungkin.



## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan buka tab **HTTPS Configuration** (Konfigurasi HTTPS) untuk menemukan bagian **TLS Version Configuration** (Konfigurasi Versi TLS).

Secara default, TLS 1.0/1.1/1.2 diaktifkan dan TLS 1.3 dinonaktifkan.

![](https://main.qcloudimg.com/raw/7445026074dc473c366db6e65b807a17.png)


### Memodifikasi konfigurasi

Buka **Modify Configuration** (Modifikasi Konfigurasi) untuk mengaktifkan dan menonaktifkan versi TLS sesuai kebutuhan.
![](https://main.qcloudimg.com/raw/0cd09ce66a94d6886d68c60f22844310.png)


**Batasan konfigurasi**

- Anda dapat mengaktifkan satu versi atau beberapa versi yang berurutan. Misalnya, Anda dapat mengaktifkan versi 1.0, 1.1 dan 1.2, tetapi tidak dapat mengaktifkan versi 1.0 dan 1.2.
- Setidaknya satu versi harus diaktifkan.
