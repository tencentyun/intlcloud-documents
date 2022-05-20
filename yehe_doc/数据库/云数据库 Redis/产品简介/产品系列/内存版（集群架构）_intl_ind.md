Edisi Memori TencentDB for Redis (arsitektur kluster) adalah edisi baru Redis yang dibuat oleh Tencent Cloud berdasarkan Edisi Komunitas Kluster Redis, yang kompatibel dengan perintah Redis 4.0 dan 5.0. Edisi Memori TencentDB for Redis menggunakan arsitektur terdistribusi untuk memungkinkan penskalaan elastis dan menampilkan fleksibilitas tinggi, ketersediaan, dan kinerja puluhan juta QPS. Secara khusus, Edisi Memori TencentDB for Redis mendukung penskalaan horizontal 1–128 pecahan dan penskalaan replika dari 1-5 set replika, dan penskalaan dan migrasi hampir tidak terlihat oleh bisnis, memaksimalkan ketersediaan sistem.
![](https://main.qcloudimg.com/raw/d023aa7ddecec8b0b42a899b7ea307b0.png)

## Kasus Penggunaan
**Skenario ketersediaan tinggi (HA) master/replika**
Edisi Memori (arsitektur kluster) memungkinkan Anda mengonfigurasi kumpulan replika untuk satu node guna mencapai ketersediaan master/replika yang tinggi. Edisi Memori menawarkan hot backup server ganda dan failover otomatis untuk memastikan keandalan dan ketersediaan layanan Redis yang tinggi.
 **Skenario pemisahan baca/tulis**  
Ketika jumlah node replika lebih besar dari atau sama dengan 1, pemisahan baca/tulis otomatis dapat diaktifkan untuk instans TencentDB for Redis guna memperluas kinerja baca node tunggal. Hingga 5 set replika dapat didukung dan bobot akses baca di seluruh node master dan node replika dapat dikonfigurasi. 
**Skenario performa tinggi untuk beberapa pecahan**
Edisi Memori (arsitektur kluster) secara otomatis mengaktifkan pemecahan otomatis dan mencapai penskalaan horizontal kinerja sistem dengan menetapkan kunci yang berbeda ke beberapa node.

## Spesifikasi Kluster
- Ukuran pecahan (GB): 2, 4, 8, 12, 16, 20, 24, 28, 32, 40, 48, 64
- Jumlah pecahan: 1, 3, 5, 8, 12, 16, 24, 32, 40, 48, 64, 80, 96, 128
- Jumlah replika: 1, 2, 3, 4, 5 

## Mode Kluster
- Dalam mode kluster, data dipecah secara otomatis. Sistem ini menyediakan penyeimbangan beban data dan kemampuan migrasi.
- Mode kluster mendukung pecahan 2-64 GB.
- Mode kluster kompatibel dengan perintah tertentu dari mode non-kluster, terutama tercermin dalam akses data lintas-slot. Untuk informasi selengkapnya, lihat [Catatan tentang Kompatibilitas Perintah](#xianzhi).

## Deskripsi Replika
- Jika hanya ada satu replika, Redis menyediakan hot backup real-time master/replika untuk keandalan dan ketersediaan data yang tinggi (HA tingkat server didukung dalam satu AZ). Ketika sistem HA mendeteksi kegagalan node, ia meminta untuk beralih ke node replika, dan menambahkan node replika baru ke sistem.
- Ketika jumlah replika lebih besar dari 1, Redis menyediakan hot backup real-time master/replika dengan node replika menjadi baca saja.

## Fitur
**Fleksibilitas** 
Edisi Memori (arsitektur kluster) mendukung penskalaan horizontal 1-128 node dan penskalaan 1-5 set replika, menjadikannya ideal untuk berbagai skenario melalui penyesuaian spesifikasi instans.
**Ketersediaan** 
Dalam Edisi Memori (arsitektur kluster), penskalaan kuantitas pecahan dan kuantitas replika hampir tidak terlihat oleh bisnis, memaksimalkan ketersediaan sistem.
 **Kompatibilitas**
Edisi Memori (arsitektur kluster) mendukung kasus penggunaan  Edisi Komunitas Kluster Redis dan Codis dan kompatibel dengan klien seperti Jedis.
 **OPS**
Edisi Memori (arsitektur kluster) memaksimalkan kemampuan sistem dan memiliki fitur-fitur canggih seperti pemantauan dan manajemen tingkat pecahan, migrasi data dan penyeimbangan beban, serta pemantauan kunci besar dan cepat, yang membantu memfasilitasi manajemen sistem total dan OPS.

## [Catatan tentang Kompatibilitas Perintah](id:xianzhi)
Edisi Memori (arsitektur kluster) menyimpan data secara terdistribusi, dan perbedaan terbesarnya dari arsitektur standar terletak pada apakah satu perintah mendukung akses multikunci atau tidak. Untuk arsitektur kluster, perintah dapat dikategorikan menjadi kustom, didukung, dan tidak didukung. Untuk daftar lengkap perintah yang kompatibel, silakan lihat [Kompatibilitas Perintah](https://intl.cloud.tencent.com/document/product/239/31958).

#### Perintah tidak didukung
Sistem akan mengembalikan kesalahan berikut:
```
 kunci *
 (kesalahan) perintah ERR tidak dikenal 'keys'
```

#### Perintah yang didukung sebagian
Edisi Memori (arsitektur kluster) kompatibel dengan klien pintar seperti JedisCluster. Untuk kompatibilitas dengan JedisCluster, TencentDB for Redis memodifikasi daftar IP yang dikembalikan oleh perintah yang didukung, dan alamat IP setiap node dalam informasi yang dikembalikan adalah VIP instans.
- CLUSTER NODES
- CLUSTER SLOTS
- CONFIG GET

#### Perintah lintas slot yang didukung
Saat ini, perintah akses lintas slot yang didukung oleh Edisi Memori (arsitektur kluster) hanya mencakup MGET, MSET, dan DEL.

#### [Perintah khusus](id:ziding)
Melalui enkapsulasi VIP, Edisi Memori (arsitektur kluster) memberikan pengalaman pengguna dalam mode kluster yang sebanding dengan edisi mandiri, membuatnya lebih mudah untuk digunakan dalam skenario yang berbeda. Untuk meningkatkan transparansi ke OPS, perintah khusus dapat digunakan. Akses ke setiap node dalam kluster didukung dengan menambahkan parameter **ID node** di sebelah kanan daftar parameter perintah asli, seperti "COMMAND arg1 arg2 ... node ID". ID node dapat diperoleh melalui perintah `cluster node` atau di konsol:
```
  10.1.1.1:2000> node kluster
  25b21f1836026bd49c52b2d10e09fbf8c6aa1fdc 10.0.0.15:6379@11896 slave 36034e645951464098f40d339386e9d51a9d7e77 0 1531471918205 1 connected
  da6041781b5d7fe21404811d430cdffea2bf84de 10.0.0.15:6379@11170 master - 0 1531471916000 2 connected 10923-16383
  36034e645951464098f40d339386e9d51a9d7e77 10.0.0.15:6379@11541 myself,master - 0 1531471915000 1 connected 0-5460
  53f552fd8e43112ae68b10dada69d3af77c33649 10.0.0.15:6379@11681 slave da6041781b5d7fe21404811d430cdffea2bf84de 0 1531471917204 3 connected
  18090a0e57cf359f9f8c8c516aa62a811c0f0f0a 10.0.0.15:6379@11428 slave ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 0 1531471917000 2 connected
  ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 10.0.0.15:6379@11324 master - 0 1531471916204 0 connected 5461-10922

  Perintah asli:
  info server
  Perintah khusus:
  info server ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171
  
  Contoh perintah SCAN:
  scan 0 238b45926a528c85f40ae89d6779c802eaa394a2
  scan 0 match a* 238b45926a528c85f40ae89d6779c802eaa394a2
  
  Contoh perintah KEYS:
  keys a* 238b45926a528c85f40ae89d6779c802eaa394a2
```

Daftar perintah khusus:
- INFO
- MEMORY
- SLOWLOG
- FLUSHDB
- PING
- KEYS (hashtag didukung dan memiliki prioritas yang cocok)
- MONITOR

#### Dukungan transaksional
Edisi Memori (arsitektur kluster) mendukung perintah transaksional. Transaksi harus dimulai dengan perintah `WATCH`, kunci transaksi harus disimpan di slot yang sama, dan kunci `WATCH` dan kunci terkait transaksi harus disimpan di slot yang sama juga. Hashtag direkomendasikan untuk transaksi multkunci dalam mode kluster.

#### Dukungan multi-database
Edisi Memori (arsitektur kluster) mendukung banyak database (256 secara default); oleh karena itu, dapat mendukung semua perintah yang terkait dengan operasi database.
