This document provides client code samples for Java to help you access a database with or without SSL encryption enabled.

## Prerequisites
- Get the **private IPv4 address** and **port** information for database connection in the **Network Info** section on the **Instance Details** page in the [TencentDB for Redis console](https://console.cloud.tencent.com/redis). For detailed directions, see [Viewing Instance Details](https://intl.cloud.tencent.com/document/product/239/47923).
- Get the account and password for database access. For detailed directions, see [Managing Account](https://intl.cloud.tencent.com/document/product/239/34590).
- Download and install [Jedis](https://github.com/xetorthio/jedis/wiki/Getting-started). The latest version is recommended.
- If you want to connect to the database over SSL, [enable SSL encryption](https://intl.cloud.tencent.com/document/product/239/48048) to get the SSL certificate file.

## Connection Sample Without SSL Encryption Enabled
You need to modify the parameters based on the comments, including IP, port, account, and password for database access.
```
import redis.clients.jedis.Jedis;

public class HelloRedis {

  public static void main(String[] args) {
        try {
            /**Enter your Redis instance's private IP, port number, instance ID, and password in the following parameters in case of private network access.
                        Configure the instance's public network address, port number, and password in case of public network access.*/
            String host = "192.xx.xx.195";
            int port = 6379;
            String instanceid = "crs-09xxxqv";
            String password = "123ad6aq";
            // Connect to Redis
            Jedis jedis = new Jedis(host, port);
            // Authenticate
            jedis.auth(instanceid + ":" + password);

            /**You can start manipulating the Redis instance. For more information, visit https://github.com/xetorthio/jedis.*/
            // Set the key
            jedis.set("redis", "tencent");
            System.out.println("set key redis suc, value is: tencent");
            // Get the key
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
![img](https://main.qcloudimg.com/raw/d6103ac896b55e6412a1dd172aedc412.jpg) 

## Connection Sample With SSL Encryption Enabled
You need to modify the parameters based on the comments, including SSL certificate file, IP, port, account, and password for database access.

```java
import org.apache.commons.pool2.impl.GenericObjectPoolConfig;
import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;

import javax.net.ssl.SSLContext;
import javax.net.ssl.SSLSocketFactory;
import javax.net.ssl.TrustManager;
import javax.net.ssl.TrustManagerFactory;
import java.io.FileInputStream;
import java.io.InputStream;
import java.security.KeyStore;
import java.security.SecureRandom;


public class Main {

    public static void main(String[] args) throws Exception {
        KeyStore trustStore = KeyStore.getInstance("jks");
        // `ca.jks` is the certificate file name.
        try (InputStream inputStream = new FileInputStream("ca.jks") ){
            trustStore.load(inputStream, null);
        }
        TrustManagerFactory trustManagerFactory =      TrustManagerFactory.getInstance("PKIX");
        trustManagerFactory.init(trustStore);
        TrustManager[] trustManagers = trustManagerFactory.getTrustManagers();

        SSLContext sslContext = SSLContext.getInstance("TLS");
        sslContext.init(null, trustManagers, new SecureRandom());
        SSLSocketFactory sslSocketFactory =  sslContext.getSocketFactory();
        GenericObjectPoolConfig genericObjectPoolConfig = new GenericObjectPoolConfig();

        //with ssl config jedis pool
        // `vip` is the private IPv4 address for database connection, `6379` is the default port number, and `pwd` is the password of the default account. You need to replace them as needed.
        JedisPool pool = new JedisPool(genericObjectPoolConfig, "vip",
                6379, 2000, "pwd", 0, true, sslSocketFactory, null, null);
        Jedis jedis = pool.getResource();
        System.out.println(jedis.ping());
        jedis.close();
    }
}
```



