### How do I view instance details in MongoDB?
On the instance list page, click the ID of an instance to go to its details page.

### How do I access a MongoDB instance?
TencentDB for MongoDB can be connected using a variety of languages, such as Shell, PHP, Node.js, Java, and Python.
For more information, please see [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092).

### What is the range of the specification for MongoDB instances? Can I increase the connection number?
Please see [Use Limits](https://intl.cloud.tencent.com/document/product/240/31183). The number of connections depends on instance specifications. You can increase the number by upgrading instance specifications.

### Is the time required for upgrading MongoDB instance specifications related to the used capacity of the instance?
The time required for upgrading an instance depends on its used capacity. Master-slave switch will occur once during the upgrade, and the instance will be temporarily inaccessible for about 10 seconds.

### How do I create an instance in MongoDB?
On the [purchase page](https://buy.cloud.tencent.com/mongodb), you can specify the specification and usage period, and click **Buy Now** to create an instance.

### How do I find an instance with assigned projects in MongoDB?
To find an instance with assigned projects, call the [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/240/34702) API to query the list of set instances.
 
### What is the number of connections in MongoDB? Can I increase the number?
Please see [Use Limits](https://intl.cloud.tencent.com/document/product/240/31183). The number of connections depends on instance specifications. You can increase the number by upgrading instance specifications.

### How do I get the slow log of a MongoDB instance?
Log in to the [console](https://console.cloud.tencent.com/mongodb/instance), and choose **Manage Database** > **Slow Query Management** on the instance management page to query slow logs.

### How do I query the instance specifications supported by MongoDB?
Call the [DescribeSpecInfo](https://intl.cloud.tencent.com/document/product/240/34701) API to query the supported instance specifications.

