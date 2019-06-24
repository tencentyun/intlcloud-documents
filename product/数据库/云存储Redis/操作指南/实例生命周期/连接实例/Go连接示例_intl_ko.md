**실행 전의 준비 사항**:

클라이언트 [Go-redis](https://github.com/alphazero/Go-Redis)를 다운로드합니다.

**예시 코드**:
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
   // Redis 서버 192.168.0.195:6379에 연결하고 instanceId 비밀번호를 라이센싱합니다.
   spec := redis.DefaultSpec().Host(host).Port(port).Password(instanceId+":"+pass);
   client, err := redis.NewSynchClientWithSpec(spec)

   if err != nil { // 연결 오류 여부

      log.Println("error on connect redis server")

      return

   }

   newvalue :=[]byte("QcloudV5!");

   err=client.Set("name",newvalue);

   if err != nil { // 설정값 오류

      log.Println(err)

      return

   }

   value, err := client.Get("name") // 값

   if err != nil { 

      log.Println(err)

      return

   }

   fmt.Println("name value is:",fmt.Sprintf("%s", value)) //출력

} 

```

**실행 결과**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/Go-1.png)

