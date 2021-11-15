## Notes
TencentDB for MongoDB provides two usernames `rwuser` and `mongouser` by default to support the MONGODB-CR and SCRAM-SHA-1 authentication methods, respectively. The connecting URIs for the two authentication methods are formed differently. For more information, please see [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092).

[Documentation of MongoDB Node.js Driver](https://docs.mongodb.com/ecosystem/drivers/node/)

## Quick Start
### Native Node.js sample code
Install the driver package through shell:
```
npm install mongodb --save
(If the installation failed, you can try another source, such as `npm config set registry http://registry.cnpmjs.org`)
npm init
```
Program code:
```
'use strict';

var mongoClient = require('mongodb').MongoClient,
    assert = require('assert');

// Form the URI
var url = 'mongodb://mongouser:thepasswordA1@10.66.161.177:27017/admin';

mongoClient.connect(url, function(err, db) {
	assert.equal(null, err);
	var db = db.db('testdb'); // Select a database
	var col = db.collection('demoCol'); // Select a collection (table)
   // Insert data
    col.insertOne(
        {
            a: 1,
            something: "yy"
        },
        // Optional parameters
        //{
        //    w: 'majority' // Enable the "Majority" mode to ensure that data are written to the Secondary nodes
        //},
        function(err, r) {
            console.info("err:", err);
            assert.equal(null, err);
            // Assertion is written successfully
            assert.equal(1, r.insertedCount);
            // Query data
            col.find().toArray(function(err, docs) {
                assert.equal(null, err);
                console.info("docs:", docs);
                db.close();
            });
        }
    );
});
```

Output:

```
[root@VM_2_167_centos node]# node index.js
docs: [ { _id: 567a1bf26773935b3ff0b42a, a: 1, something: 'yy' } ]
```

## Sample Code for Connecting to Node.js mongoose

```
var dbUri = "mongodb://" + user + ":" + password + "@" + host + ":" + port + "/" + dbName;
var opts = {
    auth: {
        authMechanism: 'MONGODB-CR', // This parameter is not required if SCRAM-SHA-1 authentication is used
        authSource: 'admin'
    }
};
var connection = mongoose.createConnection(dbUri, opts);
```
