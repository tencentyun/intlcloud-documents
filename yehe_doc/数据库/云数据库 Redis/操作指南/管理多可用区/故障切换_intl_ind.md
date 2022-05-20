
## Failover Otomatis
TencentDB for Redis mendukung failover otomatis dari node proksi dan server Redis (node penyimpanan data) untuk memastikan ketersediaan layanan.

### Failover proksi
Node proksi digunakan dalam arsitektur standar dan klaster TencentDB for Redis. Arsitektur standar memiliki tiga node proksi, sedangkan jumlah node proksi dalam arsitektur klaster meningkat secara linier dengan jumlah shard. Desain ketersediaan tinggi dari node proksi adalah sebagai berikut:
- Beberapa node proksi mendukung ketersediaan tinggi dan penyeimbang beban dari layanan proksi.
- Node proksi di-deploy pada tiga perangkat fisik untuk memastikan ketersediaan yang tinggi.
- Jika node proksi gagal, sistem pengujian akan mendeteksi node yang gagal dan menambahkan node baru secara otomatis.

### Failover server Redis
TencentDB for Redis dalam arsitektur standar atau klaster menggunakan mekanisme manajemen klaster asli Klaster Redis: protokol Gosip digunakan untuk mengetahui status node klaster, dan parameter `cluster-node-timeout` menentukan jangka waktu maksimum node tidak tersedia tanpa dianggap gagal. Nilai default parameter adalah 15000 milidetik, yang tidak boleh diubah.
Untuk informasi selengkapnya tentang cara mengidentifikasi node yang gagal, silakan lihat [Tutorial klaster Redis](https://redis.io/topics/cluster-tutorial).

## Simulasi Kegagalan
Anda dapat menggunakan fitur simulasi kegagalan di konsol TencentDB for Redis untuk melakukan simulasi atau pengujian kegagalan.
Cara kerjanya: perintah `shutdown` dikirim ke semua node master untuk memicu logika ketersediaan tinggi (HA) otomatis. Hanya instans dalam status "Running" yang dapat melakukan simulasi kegagalan.

1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dalam daftar instans, dan masuk ke halaman manajemen instans.
2. Pada tab **Node Management** (Manajemen Node), pilih **More** (Selengkapnya) > **Failure Simulation** (Simulasi Kegagalan) atau **Configuration Modification** (Modifikasi Konfigurasi) > **Failure Simulation** (Simulasi Kegagalan). 

![](https://main.qcloudimg.com/raw/4b6b66dae7776d37ffb474482d2279f7.png)

3. Di kotak dialog pop-up, masukkan kata sandi instans dan klik **OK** (OKE).
>!
>- Simulasi kegagalan akan membuat Redis tidak tersedia selama kurang dari satu menit hingga failover selesai. Data yang ditulis selama simulasi mungkin hilang.
>- Waktu henti layanan instans yang disebabkan oleh simulasi kegagalan tidak akan dihitung ke dalam "Waktu Henti Layanan Instans Tunggal" dalam Perjanjian Tingkat Layanan (SLA) Redis.
>
![](https://main.qcloudimg.com/raw/3748b50a21dfe36859dbbfc41d18da63.png)

