
>?Edisi CKV TencentDB for Redis saat ini tidak tersedia. Kami merekomendasikan [Edisi Memori TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/31959) untuk Anda.

Edisi CKV TencentDB for Redis (arsitektur standar) menggunakan arsitektur deployment node master/replika untuk menyediakan persistensi dan pencadangan data, sehingga cocok untuk skenario yang memerlukan keandalan dan ketersediaan data yang tinggi.
Node master menyediakan akses layanan harian, sedangkan node replika memastikan ketersediaan tinggi (HA). Jika node master gagal, sistem akan secara otomatis beralih ke node replika untuk menjamin kelangsungan bisnis. Edisi CKV (arsitektur standar) kompatibel dengan perintah dan protokol Redis 3.2 serta mendukung spesifikasi 4–384 GB untuk memenuhi kebutuhan penyimpanan berkapasitas besar.
![](https://main.qcloudimg.com/raw/dd4615622819ebf541e3c33d76302b73.png)

## Fitur
- **Layanan tangguh**
Dengan arsitektur master/replika server ganda, node master dan replika berada pada mesin fisik yang berbeda dengan node master yang menyediakan akses eksternal dan node replika yang menyediakan cadangan data dan HA. Anda dapat melakukan CRUD data menggunakan baris perintah atau klien Redis. Jika node master gagal, sistem HA yang dipatenkan akan secara otomatis melakukan pergantian master/replika untuk memastikan kelancaran operasi bisnis.        
-**Data yang andal**
Fitur persistensi data diaktifkan secara default dengan semua data yang disimpan dalam disk. Edisi CKV (arsitektur standar) mendukung pencadangan data. Anda dapat memutar kembali atau mengkloning instans dari set cadangan guna mengatasi maloperasi data dan masalah lainnya secara efektif.
- **Latensi rendah**
CKV menggunakan platform jaringan berkinerja tinggi dan arsitektur bebas proksi, yang secara signifikan mengurangi latensi akses dan latensi jaringan hingga 60% dalam skenario beban tinggi.
- **Replika baca saja**
Edisi CKV (arsitektur standar) dapat sangat meningkatkan kinerja baca rata-rata 40% dengan mengaktifkan replika baca saja. Fitur replika baca-saja tidak diaktifkan secara default. Anda dapat [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mengajukan fitur ini. Karena penundaan replikasi antara node master CKV dan node replika, setelah fitur replika baca-saja diaktifkan, beberapa data warisan dapat dibaca; oleh karena itu, harap konfirmasikan apakah bisnis Anda dapat menerima sedikit ketidakkonsistenan data sebelum mengaktifkan fitur ini.
- **Peningkatan lancar**
Dengan skema yang unik, Edisi CKV (arsitektur standar) dapat memastikan peningkatan versi yang tidak terlihat oleh bisnis, sehingga memaksimalkan ketersediaan layanan.

## Batasan Penggunaan

- Edisi CKV (arsitektur standar) mendukung hingga 120.000 QPS. Jika Anda membutuhkan QPS yang lebih tinggi, Anda dapat memilih arsitektur kluster yang mendukung puluhan juta QPS.
- Unit minimum `pttl` di Edisi CKV adalah yang kedua, berbeda dengan Edisi Komunitas Redis.
- Saat ini, kunci jenis string didukung, dan nilainya bisa mencapai 32 MB.
- Metode koneksi instans adalah `instance ID:password`, yang berbeda dari Edisi Memori dalam arsitektur standar atau kluster.
- Kompleksitas waktu yang diimplementasikan oleh perintah `dbsize` adalah O(n). Ketika perintah dijalankan, perlu melintasi semua kunci dalam database saat ini; oleh karena itu, harus digunakan dengan hati-hati.
- Ada kunci tipe string bawaan: `{ckv_plus_pub_sub}_patterns`, yang digunakan untuk mendukung fitur pub/sub. Jika Anda perlu menggunakan fitur ini, jangan hapus kunci ini; jika tidak, langganan akan menjadi tidak valid.
- Pemberitahuan acara saat ini tidak mendukung pemberitahuan kedaluwarsa dan kebijakan eviction.
- Kebijakan eviction saat ini hanya mendukung `volatile-lru`. Mekanisme eviction dapat dinonaktifkan dengan parameter yang sesuai `maxmemory-policy`.


## Contoh Koneksi
Edisi CKV (arsitektur standar) hanya mendukung format kata sandi: `instance id:password`. Misalnya, jika ID instans Anda adalah crs-bkuza6i3 dan kata sandinya adalah abcd1234, perintah koneksinya adalah `redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234.

## Kompatibilitas
*Perintah yang didukung oleh Edisi CKV (arsitektur standar):**

| **connection Group** | **geo Group** | **hashes Group** | **hyperloglog Group** | **keys Group** | **lists Group** | **pub/sub Group** | **server Group** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| auth | geoadd | hdel | pfadd | del | lindex | psubscribe | command |
| echo | geohash | hexists | pfcount | scan | linsert | pubsub | dbsize |
| ping | geopos | hget | pfmerge | exists | llen | publish | info |
| quit | geodist | hgetall | -　 | expire | lpop | punsubscribe | time |
| select | georadius | hincrby | -　 | expireat | lpush | subscribe | -　 |
| -　 | georadiusbymember | hincrbyfloat | -　 | keys | lpushx | unsubscribe | -　 |
| -　 |- 　 | hkeys | -　 | type | lrange | -　 | -　 |
| -　 | -　 | hlen | -　 | move | lrem | -　 | -　 |
| -　 | -　 | hmget | -　 | ttl | lset | 　- | -　 |
| -　 | -　 | hmset | -　 | persist | ltrim | -　 | -　 |
| -　 | -　 | hset | -　 | pexpire | rpop | -　 | -　 |
| -　 | -　 | hsetnx | -　 | pexpireat | rpoplpush | -　 | -　 |
| -　 | -　 | hstrlen | -　 | pttl | rpush | -　 | -　 |
| -　 | -　 | hvals | -　 | randomkey | rpushx | -　 | -　 |
| -　 | -　 | hscan | -　 | rename | -　 | -　 | -　 |
| -　 | -　 | -　 | -　 | renamenx | -　 | -　 | -　 |
| -　 | -　 | -　 | -　 | sort | -　 | -　 | -　 |


|**sets Group** | **sorted sets Group** | **strings Group** | **transactions Group** | **scripting Group** |
| --- | --- | --- | --- | --- |
| sadd | zadd | append | discard |eval|
| scard | zcard | bitcount | exec |script debug|
| sdiff | zcount | bitop | multi |script exists|
| sdiffstore | zincrby | bitpos | unwatch |script flush|
| sinter | zinterstore | decr | watch |script kill|
| sinterstore | zlexcount | decrby | -　 |script load |
| sismember | zrange | get | -　 |-  |
| smembers | zrangebylex | getbit | -　 |-  |
| smove | zrangebyscore | getrange | -　 |-  |
| spop | zrank | getset | -　 |-  |
| srandmember | zrem | incr | -　 |-  |
| srem | zremrangebylex | incrby | -　 |-  |
| sscan | zremrangebyrank | incrbyfloat | -　 |-  |
| sunion | zremrangebyscore | mget | -　 |-  |
| sunionstore | zrevrange | mset | -　 |-  |
| -　 | zrevrangebylex | msetnx | -　 |-  |
| -　 | zrevrangebyscore | psetex | -　 |-  |
| -　 | zrevrank | set | -　 |-  |
| -　 | zscan | setbit | -　 |-  |
| -　 | zscore | setex | -　 |-  |
| -　 | zunionstore | setnx | -　 |-  |
| -　 | -　 | setrange |- 　 |-  |
| -　 | -　 | strlen | -　 |-  |

**Perintah tidak didukung oleh Edisi CKV (arsitektur standar):**

| **cluster Group** | **connection Group** | **keys Group** | **lists Group** | **scripting Group** | **server Group** | **strings Group** |
| --- | --- | --- | --- | --- | --- | --- |
| cluster addslots | swapdb | touch | blpop | evalsha | bgrewriteaof | bitfield |
| cluster count-failure-reports | -　 | restore | brpop | - | bgsave |- 　 |
| cluster countkeyinslot | -　 | object | brpoplpush | - | client kill | -　 |
| cluster delslots | -　 | unlink | -　 |-  | client list | -　 |
| cluster failover | - | wait | 　- |-  | client getname | -　 |
| cluster forget | -　 | migrate | -　 |-  | client pause | 　- |
| cluster getkeysinslot | -　 | dump | 　- |- | client reply | -　 |
| cluster info | -　 | 　- | -　 | 　- | client setname | 　- |
| cluster keyslot | -　 | -　 | -　 | 　- | command count | -　 |
| cluster meet |- 　 | -　 | 　- | -　 | command getkeys | 　- |
| cluster nodes | 　- | 　- | -　 | -　 | command info | -　 |
| cluster replicate | -　 | 　- | -　 | -　 | config get | -　 |
| cluster reset | 　- | 　- | -　 |- 　 | config rewrite | -　 |
| cluster saveconfig | -　 | 　- | 　- | 　- | config set | -　 |
| cluster set-config-epoch | -　 | -　 | 　- | 　- | config resetstat | 　- |
| cluster setslot | 　- | 　- | 　- |- 　 | debug object | -　 |
| cluster slaves | 　- | 　- | 　- | -　 | debug segfault | -　 |
| cluster slots | -　 | 　- | 　- | 　- | flushall | -　 |
| readonly | -　 | 　- | 　- | -　 | flushdb | 　- |
| readwrite | -　 | -　 | -　 | 　- | lastsave | -　 |
| -　 | -　 | -　 | -　 | 　- | monitor | -　 |
| -　 | -　 | -　 | 　- | 　- | role | 　- |
| 　- | -　 | -　 | -　 | -　 | save | 　- |
| 　- | -　 | -　 | -　 | -　 | shutdown | 　- |
| -　 | -　 | -　 | -　 | -　 | slaveof | -　 |
| -　 | -　 | -　 | -　 | -　 | slowlog | -　 |
| -　 | -　 | -　 | -　 | -　 | sync | -　 |
