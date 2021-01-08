
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

   const host=192.xx.xx.195
   const port=6379
   const instanceId="84ffd722-b506-4934-9025-64xxx997b"
   const pass="123d7sq"
   // Connect to the Tendis server via the IP address "192.xx.xx.195:6379" and authorize the password of "instanceId"
   spec := redis.DefaultSpec().Host(host).Port(port).Password(instanceId+":"+pass);
   client, err := redis.NewSynchClientWithSpec(spec)

   if err != nil { // Whether an error occurs with the connection

      log.Println("error on connect redis server")

      return

   }

   newvalue :=[]byte("QcloudV5!");

   err=client.Set("name",newvalue);

   if err != nil { // Incorrect value

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

**Execution results**:
![](https://main.qcloudimg.com/raw/013f96ad8b05ed5c1eceb4638c24f3b1.png)
