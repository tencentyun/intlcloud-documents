## Perbarui Deskripsi 
TencentDB for Redis telah diperbarui dengan fitur pemantauan yang dioptimalkan di versi terbaru.
- Granularitas pemantauan sekarang dipersempit dari satu menit menjadi lima detik.
- Penundaan data pemantauan sekarang berkurang menjadi kurang dari 20 detik.
- Pemantauan, pengumpulan data, dan alarm sekarang didukung untuk node replika.
- Pemantauan, pengumpulan data, dan alarm sekarang didukung untuk node Proksi.
- Anda sekarang dapat membandingkan nilai metrik pemantauan di antara beberapa node.
- Metrik pemantauan baru didukung.

## Catatan
- Secara default, instans baru (tidak termasuk instans CKV) mendukung granularitas lima detik.
- Di masa mendatang, Anda dapat mengubah granularitas pemantauan instans yang ada dari satu menit menjadi lima detik di [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis). Harap perhatikan pemberitahuan dan notifikasi pop-up di konsol.
- Di [konsol Cloud Monitor]https://console.cloud.tencent.com/monitor/policylist/create), kebijakan alarm untuk granularitas lima detik adalah jenis kebijakan yang berbeda dari kebijakan untuk granularitas satu menit. Anda dapat mereplikasi kebijakan alarm untuk granularitas satu menit dan mengubah jenis kebijakannya ke **Memory Edition (5-second granularity)** (Edisi Memori (granularitas 5 detik)), sehingga kebijakan alarm ini dapat dikaitkan dengan instans baru yang mendukung granularitas lima detik.
![](https://main.qcloudimg.com/raw/9bfa0b792d4c0ddc4b262ea5357575e3.png)
## Pertanyaan Umum
#### Bagaimana cara mengetahui apakah instans mendukung granularitas pemantauan lima detik atau satu menit?
- Login ke [Konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik nama/ID instans dan masuk ke halaman manajemen instans, pilih **System Monitoring** (Pemantauan Sistem) > **Monitoring Metrics** (Metrik Pemantauan), dan klik daftar drop-down **Period** (Periode) di bagian atas. Jika Anda dapat memilih **5 seconds** (5 detik) dari daftar drop-down, instans ini mendukung granularitas pemantauan lima detik, jika tidak maka instans ini hanya mendukung granularitas pemantauan satu menit.
![](https://main.qcloudimg.com/raw/e7833ebba07a4dd949c911c58940a4d0.png)
- Periksa nilai bidang `InstanceSet.MonitorVersion` yang dikembalikan oleh [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065) API. Jika nilainya `5s`, instans ini mendukung granularitas pemantauan lima detik; jika nilainya `1m`, instans ini hanya mendukung granularitas pemantauan satu menit.

#### Bagaimana cara mendapatkan informasi node Proksi atau Redis?
Gunakan [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/document/product/239/38627) API untuk mendapatkan ID node Proksi dan node Redis.
>!ID node Proksi dan Redis akan berubah saat terjadi failover node, perluasan/pengurangan kapasitas instans, migrasi data, dll.
 Oleh karena itu, sebaiknya Anda mendapatkan informasi node terbaru dari API secara tepat waktu.

