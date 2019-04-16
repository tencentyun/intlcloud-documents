**実行前に必ず準備**：

[redis-py](https://github.com/andymccurdy/redis-py?spm=5176.730001.3.11.WvETSA)をダウンロードしてインストールします。


**サンプルコード**：

```
#!/usr/bin/env python 
#-*- coding: utf-8 -*- 
import redis 

#ここで接続するインスタンスのhostとportに置換 
host = '192.168.0.195' 
port = 6379 

#ここでインスタンスIDとインスタンスpasswordに置換 
user='username' 
pwd='password' 

#接続時はpasswordパラメータでAUTH情報を指定し、user、 pwdにより":"で接続する 
r = redis.StrictRedis(host=host, port=port, password=user+':'+pwd) 

#接続確立後はデータベース操作が可能。詳細は以下を参照：https://github.com/andymccurdy/redis-py 
r.set('name', 'python_test'); 
print r.get('name')
```

**実行結果**：
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/Pythpon-1.png)
