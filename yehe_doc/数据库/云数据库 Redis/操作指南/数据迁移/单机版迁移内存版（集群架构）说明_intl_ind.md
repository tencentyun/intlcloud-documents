Edisi Mandiri dapat berupa Edisi Mandiri Redis atau Edisi Standar TencentDB for Redis yang Anda buat sendiri. Dokumen ini menjelaskan masalah kompatibilitas dalam memigrasikan data dari Edisi Madiri Redis ke Edisi Kluster TencentDB for Redis.

<span id = "jrxsm"></span>
## Deskripsi Kompatibilitas
Edisi Kluster TencentDB for Redis mengadopsi arsitektur kluster yang terdiri dari proksi milik Tencent Cloud dan Edisi Kluster Komunitas Redis, yang 100% kompatibel dengan perintah Edisi Kluster Komunitas Redis.
![](https://main.qcloudimg.com/raw/4db4ee669a1e5f2730f28a901f8db0c8.png)

Masalah yang paling menantang dalam migrasi data dari Edisi Mandiri ke Edisi Kluster adalah kompatibilitas perintah dengan spesifikasi penggunaan Edisi Kluster. Anda perlu memperhatikan masalah spesifikasi penggunaan berikut:

### Operasi multikunci
Edisi Kluster Redis menggunakan algoritme hash untuk mendistribusikan kunci ke 16.000 slot. Untuk informasi selengkapnya tentang prinsip ini, silakan lihat [Spesifikasi Kluster Redis](https://redis.io/topics/cluster-spec).
- Edisi Kluster Komunitas Redis: tidak mendukung perintah akses multi-kunci lintas slot.
- Edisi Kluster TencentDB for Redis: mendukung akses multi-kunci lintas slot dari perintah `MGET`, `MSET`, dan `DEL`. Ini terutama berfungsi menggunakan proksi milik Tencent Cloud untuk mengimplementasikan komputasi perintah teragregasi di antara banyak node.
- Hashtag: dalam bisnis Anda, kunci yang perlu digunakan dalam komputasi - digabungkan ke dalam slot yang sama melalui hashtag. Untuk informasi selengkapnya tentang cara menggunakan hashtag, silakan lihat [Spesifikasi Kluster Redis](https://redis.io/topics/cluster-spec).
- Daftar perintah lintas slot:

| Grup Perintah         | Perintah          | Dukungan Lintas-Slot dalam Edisi Kluster |
| -------------- | ------------- | ------------------ |
| keys        | del           | ✓                  |
| keys        | exists        | x                  |
| keys        | rename        | x                  |
| keys        | renamenx      | x                  |
| keys        | unlink        | x                  |
| list        | rpoplpush     | x                  |
| list        | blpop         | x                  |
| list        | brpop         | x                  |
| list        | brpoplpush    | x                  |
| sets        | sdiff         | x                  |
| sets        | sdiffstore    | x                  |
| sets        | sinter        | x                  |
| sets        | sinterstore   | x                  |
| sets        | smove         | x                  |
| sets        | sunion        | x                  |
| sets        | sunionstore   | x                  |
| sorted sets | zinterstore   | x                  |
| sorted sets | zunionstore   | x                  |
| strings     | bitop         | x                  |
| strings     | mget          | ✓                  |
| strings     | mset          | ✓                  |
| strings     | msetnx        | x                  |
| hyperloglog | pfcount       | x                  |
| hyperloglog | pfmerge       | x                  |
| scripting   | eval          | x                  |
| scripting   | evalsha       | x                  |
| scripting   | script exists | x                  |
| Stream      | xread         | x                  |
| Stream      | xreadgroup    | x                  |

### Dukungan untuk Lua
- Edisi Kluster mendukung perintah Lua, tetapi akses lintas-slot ke kunci dalam skrip Lua tidak didukung.
- Parameter `KEY` harus diteruskan untuk perintah `EVAL` dan `EVALSHA`; jika tidak, parameter tersebut tidak dapat dieksekusi.
- Sub-perintah `LOAD`, `FLUSH`, `KILL`, dan `EXIST` dari `SCRIPT` akan didistribusikan ke semua node master di kluster melalui proksi.
```
> eval "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 pertama kedua
1) "key1"
2) "key2"
3) "first"
4) "second"
```
>Parameter `key1` dan `key2` harus diteruskan saat Anda menggunakan Lua.

### Dukungan transaksi
- Edisi Kluster mendukung transaksi, tetapi akses lintas slot ke kunci dalam transaksi tidak didukung.
- Anda harus terlebih dahulu menjalankan perintah `watch key`, kemudian perintah `multi` dan `exec` dalam versi saat ini. Operasi ini akan dioptimalkan pada versi mendatang untuk menghilangkan kebutuhan menjalankan `watch key` terlebih dahulu.

<span id = "zdyml"></span>
### Perintah khusus
Melalui enkapsulasi VIP, Edisi Kluster Redis memberikan pengalaman pengguna dalam mode kluster yang sebanding dengan edisi mandiri, membuatnya lebih mudah untuk digunakan dalam skenario yang berbeda. Dapat digunakan perintah khusus untuk meningkatkan transparansi ke OPS. Akses ke setiap node dalam kluster didukung dengan menambahkan parameter “node ID" di sebelah kanan daftar parameter perintah asli, seperti COMMAND arg1 arg2 ... [node ID]. ID node dapat diperoleh melalui perintah `cluster node` atau di [konsol](https://console.cloud.tencent.com/redis):
```
10.1.1.1:2000> cluster nodes25b21f1836026bd49c52b2d10e09fbf8c6aa1fdc 10.0.0.15:6379@11896 slave 36034e645951464098f40d339386e9d51a9d7e77 0 1531471918205 1 connectedda6041781b5d7fe21404811d430cdffea2bf84de 10.0.0.15:6379@11170 master - 0 1531471916000 2 connected 10923-1638336034e645951464098f40d339386e9d51a9d7e77 10.0.0.15:6379@11541 myself,master - 0 1531471915000 1 terhubung 0-546053f552fd8e43112ae68b10dada69d3af77c33649 10.0.0.15:6379@11681 slave da6041781b5d7fe21404811d430cdffea2bf84de 0 1531471917204 3 connected18090a0e57cf359f9f8c8c516aa62a811c0f0f0a 10.0.0.15:6379@11428 slave ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 0 1531471917000 2 connectedef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 10.0.0.15:6379@11324 master - 0 1531471916204 0 connected 5461-10922
Perintah asli: server info
Perintah khusus: server info  ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171SCAN 
Contoh perintah: scan 0 238b45926a528c85f40ae89d6779c802eaa394a2scan 0 match a* 238b45926a528c85f40ae89d6779c802eaa394a2KEYS 
Contoh perintah: keys a* 238b45926a528c85f40ae89d6779c802eaa394a2
```


### Metode akses klien
Sebaiknya gunakan klien mandiri (misalnya, [Jedis](https://intl.cloud.tencent.com/document/product/239/7043) tetapi bukan Kluster Jedis) untuk mengakses Edisi Kluster TencentDB for Redis, karena metode akses ini lebih efisien dan sederhana. Anda juga dapat mengakses melalui klien kluster, seperti Kluster Jedis.

### Kompatibilitas Codis
Edisi Kluster TencentDB for Redis 100% kompatibel dengan perintah Codis Server tanpa perlu modifikasi untuk bisnis Anda. Anda dapat menggunakan DTS untuk memigrasikan data dengan cepat ke TencentDB for Redis, yang memiliki keunggulan berikut dibandingkan Codis:
- Edisi Kluster TencentDB for Redis kompatibel dengan lebih banyak edisi. Codis hanya mendukung Redis v3.2 atau lebih rendah, sementara Edisi Kluster TencentDB for Redis mendukung Redis v4.0 dan v5.0 dan akan terus diperbarui secara sinkron dengan Komunitas Redis.
- Edisi Kluster TencentDB for Redis kompatibel dengan lebih banyak perintah. Codis tidak mendukung perintah pemblokiran seperti `BLPOP` dan `SUBSCRIBE`.
- Jika terjadi kunci besar dalam migrasi data dengan Codis, layanan mungkin menjadi tidak tersedia. Sebaliknya, TencentDB for Redis mendukung ekspansi lossless tanpa takut akan kunci besar.

## Pemeriksaan Kompatibilitas
Saat ini, tidak ada alat yang dapat digunakan untuk menentukan dengan tepat apakah akan ada masalah kompatibilitas dalam migrasi data dari Edisi Mandiri ke Edisi Kluster. Anda dapat menggunakan dua alat berikut untuk mengevaluasi kompatibilitas sebelum migrasi. Sebaiknya lakukan evaluasi statis, evaluasi dinamis, dan verifikasi bisnis sebelum migrasi untuk memastikan bahwa data dapat dimigrasikan dengan lancar.

### Evaluasi statis
1. Unduh [alat verifikasi statis cluster_migrate_online_check.py](https://redis-doc-2020-1254408587.cos.ap-guangzhou.myqcloud.com/cluster_migrate_check.py) dan gunakan untuk menjalankan perintah `info commandstats` untuk memeriksa apakah Edisi Mandiri pernah menjalankan perintah lintas-slot untuk menentukan apakah ada masalah kompatibilitas.
```
Penggunaan:
Kata sandi port host ./Cluster_migrate_check.py 
```
>Masuk ke Edisi Mandiri Redis yang sesuai untuk `host`, `port`, dan `password`.
2. Periksa apakah setiap item dapat lulus seperti yang diinstruksikan dalam [Deskripsi Kompatibilitas](#jrxsm) di atas.

### Evaluasi dinamis
Unduh [cluster_migrate_online_check alat verifikasi dinamis](https://redis-doc-2020-1254408587.cos.ap-guangzhou.myqcloud.com/cluster_migrate_online_check) dan menggunakannya untuk mensimulasikan eksekusi perintah `psync` pada klien untuk menyinkronkan data tambahan dari Edisi Mandiri ke Edisi Kluster TencentDB for Redis secara real-time. Dengan melakukan sinkronisasi real-time, Anda dapat memeriksa apakah ada masalah kompatibilitas dalam perintah tulis. Alat ini tidak dapat menguji kompatibilitas perintah baca.

Langkah-langkahnya adalah sebagai berikut:
1. Aktifkan Edisi Kluster TencentDB for Redis di [konsol](https://console.cloud.tencent.com/redis).
2. Gunakan alat untuk menyinkronkan data dari Edisi Mandiri ke Edisi Kluster TencentDB for Redis secara real-time.
3. Setelah periode verifikasi (seperti 6 atau 24 jam), jika alat tidak melaporkan kesalahan apa pun, perintah tulis tidak memiliki masalah kompatibilitas; jika tidak, Anda bisa mendapatkan informasi perintah yang tidak kompatibel dalam pesan kesalahannya.
```
Penggunaan:
./cluster_migrate_online_check srcip:srcport srcpasswd dstip:dstport dstpasswd 
Parameter variabel lingkungan:
export logout=1 // Digunakan untuk mencetak perintah di konsol, yang dinonaktifkan secara default
export pipeline = 2000 // Jumlah pipeline bersamaan, yaitu 1.000 secara default
```
>
>- `srcip:srcport`: Informasi alamat Edisi Mandiri Redis, yang diperlukan.
>- `dstip:dstport`: Informasi alamat Edisi KlusterTencentDB for Redis, yang bersifat opsional. Jika dibiarkan kosong, alat ini dapat digunakan sebagai monitor.
4. Periksa apakah setiap item dapat lulus seperti yang diinstruksikan dalam [Deskripsi Kompatibilitas](#jrxsm) di atas.

### Verifikasi bisnis
Untuk memastikan keberhasilan migrasi data, sebaiknya uji bisnis di lingkungan pengujian. Anda dapat menghubungkan bisnis di lingkungan pengujian ke Edisi Kluster TencentDB for Redis dan mengonfirmasi apakah semua fitur dapat berfungsi dengan baik sebelum migrasi data.

##  Migrasi Data Online dengan DTS
 Untuk petunjuk terperinci, silakan lihat [Migrasi dengan DTS](https://intl.cloud.tencent.com/document/product/239/31941).

## Kegagalan Migrasi
- Nilai parameter `client-output-buffer-limit` terlalu kecil. Sebaiknya atur menjadi 512 MB atau 1.024 MB dengan menjalankan perintah berikut:
```
config set client-output-buffer-limit "slave 1073741824 1073741824 600"
```
- Parameter belum dimasukkan untuk perintah `EVAL`.

