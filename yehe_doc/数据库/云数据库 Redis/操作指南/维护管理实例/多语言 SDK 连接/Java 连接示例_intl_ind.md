**Persiapan sebelum menjalankan**:
Unduh klien [Jedis](https://github.com/xetorthio/jedis/wiki/Getting-started).

**Kode sampel**:

```
import redis.clients.jedis.Jedis;

public class HelloRedis {

  public static void main(String[] args) {
        try:
            /**Masukkan IP pribadi instans Redis Anda, nomor port, ID instans, dan sandi dalam parameter berikut*/
            String host = "192.xx.xx.195";
            int port = 6379;
           String instanceid = "crs-09xxxqv";
            String password = "123ad6aq";
            // Hubungkan ke Redis
            Jedis jedis = new Jedis(host, port);
            // Autentikasi
            jedis.auth(instanceid + ":" + password);

            /**Anda dapat mulai memanipulasi instans Redis. Untuk informasi selengkapnya, lihat https://github.com/xetorthio/jedis */
            // Atur Kuncinya
            jedis.set("redis", "tencent");
            System.out.println("set key redis suc, value is: tencent");
            // Dapatkan Kunci
            String value = jedis.get("redis");
            System.out.println("get key redis is: " + value);

            // Tutup dan keluar
            jedis.quit();
            jedis.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Hasil eksekusi:
![](https://main.qcloudimg.com/raw/d6103ac896b55e6412a1dd172aedc412.jpg)
