
**Preparations before running**:
Run the following command to install node-redis:
`npm install hiredis redis`

**Sample code**:

```
var redis = require("redis");

/**Enter your Tendis instance private IP, port number, instance ID, and password in the following parameters*/
var host = "192.xx.xx.2",
port = "6379",
instanceid = "c53xx52f-55dc-4c22-a941-630xxx88",
pwd = "12as6zb";
// Connect to the Tendis instance
var client  = redis.createClient(port, host, {detect_buffers: true});
// Connection error
client.on("error", function(error) {
    console.log(error);
});
// Authenticate
client.auth(instanceid + ":" + pwd);

/**You can start manipulating the Tendis instance. */
// Set the key
client.set("redis", "tencent", function(err, reply){
    if (err) {
        console.log(err);  
            return;  
    }
    console.log("set key redis " + reply.toString() + ", value is tencent");  
});

// Get the key
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

**Execution results**:
![](https://main.qcloudimg.com/raw/be497d7a1db66bebccde00fc63a98d68.jpg)
