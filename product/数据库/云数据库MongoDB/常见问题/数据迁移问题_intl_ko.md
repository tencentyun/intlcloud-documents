### MongoDB 데이터베이스에서 데이터를 내보내려면 매개변수를 어떻게 설정해야 하나요?
Mongodump의 매개변수에서 readPreference=secondaryPreferred를 설정합니다.

### MongoDB는 어떤 데이터 마이그레이션을 지원하나요?
현재는 TencentDB CVM 자체 생성한 인스턴스 마이그레이션과 공중망 인스턴스 마이그레이션을 지원합니다. 자세한 내용은 [MongoDB 데이터 마이그레이션](https://cloud.tencent.com/document/product/240/8271)을 참조하십시오.

### Mongodump(전체 데이터베이스) 또는 Mongoexport(단일 클러스터)를 사용하여 어떻게 MongoDB의 데이터를 로컬 서버로 내보낼 수 있나요?

CVM에서 MongoDB가 제공하는 [shell 클라이언트](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/)로 TencentDB for MongoDB와 연결한 후, 데이터를 내보냅니다. **최신 버전의 MongoDB 클라이언트 슈트를 사용해야 합니다.**
MongoDB는 공식으로 두 가지 데이터 내보내기 도구 패키지를 제공합니다. 전체 데이터베이스를 내보낼 때, 일반적으로 mongodump를 사용하고 데이터 형식은 BSON이며 대규모 dump 시 효율이 비교적으로 높습니다. 단일 클러스터를 내보낼 때, 일반적으로 mongodump를 사용하고 데이터 형식은 JSON이며 가독성이 비교적으로 높습니다.
**1. Mongodump로 전체 데이터베이스를 내보내고 백업하기**
 내보내기 명령은 다음과 같습니다.

```
 mongodump --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb -o /data/dump_testdb
```

![이미지 설명](//bot1024-1253841380.file.myqcloud.com/598299decb2a1.png)

**2. Mongoexport로 단일 클러스터에 대해 내보내고 백업하기**
내보내기 명령은 다음과 같습니다.

```
mongoexport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection  -o /data/export_testdb_testcollection.json
```

-f 매개변수를 추가하여 필요한 필드를 지정할 수 있으며, -q 매개변수를 추가하여 조회 조건을 지정하면 내보낼 데이터를 제한할 수 있습니다.

**3. Rwuser와 Mongouser가 내보내기 명령을 입력할 때에 대한 매개변수 설명** 
[연결 예제](https://cloud.tencent.com/document/product/240/3563) 문서에 설명되어 있습니다. TecentDB for MongoDB는 기본적으로 rwuser와 mongouser 두 개 사용자 이름을 제공하며 각각 MONGODB-CR과 SCRAM-SHA-1 인증 방식을 지원합니다.

- mongouser 및 콘솔에서 생성한 모든 새 사용자의 경우, 내보내기 명령 도구를 사용할 때, 위 예제에 따라 진행하면 됩니다.
- rwuser의 경우, 각 명령에 매개변수 --authenticationMechanism=MONGODB-CR을 추가해야 합니다.

Mongodump 예제 설명:

```
 mongodump --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```

### Mongorestore(전체 데이터베이스) 또는 Mongoimport(단일 클러스터)를 사용하여 어떻게 데이터를 로컬 서버에서 MongoDB로 가져올 수 있나요?

CVM에서 MongoDB가 제공하는 [shell 클라이언트](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/)로 TencentDB for MongoDB와 연결한 후, 데이터를 가져옵니다. **최신 버전의 MongoDB 클라이언트 슈트를 사용해야 합니다.**
MongoDB는 공식으로 두 가지 데이터 가져오기 도구 패키지를 제공합니다. 전체 데이터베이스를 내보낼 때, 일반적으로 mongorestore를 사용하고 데이터 형식은 BSON이며 대규모 mongorestore 시 효율이 비교적으로 높습니다. 단일 클러스터를 내보낼 때, 일반적으로 mongoimport를 사용하고 데이터 형식은 JSON이며 가독성이 비교적으로 높습니다.    
**1. Mongorestore를 사용하여 전체 데이터베이스를 가져오고 백업하기**
가져오기 명령은 다음과 같습니다.

```
mongorestore --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --dir=/data/dump_testdb
```

![이미지 설명](//bot1024-1253841380.file.myqcloud.com/5982b30189287.png)
**2. mongoimport로 단일 클러스터를 가져오고 백업하기**
가져오기 명령은 다음과 같습니다.

```
mongoimport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection2  --file=/data/export_testdb_testcollection.json
```

**3. Rwuser와 Mongouser가 가져오기 명령을 입력할 때에 대한 매개변수 설명**
[연결 예제](https://cloud.tencent.com/document/product/240/3563) 문서에 설명되어 있습니다. TecentDB for MongoDB는 기본적으로 rwuser와 mongouser 두 개 사용자 이름을 제공하며 각각 MONGODB-CR과 SCRAM-SHA-1 인증 방식을 지원합니다.

- mongouser 및 콘솔에서 생성한 모든 새 사용자의 경우, 가져오기 명령 도구를 사용할 때, 위 예제에 따라 진행하면 됩니다.
- rwuser의 경우, 각 명령에 매개변수 --authenticationMechanism=MONGODB-CR을 추가해야 합니다.

Mongorestore 예제:

```
 mongorestore --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```

### 데이터를 MongoDB 인스턴스에 가져온 후 사용한 공간이 자체 생성한 MongoDB보다 작은 이유는 무엇인가요?

원인은 다음 몇 가지가 있습니다.
- 기존의 데이터베이스에서 추가/삭제/변경 작업을 많이 누적했을 수 있습니다.
- 쓰기 작업 시, MongoDB는 성능을 고려하여 실제 데이터보다 큰 공간을 할당했을 수 있습니다.
- 데이터 삭제 후, 기존 공간이 다시 사용되지 않았을 수 있습니다.
  따라서 온 데이터베이스 공간의 높은 공간율을 초래할 수 있습니다. 한편, 데이터 가져오기는 디스크 조각 모음과 유사한 작업으로 간주될 수 있습니다. 이렇게 하면 가져온 데이터가 더 컴팩트해지고 크기가 작아집니다.

### MongoDB의 Mongodump로 데이터를 내보낼 수 없습니다. 어떻게 해결해야 하나요?
Mongodump 사용의 관련 내용은 [가져오기/내보내기](https://cloud.tencent.com/document/product/240/5321)를 참조하십시오. Mongodump 도구는 3.2.10 이상 버전을 사용하는 것을 권장합니다.

