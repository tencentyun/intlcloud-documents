
## Notes
TencentDB for MongoDB provides two usernames `rwuser` and `mongouser` by default to support the MONGODB-CR and SCRAM-SHA-1 authentication methods, respectively. The connecting URIs for the two authentication methods are formed differently. For more information, see [Instance Connection](https://intl.cloud.tencent.com/document/product/240/7092).

[Documentation of the MongoDB Java Driver](http://mongodb.github.io/mongo-java-driver/3.2/driver/getting-started/)

Download the [JAR package](https://oss.sonatype.org/content/repositories/releases/org/mongodb/mongo-java-driver/) and select a version above 3.2.

## Getting Started
### Native Java sample code
```
package mongodbdemo;

import org.bson.*;
import com.mongodb.*;
import com.mongodb.client.*;

public class MongodbDemo {

    public static void main(String[] args) {
        String mongoUri = "mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin"; //  For multi-IP instance URIs, refer to the following format: mongodb://mongouser:******@172.xx.xx.124:27017,172.xx.xx.27:27017,172.xx.xx.136:27017/test?authSource=admin&replicaSet=cmgo-fsstfgob_0
        MongoClientURI connStr = new MongoClientURI(mongoUri);
        MongoClient mongoClient = new MongoClient(connStr);
        try {
            // Use the database `someonedb`
            MongoDatabase database = mongoClient.getDatabase("someonedb");
            // Get the handle of the collection/table `someonetable`
            MongoCollection<Document> collection = database.getCollection("someonetable");

            // Prepare to write data
            Document doc = new Document();
            doc.append("key", "value");
            doc.append("username", "jack");
            doc.append("age", 31);

            // Write data
            collection.insertOne(doc);
            System.out.println("insert document: " + doc);

            // Read data
            BsonDocument filter = new BsonDocument();
            filter.append("username", new BsonString("jack"));
            MongoCursor<Document> cursor = collection.find(filter).iterator();
            while (cursor.hasNext()) {
                System.out.println("find document: " + cursor.next());
            }
        } finally {
            // Close the connection
            mongoClient.close();
        }
    }
}
```

Output:
```
INFO: Opened connection [connectionId{localValue:2, serverValue:67621}] to 10.66.122.28:27017
insert document: Document{{key=value, username=jack, age=31, _id=56a6ebb565b33b771f9826dd}}
find document: Document{{_id=56a3189565b33b2e7ca150ba, key=value, username=jack, age=31}}
Jan 26, 2016 11:44:53 AM com.mongodb.diagnostics.logging.JULLogger log
INFO: Closed connection [connectionId{localValue:2, serverValue:67621}] to 10.66.122.28:27017 because the pool has been closed.
```

### Configuration sample for Spring Data MongoDB
This sample demonstrates how to configure the [authentication database admin](https://intl.cloud.tencent.com/document/product/240/7092#uri-.E6.96.B9.E5.BC.8F), which depends on the versions of Spring and Spring Data MongoDB you use.
```
<bean id="mongoTemplate" class="org.springframework.data.mongodb.core.MongoTemplate">
    <constructor-arg name="mongoDbFactory" ref="mongoDbFactory" />
</bean>
<bean id="mongoDbFactory" class="org.springframework.data.mongodb.core.SimpleMongoDbFactory">
    <constructor-arg name="mongo" ref="mongo" />
    <constructor-arg name="databaseName" value="your target database" />
    <constructor-arg name="credentials" ref="userCredentials" />
    <constructor-arg name="authenticationDatabaseName" value="admin" />
</bean>
<bean id="userCredentials" class="org.springframework.data.authentication.UserCredentials">
    <constructor-arg name="username" value="username" />
    <constructor-arg name="password" value="password" />
</bean>
```
