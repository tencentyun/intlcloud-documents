## 관련 설명
TecentDB for MongoDB는 기본적으로 "rwuser"와 "mongouser" 두 개 사용자 이름을 제공하며 각각 "MONGODB-CR"과 "SCRAM-SHA-1" 인증 방식을 지원합니다. 이 두 가지 인증 방식의 경우 URI를 연결 시 서로 다른 방식으로 처리해야 합니다. 자세한 내용은 [연결 예제](https://cloud.tencent.com/doc/product/240/3563) 문서를 참조하십시오.

Python 드라이브 다운로드 [pymongo](https://pypi.python.org/pypi/pymongo/)

## 빠른 시작

### Python 예제 코드 1

```
#!/usr/bin/python
import pymongo
import random

mongodbUri = 'mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin'

client = pymongo.MongoClient(mongodbUri)
db = client.somedb
db.user.drop()
element_num=10
for id in range(element_num):
    name = random.choice(['R9','cat','owen','lee','J'])
    sex = random.choice(['male','female'])
    db.user.insert_one({'id':id, 'name':name, 'sex':sex})

content = db.user.find()
for i in content:
    print i

```

### Python 예제 코드 2

```
#!/usr/bin/python
import pymongo
mongodbUri = 'mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin'
client = pymongo.MongoClient(mongodbUri)
db = client.someonedb

inserted_id = db.somecoll.insert_one({"somekey":"yiqihapi"}).inserted_id
print inserted_id

for doc in db.somecoll.find(dict(_id=inserted_id)):
        print doc

for doc in db.somecoll.find({"somekey":"yiqihapi"}):
        print doc
```

출력:


```
5734431e101e2f6d699b37ef
{u'somekey': u'yiqihapi', u'_id': ObjectId('5734431e101e2f6d699b37ef')}
{u'somekey': u'yiqihapi', u'_id': ObjectId('5734431e101e2f6d699b37ef')}
```

