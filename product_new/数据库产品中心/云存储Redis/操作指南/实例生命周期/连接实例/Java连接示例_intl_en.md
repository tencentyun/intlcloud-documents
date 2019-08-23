**Preparations before running**:

Download the [Jedis](https://github.com/xetorthio/jedis/wiki/Getting-started) client.

**Sample code**:

```
import redis.clients.jedis.Jedis;

public class HelloRedis {

  public static void main(String[] args) {
        try {
            /**For the following parameters, enter your Redis instance's private IP, port number, instance ID and password*/
            String host = "192.168.0.195";
            int port = 6379;
            String instanceid = "84ffd722-b506-4934-9025-645bb2a0997b";
            String password = "1234567q";
            // Connect to Redis
            Jedis jedis = new Jedis(host, port);
            // Authenticate
            jedis.auth(instanceid + ":" + password);

            /**You can start manipulating the Redis instance. For more information, see https://github.com/xetorthio/jedis */
            // Set the Key
            jedis.set("redis", "tencent");
            System.out.println("set key redis suc, value is: tencent");
            // Get the Key
            String value = jedis.get("redis");
            System.out.println("get key redis is: " + value);

            // Close and exit
            jedis.quit();
            jedis.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Execution result**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/JAVA-1.jpg)
