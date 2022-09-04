## Java
**keytool** is a native key and certificate management tool in Java, which is convenient for you to manage your public/private keys and certificates for authentication services. Keytool stores keys and certificates in keystore. 

Converting certificate format with keytool: 
```
keytool -importcert -trustcacerts -file <certificate file> -keystore <trust store> -storepass <password>
```
- `-file <certificate file>`: SSL certificate or TLS certificate file **MongoDB-CA.crt**
- `-keystore <trust store>`: Specified keystore name
- s`torepass <password> `: Specified keystore password

To set the keystore of JVM system property, you need to change the value of `trustStore` and `password` as required to refer to correct keystore. You also need to replace the URI combination with the user password information that is used to access the database.
```
System.setProperty("javax.net.ssl.trustStore", trustStore);
System.setProperty("javax.net.ssl.trustStorePassword", password);

import com.mongodb.MongoClientURI;
import com.mongodb.MongoClientOptions;

String uri = "mongodb://mongouser:password@10.x.x.1:27017/admin";
MongoClientOptions opt = MongoClientOptions.builder().sslEnabled(true).sslInvalidHostNameAllowed(true).build();
MongoClient client = new MongoClient(uri, options); 
```

## Go
The following is a code example of using GO language to connect to database by SSL authentication. You need to replace the path of the certificate file MongoDB-CA.crt, the account and password, IP information and port information concatenated in the URI as needed.
```
 package main

import (
    "context"
    "crypto/tls"
    "crypto/x509"
    "io/ioutil"

     "go.mongodb.org/mongo-driver/mongo"
     "go.mongodb.org/mongo-driver/mongo/options"
)

func main(){
    ca, err := ioutil.ReadFile("MongoDB-CA.crt")
    if err != nil{
        return
    }
    pool := x509.NewCertPool()
    ok := pool.AppendCertsFromPEM([]byte(ca))
    if !ok {
        return
    }
    tlsConfig := &tls.Config{
        RootCAs:      pool,
        InsecureSkipVerify: true,
    }
    uri := "mongodb://mongouser:password@10.x.x.1:27017/admin?ssl=true"
    clientOpt := options.Client().ApplyURI(uri)
    clientOpt.SetTLSConfig(tlsConfig)

     client, err := mongo.Connect(context.TODO(), clientOpt)
     if err != nil{
         return
     }
    client.Disconnect(context.TODO())
} 
```

## Python
The following is a code example of using Python language to connect database by SSL authentication. You need to replace the path of the certificate file MongoDB-CA.crt, the account and password, IP information and port information concatenated in the URI as needed.
```
 uri = "mongodb://mongouser:password@10.x.x.1:27017/admin"
client = MongoClient(uri,
           ssl=True,
           ssl_ca_certs='MongoDB-CA.crt',
           ssl_match_hostname=False) 
```

