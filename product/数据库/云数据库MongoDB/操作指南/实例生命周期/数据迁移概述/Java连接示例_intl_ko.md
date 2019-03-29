## 관련 설명
TecentDB for MongoDB는 기본적으로 "rwuser"와 "mongouser" 두 개 사용자 이름을 제공하며 각각 "MONGODB-CR"과 "SCRAM-SHA-1" 인증 방식을 지원합니다. 이 두 가지 인증 방식의 경우 URI를 연결 시 서로 다른 방식으로 처리해야 합니다. 자세한 내용은 [연결 예제](https://cloud.tencent.com/doc/product/240/3563) 문서를 참조하십시오.

Java MongoDB 드라이브 문서
http://mongodb.github.io/mongo-java-driver/3.2/driver/getting-started/
Java Jar 패키지 다운로드
https://oss.sonatype.org/content/repositories/releases/org/mongodb/mongo-java-driver/
3.2 이상 버전을 다운로드하십시오.

## 빠른 시작
### 원본 Java 예제 코드
```
package mongodbdemo;

import org.bson.*;
import com.mongodb.*;
import com.mongodb.client.*;

public class MongodbDemo {

    public static void main(String[] args) {
        String mongoUri = "mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin";
        MongoClientURI connStr = new MongoClientURI(mongoUri);
        MongoClient mongoClient = new MongoClient(connStr);
        try {
            // 이름이 someonedb인 데이터베이스 사용
            MongoDatabase database = mongoClient.getDatabase("someonedb");
            // 세트/테이블 someonetable 핸들 가져오기
            MongoCollection<Document> collection = database.getCollection("someonetable");

            // 데이터 쓰기 준비
            Document doc = new Document();
            doc.append("key", "value");
            doc.append("username", "jack");
            doc.append("age", 31);

            // 데이터 쓰기
            collection.insertOne(doc);
            System.out.println("insert document: " + doc);

            // 데이터 읽기
            BsonDocument filter = new BsonDocument();
            filter.append("username", new BsonString("username"));
            MongoCursor<Document> cursor = collection.find(filter).iterator();
            while (cursor.hasNext()) {
                System.out.println("find document: " + cursor.next());
            }
        } finally {
            //연결 종료
            mongoClient.close();
        }
    }
}
```

출력

```
INFO: Opened connection [connectionId{localValue:2, serverValue:67621}] to 10.66.122.28:27017
insert document: Document{{key=value, username=jack, age=31, _id=56a6ebb565b33b771f9826dd}}
find document: Document{{_id=56a3189565b33b2e7ca150ba, key=value, username=jack, age=31}}
Jan 26, 2016 11:44:53 AM com.mongodb.diagnostics.logging.JULLogger log
INFO: Closed connection [connectionId{localValue:2, serverValue:67621}] to 10.66.122.28:27017 because the pool has been closed.
```

### Spring Data MongoDB 구성 예제
본 예제는 [인증 데이터베이스 admin](https://cloud.tencent.com/document/product/240/3563#.E8.AE.A4.E8.AF.81.E6.95.B0.E6.8D.AE.E5.BA.93)의 구성 방법을 보여줍니다. 사용하는 Spring과 Spring Data MongoDB의 버전을 참조하여 구성하십시오.
```
<bean id="mongoTemplate" class="org.springframework.data.mongodb.core.MongoTemplate">
    <constructor-arg name="mongoDbFactory" ref="mongoDbFactory" />
</bean>
<bean id="mongoDbFactory" class="org.springframework.data.mongodb.core.SimpleMongoDbFactory">
    <constructor-arg name="mongo" ref="mongo" />
    <constructor-arg name="databaseName" value="귀하의 대상 데이터베이스" />
    <constructor-arg name="credentials" ref="userCredentials" />
    <constructor-arg name="authenticationDatabaseName" value="admin" />
</bean>
<bean id="userCredentials" class="org.springframework.data.authentication.UserCredentials">
    <constructor-arg name="username" value="사용자 이름" />
    <constructor-arg name="password" value="비밀번호" />
</bean>
```
