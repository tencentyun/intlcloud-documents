**Preparations before running**:
Download and install [redis-py](https://github.com/andymccurdy/redis-py?spm=5176.730001.3.11.WvETSA).

**Sample Code**:

```
#!/usr/bin/env python 
#-*- coding: utf-8 -*- 
import redis 

#Replace with the connected instance's host and port here 
host = '192.168.0.195' 
port = 6379 

#Replace with the instance ID and instance password here 
user='username' 
pwd='password' 

#When connecting, specify the AUTH information through the password parameter in the format of user+'@'+pwd 
r = redis.StrictRedis(host=host, port=port, password=user+'@'+pwd) 

#Database operations can be performed after the connection is established. For more information, see https://github.com/andymccurdy/redis-py 
r.set('name', 'python_test'); 
print r.get('name')
```

**Execution results**:
![](https://main.qcloudimg.com/raw/b819ac84617439c8dcb107b0d7f4c641.png)
