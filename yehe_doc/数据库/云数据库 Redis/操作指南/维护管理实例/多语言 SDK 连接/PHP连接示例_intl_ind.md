**Persiapan sebelum menjalankan**:

Unduh klien [phpredis](https://github.com/phpredis/phpredis).

**Kode sampel**:

```
<?php
  /**Untuk parameter berikut, masukkan IP pribadi instans Redis Anda, nomor port, ID instans, dan kata sandi*/
  $host = "192.xx.xx.2";
  $port = 6379;
  $instanceid = "c532952f-55dc-4c22-a941-63057e560788";
  $pwd = "123tj6na";

  $redis = new Redis();
  // Hubungkan ke Redis
  if ($redis->connect($host, $port) == false) {
    die($redis->getLastError());
  }
  // Autentikasi
  if ($redis->auth($instanceid . ":" . $pwd) == false) {
    die($redis->getLastError());
  }
  
  /**Anda dapat mulai memanipulasi instans Redis. Untuk informasi selengkapnya, lihat https://github.com/phpredis/phpredis */
  
  // Atur Kuncinya
  if ($redis->set("redis", "tencent") == false) {
    die($redis->getLastError());
  }
  echo "set key redis suc, value is:tencent\n";
  
  // Dapatkan Kunci
  $value = $redis->get("redis");
  echo "get key redis is:".$value."\n";
?>
```



**Hasil eksekusi**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/PHP-1.jpg)
