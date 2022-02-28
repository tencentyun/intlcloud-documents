
After a TencentDB for MongoDB instance is initialized, you can read, write, and query it by using either MongoDB shell or drivers in various programming languages.

## Background
### Through shell
MongoDB shell is an interactive JavaScript command line tool that comes with MongoDB and encapsulates many common commands. After installing MongoDB shell on a CVM instance, you can run shell commands to connect to the MongoDB instance and query, write/read, or update database data.

### Through URI
A Uniform Resource Identifier (URI) uniquely identifies a resource on the Web. MongoDB recommends using URIs to connect to MongoDB databases, which is supported by most drivers.

Typical samples of URI connection are as follows:
```
mongodb://username:password@IP:27017/admin
```
```
mongodb://username:password@IP:27017/somedb?authSource=admin
```
```
mongodb://username:password@IP:27017/somedb?authSource=admin&readPreference=secondaryPreferred
```

URI parameters are described as follows. For more information, see [MongoDB official documentation](https://docs.mongodb.com/manual/reference/connection-string/).

| Parameter | Description | Required |
|---------|---------|---------|
| mongodb:// | A specific string indicating MongoDB protocol | Yes |
| username | Username used to log in to MongoDB | Yes. For more information, see [Default user](#mryh). |
| password | Password used to log in to MongoDB | Yes |
| hostX:portX | MongoDB IP and port | Yes |
| /admin | Database to be authenticated, which is always `admin` for TencentDB for MongoDB | Yes. For more information, see [Authentication database](#rzsjk). |
| authMechanism=MONGODB-CR | Authentication mechanism | Yes. For more information, see [Authentication mechanism](#rzjz). |
| authSource=admin | Database used for authentication, which is always `admin` for TencentDB for MongoDB | Yes. For more information, see [Authentication database](#rzsjk). |
| readPreference=secondaryPreferred | Read a secondary node first | No. For more information, see [Read preference](#dczdzcyxj). |

## Notes
A [CVM](https://intl.cloud.tencent.com/document/product/213/10517) instance can be used to connect to the private network address that is automatically assigned to a TencentDB instance. This access method relies on the high-speed private network of Tencent Cloud and features low delay. Both instances should be under the same account and reside in the same VPC in the same region or reside in the classic network. Public network access is not supported for the time being.

## Connecting to Databases Through Shell
The following describes how to connect to databases through MongoDB shell.

### Prerequisites
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- Create a Linux [CVM](https://intl.cloud.tencent.com/document/product/213/10517) instance in the same VPC and the same region as the TencentDB for MongoDB instance.

### Directions
#### Step 1. Log in to the CVM instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. On the left sidebar, select **Instances**.
3. Select a region at the top of the **Instances** page.
4. In the instance list, locate the CVM instance you created and click **Log In** in the **Operation** column.
5. Enter the user password you set when creating the CVM instance and log in.

#### Step 2. Download and decompress MongoDB shell
1. Go to the MongoDB shell installation directory and run the `mkdir` command to create a folder for easy management.
2. Go to the created folder and run the `wget` command to download MongoDB shell, as shown below:
```
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-XX.XX.XX.tgz
```
>?Please select a MongoDB shell whose version matches both TencentDB for MongoDB and the CVM operating system. For more information, see the [download address](https://www.mongodb.com/try/download/community).
3. Run the `tar` command to decompress the downloaded installer of MongoDB shell, as shown below:
```
tar zxvf mongodb-linux-x86_64-rhel70-XX.XX.XX.tgz
```

#### Step 3. Connect to MongoDB
1. Run the `cd` command to enter the directory of the decompressed MongoDB shell, as shown below:
```
cd mongodb-linux-x86_64-rhel70-XX.XX.XX
```
2. Run the following command to connect to MongoDB.
```
./bin/mongo -umongouser -plxh***** 172.xx.xx.xx:27017/admin 
```
Where, `-u` refers to the username used to connect to the database and `-p` the password. `172.xx.xx.xx` is the IP of the MongoDB instance and `27017` the port, both of which should be replaced by the actual configurations. If the connection is successful, the following message will be displayed:
```
MongoDB shell version v4.2.16
connecting to: mongodb://172.x.x.X:27017/admin?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("aeb18f32-6413-49da-864a-5123b4d2****") }
MongoDB server version: 4.2.11
Welcome to the MongoDB shell.
```
<dx-alert infotype="explain" title="">
- For a replica set instance, you can connect to the address of the primary node, secondary node 1, or secondary node 2.
     Primary node: if you connect to the primary node, you can write to or read from the database.
     Secondary node: if you connect to a secondary node, you can only read from the database.
- For a sharded cluster instance, you can connect to the address of any mongos node.
</dx-alert>

## Connecting to Databases Through URI
The following describes how to use URIs to connect to TencentDB for MongoDB from the SDK client which supports various programing languages.

### Prerequisites
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- Prepare a running environment for the SDK client which supports various programing languages.

### [Connection sample](id:ljsl)
To connect to TencentDB for MongoDB, the driver version 3.2 or above is required. Please use the latest version of the client driver to ensure the best compatibility with the shell kit, Java jar package, PHP expansion, Node.js module, etc. For more information, see [MongoDB Drivers](https://docs.mongodb.com/ecosystem/drivers/).

SDK connection samples in various programing languages supported by TencentDB for MongoDB are listed below. Based on those samples, you can configure URIs to connect to, write to, or read from the database.
- [Shell Connection Sample](https://intl.cloud.tencent.com/document/product/240/3978).
- [PHP Connection Sample](https://intl.cloud.tencent.com/document/product/240/3977)
- [Node.js Connection Sample](https://intl.cloud.tencent.com/document/product/240/3979)
- [Mongoose Connection Sample](https://intl.cloud.tencent.com/document/product/240/3979#node.js-mongoose-.E8.BF.9E.E6.8E.A5.E7.A4.BA.E4.BE.8B)
- [Java Connection Sample](https://intl.cloud.tencent.com/document/product/240/3980)
- [Python Connection Sample](https://intl.cloud.tencent.com/document/product/240/3981)
- [Go Connection Sample](https://intl.cloud.tencent.com/document/product/240/38899)
- [PHP Reconnection Sample](https://intl.cloud.tencent.com/document/product/240/4980)

## Connecting to a MongoDB 4.0 Replica Set Instance Through URI
The connection method for MongoDB replica set instances (v4.0) is different from that of other versions. Three IPs are provided on v4.0 for access, corresponding to three nodes in a replica set. When connecting to the instance in a production environment, you are recommended to configure three IPs in the connection string to make the connection more secure and efficient.

### Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. Select **NoSQL Database** > **MongoDB** > **Replica Set Instance** on the left sidebar.
3. Select the region where your instance resides in the upper-left corner on the displayed page.
4. Click the ID of the target v4.0 instance in the instance list and enter the instance details page.
5. In the **Basic Info** block, click **Copy Connection String** next to **Private IPv4 Address** to get the instance URI in the following format:
```
mongodb://mongouser:******@192.168.xx.xx:27017,192.168.x.xx:27017,192.168.x.xx:27017/admin?authSource=admin&replicaSet=cmgo-******
```
![](https://qcloudimg.tencent-cloud.cn/raw/dede12bbaa607c608886ab323bd0b8b5.png)
6. Use the URI to connect to the replica set instance. For more information, see [Connection sample](#ljsl).

## References
#### [Default user](id:mryh)
TencentDB for MongoDB v3.2 uses both `mongouser`and `rwuser` as the default users, while other versions only use `mongouser` as the default user. On the **Database Management** page in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb), you can view system accounts (i.e., default users) and manage permissions as needed.

- Only **rwuser** is authenticated with MONGODB-CR. Below is a sample URI:
```
mongodb://rwuser:password@10.66.100.186:27017/admin?authMechanism=MONGODB-CR
```
```
mongodb://rwuser:password@10.66.100.186:27017/somedb?authMechanism=MONGODB-CR&authSource=admin
```
- Both **mongouser** and users created in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) are authenticated with SCRAM-SHA-1. Below is a sample URI:
```
mongodb://mongouser:password@10.66.100.186:27017/admin
```
```
mongodb://mongouser:password@10.66.100.186:27017/somedb?authSource=admin
```

#### [Authentication database](id:rzsjk)
TencentDB for MongoDB uses the `admin` database as the authentication database during login authentication, so the port in a URI must be followed by `/admin` to specify it. After authentication, you can switch to a specific business database for reads/writes. Below is a sample URI:
```
mongodb://username:password@IP:27017/admin
```
You can also directly access the target database by specifying the target database for reads/writes and an additional authentication database parameter (`authSource=admin`). Below is a sample URI:
```
mongodb://username:password@IP:27017/somedb?authSource=admin
```
You must use one of the above methods to add `admin` as the authentication database into the URI.

#### [Authentication mechanism](id:rzjz)
TencentDB for MongoDB supports the MONGODB-CR and SCRAM-SHA-1 authentication mechanisms as well as the `rwuser` and `mongouser` default users. You can create other users in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb). Different users adopt different authentication mechanisms.

| Username | Authentication Mechanism | URI Requirement |
|---------|---------|---------|
| rwuser | MONGODB-CR | The parameter `authMechanism=MONGODB-CR` must be added. |
| mongouser and users created in the console | SCRAM-SHA-1 (recommended) | No parameter needs to be added. |

#### [Read preference](id:dczdzcyxj)
TencentDB for MongoDB provides a load balancer IP to access the entire replica set. To read from a secondary node, you need to add the `readPreference` parameter in the URI. Parameter values are described below:

| Value | Description | Default |
|---------|---------|---------|
| primary | Reads the primary node only. | Yes |
| primaryPreferred | Reads the primary node first. If it is not available, a secondary node will be read. | No |
| secondary | Reads a secondary node only. If it is not available, an error will be reported. | No |
| secondaryPreferred | Reads a secondary node first. If it is not available, the primary node will be read. |No |

To read a secondary node first, you can configure the URI as follows:
```
mongodb://username:password@IP:27017/admin?readPreference=secondaryPreferred
```

