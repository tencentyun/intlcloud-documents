

## Ikhtisar Konfigurasi
Selain sumber daya, CDN Tencent Cloud juga akan meng-cache header berikut dari server asal dan mengembalikannya ke pengguna secara default:
+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges

Jika server asal Anda memiliki header khusus yang perlu di-cache dan dikembalikan ke pengguna oleh CDN, Anda dapat mengaktifkan cache header.

## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **Cache Configuration** (Konfigurasi Cache) untuk menemukan bagian **HTTP Header Cache Configuration** (Konfigurasi Cache Header HTTP). Konfigurasi diaktifkan secara default, dan Anda dapat menonaktifkannya sesuai kebutuhan.
![](https://main.qcloudimg.com/raw/0fb4739f743b6242c463672a2f059098.png)





