Jika Anda melakukan push pada streaming melalui RTMP dan memutar streaming melalui HTTP-FLV, secara umum streaming akan memiliki latensi sekitar 2‒3 detik. Jika Anda mengalami latensi tinggi, ikuti langkah-langkah di bawah ini untuk mengatasi masalah.

### Langkah 1. Periksa protokol pemutaran ulang

Latensi cenderung tinggi jika Anda menggunakan HLS (M3U8) untuk pemutaran ulang. HLS adalah protokol streaming yang dikembangkan oleh Apple. HLS bekerja dengan memecah streaming menjadi (biasanya 3 atau 4) segmen TS berdurasi 5 detik atau lebih lama, yang menghasilkan latensi keseluruhan sebesar 10‒30 detik.

Oleh karena itu, jika Anda perlu menggunakan HLS (M3U8) untuk pemutaran ulang, turunkan latensi dengan mengurangi jumlah segmen atau durasi setiap segmen, tetapi cara ini dapat meningkatkan kemacetan. Anda dapat [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category) atau menghubungi teknisi dukungan teknis kami untuk mendapatkan bantuan.

### Langkah 2. Periksa pengaturan pemutar

Pemutar SDK MLVB mendukung tiga mode kontrol latensi: Speedy (Cepat), Smooth (Lancar), dan Auto (Otomatis). Informasi selengkapnya tentang pengaturan dapat dilihat di [Latency Control (Kontrol Latensi)](https://intl.cloud.tencent.com/document/product/1071/38160).

**Speedy** (Cepat): mode ini mempertahankan latensi tetap 2‒3 detik atau lebih rendah di sebagian besar skenario aplikasi dan cocok untuk showroom langsung.
**Smooth** (Lancar): mode ini mempertahankan latensi tetap 5 detik atau lebih rendah di sebagian besar skenario aplikasi dan cocok untuk skenario aplikasi yang memerlukan pemutaran ulang lancar, tetapi tidak sensitif terhadap latensi, misalnya streaming game.

### Langkah 3. Tambahkan watermark pada video di sisi klien
Dengan Tencent Cloud, Anda dapat menambahkan watermark pada video di cloud, tetapi cara ini akan meningkatkan latensi sebesar 1‒2 detik. Oleh karena itu, jika Anda menggunakan SDK MLVB, sebaiknya tambahkan watermark pada video di sisi host, bukan di cloud, untuk menurunkan latensi.

### Langkah 4. Periksa pusher pihak ketiga
Kami menjamin pengalaman streaming terbaik melalui berbagai solusi terintegrasi. Namun, jika Anda menggunakan perangkat lunak pihak ketiga untuk push streaming, kami merekomendasikan Anda untuk membandingkan pusher Anda dengan pusher Tencent Cloud menggunakan [demo uji coba](https://intl.cloud.tencent.com/document/product/1071/38147) SDK MLVB untuk mengetahui pusher Anda menyebabkan latensi tinggi atau tidak. Banyak pusher pihak ketiga cenderung meningkatkan ukuran buffer untuk mengurangi masalah bandwidth upstream yang rendah.

### Langkah 5. Periksa pengaturan OBS
Jika Anda menggunakan OBS untuk melakukan push pada streaming dan mengalami latensi tinggi, periksa konfigurasi [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569) Anda. Pastikan Anda mengatur interval keyframe ke 1 atau 2 detik.

### Langkah 6. Gunakan LEB
Jika semua cara di atas tidak dapat mengatasi masalah, Anda dapat mencoba layanan LEB Tencent Cloud. Layanan ini menyediakan latensi lebih rendah dibandingkan LVB dan menawarkan streaming dengan latensi milidetik. Informasi lebih lanjut dapat dilihat di [LEB](https://intl.cloud.tencent.com/document/product/267/41030).
