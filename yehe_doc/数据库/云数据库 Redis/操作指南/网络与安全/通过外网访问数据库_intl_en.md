## Connecting to Database from Local Windows at Public Network Address
redis-cli is the native command line tool offered by Redis. You can install it on your local device and use it to connect to TencentDB for Redis at a public network address for data management. 

**Connect via redis-cli**

1. [Download redis-cli](https://github.com/microsoftarchive/redis/releases) and decompress the package to the installation directory, such as `D:\Temp\Redis-x64-3.2.100`.
2. On the local device, press **Windows + R** to open the **Run** window, enter **cmd**, and click **OK** to open Windows Command Prompt.
3. Run the following command to enter the installation directory of redis-cli.
```
cd /d <path> 
```
Here, `path` is the installation directory of redis-cli. For example, run `cd /d D:\Temp\Redis-x64-3.2.100`.
4. Run the following command to access the database:
```
redis-cli -h <hostname> -p <port> -a <password>
```
Here, `hostname` is the [public network address](https://intl.cloud.tencent.com/document/product/239/43452) of the database instance, `port` is the port of the public network address, and `password` is the default password of the instance account. If you use a [custom account](https://intl.cloud.tencent.com/document/product/239/34590) for connection, use `account name@password` as the password parameter for authentication.
An execution example is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/fff9e2358332579cd84411647e13b6c2.png)

**Connect via Redis client**
Download the Redis client for Windows, configure the following parameters, and click **Test Connection** to connect to the database instance.

| Parameter | Description |
| -------- | ------------------------------------------------------------ |
| **Name** | Database instance connection name.                                   |
| **Address** | Public network address and port number of the database instance.                       |
| **Auth** | Database instance connection password. If you use the default account, directly enter the instance password. If you use a [custom account](https://intl.cloud.tencent.com/document/product/239/34590), enter `account name@password` for authentication. |

## Connecting to Database from Local Linux at Public Network Address with redis-cli
1. Download the latest stable version of the source code package. 6.2.6 is used as an example here.
```
wget https://download.redis.io/releases/redis-6.2.6.tar.gz
```
2. Run the following command to decompress the source code package:
```
tar -zxvf redis-6.2.6.tar.gz
```
3. Enter the source code directory and compile source code files.
```
cd redis-6.2.6/
```
4. Wait patiently as the compilation time varies by server configuration.
```
make
```
5. Run the following command to connect to the database at the public network address. The following is the default path of redis-cli.
```
src/redis-cli -h <hostname> -p <port> -a <password>
```
Here, `hostname` is the public network address of the database instance, `port` is the port of the public network address, and `password` is the default password of the instance account. If you use a [custom account](https://intl.cloud.tencent.com/document/product/239/34590) for connection, use `account name@password` as the password parameter for authentication.

   
