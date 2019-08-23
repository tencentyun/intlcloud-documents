**Preparations before running**:

Download the [Go-redis](https://github.com/alphazero/Go-Redis) client.

**Sample code**:
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
   // Connect to the Redis server 192.168.0.195:6379 and authorize the instanceId password
   spec := redis.DefaultSpec().Host(host).Port(port).Password(instanceId+":"+pass);
   client, err := redis.NewSynchClientWithSpec(spec)

   if err != nil { // Whether the connection is incorrect

      log.Println("error on connect redis server")

      return

   }

   newvalue :=[]byte("QcloudV5!");

   err=client.Set("name",newvalue);

   if err != nil { // Incorrect value set

      log.Println(err)

      return

   }

   value, err := client.Get("name") // Value

   if err != nil { 

      log.Println(err)

      return

   }

   fmt.Println("name value is:",fmt.Sprintf("%s", value)) // Output

} 

```

**Execution result**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/Go-1.png)
