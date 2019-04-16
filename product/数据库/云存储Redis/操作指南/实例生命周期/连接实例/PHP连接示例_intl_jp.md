**実行前に必ず準備**：

クライアントの [phpredis](https://github.com/phpredis/phpredis)をダウンロードします。

**サンプルコード**：

```
<?php
  /**以下のパラメータにはそれぞれRedisインスタンスのイントラネットIP、ポート番号、インスタンスIDとパスワードを入力*/
  $host = "192.168.0.2";
  $port = 6379;
  $instanceid = "c532952f-55dc-4c22-a941-63057e560788";
  $pwd = "1234567q";

  $redis = new Redis();
  //Redisに接続
  if ($redis->connect($host, $port) == false) {
    die($redis->getLastError());
  }
  //認証
  if ($redis->auth($instanceid . ":" . $pwd) == false) {
    die($redis->getLastError());
  }
  
  /**続いてRedisインスタンスの操作開始が可能。以下を参照：https://github.com/phpredis/phpredis */
  
  //Key設定
  if ($redis->set("redis", "tencent") == false) {
    die($redis->getLastError());
  }
  echo "set key redis suc, value is:tencent\n";
  
  //Key取得
  $value = $redis->get("redis");
  echo "get key redis is:".$value."\n";
?>
```



**実行結果**：
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/PHP-1.jpg)
