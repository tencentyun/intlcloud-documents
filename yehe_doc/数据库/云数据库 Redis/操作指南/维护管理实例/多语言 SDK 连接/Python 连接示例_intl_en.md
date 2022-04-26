
**Preparations before running**:
Download and install [redis-py](https://github.com/andymccurdy/redis-py?spm=5176.730001.3.11.WvETSA).

**Sample code**:
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
![](https://main.qcloudimg.com/raw/b819ac84617439c8dcb107b0d7f4c641.png)
