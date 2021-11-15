**Preparations before running**:
Download the [phpredis](https://github.com/phpredis/phpredis) client.

**Sample code**:
```
<?php
  /**Enter your Tendis instance private IP, port number, instance ID, and password in the following parameters*/
  $host = "192.xx.xx.2";
  $port = 6379;
  $pwd = "123tj6na";

  $redis = new Redis();
  // Connect to the Tendis instance
  if ($redis->connect($host, $port) == false) {
    die($redis->getLastError());
  }
  // Authenticate
  if ($redis->auth($pwd) == false) {
    die($redis->getLastError());
  }

  /**You can start manipulating the Tendis instance. For more information, please visit https://github.com/phpredis/phpredis. */

  // Set the key
  if ($redis->set("redis", "tencent") == false) {
    die($redis->getLastError());
  }
  echo "set key redis suc, value is:tencent\n";

  // Get the key
  $value = $redis->get("redis");
  echo "get key redis is:".$value."\n";
?>
```

**Execution results**:
![](https://main.qcloudimg.com/raw/62e281a52fd9e18178866e70236c6755.jpg)
