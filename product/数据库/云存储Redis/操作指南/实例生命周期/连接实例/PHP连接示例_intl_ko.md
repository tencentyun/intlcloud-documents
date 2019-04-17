**실행 전의 준비 사항**:

클라이언트 [phpredis](https://github.com/phpredis/phpredis)를 다운로드합니다.

**예시 코드**:

```
<?php
  /**다음 매개변수에 귀하의 Redis 인스턴스 사설 IP, 포트 번호, 인스턴스 ID와 비밀번호를 입력합니다.*/
  $host = "192.168.0.2";
  $port = 6379;
  $instanceid = "c532952f-55dc-4c22-a941-63057e560788";
  $pwd = "1234567q";

  $redis = new Redis();
  //Redis 연결
  if ($redis->connect($host, $port) == false) {
    die($redis->getLastError());
  }
  //인증
  if ($redis->auth($instanceid . ":" . $pwd) == false) {
    die($redis->getLastError());
  }
  
  /**이제 Redis 인스턴스를 조작할 수 있습니다. 세부 정보: https://github.com/phpredis/phpredis */
  
  //Key 설정
  if ($redis->set("redis", "tencent") == false) {
    die($redis->getLastError());
  }
  echo "set key redis suc, value is:tencent\n";
  
  //Key 획득
  $value = $redis->get("redis");
  echo "get key redis is:".$value."\n";
?>
```



**실행 결과**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/PHP-1.jpg)

