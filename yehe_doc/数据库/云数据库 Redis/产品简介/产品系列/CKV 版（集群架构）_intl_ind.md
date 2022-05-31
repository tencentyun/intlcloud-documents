
>?Edisi CKV TencentDB for Redis saat ini tidak tersedia. Kami merekomendasikan [Edisi Memori TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/18336) untuk Anda.

Edisi CKV TencentDB for Redis (arsitektur kluster) menyediakan instans kluster replika ganda, yang memecahkan hambatan utas tunggal untuk memenuhi kebutuhan bisnis Anda akan kapasitas besar atau kinerja tinggi. Edisi CKV (arsitektur kluster) kompatibel dengan protokol dan perintah Redis 3.2 dan mendukung hingga 128 pecahan dengan kapasitas 12 GB–48 TB.

## Fitur
- **Layanan tangguh**
Dengan arsitektur master/replika server ganda, node master dan replika berada pada mesin fisik yang berbeda dengan node master yang menyediakan akses eksternal dan node replika yang menyediakan cadangan data dan ketersediaan tinggi (HA). Anda dapat melakukan CRUD data menggunakan baris perintah atau klien Redis. Jika node master gagal, sistem HA yang dipatenkan akan secara otomatis melakukan pergantian master/replika untuk memastikan kelancaran operasi bisnis.        
- **Data yang andal**
Fitur persistensi data diaktifkan secara default dengan semua data yang disimpan dalam disk. Edisi CKV (arsitektur kluster) mendukung pencadangan data. Anda dapat memutar kembali atau mengkloning instans dari set cadangan guna mengatasi maloperasi data dan masalah lainnya secara efektif.
-**Latensi lebih rendah**
CKV menggunakan platform jaringan berkinerja tinggi dan arsitektur bebas proksi, yang secara signifikan mengurangi latensi akses dan latensi jaringan hingga 60% dalam skenario beban tinggi.
- **Replika baca saja**
Edisi CKV (arsitektur kluster) dapat sangat meningkatkan kinerja baca rata-rata 40% dengan mengaktifkan replika baca saja. Fitur replika baca-saja tidak diaktifkan secara default. Anda dapat [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mengajukan fitur ini. Karena penundaan replikasi antara node master CKV dan node replika, setelah fitur replika baca-saja diaktifkan, beberapa data warisan dapat dibaca; oleh karena itu, harap konfirmasikan apakah bisnis Anda dapat menerima sedikit ketidakkonsistenan data sebelum mengaktifkan fitur ini.
- **Peningkatan lancar**
Dengan skema yang unik, Edisi CKV (arsitektur kluster) dapat memastikan peningkatan versi yang tidak terlihat oleh bisnis, sehingga memaksimalkan ketersediaan layanan.

## Kasus Penggunaan
- **Volume data yang besar dalam satu instans**
Edisi CKV (arsitektur kluster) menggunakan arsitektur terdistribusi, sehingga cocok untuk menyimpan data dalam jumlah besar dalam satu instans. Kapasitasnya dapat melebihi 384 GB Edisi CKV (arsitektur standar).
- **QPS tinggi dan persyaratan konkurensi**
Edisi CKV (arsitektur kluster) menggunakan arsitektur terdistribusi dengan baca dan tulis tersebar di beberapa node. Dengan kondisi kunci terdistribusi secara merata, QPS-nya dapat meningkat secara linier dengan jumlah node. Saat ini, Edisi CKV mendukung maksimum 128 pecahan dan 10 juta QPS.
- **Dukungan protokol tidak sensitif**
Edisi CKV (arsitektur kluster) mendukung protokol yang sedikit lebih sedikit daripada edisi sumber terbuka.

## Contoh Koneksi
Edisi CKV (arsitektur kluster) hanya mendukung format kata sandi: `instance id:password`. Misalnya, jika ID instans Anda adalah crs-bkuza6i3 dan kata sandinya adalah abcd1234, perintah koneksinya adalah redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234.


## Batasan Penggunaan
- Unit minimum `pttl` di Edisi CKV adalah yang kedua, berbeda dengan Edisi Komunitas Redis.
- Saat ini, kunci jenis string didukung, dan nilainya bisa mencapai 32 MB, yang berbeda dari Edisi Komunitas Redis.
- Kecuali MSET dan MGET, operasi batch lainnya mengharuskan semua kunci berada di slot yang sama, jika tidak, pesan kesalahan "CROSSSLOT Keys in request don't hash to the same slot" dapat terjadi.
- Saat pecahan penuh, `subscribe`/`psubscribe` menggunakan sejumlah memori tertentu, yang memengaruhi penambahan langganan baru, tetapi tidak memengaruhi publikasi saluran langganan.

## Catatan
- Saat ini, ukuran satu pecahan di Edisi CKV (arsitektur kluster) adalah 4 GB secara default; oleh karena itu, disarankan agar nilai satu kunci tidak melebihi 4 GB.
- Edisi CKV (arsitektur kluster) saat ini menyediakan pemantauan pada dimensi kluster.


## Kompatibilitas

**Perintah yang didukung oleh Edisi CKV (arsitektur kluster):**
 
| **connection Group** | **geo Group** | **hashes Group** | **hyperloglog Group** | **keys Group** | **lists Group** | **pub/sub Group** | 
| --- | --- | --- | --- | --- | --- | --- |
| auth | geoadd | hdel | pfadd | del | lindex | psubscribe | 
| echo | geohash | hexists | pfcount | exists | linsert | pubsub | 
| ping | geopos | hget | pfmerge | expire | llen | publish  time |
| quit | geodist | hgetall | -　 | expireat| lpop | punsubscribe | 
| select | georadius | hincrby | -　 | type | lpush | subscribe | 
| -　 | georadiusbymember | hincrbyfloat | - | ttl| lpushx | unsubscribe |
| -　 | -　 | hkeys | -　 | persist | lrange | -　 |
| -　 | -　 | hlen | -　 | pexpire | lrem | -　 |
| -　 | -　 | hmget | -　 | pexpireat | lset | -　 |
| -　 | -　 | hmset | -　 | pttl | ltrim | -　 |
| -　 | -　 | hset | -　 | rename | rpop | -　 |
| -　 | -　 | hsetnx | -　 | renamenx | rpoplpush | -　 | 
| -　 | -　 | hstrlen | -　 | sort | rpush | -　 |
| -　 | -　 | hvals | -　 | - | rpushx | -　 |
| -　 |- 　 | hscan | -　 |-  | -　 | -　 |

|**sets Group** | **sorted sets Group** | **strings Group** | **transactions Group** |**server Group** | 
| --- | --- | --- | --- | --- |
| sadd | zadd | append | discard | command |
| scard | zcard | bitcount | exec | dbsize |
| sdiff | zcount | bitop | multi |- |
| sdiffstore | zincrby | bitpos | unwatch |- |
| sinter | zinterstore | decr | watch |- |
| sinterstore | zlexcount | decrby | -　 |- |
| sismember | zrange | get | -　 |- |
| smembers | zrangebylex | getbit | -　 |- |
| smove | zrangebyscore | getrange | -　 |- |
| spop | zrank | getset | -　 |- |
| srandmember | zrem | incr | -　 |- |
| srem | zremrangebylex | incrby | -　 |- |
| sscan | zremrangebyrank | incrbyfloat | -　 |- |
| sunion | zremrangebyscore | mget | -　 |- |
| sunionstore | zrevrange | mset | -　 |- |
| -　 | zrevrangebylex | msetnx | -　 |- |
| -　 | zrevrangebyscore | psetex | -　 |- |
| -　 | zrevrank | set | -　 |- |
| -　 | zscan | setbit |- 　 |- |
| -　 | zscore | setex | -　 |- |
| -　 | zunionstore | setnx | -　 |- |
| -　 | -　 | setrange | -　 |- |
| -　 | -　 | strlen | -　 |- |

**Perintah tidak didukung oleh Edisi CKV (arsitektur kluster):**

| **cluster Group** | **connection Group** | **keys Group** | **lists Group** | **scripting Group** | **server Group** | **strings Group** |
| --- | --- | --- | --- | --- | --- | --- |
| cluster addslots | swapdb | touch | blpop | eval | bgrewriteaof | bitfield |
| cluster count-failure-reports | -　 | restore | brpop | evalsha | bgsave | -　 |
| cluster delslots | -　 | object | brpoplpush | script debug | client kill | -　 |
| cluster failover | -　 | unlink | -　 | script exists | client list | -　 |
| cluster forget | -　 | wait | -　 | script flush | client getname | -　 |
| cluster meet | -　 | migrate | -　 | script kill | client pause | -　 |
|cluster replicate  | -　 | dump | -　 | script load | client reply | -　 |
| cluster reset | -　 | scan | -　 | -　 | client setname | -　 |
| cluster saveconfig | -　 |keys 　 | 　- | -　 | command count | -　 |
|cluster set-config-epoch  | -　 |move 　 | -　 | -　 | command getkeys | -　 |
| cluster setslot | -　 |randomkey 　 | -　 | -　 | command info | -　 |
|cluster slaves  | -　 | -　 | -　 | -　 | config get | 　- |
|readonly  | -　 | -　 | -　 | -　 | config rewrite |- 　 |
| readwrite |- 　 | -　 | -　 | -　 | config set | -　 |
| - | -　 | -　 | -　 | -　 | config resetstat | -　 |
| - | -　 | -　 | -　 | -　 | debug object | -　 |
| - | -　 | -　 | -　 | -　 | debug segfault | -　 |
| - | -　 | -　 | -　 | -　 | flushall | -　 |
|-  | -　 | -　 | -　 | -　 | flushdb | -　 |
| - | -　 | -　 | -　 | -　 | lastsave | -　 |
| -　 | -　 | -　 | -　 | -　 | monitor | -　 |
| -　 | -　 | -　 | -　 | -　 | role | -　 |
| -　 | -　 | -　 | -　 | -　 | save | -　 |
| -　 | -　 | -　 | -　 | -　 | shutdown | -　 |
| -　 | -　 | -　 | -　 | -　 | slaveof | -　 |
| -　 | -　 | -　 | -　 | -　 | slowlog | -　 |
| -　 | -　 | -　 | -　 | -　 | sync | -　 |
| -　 | -　 | -　 | -　 | -　 | info | 　- |


