
## Ikhtisar Konfigurasi

Secara default, CDN mendukung port 80, 8080, dan 443. Anda dapat menonaktifkan salah satu dari port tersebut sesuai kebutuhan.

>! 
>- Konfigurasi port sekarang hanya tersedia di Tiongkok Daratan. Jika nama domain dikonfigurasi untuk akselerasi global, perubahan konfigurasi hanya akan diterapkan di Tiongkok Daratan.
>- Fitur ini mungkin tidak tersedia di beberapa platform. Kami akan menyelesaikan peningkatan server sesegera mungkin.

## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **Access Control** (Kontrol Akses) untuk menemukan bagian **Chinese Mainland Access Port Configuration** (Konfigurasi Port Akses Tiongkok Daratan).

Port 80, 8080, dan 443 diaktifkan secara default.
![](https://main.qcloudimg.com/raw/a9f3930bb87a720acd8a09fb07f333d2.png)

### Memodifikasi konfigurasi

Anda dapat menonaktifkan dan mengaktifkan port sesuai kebutuhan.

**Batasan modifikasi**

- Jika akses HTTPS atau pengalihan HTTPS paksa diaktifkan untuk nama domain, Port 443 tidak dapat dinonaktifkan.
- Port 80 atau 8080 harus dibuka.



## Sampel Konfigurasi

Jika **Chinese Mainland Access Port Configuration** (Konfigurasi Port Akses Tiongkok Daratan) dari nama domain akselerasi `www.test.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/a420e4f25d322855ee04b41c408ea9ab.png)

Maka akses aktualnya adalah sebagai berikut:

Simpul CDN menolak semua permintaan akses dari port 8080.
- Jika nama domain dikonfigurasi untuk akselerasi global, konfigurasi hanya akan diterapkan di Tiongkok Daratan, yang berarti bahwa simpul CDN akan menolak permintaan akses dari port 8080.

