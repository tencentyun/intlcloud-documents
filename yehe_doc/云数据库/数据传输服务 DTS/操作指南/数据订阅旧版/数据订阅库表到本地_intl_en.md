
This document provides a simple example that walks you through how to pull a table from data subscription to a local file system as well as a simple [Local Demo](https://main.qcloudimg.com/raw/f145138da95d16063a3219f030f24625/LocalDemo.zip). The following operations are performed on CentOS.

## Configuring Environment
- Java environment configuration
```
 yum install java-1.8.0-openjdk-devel 
```
- [Download the data subscription SDK](https://main.qcloudimg.com/raw/2aa7b213535065def5655712c8494182/binlogsdk-2.7.0-official.jar)

## Getting Key
Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to get a key.

## Selecting Data Subscription
1. Log in to the [DTS console](https://console.cloud.tencent.com/dtsnew/migrate/page), and select **Data Subscription** on the left to go to the data subscription page.
2. Select the name of the TencentDB instance to be synced, click **Start**, return to the data subscription page, and click the data subscription you created. For detailed directions, please see [How to Get a Data Subscription](https://intl.cloud.tencent.com/document/product/571/8774).
3. Check the corresponding DTS channel, IP, and port and enter them together with the obtained key into the corresponding `LocalDemo.java` file.
```
  // Enter the key obtained from TencentCloud API here
        context.setSecretId("AKIDfdsfdsfsdt1331431sdfds"); Enter the `secretID` obtained from TencentCloud API
        context.setSecretKey("test111usdfsdfsddsfRkeT"); Enter
        the `secretKey` obtained from TencentCloud API
	// Enter the IP and port obtained through data subscription in the DTS service here
        context.setServiceIp("10.66.112.181"); Enter the IP obtained from the data subscription configuration
        context.setServicePort(7507);
        Enter the port obtained from the data subscription configuration
        final DefaultSubscribeClient client = new DefaultSubscribeClient(context);
	// Enter the names of both the database and table to sync and modify the name of the file where they will be stored
        final String targetDatabase = "test"; Enter the name of the database to subscribe to
        final String targetTable = "alantest"; Enter the name of the table to subscribe to

        final String fileName = "test.alan.txt"; Enter the name of the local file for storage
        
          client.addClusterListener(listener);
	// Enter the `dts-channel` configuration information obtained from the data subscription configuration here
	client.askForGUID("dts-channel-e4FQxtYV3It4test"); Enter the DTS channel name obtained from the data subscription
        client.start();
```


## Compiling and Testing
1. 
```
javac -classpath binlogsdk-2.6.0-release.jar -encoding UTF-8 LocalDemo.java
```
2. Launch the program. If no errors are reported, the program works properly. Check the previously configured local file.
```
java -XX:-UseGCOverheadLimit -Xms2g -Xmx2g -classpath .:binlogsdk-2.6.0-release.jar LocalDemo
```
3. Check the previously configured `test.alan.txt` file and you can see that data has been pulled into it.
```
[root@VM_71_10_centos ~]# cat test.alan.txt  
checkpoint:144251@3@357589@317713
record_id:000001000000000004D9110000000000000001
record_encoding:utf8
fields_enc:latin1,utf8
gtid:4f21864b-3bed-11e8-a44c-5cb901896188:1562
source_category:full_recorded
source_type:mysql
table_name:alantest
record_type:INSERT
db:test
timestamp:1523356039
primary:
Field name: id
Field type: 3
Field length: 2
Field value: 26
Field name: name
Field type: 253
Field length: 4
Field value: alan
```

