Tencent Cloud Monitor mengumpulkan dan menampilkan data dari instance CLB dan server asli, membantu Anda memperoleh statistik CLB, memverifikasi apakah sistem berjalan normal dan membuat alarm.Untuk informasi selengkapnya mengenai Tencent Cloud Monitor, lihat dokumentasi [Cloud Monitor Dasar](https://intl.cloud.tencent.com/doc/product/248).

Tencent Cloud menyediakan fitur Cloud Monitor untuk semua pengguna secara default dan tidak membutuhkan aktivasi manual.Anda bisa menggunakan Cloud Monitor untuk mengumpulkan data pemantauan instance CLB Anda dan menampilkan data dengan metode berikut.

## Metode Konsol CLB
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb), klik ikon bilah pemantauan di samping ID instance CLB, dan kemudian jelajahi data performa instance tersebut di jendela floating.
![](https://main.qcloudimg.com/raw/6580c81d6fd1eee2234fcb5262a976bb.png)
2.Klik ID/Nama instance CLB untuk mengakses halaman detailnya.Klik **Monitoring** (Pemantauan) untuk melihat data pemantauannya.
![](https://main.qcloudimg.com/raw/3eb231b336c9325ae16bfe2937e41b39.png)

## Metode Konsol Cloud Monitor
Masuk ke [Konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) untuk melihat data pemantauan CLB.Klik **Cloud Load Balancer** (Penyeimbang Beban Cloud)(https://console.cloud.tencent.com/monitor/clb) di bilah sisi kiri, dan klik ID/nama instance CLB untuk mengakses halaman detail pemantauannya.Anda bisa melihat data pemantauan instance CLB dan memperluas daftar drop-down untuk melihat informasi pemantauan pendengar dan server asli.

## Metode API
Gunakan `GetMonitorData` API untuk mendapatkan data pemantauan semua produk.Untuk informasi selengkapnya, lihat [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881), [Metrik Pemantauan CLB Jaringan Publik](https://intl.cloud.tencent.com/document/product/248/10997), [Protokol Lapisan 4 CLB Jaringan Pribadi](https://intl.cloud.tencent.com/document/product/248/39529), dan [Protokol Lapisan 7](https://intl.cloud.tencent.com/document/product/248/39530).
