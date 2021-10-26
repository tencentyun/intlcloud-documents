## Skenario Konfigurasi
Saat CDN Tencent Cloud meneruskan permintaan ke server asal, periode waktu habis default untuk koneksi TCP adalah 5 detik, dan periode waktu habis default untuk pemuatan data selama tarik-asal adalah 10 detik. Jika durasi tarik-asal melebihi batas waktu yang disebutkan di atas, kegagalan akan sering terjadi.

Anda dapat menyesuaikan periode waktu habis untuk koneksi TCP tarik-asal dan pemuatan data sesuai dengan kondisi pemrosesan data server asal dan lingkungan jaringan untuk memastikan tarik-asal yang normal.

## Panduan Konfigurasi

### Melihat konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik nama domain untuk masuk ke halaman konfigurasinya. Anda akan menemukan konfigurasi waktu habis tarik-asal pada tab **Origin Configuration** (Konfigurasi Asal). Secara default:
- Periode waktu habis koneksi TCP adalah 5 detik.
- Periode waktu habis pemuatan tarik-asal adalah 10 detik.

![](https://main.qcloudimg.com/raw/061fef4060d6aae5d16b3522b23fbbea.png)

### Memodifikasi konfigurasi
Anda dapat mengeklik **Edit** di sebelah kanan untuk memodifikasi periode waktu habis terkait sesuai kebutuhan:
- Periode waktu habis koneksi TCP dapat diatur ke 5–60 detik.
![](https://main.qcloudimg.com/raw/f70013c886612ef4dc33c353d8612336.png)
- Periode waktu habis pemuatan tarik-asal dapat diatur ke 5–60 detik.
![](https://main.qcloudimg.com/raw/e9c2cf6344275d477272ab2ba8c7e3b0.png)

>Jika nama domain akselerasi Anda dikonfigurasi untuk akselerasi global, periode waktu habis tarik-asal yang dikonfigurasi akan diterapkan secara global. Konfigurasi ini tidak membedakan antara permintaan dari Tiongkok Daratan dan dari luar Tiongkok Daratan.

