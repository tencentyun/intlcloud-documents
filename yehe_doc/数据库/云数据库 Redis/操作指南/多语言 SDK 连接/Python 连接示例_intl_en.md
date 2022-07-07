
This document provides client code samples for Python to help you access a database with or without SSL encryption enabled.

## Prerequisites
- Get the **private IPv4 address** and **port** information for database connection in the **Network Info** section on the **Instance Details** page in the [TencentDB for Redis console](https://console.cloud.tencent.com/redis). For detailed directions, see [Viewing Instance Details](https://intl.cloud.tencent.com/document/product/239/47923).
- Get the account and password for database access. For detailed directions, see [Managing Account](https://intl.cloud.tencent.com/document/product/239/34590).
- Download and install [redis-py](https://github.com/andymccurdy/redis-py?spm=5176.730001.3.11.WvETSA). The latest version is recommended.
- If you want to connect to the database over SSL, [enable SSL encryption](https://intl.cloud.tencent.com/document/product/239/48048) to get the SSL certificate file.

## Connection Sample Without SSL Encryption Enabled
You need to modify the parameters based on the comments, including IP, port, account, and password for database access.
```
#!/usr/bin/env python3
#-*- coding: utf-8 -*- 
import redis 

#Replace with the connected instance host and port here 
host = '192.xx.xx.195' 
port = 6379 

#Replace with the instance ID and password here 
user='username' 
pwd='password' 

#When connecting, specify the AUTH information through the `password` parameter. If you connect through the default account, it is `pwd`. If you connect through a custom account, it is `user+'@'+pwd`
r = redis.StrictRedis(host=host, port=port, password=user+'@'+pwd) 

#Database operations can be performed after the connection is established. For more information, visit https://github.com/andymccurdy/redis-py 
r.set('name', 'python_test'); 
print r.get('name')
```

 **Execution result**:
![img](https://main.qcloudimg.com/raw/b819ac84617439c8dcb107b0d7f4c641.png) 

## Connection Sample With SSL Encryption Enabled
You need to modify the parameters based on the comments, including SSL certificate file, IP, port, account, and password for database access.
```
import redis3 as redis3

if __name__ == "__main__":
#`vip` is the private IPv4 address for database connection, `6379` is the default port number, `pwd` is the password of the default account, and `ca.pem` is the obtained SSL certificate file. You need to replace them as needed.
    client = redis3.Redis(host="vip", port=6379, password="pwd", ssl=True, ssl_cert_reqs="required",
                          ssl_ca_certs="ca.pem")
    print(client.ping())
```

