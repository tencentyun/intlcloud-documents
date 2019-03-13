>!local 데이터베이스는 복제본 세트의 구성 정보, oplog 등 메타 데이터를 주로 저장하고 admin 데이터베이스는 사용자, 롤 등의 정보를 주로 저장합니다. 데이터 손상, 인증 실패 등을 방지하기 위해 TencentDB for MongoDB는 local과 admin 데이터베이스를 인스턴스에 가져옵니다.

CVM에서 MongoDB가 제공하는 shell 클라이언트로 TencentDB for MongoDB를 연결하여 데이터를 가져오거나 내보낼 수 있습니다. 최신 버전의 MongoDB 클라이언트 슈트를 사용해야 합니다. 구체적인 방법은 [작업 가이드 > 연결 예제](https://cloud.tencent.com/document/product/240/3563)를 참조하십시오.

## 가져오기 명령
#### mongodump와 mongorestore

MongoDB는 공식으로 두 가지 데이터 가져오기/내보내기 도구 패키지를 제공합니다. 전체 데이터베이스를 가져오기/내보내기 시, 일반적으로 [mongodump](https://docs.mongodb.com/manual/reference/program/mongodump/)와 [mongorestore](https://docs.mongodb.com/manual/reference/program/mongorestore/)를 사용합니다. 데이터 형식은 BSON이고 대규모 dump와 restore 시 효율이 비교적으로 높습니다.

mongodump 가져오기 명령은 다음과 같습니다.
```
mongodump --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb -o /data/dump_testdb
```

![mongodump 예제 스크린샷](https://mc.qcloudimg.com/static/img/4071cfd5d9b54c720349f41fc2e07b0c/dump_default.png)
mongorestore 가져오기 명령은 다음과 같습니다.
```
mongorestore --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --dir=/data/dump_testdb
```

![mongorestore 예제 스크린샷](https://mc.qcloudimg.com/static/img/335dbef8f11a5417e42740472df1a5b8/restore_default.png)

## 내보내기 명령
#### mongoexport와 mongoimport

단일 집합에 대해 내보내기/가져오기 시, 일반적으로 [mongoexport](https://docs.mongodb.com/manual/reference/program/mongoexport/)와 [mongoimport](https://docs.mongodb.com/manual/reference/program/mongoimport/)를 사용합니다. 데이터 형식은 JSON이고 가독성이 비교적으로 높습니다.

mongoexport 내보내기 명령은 다음과 같습니다.

```
mongoexport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection -o /data/export_testdb_testcollection.json
```

또한, -f 매개변수를 추가하여 필요한 필드를 지정할 수 있으며, -q 매개변수를 추가하여 조회 조건을 지정하면 내보낼 데이터를 제한할 수 있습니다.

-fongoimport 내보내기 명령은 다음과 같습니다.

```
mongoimport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection2 --file=/data/export_testdb_testcollection.json
```

## 여러 인증 방식의 매개변수 설명

[연결 예제](https://cloud.tencent.com/doc/product/240/3563)에 설명되어 있습니다. TencentDB for MongoDB는 기본적으로 "rwuser"와 "mongouser"를 제공하여 각각 "MONGODB-CR"와 "SCRAM-SHA-1" 인증 방식을 지원합니다.
- "mongouser" 및 콘솔에서 생성한 모든 새 사용자의 경우, 내보내기/가져오기 명령 도구를 사용할 때, 위 예제에 따라 진행하면 됩니다.
- "rwuser"의 경우, 각 명령에 매개변수 "--authenticationMechanism=MONGODB-CR"을 추가해야 합니다.

mongodump 예제:
```
mongodump --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```
