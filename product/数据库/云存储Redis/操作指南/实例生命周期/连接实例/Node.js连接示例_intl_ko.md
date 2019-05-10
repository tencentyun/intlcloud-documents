**실행 전의 준비 사항**:
다음 명령을 실행하고 node-redis를 설치합니다.
`npm install hiredis redis`

**예시 코드**:

```
var redis = require("redis");

/**다음 매개변수에 귀하의 Redis 인스턴스 사설 IP, 포트 번호, 인스턴스 ID와 비밀번호를 입력합니다.*/
var host = "192.168.0.2",
port = "6379",
instanceid = "c532952f-55dc-4c22-a941-63057e560788",
pwd = "1234567q";
//Redis 연결
var client  = redis.createClient(port, host, {detect_buffers: true});
// Redis 연결 오류
client.on("error", function(error) {
    console.log(error);
});
//인증
client.auth(instanceid + ":" + pwd);

/**이제 Redis 인스턴스를 조작할 수 있습니다.*/
//Key 설정
client.set("redis", "tencent", function(err, reply){
    if (err) {
        console.log(err);  
            return;  
    }
    console.log("set key redis " + reply.toString() + ", value is tencent");  
});

//Key 획득
client.get("redis", function (err, reply) {
    if (err) {
        console.log(err);  
        return;  
    }
    console.log("get key redis is:" + reply.toString());
//프로그램 종료 시 클라이언트 종료
    client.end();
});
```

**실행 결과**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/NodeJS-1.jpg)

