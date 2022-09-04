## Overview
When using Mongo Shell to connect to database, you can enable Secure Sockets Layer (SSL) encryption feature to improve the security of the data linkage. The network connection can be encrypted at the transport layer with the SSL encryption feature to improve the communication data security and ensure data integrity.

## Prerequisite
- Create a Linux [CVM](https://intl.cloud.tencent.com/document/product/213/10517) instance in the same VPC and the same region as the TencentDB for MongoDB instance.
- You have obtained the username and password information for database instance access on the **Account Management** tab on the **Database Management** page. For detailed directions, see [Account Management](https://intl.cloud.tencent.com/document/product/240/44183).
- You have obtained the private IP and port for database instance access in the **Instance List**. For detailed directions, see [Viewing Instance Details](https://intl.cloud.tencent.com/document/product/240/44179).
- SSL encryption feature has been enabled on the instance. For details, see [Enabling SSL Authentication](https://intl.cloud.tencent.com/document/product/240/48468)

## Directions
This document uses the Linux operating system as an example to demonstrate the specific operation process.

1. Download SSL CA certificate. For detailed directions, see [Enabling SSL Authentication] (https://intl.cloud.tencent.com/document/product/240/48468)
2. Upload the certificate file **MongoDB-CA.crt** to the CVM server with Mongo Shell installed.
3. On the CVM server with Mongo Shell installed, execute the following command to connect to the MongoDB database.
>? For MongoDB 4.2 and later, Transport Layer Security (TLS) is used to perform data authentication. TLS is the security protocol of transport layer, an upgraded version of SSL. When you are not sure whether to use SSL authentication or TLS authentication, you can execute `./mongo_ssl -h` to confirm the authentication method.
>
 - **SSL Authentication**
```
./bin/mongo -umongouser -plxh***** 172.xx.xx.xx:27017/admin --ssl --sslCAFile MongoDB-CA.crt --sslAllowInvalidHostnames
```
Please replace the following parameters as needed.
    - -u: Database connection username
    - -p: Username password
    - `172.xx.xx.xx` and `27017` specify the IP (port number included) and port of the TencentDB for MongoDB instance respectively. If you forgot the username and password, view and modify the account and password as instructed in [Account Management](https://intl.cloud.tencent.com/document/product/240/44183).
    - --sslCAFile: Certificate file path of SSL authentication
 - **TLS Authentication**：
```
./bin/mongo -umongouser -plxh***** 172.xx.xx.xx:27017/admin --tls --tlsCAFile /data/MongoDB-CA.crt --tlsAllowInvalidHostnames 
```
 --tlsCAFile: Certificate file path of TLS authentication
4. After a successful connection, the following information will be displayed:
```
MongoDB shell version v4.2.16
connecting to: mongodb://172.x.x.X:27017/admin?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("aeb18f32-6413-49da-864a-5123b4d2****") }
MongoDB server version: 4.2.11
Welcome to the MongoDB shell.
```

## References
For SDK connection in other languages, see [Using Multi-Language SDKs to Connect to Database by SSL Authentication] (https://intl.cloud.tencent.com/document/product/240/48470)
