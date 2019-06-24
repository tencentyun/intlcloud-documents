**実行前に必ず準備**：
以下のコマンドを実行し、node-redisをインストールします：
`npm install hiredis redis`

**サンプルコード**：

```
var redis = require("redis");

/**以下のパラメータにはそれぞれRedisインスタンスのイントラネットIP、ポート番号、インスタンスIDとパスワードを入力*/
var host = "192.168.0.2",
port = "6379",
instanceid = "c532952f-55dc-4c22-a941-63057e560788",
pwd = "1234567q";
//Redisに接続
var client  = redis.createClient(port, host, {detect_buffers: true});
// Redis接続エラー
client.on("error", function(error) {
    console.log(error);
});
//認証
client.auth(instanceid + ":" + pwd);

/**続いてRedisインスタンスの操作開始が可能 */
//Key設定
client.set("redis", "tencent", function(err, reply){
    if (err) {
        console.log(err);  
            return;  
    }
    console.log("set key redis " + reply.toString() + ", value is tencent");  
});

//Key取得
client.get("redis", function (err, reply) {
    if (err) {
        console.log(err);  
        return;  
    }
    console.log("get key redis is:" + reply.toString());
//プログラムが終了してクライアントをシャットダウン
    client.end();
});
```

**実行結果**：
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/NodeJS-1.jpg)
