Cloud Monitor mengumpulkan data mentah dari instance CLB yang sedang berjalan dan menampilkan entri data dalam grafik intuitif.Statistik akan disimpan selama satu bulan secara default.Anda bisa mengamati operasi instance dalam satu bulan untuk terus mengetahui status layanan aplikasi.

Anda bisa membuka [Konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) untuk melihat data pemantauan CLB.Klik **Cloud Product Monitoring** (Pemantauan Produk Cloud) -> [**Cloud Load Balancer** (Penyeimbang Beban Cloud)](https://console.cloud.tencent.com/monitor/clb) dan kemudian klik ID instance CLB untuk masuk ke halaman detail pemantauan.Anda bisa melihat data pemantauan instance CLB, dan memperluasnya untuk melihat informasi pemantauan pendengar dan server asli.

## Level Instance CLB
>?Pemanfaatan bandwidth masuk dan pemanfaatan bandwidth keluar berlaku untuk semua wilayah layanan kecuali Tokyo dan Bangkok.Kedua metrik ini hanya untuk akun tagihan per IP.Untuk memeriksa tipe akun Anda, silakan lihat [Memeriksa Tipe Akun](https://intl.cloud.tencent.com/document/product/684/15246).

| Metrik | Unit | Deskripsi |
|----|------|----|
| Bandwidth masuk | Mbps | Bandwidth yang digunakan klien untuk mengakses CLB melalui jaringan publik dalam periode referensi. |
| Bandwidth keluar | Mbps | Bandwidth yang digunakan CLB untuk mengakses jaringan publik dalam periode referensi. |
| Paket masuk | Paket | Jumlah paket data permintaan yang diterima oleh CLB per detik dalam periode referensi. |
| Paket keluar | Paket | Jumlah paket data yang dikirim oleh CLB per detik dalam periode referensi. |
|Koneksi yang diturunkan | Koneksi  | Jumlah koneksi yang diturunkan oleh CLB per detik dalam periode referensi.|
|Bandwidth masuk yang diturunkan | bps  | Bandwidth masuk yang diturunkan oleh CLB per detik dalam periode referensi.|
|Bandwidth keluar yang diturunkan | bps  | Bandwidth keluar yang diturunkan oleh CLB per detik dalam periode referensi.|
|Paket data masuk yang diturunkan | Paket | Jumlah paket data masuk yang diturunkan oleh CLB per detik dalam periode referensi. |
|Paket data keluar yang diturunkan | Paket | Jumlah paket data masuk yang diturunkan oleh CLB per detik dalam periode referensi. |
|Pemanfaatan bandwidth masuk | %  | Pemanfaatan bandwidth masuk CLB dalam periode referensi.|
|Pemanfaatan bandwidth keluar | %  | Pemanfaatan bandwidth keluar CLB dalam periode referensi.|


## Level (TCP/UDP) Pendengar Lapisan 4
Pendengar lapisan 4 memungkinkan Anda melihat metrik pemantauan dalam tiga level:
- Level pendengar
- Level server asli
- Level port server asli

| Metrik | Unit | Deskripsi |
|----|------|----|
| Koneksi | Jumlah | Jumlah koneksi pada pendengar dalam periode referensi. |
| Koneksi baru | Jumlah | Jumlah koneksi baru pada pendengar dalam periode referensi. |
| Bandwidth masuk | Mbps | Bandwidth yang digunakan klien untuk mengakses CLB melalui jaringan publik dalam periode referensi. |
| Bandwidth keluar | Mbps | Bandwidth yang digunakan CLB untuk mengakses jaringan publik dalam periode referensi. |
| Paket masuk | Paket | Jumlah paket data permintaan yang diterima oleh CLB per detik dalam periode referensi. |
| Paket keluar | Paket | Jumlah paket data yang dikirim oleh CLB per detik dalam periode referensi. |

## Level (HTTP/HTTPS) Pendengar Lapisan 7
Pendengar lapisan 7 memungkinkan Anda melihat metrik pemantauan dalam lima level:
- Level pendengar
- Level nama domain
- Level jalur penerusan URL
- Level server asli
- Level port server asli

| Metrik | Unit | Deskripsi |
|----|------|----|
| Koneksi | - | Jumlah koneksi pada pendengar dalam periode referensi. |
| Koneksi baru | - | Jumlah koneksi baru pada pendengar dalam periode referensi. |
| Bandwidth masuk | Mbps | Bandwidth yang digunakan klien untuk mengakses CLB melalui jaringan publik dalam periode referensi. |
| Bandwidth keluar | Mbps | Bandwidth yang digunakan CLB untuk mengakses jaringan publik dalam periode referensi. |
| Paket masuk | Paket | Jumlah paket data permintaan yang diterima oleh CLB per detik dalam periode referensi. |
| Paket keluar | Paket | Jumlah paket data yang dikirim oleh CLB per detik dalam periode referensi. |
| Durasi permintaan rata-rata | ms | Durasi permintaan rata-rata CLB dalam periode referensi.Durasi dimulai dari titik saat instance CLB menerima byte pertama dari klien dan berakhir saat instance CLB mengirim byte terakhir kepada klien. |
| Durasi permintaan maksimum | ms | Durasi permintaan maksimum CLB dalam periode referensi.Durasi dimulai dari titik saat instance CLB menerima byte pertama dari klien dan berakhir saat instance CLB mengirim byte terakhir kepada klien. |
| Durasi respons rata-rata | ms | Durasi respons rata-rata server asli dalam periode referensi.Durasi mengacu pada seluruh durasi permintaan, mulai dari titik saat instance CLB tersambung ke server asli dan berakhir saat server asli menerima byte respons terakhir. |
| Durasi respons maksimum | ms | Durasi respons maksimum server asli dalam periode referensi.Durasi mengacu pada seluruh durasi permintaan, mulai dari titik saat instance CLB tersambung ke server asli dan berakhir saat server asli menerima byte respons terakhir. |
| Permintaan habis waktu | Permintaan/menit |  Jumlah permintaan yang habis waktu dalam periode referensi.  |
| Permintaan berhasil per menit | Permintaan/menit |  Jumlah permintaan CLB berhasil per menit dalam periode referensi.|
| Permintaan per detik | - | Jumlah permintaan CLB per detik dalam periode referensi, yaitu, QPS. |
| Kode status 2xx | - | Jumlah kode status 2xx yang dikembalikan oleh server asli dalam periode referensi. |
| Kode status 3xx | - | Jumlah kode status 3xx yang dikembalikan oleh server asli dalam periode referensi. |
| Kode status 4xx | - | Jumlah kode status 4xx yang dikembalikan oleh server asli dalam periode referensi. |
| Kode status 5xx | - | Jumlah kode status 5xx yang dikembalikan oleh server asli dalam periode referensi. |
| Kode status 404 | - | Jumlah kode status 404 yang dikembalikan oleh server asli dalam periode referensi. |
| Kode status 502 | - | Jumlah kode status 502 yang dikembalikan oleh server asli dalam periode referensi. |
| Kode status 3xx yang dikembalikan oleh CLB | - | Jumlah kode status 3xx yang dikembalikan oleh CLB dalam periode referensi (jumlah kode kembali CLB dan server asli).|
| Kode status 4xx yang dikembalikan oleh CLB | - | Jumlah kode status 4xx yang dikembalikan oleh CLB dalam periode referensi (jumlah kode kembali CLB dan server asli).|
| Kode status 5xx yang dikembalikan oleh CLB | - | Jumlah kode status 5xx yang dikembalikan oleh CLB dalam periode referensi (jumlah kode kembali CLB dan server asli).|
| Kode status 404 yang dikembalikan oleh CLB | - | Jumlah kode status 404 yang dikembalikan oleh CLB dalam periode referensi (jumlah kode kembali CLB dan server asli).|
| Kode status 502 yang dikembalikan oleh CLB | - | Jumlah kode status 502 yang dikembalikan oleh CLB dalam periode referensi (jumlah kode kembali CLB dan server asli).|

>!Jika Anda ingin melihat data pemantauan instance CVM di bawah pendengar, silakan masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb), klik ikon bilah pemantauan di dekat ID instance CLB, dan kemudian jelajahi data performa setiap instance di jendela floating.

