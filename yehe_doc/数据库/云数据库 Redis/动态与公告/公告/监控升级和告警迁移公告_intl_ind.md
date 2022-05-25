
## Memantau Granularitas
TencentDB for Redis kini mendukung granularitas pemantauan satu menit dan lima detik. Sejak Oktober 2020, pemantauan pada granularitas lima detik telah didukung, memberikan lebih banyak metrik pemantauan dan data pemantauan proksi. Untuk informasi selengkapnya, lihat [Memperbarui Catatan Pemantauan pada Granularitas Lima Detik](https://intl.cloud.tencent.com/document/product/239/38742).

### Perubahan granularitas pemantauan
#### Granularitas pemantauan satu menit
- Instans yang dibuat sebelum 20 Oktober 2020 hanya mendukung [granularitas pemantauan satu menit](https://intl.cloud.tencent.com/document/product/239/34589), tetapi secara bertahap ditingkatkan untuk mendukung granularitas lima detik.
- Melihat data pemantauan dari konsol Cloud Monitor **[Cloud Monitor console (konsol Cloud Monitor)](https://console.cloud.tencent.com/monitor/product/redis)** > **TencentDB** > **Redis (1-minute granularity)** (Redis (granularitas 1 menit)).

#### Granularitas pemantauan lima detik
- Instans yang dibuat setelah 20 Oktober 2020 mendukung granularitas pemantauan satu menit dan [lima detik](https://intl.cloud.tencent.com/document/product/239/38743).
- Melihat data pemantauan dari konsol Cloud Monitor **[Cloud Monitor console (Konsol Cloud Monitor)](https://console.cloud.tencent.com/monitor/product/redis_mem_edition)** > **TencentDB** > **Redis (5-second granularity)** (Redis (granularitas 5 menit).


### Catatan peningkatan granularitas pemantauan
Untuk mendukung granularitas pemantauan lima detik, proksi instans TencentDB for Redis Anda perlu ditingkatkan ke versi terbaru.
Perhatikan bahwa peningkatan proksi akan menyebabkan pemutusan hubungan singkat. Bisnis perlu menyambung kembali ke proksi setelah peningkatan selesai.
1. Peningkatan oleh backend Tencent Cloud: Tencent Cloud meningkatkan semua instans untuk mendukung granularitas pemantauan lima detik. Anda akan diberi tahu melalui SMS, email, atau Pusat Pesan sebelum peningkatan dimulai.
2. Peningkatan oleh Anda sendiri di konsol TencentDB: Anda dapat segera meningkatkan secara manual di konsol.
3. Setelah semua instans ditingkatkan, granularitas pemantauan satu menit tidak akan didukung lagi.
<span id="jjzbbh"></span>
### Perubahan metrik pemantauan
Setelah granularitas pemantauan dipersempit dari satu menit menjadi lima detik, nama metrik pemantauan diubah dan beberapa metrik baru didukung, seperti yang ditunjukkan di bawah ini:

| Metrik Pemantauan (Satu menit)         | Metrik Pemantauan (Lima detik)          | Deskripsi                                                     |
| ---------------- | ---------------- | ------------------------------------------------------------ |
| CpuUsMin         | CpuUtil          | Penggunaan CPU rata-rata                                                |
| CpuMaxUs         | CpuMaxUtil       | Penggunaan CPU maksimum dari node (pecahan atau replika) dalam instans                      |
| StorageMin       | MemUsed          | Kapasitas memori yang sebenarnya digunakan, termasuk data dan cache                          |
| StorageUsMin     | MemUtil          | Rasio memori yang sebenarnya digunakan dengan total memori yang diminta                                 |
| StorageMaxUs     | MemMaxUtil       | Pemanfaatan memori maksimum node (pecahan atau replika) dalam instans                     |
| KeysMin          | Keys             | Jumlah total kunci yang disimpan dalam sebuah instans (kunci tingkat pertama)                               |
| ExpiredKeysMin   | Expired          | Jumlah kunci yang kedaluwarsa dalam jendela waktu, yang sama dengan nilai `expired_keys` yang dikeluarkan oleh perintah `info`      |
| EvictedKeysMin   | Evicted          | Jumlah kunci yang dikeluarkan dalam jendela waktu, yang sama dengan nilai `evicted_keys` yang dikeluarkan oleh perintah `info`      |
| ConnectionsMin   | Connections      | Jumlah koneksi TCP ke sebuah instans                                      |
| ConnectionsUsMin | ConnectionsUtil  | Rasio jumlah koneksi TCP dengan jumlah koneksi maksumum                                |
| InFlowMin        | InFlow           | Lalu lintas masuk pribadi                                                   |
| InFlowUs         | InBandwidthUtil  | Rasio lalu lintas masuk pribadi yang sebenarnya digunakan dengan lalu lintas maksimum                                |
|  -                | InFlowLimit      | Berapa kali lalu lintas masuk memicu batas lalu lintas                                         |
| OutFlowMin       | OutFlow          | Lalu lintas keluar pribadi                                                   |
| OutFlowUs        | OutBandwidthUtil | Rasio lalu lintas keluar pribadi yang sebenarnya digunakan dengan lalu lintas maksimum                               |
|  -                | OutFlowLimit     | Berapa kali lalu lintas keluar memicu batas lalu lintas                                         |
| LatencyMin       | LatencyAvg           | Latensi eksekusi rata-rata antara proksi dan server Redis                         |
|   -               | LatencyMax                 | Latensi eksekusi maksimum antara proxy dan server Redis                          |
|   -               | LatencyP99                  | Latensi P99 antara proksi dan server Redis                       |
| LatencyGetMin    | LatencyRead       | Latensi eksekusi rata-rata perintah baca antara proksi dan server Redis                       |
| LatencySetMin    | LatencyWrite       | Latensi eksekusi rata-rata dari perintah tulis antara proksi dan server Redis                       |
| LatencyOtherMin  | LatencyOther     | Latensi eksekusi rata-rata perintah (tidak termasuk perintah tulis dan baca) antara proksi dan server Redis          |
| QpsMin           | Commands            | QPS, yaitu jumlah eksekusi perintah per detik                                            |
| StatGetMin       | CmdRead          | Jumlah eksekusi perintah baca. Untuk informasi selengkapnya tentang jenis perintah baca, lihat "Fitur Pemantauan > Kategori perintah".               |
| StatSetMin       | CmdWrite          | Jumlah eksekusi perintah tulis. Untuk informasi selengkapnya tentang jenis perintah tulis, lihat "Fitur Pemantauan > Kategori perintah".               |
| StatOtherMin     | CmdOther         | Jumlah eksekusi perintah (tidak termasuk perintah baca atau tulis). Untuk informasi selengkapnya tentang jenis perintah, lihat "Fitur Pemantauan > Kategori perintah". |
| BigValueMin      | CmdBigValue      | Jumlah eksekusi permintaan yang lebih besar dari 32 KB per detik                               |
|  -                | CmdKeyCount           | Jumlah kunci yang diakses oleh perintah per detik                                            |
|  -                | CmdMget                 | Jumlah eksekusi perintah Mget per detik                                             |
| SlowQueryMin     | CmdSlow          | Jumlah eksekusi perintah dengan latensi lebih besar dari konfigurasi `slowlog\-log\-slower\-than`            |
| StatSuccessMin   | CmdHits           | Jumlah kunci yang berhasil diminta oleh perintah baca, yang sama dengan nilai output metrik `keyspace_hits` menggunakan perintah `info`     |
| StatMissedMin    | CmdMiss          | Jumlah kunci yang tidak berhasil diminta oleh perintah baca, yang sama dengan nilai output metrik `keyspace_misses` menggunakan perintah `info` |
| CmdErrMin        | CmdErr           | Jumlah kesalahan eksekusi perintah per detik. Misalnya, perintah tidak ada, parameter salah, dll.           |
| CacheHitRatioMin | CmdHitsRatio     | Kunci menghasilkan/(Kunci menghasilkan + Kunci meleset). Metrik ini mencerminkan cache meleset.    |

### Melihat granularitas pemantauan sebuah instans
- Periksa nilai bidang `InstanceSet.MonitorVersion` yang dikembalikan oleh [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065) API. Jika nilainya `5s`, instans ini mendukung granularitas pemantauan selama lima detik; jika nilainya `1m`, berarti hanya mendukung granularitas pemantauan satu menit.
- Masuk ke [Konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik nama/ID instans dan masuk ke halaman manajemen instans, pilih **System Monitoring** (Pemantauan Sistem) > **Monitoring Metrics** (Metrik Pemantauan), dan klik daftar drop-down **Period** (Periode) di bagian atas. Jika Anda dapat memilih **5 detik** dari daftar drop-down, instans ini mendukung granularitas pemantauan lima detik, atau hanya mendukung granularitas pemantauan satu menit.


## Perubahan Alarm
### Perubahan konfigurasi kebijakan alarm
Setelah metrik pemantauan ditingkatkan, Anda perlu mengonfigurasi kebijakan alarm granularitas satu menit dan granularitas lima detik di jendela yang berbeda di [konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/alarm2/policy/create), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/b2c030de1c2e925a6421813c43dd7862.png)

### Dampak peningkatan pemantauan
Setelah granularitas pemantauan dipersempit dari satu menit menjadi lima detik, Anda perlu memigrasikan kebijakan alarm granularitas satu menit ke kebijakan alarm granularitas lima detik. Metrik pemantauan yang berlaku untuk kebijakan alarm granularitas lima detik berbeda dari yang berlaku untuk kebijakan alarm granularitas satu menit. Untuk informasi selengkapnya, lihat [Perubahan metrik pemantauan](#jjzbbh).
Setelah granularitas pemantauan dipersempit menjadi lima detik:
- Data pemantauan pada granularitas satu menit dan lima detik dilaporkan sementara, yaitu Cloud Monitor akan berhenti melaporkan data granularitas satu menit di masa mendatang.
- Kebijakan alarm granularitas satu menit berlaku sementara.
- Kebijakan alarm granularitas lima detik default dikaitkan. Harap tentukan penerima alarm untuk kebijakan default.

### Memigrasikan kebijakan alarm
- Migrasi manual: salin kebijakan alarm granularitas satu menit yang ada sebagai kebijakan alarm granularitas lima detik, tetapi Anda perlu mengonfigurasi penerima alarm untuk kebijakan alarm granularitas lima detik.
- Migrasi otomatis: setelah pemutakhiran granularitas pemantauan selesai, kebijakan alarm granularitas satu menit yang ada akan secara otomatis dimigrasikan ke kebijakan alarm granularitas lima detik, dan Anda akan diberi tahu melalui SMS, email, atau Pusat Pesan.
