### How do I view instance details in MongoDB?
On the instance list page, click the name of an instance to go to its details page.

### How do I access a MongoDB instance?
TencentDB for MongoDB can be connected using a variety of languages, such as Shell, PHP, Node.js, Java, and Python.
For more information, see [Connection Example](https://cloud.tencent.com/document/product/240/3563).

### What is the range of the specification for MongoDB instances?  Can I increase the connection number?
See [Limitation](https://cloud.tencent.com/document/product/240/622). The number of connections depends on the instance specification. You can increase the number by upgrading your instance.

#### Is the time required for upgrading a MongoDB instance related to the its used capacity?
The time required for upgrading an instance depends on its used capacity. Switching between primary and secondary nodes will happen once during the upgrade, and the instance will be temporarily inaccessible for about ten seconds.

### How do I create an instance in MongoDB?
On the [purchase page](https://buy.cloud.tencent.com/mongodb), you can specify the specification and usage period, and click **Buy Now** to create an instance.

### How do I find an instance with assigned projects in MongoDB?
To find an instance with assigned projects, see the API [DescribeMongoDBInstances](https://cloud.tencent.com/document/product/240/8312) to query the list of replica set instances.
 
### ### What is the number of connections in MongoDB? Can I upgrade the number? Can I increase the number?
See [Limitation](https://cloud.tencent.com/document/product/240/622). The number of connections depends on the instance specification. You can increase the number by upgrading your instance.

### How do I get the slow operation log of a MongoDB instance?
You can find the detailed information at Slow Operation Log on the official website.

### How do I query the instance specifications supported by MongoDB?
Use the API [DescribeMongoDBProduct](https://cloud.tencent.com/document/product/240/8318) for query.


