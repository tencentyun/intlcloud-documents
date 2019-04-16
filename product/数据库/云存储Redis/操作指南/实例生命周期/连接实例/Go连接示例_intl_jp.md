**実行前に必ず準備**：

クライアントの [Go-redis](https://github.com/alphazero/Go-Redis)をダウンロードします。

**サンプルコード**：
```
package main

import(

   "fmt"

   "redis"

   "log"

)

func main() {

   const host=192.168.0.195
   const port=6379
   const instanceId="84ffd722-b506-4934-9025-645bb2a0997b"
   const pass="1234567q"
   // Redis サーバの 192.168.0.195:6379 に接続し、instanceId とパスワードの権限設定をする
   spec := redis.DefaultSpec().Host(host).Port(port).Password(instanceId+":"+pass);
   client, err := redis.NewSynchClientWithSpec(spec)

   if err != nil { // 接続エラーがないか

      log.Println("error on connect redis server")

      return

   }

   newvalue :=[]byte("QcloudV5!");

   err=client.Set("name",newvalue);

   if err != nil { // 設定値エラー

      log.Println(err)

      return

   }

   value, err := client.Get("name") // 値

   if err != nil { 

      log.Println(err)

      return

   }

   fmt.Println("name value is:",fmt.Sprintf("%s", value)) //出力

} 

```

**実行結果**：
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/Go-1.png)
