**실행 전의 준비 사항**:

클라이언트 [Jedis](https://github.com/xetorthio/jedis/wiki/Getting-started)를 다운로드합니다.

**예시 코드**:

```
import redis.clients.jedis.Jedis;

public class HelloRedis {

  public static void main(String[] args) {
        try {
            /**다음 매개변수에 귀하의 Redis 인스턴스 사설 IP, 포트 번호, 인스턴스 ID와 비밀번호를 입력합니다.*/
            String host = "192.168.0.195";
            int port = 6379;
            String instanceid = "84ffd722-b506-4934-9025-645bb2a0997b";
            String password = "1234567q";
            //Redis 연결
            Jedis jedis = new Jedis(host, port);
            //인증
            jedis.auth(instanceid + ":" + password);

            /**이제 Redis 인스턴스를 조작할 수 있습니다. 세부 정보: https://github.com/xetorthio/jedis */
            //Key 설정
            jedis.set("redis", "tencent");
            System.out.println("set key redis suc, value is: tencent");
            //Key 획득
            String value = jedis.get("redis");
            System.out.println("get key redis is: " + value);

            //종료하고 퇴장
            jedis.quit();
            jedis.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**실행 결과**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/JAVA-1.jpg)

