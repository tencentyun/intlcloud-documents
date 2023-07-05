**Pemantauan dan Peringatan** membantu memastikan keandalan, ketersediaan, dan performa CVM yang tinggi. Dokumen ini menjelaskan fitur pemantauan dan alarm CVM. Untuk mengetahui informasi selengkapnya, lihat dokumentasi [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248?).

## Ikhtisar
Pemantauan dan Peringatan CVM menampilkan data pemantauan lengkap dari berbagai metrik kunci CVM secara real-time. Dengan fitur ini, Anda dapat memiliki pemahaman yang komprehensif mengenai penggunaan sumber daya, performa, dan status berjalannya instans CVM. Anda juga dapat mengonfigurasi ambang batas alarm kustom dan aturan notifikasi.

## Fitur Dasar
Anda dapat mengakses fitur pemantauan dan alarm CVM berikut di konsol Cloud Monitor:

| Komponen | Kemampuan | Fitur Utama |
| ----- | -------------- | --------------------------------------- |
| [Ikhtisar Pemantauan](https://console.cloud.tencent.com/monitor/overview)  | Menampilkan informasi pemantauan keseluruhan untuk layanan Tencent Cloud          | Memberikan informasi dan alarm keseluruhan untuk layanan Tencent Cloud                     |
| [Kebijakan Alarm](https://console.cloud.tencent.com/monitor/policylist)  | Menampilkan daftar kebijakan alarm kustom   | Mendukung konfigurasi alarm untuk CVM         |
| [Cloud Virtual Machine](https://console.cloud.tencent.com/monitor/product/cvm) | Menampilkan informasi pemantauan CVM tertentu      | Memungkinkan Anda melihat data pemantauan CVM |
| [Dasbor](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=8) | Menampilkan dasbor pemantauan kustom | Menampilkan data pemantauan secara grafis untuk memfasilitasi analisis metrik dinamis |
| [Pemantauan Kustom](https://console.cloud.tencent.com/monitor/indicator-manage) | Menampilkan metrik pemantauan kustom | Memungkinkan Anda melihat metrik data yang dilaporkan dan pemantauan kustom yang telah ditentukan sebelumnya            |
| [Pemantauan Lalu Lintas](https://console.cloud.tencent.com/monitor/flow)  | Menampilkan pemantauan lalu lintas           | Memungkinkan Anda melihat keseluruhan penggunaan bandwidth                              |

Untuk mengetahui informasi selengkapnya tentang Cloud Monitor, lihat [Ikhtisar Produk](https://intl.cloud.tencent.com/document/product/248/32799)

## Kasus Penggunaan
- **Pengelolaan harian:** masuk ke konsol Cloud Monitor dan lihat status berjalannya setiap produk yang dipantau.
- **Pengecualian pemecahan masalah:** Cloud Monitor akan segera mengirimkan notifikasi alarm kepada Anda saat data pemantauan mencapai ambang batas alarm, sehingga Anda dapat memecahkan masalah tersebut.
- **Perluasan tepat waktu:** Anda dapat mengonfigurasi kebijakan alarm untuk bandwidth, jumlah koneksi, penggunaan disk, dan item pemantauan lainnya untuk memeriksa status keseluruhan layanan Tencent Cloud Anda. Anda akan menerima notifikasi alarm ketika bisnis melonjak dan dapat memperluas CVM Anda untuk menyesuaikannya.

## Item Pemantauan
Untuk mengukur performa instans, Anda setidaknya harus memantau item berikut:

| Item Pemantauan | Metrik Pemantauan |
|---------|---------|
| Penggunaan CPU | cpu_usage|
| Penggunaan memori | mem_usage |
| Bandwidth keluar jaringan pribadi | lan_outtraffic |
| Bandwidth masuk jaringan pribadi| lan_intraffic |
| Bandwidth keluar jaringan publik | wan_outtraffic |
| Bandwidth masuk jaringan publik | wan_intraffic |
| Penggunaan disk | disk_usage |
| Waktu tunggu Disk I/O | disk_io_await |

## Data Pemantauan
- **Interval pemantauan:** Cloud Monitor menyediakan data pemantauan pada berbagai perincian statistik, termasuk 1 menit, 5 menit, 1 jam, dan 1 hari. CVM mendukung perincian pemantauan berdurasi 1 menit, artinya data dikumpulkan setiap 1 menit. Interval default adalah 5 menit.
- **Penyimpanan data:** data pemantauan dengan perincian 1 menit, 5 menit, dan 1 jam akan disimpan selama 31 hari; data pemantauan dengan perincian 1 hari akan disimpan selama setengah tahun.
- **Tampilan alarm:** data ditampilkan dalam diagram yang mudah dibaca. Konsol Cloud Monitor menampilkan data pemantauan semua produk untuk memberikan Anda gambaran menyeluruh mengenai status yang sedang berjalan.
- **Pengaturan alarm:** Anda dapat menetapkan batasan untuk metrik pemantauan. Ketika kondisi terpenuhi, notifikasi alarm akan segera dikirim ke grup penerima. Untuk mengetahui informasi selengkapnya, lihat [Mengonfigurasi Kebijakan Alarm](https://intl.cloud.tencent.com/document/product/248/38908).
- **Pengaturan dasbor:** Anda dapat membuat dasbor metrik pemantauan untuk menganalisis metrik abnormal secara dinamis dan melihat perubahan metrik secara real-time untuk perluasan sumber daya yang cepat. Untuk mengetahui informasi selengkapnya, lihat [Membuat Dasbor](https://intl.cloud.tencent.com/document/product/248/38468).
