
**Preparations before running**:
Download and install [redis-py](https://github.com/andymccurdy/redis-py?spm=5176.730001.3.11.WvETSA).

**Sample code**:

```
#!/usr/bin/env python 
#-*- coding: utf-8 -*- 
import redis 

#Replace with the host address and port number of the instance to be connected 
host = '192.xx.xx.195' 
port = 6379 

#Replace with the password of the instance to be connected 

pwd='password' 

#When connecting, specify the AUTH information through the "password" parameter. 
r= redis.StrictRedis(host=host, port=port, password=pwd)

#Database operations can be performed after the connection is established. For more information, please visit https://github.com/andymccurdy/redis-py. 
r.set('name', 'python_test'); 
print r.get('name')
```

**Execution results**:
![](https://main.qcloudimg.com/raw/b819ac84617439c8dcb107b0d7f4c641.png)
