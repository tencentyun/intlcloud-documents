**Preparations before running**:
Run the following command to install node-redis:
`npm install hiredis redis`

**Sample code**:

```
var redis = require("redis");

/**For the following parameters, enter your Redis instance's private IP, port number, instance ID and password*/
var host = "192.168.0.2",
port = "6379",
instanceid = "c532952f-55dc-4c22-a941-63057e560788",
pwd = "1234567q";
// Connect to Redis
var client  = redis.createClient(port, host, {detect_buffers: true});
// Redis connection error
client.on("error", function(error) {
    console.log(error);
});
// Authenticate
client.auth(instanceid + ":" + pwd);

/**You can start manipulating the Redis instance */
// Set the Key
client.set("redis", "tencent", function(err, reply){
    if (err) {
        console.log(err);  
            return;  
    }
    console.log("set key redis " + reply.toString() + ", value is tencent");  
});

// Get the Key
client.get("redis", function (err, reply) {
    if (err) {
        console.log(err);  
        return;  
    }
    console.log("get key redis is:" + reply.toString());
// End the program and close the client
    client.end();
});
```

**Execution result**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/NodeJS-1.jpg)
