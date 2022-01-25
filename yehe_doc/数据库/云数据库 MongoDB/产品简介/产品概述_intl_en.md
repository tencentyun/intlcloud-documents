
## Overview
TencentDB for MongoDB is a high-performance distributed file storage database service created by Tencent Cloud based on MongoDB, an open-source non-relational database. It is fully compatible with the MongoDB protocol and has a rich set of features, such as multi-node high-availability architecture, backup and restoration, elastic scaling, disaster recovery, managed OPS, and performance tuning.

>?MongoDB® is a registered trademark of MongoDB, Inc. TencentDB for MongoDB is not authorized by or affiliated with MongoDB, Inc. Tencent's use of MongoDB software is based on open-source licenses.


## Data Structure
MongoDB is a document-oriented NoSQL (non-relational) database. Its data structure consists of fields and values like JSON objects. Below is an example:
```
{
	name:"John Smith",
    sex:"Male",
    age:25,
    status:"A",
    groups:["news","sports"]
}
```

## Storage Structure
MongoDB's storage structure consists of the following three units:
- Document: it is the most basic unit in MongoDB and composed of BSON key-value pairs.
```
{name:"Jane Smith",sex:"Female",age:25,status:"A"}
```
- Collection: a MongoDB collection can contain multiple documents. For example, you can insert documents with different data structures into the same collection.
```
{name:"Jane Smith",sex:"Female",age:25,status:"A"}
{name:"Jane Smith",sex:"Female",age:25,status:"A"}
{name:"Harry Smith",sex:"Male",age:26,status:"A",groups:["news","sports"]}
```
- Database: a MongoDB database can contain multiple collections, and you can create multiple databases.

## Why TencentDB for MongoDB
For more information, see [Benefits](https://intl.cloud.tencent.com/document/product/240/3545) and [Use Cases](https://intl.cloud.tencent.com/document/product/240/7086).

## Understanding TencentDB for MongoDB
You can gradually understand TencentDB for MongoDB's terms, system architectures, use limits, and advanced operations. 

## Activating TencentDB for MongoDB
You can learn more about the billable items of TencentDB for MongoDB in [Billing Overview](https://intl.cloud.tencent.com/document/product/240/3550), select an appropriate billing mode as needed, and log in to the [purchase page](https://buy.intl.cloud.tencent.com/mongodb) with your Tencent Cloud account to activate the service.


