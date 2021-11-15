
After you initialize your instance, you can access the database by using MongoDB shell or drivers in various programming languages to perform management operations.

A [CVM](https://intl.cloud.tencent.com/document/product/213/10517) instance can be used to connect to the private IP that is automatically assigned to a TencentDB instance. This access method relies on the high-speed private network of Tencent Cloud and features low delay. Both instances should be under the same account and reside in the same VPC in the same region or reside in the classic network. Public network access is not supported for the time being.
>?CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [CCN](https://intl.cloud.tencent.com/document/product/1003/30049).

## Prerequisites
To connect to a TencentDB for MongoDB instance, a driver on v3.2 or above is required. You are recommended to use the latest version of client driver to ensure optimal compatibility, such as shell kit, Java jar package, PHP expansion, and Node.js module. For more information, please see [MongoDB Drivers](https://docs.mongodb.com/ecosystem/drivers/).

## Connection Methods
### Through shell
The mongo shell is an interactive JavaScript shell that comes with MongoDB where you can use command lines to interact with MongoDB instances. You can use the mongo shell to query and update data as well as perform administrative operations.

The mongo shell is included as part of the MongoDB server installation. You need to download and install MongoDB server and then use the mongo shell to connect to your TencentDB for MongoDB instance. To download the MongoDB server, please visit [here](https://www.mongodb.com/download-center#community). The specific connection steps are as follows:
```
    cd <mongodb installation dir>
	./bin/mongo -umongouser -plxh2081* 172.x.x.56:27017/admin
```
>?In the above example, the `-u` parameter specifies the [username](#mryh), the `-p` parameter specifies the password, and `172.x.x.56` and `27017` specify the IP and port of the MongoDB instance, respectively.

### Through URI
MongoDB can be connected to by passing in parameters or by using URI (supported by most drivers). Connection to MongoDB through URI is officially recommended by MongoDB.
>?The connection method for MongoDB replica set instances (v4.0) is different from that of other editions. Three IPs are provided on v4.0 for access, corresponding to three nodes in a replica set. When connecting your business in a production environment, you are recommended to configure three IPs in the connection string to make the connection more secure and efficient. For more information, please see [Replica Set Instance (v4.0) Connection Description](https://intl.cloud.tencent.com/document/product/240/35062).
>
Below are some typical URIs:
- Sample 1
```
mongodb://username:password@IP:27017/admin
```
- Sample 2
```
mongodb://username:password@IP:27017/somedb?authSource=admin
```
- Sample 3
```
mongodb://username:password@IP:27017/somedb?authSource=admin&readPreference=secondaryPreferred
```

The parameters in the above URIs are described as follows:

| Parameter | Description | Required |
|---------|---------|---------|
| mongodb:// | A specific string indicating the MongoDB protocol | Yes |
| username | Username used to log in to MongoDB instance | Yes. For more information, please see [Default user](#mryh) below |
| password | User password used to log in to MongoDB instance | Yes |
| IP:27017 | IP and port of MongoDB instance | Yes |
| /admin | Database to be authenticated, which is always `admin` for TencentDB for MongoDB | Yes. For more information, please see [Authentication database](#rzsjk) below |
| authMechanism=MONGODB-CR | Authentication mechanism | For more information, please see [Authentication mechanism](#rzjz) below |
| authSource=admin | Database used for authentication, which is always `admin` for TencentDB for MongoDB | Yes. For more information, please see [Authentication database](#rzsjk) below |
| readPreference=secondaryPreferred | You can specify to read a secondary database first | No. For more information, please see [Primary/Secondary priority for read operations](#dczdzcyxj) |

Only some of the parameters for the URI used to connect to MongoDB are listed here. For more information, please see [Connection String URI Format](https://docs.mongodb.com/manual/reference/connection-string/).


<span id="mryh"></span>
#### Default user
TencentDB for MongoDB's default user varies by version. Default users `rwuser` and `mongouser` have been built in the latest instances. Legacy instances only have `rwuser`. We will upgrade the legacy instances and will contact you before the upgrade. You can view user accounts and manage their permissions to meet your actual business needs on the database management page in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).

- **Sample URI for `rwuser` (authenticated with MONGODB-CR)**
Only `rwuser` is authenticated with MONGODB-CR:
```
mongodb://rwuser:password@10.66.100.186:27017/admin?authMechanism=MONGODB-CR
Or
mongodb://rwuser:password@10.66.100.186:27017/somedb?authMechanism=MONGODB-CR&authSource=admin
```

- **Sample URI for `mongouser` (authenticated with SCRAM-SHA-1)**
Both `mongouser` and users created in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) are authenticated with SCRAM-SHA-1:
```
mongodb://mongouser:password@10.66.100.186:27017/admin
Or
mongodb://mongouser:password@10.66.100.186:27017/somedb?authSource=admin
```

<span id="rzsjk"></span>
#### Authentication database
TencentDB for MongoDB uses the `admin` database as the authentication database during login authentication, so the port in a URI must be followed by `/admin` to specify it. After authentication, you can switch to a specific business database for reads/writes. Below is a sample URI:
```
mongodb://username:password@IP:27017/admin
```
You can also directly access the target database by specifying the target database for reads/writes and an additional authentication database parameter (`authSource=admin`). Below is a sample URI:
```
mongodb://username:password@IP:27017/somedb?authSource=admin
```
You must use one of the above methods to add `admin` as the authentication database into the URI.

<span id="rzjz"></span>
#### Authentication mechanism
MongoDB supports multiple authentication mechanisms, and SCRAM-SHA-1 is recommended officially.
TencentDB for MongoDB supports two authentication methods: MONGODB-CR and SCRAM-SHA-1.
TencentDB for MongoDB has two default users (`rwuser` and `mongouser`) and supports creating other users in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb). These users are divided into two categories and subject to different authentication mechanisms as detailed below:

| Username | Authentication Mechanism | Processing in URI |
|---------|---------|---------|
| `rwuser` | MONGODB-CR | The parameter `authMechanism=MONGODB-CR` must be added |
| `mongouser` and other users created in the console | SCRAM-SHA-1 (recommended) | No parameter needs to be added |

<span id="dczdzcyxj"></span>
#### Primary/Secondary priority for read operations
TencentDB for MongoDB provides a load balancing IP to access the entire replica set. If you want to specify to read a secondary database, add the `readPreference` parameter in the URI. Relevant values are described as follows:

| Value | Description | Default |
|---------|---------|---------|
| primary | Reads the primary node only. | Yes |
| primaryPreferred | Reads the primary node first. If it is not available, a secondary node will be read. | No |
| secondary | Reads a secondary node only. If it is not available, an error will be reported. | No |
| secondaryPreferred | Reads a secondary node first. If it is not available, the primary node will be read. |No |

To specify to read a secondary node first, you can configure the URI as follows:
```
mongodb://username:password@IP:27017/admin?readPreference=secondaryPreferred
```

## Connection Samples
### Through shell
- [Shell Connection Sample](https://intl.cloud.tencent.com/document/product/240/3978)

### Through URI
- [PHP Connection Sample](https://intl.cloud.tencent.com/document/product/240/3977)
- [Node.js Connection Sample](https://intl.cloud.tencent.com/document/product/240/3979)
- [Mongoose Connection Sample](https://intl.cloud.tencent.com/document/product/240/3979#node.js-mongoose-.E8.BF.9E.E6.8E.A5.E7.A4.BA.E4.BE.8B)
- [Java Connection Sample](https://intl.cloud.tencent.com/document/product/240/3980)
- [Python Connection Sample](https://intl.cloud.tencent.com/document/product/240/3981)
- [Go Connection Sample](https://intl.cloud.tencent.com/document/product/240/38899)
- [Reconnection mechanism](https://intl.cloud.tencent.com/document/product/240/4980)
