**실행 전의 준비 사항**:

[redis-py](https://github.com/andymccurdy/redis-py?spm=5176.730001.3.11.WvETSA)를 다운로드하고 설치합니다.


**예시 코드**:

```
#!/usr/bin/env python 
#-*- coding: utf-8 -*- 
import redis 

#여기는 연결한 인스턴스 호스트와 포트로 교체합니다. 
host = '192.168.0.195' 
port = 6379 

#여기는 인스턴스 ID와 인스턴스 비밀번호로 교체합니다. 
user='username' 
pwd='password' 

#연결 시 password 매개변수를 통해 AUTH 정보를 지정하고, user와 pwd가 ":"로 결합된 조합입니다. 
r = redis.StrictRedis(host=host, port=port, password=user+':'+pwd) 

#연결 생성 후 데이터베이스 작업을 진행할 수 있습니다. 세부 정보: https://github.com/andymccurdy/redis-py 
r.set('name', 'python_test'); 
print r.get('name')
```

**실행 결과**:
![](//qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/Pythpon-1.png)

