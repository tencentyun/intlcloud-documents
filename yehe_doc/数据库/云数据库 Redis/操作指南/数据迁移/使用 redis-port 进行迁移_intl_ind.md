## Ikhtisar
Unduh [redis-port (Linux 64-bit)](https://redis-doc-2020-1254408587.cos.ap-guangzhou.myqcloud.com/redis-port.tgz).

redis-port adalah kumpulan alat sumber terbuka yang terutama digunakan untuk sinkronisasi database, impor data, dan ekspor data antara node Redis, dan mendukung migrasi data Redis lintas edisi. Toolkit ini berisi alat-alat berikut:
- redis-sync: digunakan untuk migrasi data di antara instans Redis.
- redis-restore: mendukung impor file cadangan Redis (dalam format RDB) ke instans Redis yang ditentukan.
- redis-dump: mendukung pencadangan data Redis dalam format RDB.
- redis-decode: mendukung decoding file cadangan Redis RDB menjadi file yang dapat dibaca.

## Versi yang Kompatibel
- Mendukuing instans sumber pada Redis 2.8, 3.0, 3.2, dan 4.0.
- Instans target pada Redis 2.8, 3.0, 3.2, dan 4.0, dan di semua edisi TencentDB didukung, termasuk Edisi Memori Redis dan Edisi CKV.


## Migrasi Online Melalui redis-sync
**Cara kerjanya**
- redis-sync memiliki dua modul yang disimulasikan sebagai node replikasi guna menyinkronkan data dari instans sumber dan menerjemahkan data yang direplikasi menjadi perintah tulis untuk memperbarui instans target.
- Replikasi data dilakukan dalam dua fase: sinkronisasi penuh dan sinkronisasi tambahan.

**Deskripsi parameter:**
- -n: jumlah tugas menulis bersamaan. Sebaiknya biarkan kosong atau atur ke jumlah inti CPU * 2.
- -m: alamat instans sumber dalam format `"password"@ip:port` atau `ip:port` (dalam mode bebas kata sandi).
- -t: alamat instans target dalam format `"password"@ip:port` atau `ip:port` (dalam mode bebas kata sandi).
- --tmpfile=FILE: nama file sementara.
- --tmpfile-size=SIZE: ukuran maksimum file sementara.
- --help: perintah bantuan.

**Sampel:**
```
./redis-sync -m 127.0.0.1:6379 -t "xxx2018"@10.0.5.8:6379
```

**Output log**: (Log output:)

```
[root@VM_5_16_centos bin]# ./redis-sync -m 127.0.0.1:6379 -t "xxx2018"@10.0.5.8:6379
2019/02/21 09:56:00 sync.go:76: [INFO] sync: master = "127.0.0.1:6379", target = "xxx2018@10.0.5.8:6379"
2019/02/21 09:56:01 sync.go:103: [INFO] +
2019/02/21 09:56:01 sync.go:109: [INFO] sync: runid = "f63e2ad58e2fcc15c8cc122f15778389a012c1a4", offset = 18576271
2019/02/21 09:56:01 sync.go:110: [INFO] sync: rdb file = 9063349 (8.64mb)
2019/02/21 09:56:01 sync.go:208: [INFO] sync: (r/f,s/f,s) = (read,rdb.forward,rdb.skip/rdb.forward,rdb.skip)
2019/02/21 09:56:02 sync.go:250: [INFO] sync: rdb = 9063349 - [100.00%] (r/f,s/f,s)=(1703936/71754,0/0,0) ~ (1.62mb/-,-/-,-) ~ speed=(1.62mb/71754,0/0,0)
2019/02/21 09:56:03 sync.go:250: [INFO] sync: rdb = 9063349 - [100.00%] (r/f,s/f,s)=(3407872/153850,0/0,0) ~ (3.25mb/-,-/-,-) ~ speed=(1.62mb/82096,0/0,0)
2019/02/21 09:57:54 sync.go:250: [INFO] sync: rdb = 9063349 - [100.00%] (r/f,s/f,s)=(80487526/411969,0/1587212,0) ~  (76.76mb/-,-/-,-) ~ speed=(0/0,0/0,0)
```

**Petunjuk penggunaan:**
- Kapasitas database instans target harus lebih besar daripada instans sumber; jika tidak, migrasi akan gagal.
- Jika migrasi terganggu karena alasan seperti kegagalan jaringan, Anda harus mengosongkan instans target terlebih dahulu, kemudian melakukan migrasi lagi; jika tidak, mungkin ada data kotor.
- Kemajuan migrasi ditampilkan di log, "sync: rdb = 9063349 - [100.00%]" menunjukkan bahwa data lengkap telah disinkronkan dan sinkronisasi data tambahan sedang berlangsung, sementara "speed=(0/0,0/0,0)" menunjukkan bahwa data tambahan telah disinkronkan.
- Anda dapat menghentikan sinkronisasi dan migrasi data dengan menekan Ctrl + C atau melalui cara lain.

## Mengimpor Data Melalui redis-restore
redis-restore mendukung impor file cadangan Redis (dalam format RDB) pada Redis 2.8, 3.0, 3.2, dan 4.0 serta file AOF ke dalam instans Redis yang ditentukan.

**Deskripsi parameter:**
- -n: jumlah tugas menulis bersamaan. Sebaiknya biarkan kosong atau atur ke jumlah inti CPU * 2.
- -i: Jalur file RDB.
- -t: alamat instans target dalam format `"password"@ip:port` atau `ip:port` (dalam mode bebas kata sandi).
- -a: Jalur file AOF.
- --db=DB: ID database instans Redis target untuk impor file cadangan, yang harus sama dengan instans sumber.
- --unixtime-in-milliseconds=EXPR: nilai waktu kedaluwarsa kunci diperbarui dalam proses impor data.
- --help: perintah bantuan.

**Sampel:**
```
./redis-restore dump.rdb -t 127.0.0.1:6379
```


## Mencadangkan Data Melalui redis-dump
redis-dump mendukung pencadangan data Redis ke dalam file RDB dan data tambahan ke dalam file AOF.
>?TencentDB for Redis saat ini tidak mendukung pencadangan data melalui redis-dump. Anda dapat mencadangkan dan mengunduh data di Konsol TencentDB for Redis atau melalui API. Namun, Anda dapat menggunakan redis-dump untuk mencadangkan instans Redis yang Anda buat sendiri.

**Deskripsi parameter:**
- -n: jumlah tugas menulis bersamaan. Sebaiknya biarkan kosong atau atur ke jumlah inti CPU * 2.
- -m: Alamat instansa Redis dalam format `"password"@ip:port` atau `ip:port` (dalam mode bebas kata sandi).
- -o: jalur ke file RDB output.
- -a: jalur ke file AOF output.
- --help: perintah bantuan.

**Sampel:**
```
./redis-dump  127.0.0.1:6379 -o dump.rdb
```

