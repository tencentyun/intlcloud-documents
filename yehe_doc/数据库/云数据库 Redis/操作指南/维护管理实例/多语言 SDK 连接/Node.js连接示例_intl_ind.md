**Persiapan sebelum menjalankan**:
Jalankan perintah berikut untuk menginstal node-redis:
`npm install hiredis redis`

**Kode sampel**:

```
var redis = require("redis");

/**Untuk parameter berikut, masukkan IP pribadi instans Redis Anda, nomor port, ID instans, dan kata sandi*/
var host = "192.xx.xx.2",
port = "6379",
instanceid = "c53xx52f-55dc-4c22-a941-630xxx88",
pwd = "12as6zb";
// Hubungkan ke Redis
var client  = redis.createClient(port, host, {detect_buffers: true});
// Kesalahan koneksi Redis
client.on("error", function(error) {
    console.log(error);
});
// Autentikasi
client.auth(instanceid + ":" + pwd);

/**Anda dapat mulai memanipulasi instans Redis */
// Atur Kuncinya
client.set("redis", "tencent", function(err, reply){
    if (err) {
        console.log(err);  
            return;  
    }
    console.log("set key redis " + reply.toString() + ", value is tencent");  
});

// Dapatkan Kunci
client.get("redis", function (err, reply) {
    if (err) {
        console.log(err);  
        return;  
    }
    console.log("get key redis is:" + reply.toString());
// Akhiri program dan tutup klien
    client.end();
});
```

**Hasil eksekusi**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/NodeJS-1.jpg)
