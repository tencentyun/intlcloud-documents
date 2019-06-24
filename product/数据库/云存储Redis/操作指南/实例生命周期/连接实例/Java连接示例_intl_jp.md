**実行前に必ず準備**：

クライアントの [Jedis](https://github.com/xetorthio/jedis/wiki/Getting-started)をダウンロードします。

**サンプルコード**：

```
import redis.clients.jedis.Jedis;

public class HelloRedis {

  public static void main(String[] args) {
        try {
            /**以下のパラメータにはそれぞれRedisインスタンスのイントラネットIP、ポート番号、インスタンスIDとパスワードを入力*/
            String host = "192.168.0.195";
            int port = 6379;
            String instanceid = "84ffd722-b506-4934-9025-645bb2a0997b";
            String password = "1234567q";
            //Redisに接続
            Jedis jedis = new Jedis(host, port);
            //認証
            jedis.auth(instanceid + ":" + password);

            /**続いてRedisインスタンスの操作開始が可能。https://github.com/xetorthio/jedis */を参照しても良い。
            //Key設定
            jedis.set("redis", "tencent");
            System.out.println("set key redis suc, value is: tencent");
            //Key取得
            String value = jedis.get("redis");
            System.out.println("get key redis is: " + value);

            //シャットダウンとログアウト
            jedis.quit();
            jedis.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**実行結果**：
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/JAVA-1.jpg)
