**Persiapan sebelum menjalankan**:

Unduh klien [Go-redis](https://github.com/alphazero/Go-Redis).

**Kode sampel**:
```
package main

import(

   "fmt"

   "redis"

   "log"

)

func main() {

   const host=192.xx.xx.195
   const port=6379
   const instanceId="84ffd722-b506-4934-9025-64xxx997b"
   const pass="123d7sq"
   // Hubungkan ke server Redis 192.xx.xx.195:6379 dan otorisasi kata sandi instanceId
   spec := redis.DefaultSpec().Host(host).Port(port).Password(instanceId+":"+pass);
   client, err := redis.NewSynchClientWithSpec(spec)

   if err != nil { // Apakah koneksinya salah

      log.Println("error on connect redis server")

      return

   }

   newvalue :=[]byte("QcloudV5!");

   err=client.Set("name",newvalue);

   if err != nil { // Nilai salah ditetapkan

      log.Println(err)

      return

   }

   value, err := client.Get("name") // Nilai

   if err != nil { 

      log.Println(err)

      return

   }

   fmt.Println("name value is:",fmt.Sprintf("%s", value)) // Output

} 

```

**Hasil eksekusi**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/Go-1.png)
