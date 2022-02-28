
After you connect to the database instance, you can create databases and write data to them.

## Creating a Database
The syntax to create a MongoDB database is as follows: 
```
use DATABASE_NAME
```

Create a database named "myFirstDB" and insert a document to it:
```
> use myFirstDB
switched to db myFirstDB
> db.myFirstDB.insert({"test":"myFirstDB"})
WriteResult({ "nInserted" : 1 })
```

Show the database you created:
```
> show dbs
admin      0.000GB
config     0.000GB
local      0.041GB
myFirstDB  0.000GB
```

## Creating a Collection
In MongoDB, you can use the `createCollection()` method to create a collection.
Syntax:
```
db.createCollection(name, options)
```
Parameter description:
- name: the name of the collection to create
- options: (optional) options of memory size and index

| options Field | Type |      | Description                                                         |
| ----------- | ---- | ---- | ------------------------------------------------------------ |
| capped      | BOOL | No   | Whether to set a maximum size in bytes for the collection. Valid values: `true` (the `size` field must be specified), `false` (default) |
| autoIndexId | BOOL | No   | Whether to automatically create an index on the `\_id` field. Valid values: `true`, `false` (default) |
| size        | number | No   | The maximum size in bytes of the collection                                       |
| max         | number | No   | The maximum number of documents in the collection                                 |

Create a collection named "FirstCol" in the myFirstDB database:
```
> use myFirstDB
switched to db myFirstDB
> db.createCollection("FirstCol")
{
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1634821900, 2),
                "signature" : {
                        "hash" : BinData(0,"WFu7yj8wjeUBWG3b+oT84Q8wIw8="),
                        "keyId" : NumberLong("6990600483068968961")
                }
        },
        "operationTime" : Timestamp(1634821900, 2)
}
```

Show the collection you created:
```
> show collections
FirstCol
```

The following sample shows that the FirstCol collection you created can have up to 10,000 documents whose total size cannot exceed 6,142,800 bytes.
```
> db.createCollection("FirstCol", { capped : true, autoIndexId : true, size : 6142800, max : 10000 } )
{
        "note" : "the autoIndexId option is deprecated and will be removed in a future release",
        "ok" : 1,
        "$clusterTime" : {
                "clusterTime" : Timestamp(1634821879, 1),
                "signature" : {
                        "hash" : BinData(0,"EuIbp2fu9Yh38HOBHLgYqljdKaE="),
                        "keyId" : NumberLong("6990600483068968961")
                }
        },
        "operationTime" : Timestamp(1634821879, 1)
}
```

## Inserting a Document
- In MongoDB, you can use the `insert()` or `save()` method to insert a document to a collection, as shown below:
```
> db.FirstCol.insert({name:"Jane Smith",sex:"Female",age:25,status:"A"})
WriteResult({ "nInserted" : 1 })
```
Show the document inserted to the collection:
```
> db.FirstCol.find()
{ "_id" : ObjectId("61716957a6fe1ef4d7eae979"), "name" : "Jane Smith", "sex" : "Female", "age" : 25, "status" : "A" }
```
  
- You can use `db.collection.insertMany()` to insert one or more documents to a collection, as shown below:
```
db.collection.insertMany(
   [ <document 1> , <document 2>, ... ]
   )
```
Sample:
```
> db.FirstCol.insertMany([{name:"Mary Smith",sex:"Female",age:25,status:"A"},{name:"John White",sex:"Male",age:26,status:"B"},{name:"Michael White",sex:"Male",age:26,status:"A",groups:["news","sports"]}])
{
       
        "acknowledged" : true,
        "insertedIds" : [
                ObjectId("617282a3a4bb72d733b5c6d7"),
                ObjectId("617282a3a4bb72d733b5c6d8"),
                ObjectId("617282a3a4bb72d733b5c6d9")
        ]
}
```

## Updating a Database
In MongoDB, you can use `update()` to update documents in a collection.

Update the data in the FirstCol collection where `name` is `Mary Smith`:
```
> db.FirstCol.update({name:"Mary Smith",sex:"Female",age:25,status:"A"},{$set:{'age':28}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```

Show the result:
```
> db.FirstCol.find().pretty()
{
        "_id" : ObjectId("618904b6258a6c38daf13abd"),
        "name" : "Mary Smith",
        "sex" : "Female",
        "age" : 28,
        "status" : "A"
}
{
        "_id" : ObjectId("618904b6258a6c38daf13abe"),
        "name" : "John White",
        "sex" : "Male",
        "age" : 26,
        "status" : "B"
}
{
        "_id" : ObjectId("618904b6258a6c38daf13abf"),
        "name" : "Michael White",
        "sex" : "Male",
        "age" : 26,
        "status" : "A",
        "groups" : [
                "news",
                "sports"
        ]
}
```

## Deleting a Database
In MongoDB, you can use `remove()` to delete documents from a collection, as shown below:
```
> db.FirstCol.remove({name:"Mary Smith",sex:"Female",age:28,status:"A"})
WriteResult({ "nRemoved" : 1 })
```

Show the result:
```
> db.FirstCol.find().pretty()
{
        "_id" : ObjectId("618904b6258a6c38daf13abe"),
        "name" : "John White",
        "sex" : "Male",
        "age" : 26,
        "status" : "B"
}
{
        "_id" : ObjectId("618904b6258a6c38daf13abf"),
        "name" : "Michael White",
        "sex" : "Male",
        "age" : 26,
        "status" : "A",
        "groups" : [
                "news",
                "sports"
        ]
}
```

## References
For more information, see [MongoDB official documentation](https://docs.mongodb.com/manual/reference/connection-string/).
