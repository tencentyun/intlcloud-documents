**Preparations before running**:
Download the [Jedis](https://github.com/xetorthio/jedis/wiki/Getting-started) client.

**Sample code**:

```
import redis.clients.jedis.Jedis;

public class HelloRedis {

  public static void main(String[] args) {
        try:
            /**Enter your Redis instance private IP, port number, instance ID, and password in the following parameters*/
            String host = "192.xx.xx.195";
            int port = 6379;
           String instanceid = "crs-09xxxqv";
            String password = "123ad6aq";
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

**Execution results**:
![](https://main.qcloudimg.com/raw/d6103ac896b55e6412a1dd172aedc412.jpg)
