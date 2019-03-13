## 関連説明
TencentDB for MongoDBはデフォルトで「rwuser」と「mongouser」の2つのユーザー名を提供し、それぞれ「MONGODB-CR」と「SCRAM-SHA-1」の2つの認証方法をサポートしています。この2つの認証方法について、URI接続は異なる方法で処理する必要があります。詳細は[接続例](https://cloud.tencent.com/doc/product/240/3563)のドキュメントを参照してください。

Java MongoDBドライバーのドキュメント
http://mongodb.github.io/mongo-java-driver/3.2/driver/getting-started/
Java Jarパッケージのダウンロード
https://oss.sonatype.org/content/repositories/releases/org/mongodb/mongo-java-driver/
3.2以上のバージョンをダウンロードしてください

## クイックスタート
### ネイティブJavaサンプルコード
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
            // someonedbという名前のデータベースを使います
            MongoDatabase database = mongoClient.getDatabase("someonedb");
            // コレクション/テーブルsomeonetableのハンドルを取得します
            MongoCollection<Document> collection = database.getCollection("someonetable");

            // データを書き込む準備をします
            Document doc = new Document();
            doc.append("key", "value");
            doc.append("username", "jack");
            doc.append("age", 31);

            // データを書き込みます
            collection.insertOne(doc);
            System.out.println("insert document: " + doc);

            // データを読み取ります
            BsonDocument filter = new BsonDocument();
            filter.append("username", new BsonString("username"));
            MongoCursor<Document> cursor = collection.find(filter).iterator();
            while (cursor.hasNext()) {
                System.out.println("find document: " + cursor.next());
            }
        } finally {
            //接続を閉じます
            mongoClient.close();
        }
    }
}
```

出力

```
INFO: Opened connection [connectionId{localValue:2, serverValue:67621}] to 10.66.122.28:27017
insert document: Document{{key=value, username=jack, age=31, _id=56a6ebb565b33b771f9826dd}}
find document: Document{{_id=56a3189565b33b2e7ca150ba, key=value, username=jack, age=31}}
Jan 26, 2016 11:44:53 AM com.mongodb.diagnostics.logging.JULLogger log
INFO: Closed connection [connectionId{localValue:2, serverValue:67621}] to 10.66.122.28:27017 because the pool has been closed.
```

### Spring Data MongoDB構成例
この例は主に[認証データベースadmin](https://cloud.tencent.com/document/product/240/3563#.E8.AE.A4.E8.AF.81.E6.95.B0.E6.8D.AE.E5.BA.93)の構成方法を反映するためのもので、詳細は使用しているSpringとSpring Data MongoDBのバージョンを参照してください。
```
<bean id="mongoTemplate" class="org.springframework.data.mongodb.core.MongoTemplate">
    <constructor-arg name="mongoDbFactory" ref="mongoDbFactory" />
</bean>
<bean id="mongoDbFactory" class="org.springframework.data.mongodb.core.SimpleMongoDbFactory">
    <constructor-arg name="mongo" ref="mongo" />
    <constructor-arg name="databaseName" value="お客様のターゲットデータベース" />
    <constructor-arg name="credentials" ref="userCredentials" />
    <constructor-arg name="authenticationDatabaseName" value="admin" />
</bean>
<bean id="userCredentials" class="org.springframework.data.authentication.UserCredentials">
    <constructor-arg name="username" value="ユーザー名" />
    <constructor-arg name="password" value="パスワード" />
</bean>
```

