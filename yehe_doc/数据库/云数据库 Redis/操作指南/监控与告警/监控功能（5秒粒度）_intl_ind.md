TencentDB for Redis menyediakan layanan pemantauan yang lengkap dan mudah digunakan di mana Anda tidak perlu khawatir tentang, misalnya, mengumpulkan data pemantauan atau OPS dari sistem pemantauan. Layanan pemantauan mencakup pemantauan Proksi, pemantauan Redis, dan pemantauan instans yang merangkum data pemantauan seluruh instans.
- Pemantauan proksi: memberikan informasi pemantauan semua node Proksi dalam satu instans. Instans TencentDB for Redis dalam arsitektur standar atau klaster memiliki node Proksi.
- Pemantauan Redis: memberikan informasi pemantauan node master dan replika Redis.
- Pemantauan instans: merangkum data pemantauan seluruh instans (termasuk node Proksi dan node Proksi) dan menggabungkan data sesuai dengan algoritme agregasi SUM, AVG, MAX, dan LAST.
![](https://main.qcloudimg.com/raw/2ff4346f6da8cfec08adb7bbdd331455.png)
## Deskripsi Granularitas Pemantauan Lima detik
- Secara default, instans baru (tidak termasuk instans CKV) mendukung glanuralitas lima detik.
- Di masa mendatang, Anda dapat mengubah glanularitas pemantauan instans yang ada dari satu menit menjadi lima detik di [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis). Harap perhatikan pemberitahuan dan notifikasi pop-up di konsol.
- Di [konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/policylist/create), kebijakan alarm untuk glanularitas lima detik adalah jenis kebijakan yang berbeda dari glanularitas satu menit. Anda dapat mereplikasi kebijakan alarm untuk glanuralitas satu menit dan mengubah jenis kebijakan ke **Memory Edition (5-second granularity)** (Edisi Memori (granularitas 5 detik)), sehingga kebijakan alarm ini dapat dikaitkan dengan instans baru yang mendukung glanuralitas lima detik.
![](https://main.qcloudimg.com/raw/9bfa0b792d4c0ddc4b262ea5357575e3.png)
## Melihat Granularitas Pemantauan Instans
- Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dan masuk ke halaman manajemen instans, pilih **System Monitoring** (Pemantauan Sistem) > **Monitoring Metrics** (Metrik Pemantauan), dan klik daftar drop-down **Period** (Periode) di bagian atas. Jika Anda dapat memilih **5 seconds** (5 detik) dari daftar drop-down, instans ini mendukung granularitas pemantauan lima detik, jika tidak maka instans ini hanya mendukung granularitas pemantauan satu menit.
![](https://main.qcloudimg.com/raw/e7833ebba07a4dd949c911c58940a4d0.png)
- Periksa nilai bidang `InstanceSet.MonitorVersion` yang dikembalikan oleh API [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065). Jika nilainya `5s`, instans ini mendukung granularitas pemantauan selama lima detik; jika nilainya `1m`, iinstans ini hanya mendukung granularitas pemantauan satu menit.

## Memantau Granularitas dan Memantau Periode Penyimpanan Data
TencentDB for Redis saat ini mendukung metrik pemantauan pada granularitas lima detik, satu menit, lima menit, satu jam, atau satu hari. Untuk periode penyimpanan data pemantauan di setiap granularitas, silakan lihat [Batas Penggunaan](https://intl.cloud.tencent.com/document/product/248/32803).

## Melihat Informasi Pemantauan
Anda dapat melihat informasi pemantauan TencentDB for Redis di daftar instans dan di halaman pemantauan instans di konsol TencentDB for Redis, atau di konsol Cloud Monitor.
- Daftar Instans: login ke [konsolTencentDB for Redis](https://console.cloud.tencent.com/redis), klik ikon **View Monitoring** (Lihat Pemantauan) dalam daftar instans seperti yang ditunjukkan di bawah ini, dan lihat metrik pemantauan di jendela pop-up di sebelah kanan.
![](https://main.qcloudimg.com/raw/e4e9781c7dc38505a1e08624f72f9dff.png)
- Halaman pemantauan instans: login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dalam daftar instans dan masuk ke halaman manajemen instans, pilih **System Monitoring** (Pemantauan Sistem), dan lihat data pemantauan di tab **Monitoring Metrics** (Metrik Pemantauan).
![](https://main.qcloudimg.com/raw/aba46b1c932f11f173634f596b1dd69f.png)
- Konsol Cloud Monitor: login ke [konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/product/redis_mem_edition) untuk melihat ringkasan data pemantauan.
![](https://main.qcloudimg.com/raw/7289958cd8a4f4c8b4374d50031eb438.png)


## Deskripsi Metrik Pemantauan
### Pemantauan node proksi
Setiap instans TencentDB for Redis berisi setidaknya 3 node Proksi. Pada umumnya, jumlah node Proksi 1,5 kali lipat dari jumlah node Redis. Node Proksi mendukung metrik pemantauan berikut:

<table>
<thead><tr><th>Kategori</th><th>Metrik</th><th>Parameter</th><th>Unit</th><th>Deskripsi</th></tr></thead>
<tbody>
<tr>
<td>CPU</td><td>Penggunaan CPU</td><td>cpu_util</td><td>%</td><td>Penggunaan CPU Proksi</td></tr>
<tr>
<td rowspan=5>Permintaan</td><td>Total permintaan</td><td>proxy_commands</td><td>permintaan/detik</td><td>Jumlah eksekusi perintah proksi per detik</td></tr>
<tr>
<td>Permintaan kunci</td><td>cmd_key_count</td><td>kunci/detik</td><td>Jumlah kunci yang diakses oleh perintah per detik</td></tr>
<tr>
<td>Permintaan Mget</td><td>cmd_mget</td><td>permintaan/detik</td><td>Jumlah eksekusi perintah Mget per detik</td></tr>
<tr>
<td>Kesalahan eksekusi</td><td>cmd_err</td><td>kesalahan/detik</td><td>Jumlah kesalahan eksekusi perintah Proksi per detik. Misalnya, perintah tidak ada, parameter salah, dll.</td></tr>
<tr>
<td>Permintaan bernilai besar</td><td>cmd_big_value</td><td>permintaan/detik</td><td>Jumlah eksekusi permintaan yang lebih besar dari 32 KB per detik</td></tr>
<tr>
<td rowspan=8>Jaringan</td><td>Koneksi</td><td>connections</td><td>-</td><td>Jumlah koneksi TCP ke sebuah instans</td></tr>
<tr>
<td>Penggunaan koneksi</td><td>connections_util</td><td>%</td><td>Rasio jumlah koneksi TCP terhadap jumlah koneksi maksimum</td></tr>
<tr>
<td>Lalu lintas masuk</td><td>in_flow</td><td>MB/detik</td><td>Lalu lintas masuk pribadi</td></tr>
<tr>
<td>Pemanfaatan lalu lintas masuk</td><td>in_bandwidth_util</td><td>%</td><td>Rasio lalu lintas masuk pribadi yang digunakan terhadap lalu lintas maksimum</td></tr>
<tr>
<td>Jumlah batas lalu lintas masuk</td><td>in_flow_limit</td><td>-</td><td>Berapa kali lalu lintas masuk memicu batas lalu lintas</td></tr>
<tr>
<td>Lalu lintas keluar</td><td>out_flow</td><td>MB/detik</td><td>Lalu lintas keluar pribadi</td></tr>
<tr>
<td>Pemanfaatan lalu lintas keluar</td><td>out_bandwidth_util</td><td>%</td><td>Rasio lalu lintas keluar pribadi yang digunakan terhadap lalu lintas maksimum</td></tr>
<tr>
<td>Jumlah batas lalu lintas keluar</td><td>out_flow_limit</td><td>-</td><td>Berapa kali lalu lintas keluar memicu batas lalu lintas</td></tr>
<tr>
<td rowspan=5>Latensi</td><td>Latensi eksekusi rata-rata</td><td>llatency_avg</td><td>milidetik</td><td>Latensi eksekusi rata-rata antara proksi dan server Redis</td></tr>
<tr>
<td>Latensi eksekusi maksimum</td><td>latency_maksimum</td><td>milidetik</td><td>Latensi eksekusi maksimum antara proksi dan server Redis</td></tr>
<tr>
<td>Latensi baca rata-rata</td><td>latency_read</td><td>milidetik</td><td>Latensi eksekusi rata-rata perintah baca antara proksi dan server Redis. Untuk informasi lebih lanjut tentang jenis perintah baca, silakan lihat <a href="#mlfl">Jenis perintah</a>.</td></tr>
<tr>
<td>Latensi tulis rata-rata</td><td>latency_write</td><td>milidetik</td><td>Latensi eksekusi rata-rata perintah tulis antara proksi dan server Redis. Untuk informasi lebih lanjut tentang jenis perintah tulis, silakan lihat <a href="#mlfl">Jenis perintah</a>.</td></tr>
<tr>
<td>Latensi rata-rata perintah lain</td><td>latency_other</td><td>milidetik</td><td>Latensi eksekusi rata-rata perintah (tidak termasuk perintah tulis dan baca) antara proksi dan server Redis</td></tr>
</tbody></table>

### Pemantauan node Redis
Pemantauan node Redis mencakup informasi pemantauan semua node master dan node replika dalam sebuah instans atau klaster. Metrik pemantauan berikut didukung:

<table>
<thead><tr><th>Kategori</th><th>Metrik</th><th>Parameter</th><th>Unit</th><th>Deskripsi</th></tr></thead>
<tbody>
<tr>
<td>CPU</td><td>Penggunaan CPU</td><td>cpu_util</td><td>%</td><td>Penggunaan CPU rata-rata</td></tr>
<tr>
<td  rowspan=2>Jaringan</td><td>Koneksi</td><td>connections</td><td>-</td><td>Jumlah koneksi antara proksi dan node</td></tr>
<tr>
<td>Penggunaan koneksi</td><td>connections_util</td><td>%</td><td>Penggunaan koneksi dari node</td></tr>
<tr>
<td  rowspan=6>Memori</td><td>Memori yang digunakan</td><td>mem_used</td><td>MB</td><td>Kapasitas memori yang telah digunakan, termasuk kapasitas untuk data dan cache</td></tr>
<tr>
<td>Penggunaan memori</td><td>mem_util</td><td>%</td><td>Rasio memori yang sebenarnya digunakan terhadap total memori yang diminta</td></tr>
<tr>
<td>Total kunci</td><td>kunci</td><td>-</td><td>Jumlah total kunci (kunci level-1) dalam penyimpanan instans</td></tr>
<tr>
<td>Kunci kedaluwars</td><td>kedaluwarsa</td><td>-</td><td>Jumlah kunci yang kedaluwarsa dalam suatu periode waktu, yang sama dengan nilai `expired_keys` yang dikeluarkan oleh perintah `info`</td></tr>
<tr>
<td>Kunci yang dihapus</td><td>dihapus</td><td>-</td><td>Jumlah kunci yang dihapus dalam suatu periode waktu, yang sama dengan nilai `evicted_keys` yang dikeluarkan oleh perintah `info`</td></tr>
<tr>
<td>Penundaan replikasi</td><td>repl_delay</td><td>Byte</td><td>Penundaan perintah antara node replika dan node master</td></tr>
<tr>
<td  rowspan=4>Permintaan</td><td>Total permintaan</td><td>perintah</td><td>permintaan/detik</td><td>QPS, yaitu jumlah eksekusi perintah per detik</td></tr>

<tr>
<td>Permintaan baca</td><td>cmd_read</td><td>permintaan/detik</td><td>Jumlah eksekusi perintah baca per detik. Untuk informasi lebih lanjut tentang jenis perintah baca, silakan lihat <a href="#mlfl">Jenis perintah</a>.</td></tr>
<tr>
<td>Permintaan tulis</td><td>cmd_write</td><td>permintaan/detik</td><td>Jumlah eksekusi perintah tulis per detik. Untuk informasi lebih lanjut tentang jenis perintah tulis, silakan lihat <a href="#mlfl">Jenis perintah</a>.</td></tr>
<tr>
<td>Permintaan lainnya</td><td>cmd_other</td><td>permintaan/detik</td><td>Jumlah eksekusi perintah (tidak termasuk perintah tulis dan baca) per detik</td></tr>
<tr>
<td  rowspan=4>Respons</td><td>Kueri lambat</td><td>cmd_slow</td><td>-</td><td>Jumlah eksekusi perintah dengan latensi lebih besar dari konfigurasi `slowlog\-log\-slower\-than`</td></tr>
<tr>
<td>Hit permintaan baca</td><td>cmd_hits</td><td>-</td><td>Jumlah kunci yang berhasil diminta oleh perintah baca, yang sama dengan nilai keluaran metrik `keyspace_hits` oleh perintah `info`</td></tr>
<tr>
<td>Baca permintaan miss</td><td>cmd_miss</td><td>-</td><td>Jumlah kunci yang tidak berhasil diminta oleh perintah baca, yang sama dengan nilai metrik `keyspace_misses` yang dikeluarkan oleh perintah `info`</td></tr>
<tr>
<td>Tingkat hit permintaan baca</td><td>cmd_hits_ratio</td><td>%</td><td>Hit kunci/(Hit kunci + miss kunci). Metrik ini mencerminkan miss cache.</td></tr>
</tbody></table>

### Pemantauan instans
Pemantauan instans mencakup semua data pemantauan instans, termasuk data pemantauan node Proksi dan node Redis, yang dikumpulkan oleh algoritme SUM, AVG, MAX, dan LAST.

<table>
<thead><tr><th>Kategori</th><th>Metrik</th><th>Tampilan Node Terkait</th><th>Parameter</th><th>Unit</th><th>Deskripsi</th></tr></thead>
<tbody>
<tr>
<td  rowspan=2>CPU</td><td>Penggunaan CPU</td><td>node Redis</td><td>cpu_util</td><td>%</td><td>Penggunaan CPU rata-rata</td></tr>
<tr>
<td>Penggunaan CPU node maksimum</td><td>node Redis</td><td>cpu_max_util</td><td>%</td><td>Penggunaan CPU Maksimum di antara semua node (shard atau replika) dalam sebuah instans</td></tr>
<tr>
<td  rowspan=6>Memori</td><td>Memori yang digunakan</td><td>node Redis</td><td>mem_used</td><td>MB</td><td>Kapasitas memori yang sebenarmya digunakan, termasuk kapasitas untuk data dan cache</td></tr>
<tr>
<td>Penggunaan memori</td><td>node Redis</td><td>mem_util</td><td>%</td><td>Rasio memori yang sebenarnya digunakan terhadap total memori yang diminta</td></tr>
<tr>
<td>Penggunaan memori node maksimum</td><td>node Redis</td><td>mem_max_util</td><td>%</td><td>Penggunaan memori maksimum di antara semua node (shard atau replika) dalam sebuah instans</td></tr>
<tr>
<td>Total kunci</td><td>node Redis</td><td>kunci</td><td>-</td><td>Jumlah total kunci (kunci level-1) dalam penyimpanan instans</td></tr>
<tr>
<td>Kunci kedaluwarsa</td><td>node Redis</td><td>kedaluwarsa</td><td>-</td><td>Jumlah kunci yang kedaluwarsa dalam suatu periode waktu, yang sama dengan nilai `expired_keys` yang dikeluarkan oleh perintah `info`</td></tr>
<tr>
<td>Kunci yang dihapus</td><td>node Redis</td><td>dihapus</td><td>-</td><td>Jumlah kunci yang dihaus dalam suatu periode waktu, yang sama dengan nilai `evicted_keys` yang dikeluarkan oleh perintah `info`</td></tr>
<tr>
<td  rowspan=13>Jaringan</td><td>Koneksi</td><td>node Proksi</td><td>koneksi</td><td>-</td><td>Jumlah koneksi TCP ke sebuah instans</td></tr>
<tr>
<td>Penggunaan koneksi</td><td>node Proksi</td><td>connections_util</td><td>%</td><td>Rasio jumlah koneksi TCP terhadap jumlah koneksi maksimum</td></tr>
<tr>
<td>Lalu lintas masuk</td><td>node Proksi</td><td>in_flow</td><td>MB/detik</td><td>Lalu lintas masuk pribadi</td></tr>
<tr>
<td>Pemanfaatan lalu lintas masuk</td><td>node Proksi</td><td>in_bandwidth_util</td><td>%</td><td>Rasio lalu lintas masuk pribadi yang sebenarnya digunakan terhadap lalu lintas maksimum</td></tr>
<tr>
<td>Jumlah batas lalu lintas masuk</td><td>node Proksi</td><td>in_flow_limit</td><td>-</td><td>Berapa kali lalu lintas masuk memicu batas lalu lintas</td></tr>
<tr>
<td>Lalu lintas keluar</td><td>node Proksi</td><td>out_flow</td><td>MB/detik</td><td>Lalu lintas keluar pribadi</td></tr>
<tr>
<td>Pemanfaatan lalu lintas keluar</td><td>node Proksi</td><td>out_bandwidth_util</td><td>%</td><td>Rasio lalu lintas keluar pribadi yang sebenarnya digunakan terhadap lalu lintas maksimum</td></tr>
<tr>
<td>Jumlah batas lalu lintas keluar</td><td>node Proksi</td><td>out_flow_limit</td><td>-</td><td>Berapa kali lalu lintas keluar memicu batas lalu lintas</td></tr>
<tr>
<td>Latensi eksekusi rata-rata</td><td>node Proksi</td><td>latency_avg</td><td>milidetik</td><td>Latensi eksekusi rata-rata antara proksi dan server Redis</td></tr>
<tr>
<td>Latensi eksekusi maksimum</td><td>node Proksi</td><td>latency_max</td><td>milidetik</td><td>Latensi eksekusi maksimum antara proksi dan server Redis</td></tr>
<tr>
<td>Latensi baca rata-rata</td><td>node Proksi</td><td>latency_read</td><td>milidetik</td><td>Latensi eksekusi rata-rata perintah baca antara proksi dan server Redis. Untuk informasi lebih lanjut tentang jenis perintah baca, silakan lihat <a href="#mlfl">Jenis perintah</a>.</td></tr>
<tr>
<td>Latensi tulis rata-rata</td><td>node Proksi</td><td>latency_write</td><td>milidetik</td><td>Latensi eksekusi rata-rata perintah tulis antara proksi dan server Redis. Untuk informasi lebih lanjut tentang jenis perintah tulis, silakan lihat <a href="#mlfl">Jenis perintah</a>.</td></tr>
<tr>
<td>Latensi rata-rata dari perintah lain</td><td>node Proksi</td><td>latency_other</td><td>milidetik</td><td>Latensi eksekusi rata-rata perintah (tidak termasuk perintah tulis dan baca) antara proksi dan server Redis</td></tr>
<tr>
<td  rowspan=12>Permintaan</td><td>Total permintaan</td><td>node Redis</td><td>perintah</td><td>permintaan/detik</td><td>QPS, yaitu jumlah eksekusi perintah per detik</td></tr>
<tr>
<td>Permintaan baca</td><td>node Redis</td><td>cmd_read</td><td>permintaan/detik</td>
<td>Jumlah eksekusi perintah baca per detik. Untuk informasi lebih lanjut tentang jenis perintah baca, silakan lihat <a href="#mlfl">Jenis perintah</a>.</td></tr>
<tr>
<td>Permintaan tulis</td><td>node Redis</td><td>cmd_write</td><td>permintaan/detik</td><td>Jumlah eksekusi perintah tulis per detik. Untuk informasi lebih lanjut tentang jenis perintah tulis, silakan lihat <a href="#mlfl">Jenis perintah</a>.</td></tr>
<tr>
<td>Permintaan lainnya</td><td>node Redis</td><td>cmd_other</td><td>permintaan/detik</td><td>Jumlah eksekusi perintah (tidak termasuk perintah tulis dan baca) per detik</td></tr>
<tr>
<td>Permintaan bernilai besar</td><td>node Proksi</td><td>cmd_big_value</td><td>permintaan/detik</td><td>Jumlah eksekusi perintah yang lebih besar dari 32 KB per detik</td></tr>
<tr>
<td>Permintaan kunci</td><td>node Proksi</td><td>cmd_key_count</td><td>kunci/detik</td><td>Jumlah kunci yang diakses oleh perintah per detik</td></tr>
<tr>
<td>Permintaan Mget</td><td>node Proksi</td><td>cmd_mget</td><td>permintaan/detik</td><td>Jumlah eksekusi perintah Mget per detik</td></tr>
<tr>
<td>Kueri lambat</td>
<td>Node Redis</td><td>cmd_slow</td><td>-</td><td>Jumlah eksekusi perintah dengan latensi lebih besar dari konfigurasi `slowlog\-log\-slower\-than`</td></tr>
<tr>
<td>Hit permintaan baca</td><td>node Redis</td><td>cmd_hits</td><td>-</td><td>Jumlah kunci yang berhasil diminta oleh perintah baca, yang sama dengan nilai metrik `keyspace_hits` yang dikeluarkan oleh perintah `info`</td></tr>
<tr>
<td>Miss permintaan baca</td><td>node Redis</td><td>cmd_miss</td><td>-</td><td>Jumlah kunci yang tidak berhasil diminta oleh perintah baca, yang sama dengan nilai metrik `keyspace_misses` yang dikeluarkan oleh perintah `info`</td></tr>
<tr>
<td>Kesalahan eksekusi</td><td>node Proksi</td><td>cmd_err</td><td>-</td><td>Jumlah kesalahan eksekusi perintah. Misalnya, perintah tidak ada, parameter salah, dll.</td></tr>
<tr>
<td>Tingkat hit permintaan baca</td><td>node Redis</td><td>cmd_hits_ratio</td><td>%</td><td>Hit kunci/(Hit kunci + Miss kunci). Metrik ini mencerminkan miss cache.</td></tr>
</tbody></table>

### [Jenis perintah](id:mlfl)

| Jenis | Perintah |
| -------- | ------------------------------------------------------------ |
| Perintah baca   | get, strlen, exists, getbit, getrange, substr, mget, llen, lindex, lrange, sismember, scard, srandmember,<br>sinter, sunion, sdiff, smembers, sscan, zrange, zrangebyscore, zrevrangebyscore, zrangebylex,<br>zrevrangebylex, zcount, zlexcount, zrevrange, zcard, zscore, zrank, zrevrank, zscan, hget, hmget,<br>hlen, hstrlen, hkeys, hvals, hgetall, hexists, hscan, randomkey, keys, scan, dbsize, type, ttl, touch, pttl,<br>dump, object, memory, bitcount, bitpos, georadius_ro, georadiusbymember_ro, geohash, geopos, geodist, pfcount |
| Perintah tulis  | set, setnx, setex, psetex, append, del, unlink, setbit, bitfield, setrange, incr, decr, rpush, lpush, rpushx,<br>lpushx, linsert, rpop, lpop, brpop, brpoplpush, blpop, lset, ltrim, lrem, rpoplpush, sadd, srem, smove, spop,<br>sinterstore, sunionstore, sdiffstore, zadd, zincrby, zrem, zremrangebyscore, zremrangebyrank,<br>zremrangebylex, zunionstore, zinterstore, hset, hsetnx, hmset, hincrby, hincrbyfloat, hdel, incrby, decrby,<br>incrbyfloat, getset, mset, msetnx, swapdb, move, rename, renamenx, expire, expireat, pexpire, pexpireat,<br>flushdb, flushall, sort, persist, restore, restore-asking, migrate, bitop, geoadd, georadius, georadiusbymember,<br>pfadd, pfmerge, pfdebug |

## Mengkueri Informasi Node
Gunakan API [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/document/product/239/38627) untuk mendapatkan ID node Proksi dan node Redis.
>!ID node Proksi dan Redis akan berubah saat terjadi failover node, perluasan/pengurangan kapasitas instans, migrasi data, dll. Oleh karena itu, sebaiknya Anda mendapatkan informasi node terbaru dari API secara tepat waktu.

