**Preparations before running**:

Download the [phpredis](https://github.com/phpredis/phpredis) client.

**Sample code**:

```
<?php
  /**For the following parameters, enter your Redis instance's private IP, port number, instance ID and password*/
  $host = "192.168.0.2";
  $port = 6379;
  $instanceid = "c532952f-55dc-4c22-a941-63057e560788";
  $pwd = "1234567q";

  $redis = new Redis();
  // Connect to Redis
  if ($redis->connect($host, $port) == false) {
    die($redis->getLastError());
  }
  // Authenticate
  if ($redis->auth($instanceid . ":" . $pwd) == false) {
    die($redis->getLastError());
  }
  
  /**You can start manipulating the Redis instance. For more information, see https://github.com/phpredis/phpredis */
  
  // Set the Key
  if ($redis->set("redis", "tencent") == false) {
    die($redis->getLastError());
  }
  echo "set key redis suc, value is:tencent\n";
  
  // Get the Key
  $value = $redis->get("redis");
  echo "get key redis is:".$value."\n";
?>
```



**Execution result**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/PHP-1.jpg)
