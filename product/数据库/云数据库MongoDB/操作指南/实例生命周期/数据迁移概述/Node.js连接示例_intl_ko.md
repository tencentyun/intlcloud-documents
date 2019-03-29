## 관련 설명
TecentDB for MongoDB는 기본적으로 "rwuser"와 "mongouser" 두 개 사용자 이름을 제공하며 각각 "MONGODB-CR"과 "SCRAM-SHA-1" 인증 방식을 지원합니다. 이 두 가지 인증 방식의 경우 URI를 연결 시 서로 다른 방식으로 처리해야 합니다. 자세한 내용은 [연결 예제](https://cloud.tencent.com/doc/product/240/3563) 문서를 참조하십시오.

Node.js MongoDB의 드라이브 문서:
https://docs.mongodb.org/ecosystem/drivers/node-js/

## 빠른 시작
### Node.js 원본 예제 코드
Shell 설치 드라이브 패키지:
```
npm install mongodb --save
(설치에 성공하지 못했을 경우, 원본을 교체하십시오.npm config set registry http://registry.cnpmjs.org)
npm init
```
응용프로그램 코드:
```
'use strict';

var mongoClient = require('mongodb').MongoClient,
    assert = require('assert');

// URI 병합
var url = 'mongodb://mongouser:thepasswordA1@10.66.161.177:27017/admin';

mongoClient.connect(url, function(err, db) {
	assert.equal(null, err);
	var db = db.db('testdb'); // 데이터베이스 1개 선택
	var col = db.collection('demoCol'); // 세트(테이블) 1개 선택
   // 데이터 삽입
    col.insertOne(
        {
            a: 1,
            something: "yy"
        },
        //선택 가능한 매개변수
        //{
        //    w: 'majority' // "과반수" 모드를 활성화하여 데이터를 하위 노드에 쓰도록 보장합니다
        //},
        function(err, r) {
            console.info("err:", err);
            assert.equal(null, err);
            // 어설션 쓰기 성공
            assert.equal(1, r.insertedCount);
            // 데이터 조회
            col.find().toArray(function(err, docs) {
                assert.equal(null, err);
                console.info("docs:", docs);
                db.close();
            });
        }
    );
});
```

출력:

```
[root@VM_2_167_centos node]# node index.js
docs: [ { _id: 567a1bf26773935b3ff0b42a, a: 1, something: 'yy' } ]
```

## Node.js mongoose 연결 예제

```
var dbUri = "mongodb://" + user + ":" + password + "@" + host + ":" + port + "/" + dbName;
var opts = {
    auth: {
        authMechanism: 'MONGODB-CR', // SCRAM-SHA-1로 인증하면 이 매개변수가 필요하지 않습니다.
        authSource: 'admin'
    }
};
var connection = mongoose.createConnection(dbUri, opts);
```
