This document provides a simple example that walks you through how to pull a table from data subscription to Redis as well as a simple [Redis Demo](https://main.qcloudimg.com/raw/0a3b560fad57a27440f9445039552d2b/RedisDemo.zip). The following operations are performed on CentOS.

## Configuring Environment
- Java environment configuration 
```
yum install java-1.8.0-openjdk-devel 
```
- [Download the data subscription SDK](https://main.qcloudimg.com/raw/2aa7b213535065def5655712c8494182/binlogsdk-2.7.0-official.jar)
- [Download jedis-2.9.0.jar](https://main.qcloudimg.com/raw/130e0f114f84e6e7eb9cc16d2fecd58c/jedis-2.9.0.zip)

## Getting Key
Log in to the [CAM Console](https://console.cloud.tencent.com/cam/capi) to get a key.

## Selecting Data Subscription
1. Log in to the [DTS Console](https://console.cloud.tencent.com/dtsnew/migrate/page) and select **Data Subscription** on the left sidebar to enter the data subscription page.
2. Select the name of the TencentDB instance to be synced, click "Start", return to the data subscription page, and click the data subscription you created. For detailed directions, please see [How to Get a Data Subscription](https://intl.cloud.tencent.com/document/product/571/8774).
3. Check the corresponding DTS channel, IP, and port and enter them together with the obtained key into the corresponding `RedisDemo.java`.

```
 context.setSecretId("AKIDfdsfdsfsdt1331431sdfds"); Enter the `secretID` obtained from TencentCloud API.
        context.setSecretKey("test111usdfsdfsddsfRkeT"); Enter the `secretKey` obtained from TencentCloud API.
    // Enter the IP and port obtained through data subscription in the DTS service here
        context.setServiceIp("10.66.112.181"); Enter the IP obtained from the data subscription configuration
        context.setServicePort(7507); Enter the port obtained from the data subscription configuration

        // Create a consumer
        //SubscribeClient client=new DefaultSubscribeClient(context,true);
        final DefaultSubscribeClient client = new DefaultSubscribeClient(context);

        final Jedis jedis = new Jedis("127.0.0.1", 6379); Enter your corresponding Redis host and port

        final String targetDatabase = "test"; Enter the name of the database to subscribe to
        final String targetTable = "alantest"; Enter the name of the table to subscribe to. The table has two fields, namely, `id` and `name`, of which `id` is the primary key

        // Create a subscription listener
        ClusterListener listener = new ClusterListener() {
            @Override
            public void notify(List<ClusterMessage> messages) throws Exception {
		//                System.out.println("--------------------:" + messages.size());
                for(ClusterMessage m:messages){
                    DataMessage.Record record = m.getRecord();
                    // Filter out uninteresting subscription messages
	            if(!record.getDbName().equalsIgnoreCase(targetDatabase) || !record.getTablename().equalsIgnoreCase(targetTable)){
                        // Note: Ack must be performed for uninteresting messages too
                        m.ackAsConsumed();
                        continue;
                    }

                    if(record.getOpt() != DataMessage.Record.Type.BEGIN && record.getOpt() != DataMessage.Record.Type.COMMIT){
                        List<DataMessage.Record.Field> fields = record.getFieldList();

                        //INSERT RECORD
                        //String pk = record.getPrimaryKeys();
			
                        if(record.getOpt() == DataMessage.Record.Type.INSERT){
			    
			    String keyid="";
			    String value="";
                            for (DataMessage.Record.Field field : fields) {

                                // Get the `id` value as the primary key first, find the `name` column, and insert the corresponding values of `key` and `name` in Redis
				if(field.getFieldname().equalsIgnoreCase("id")){
                                    keyid=field.getValue();
               continue;
                                }
				if(field.getFieldname().equalsIgnoreCase("name")){
				    value=field.getValue();
                                  
                                }
				jedis.set(keyid, value);
                            }

                        }
  
```


## Compiling and Testing
1. 
```
[root@VM_71_10_centos ~]# javac -classpath binlogsdk-2.6.0-release.jar:jedis-2.9.0.jar -encoding UTF-8 RedisDemo.java 
```
2. Launch the program. If no errors are reported, the program works properly. Check the previously configured local file.
```
 java -XX:-UseGCOverheadLimit -Xms2g -Xmx2g -classpath .:binlogsdk-2.6.0-release.jar:jedis-2.9.0.jar RedisDemo
```
3. Perform `INSERT` and `UPDATE` operations. If you find that the data has been indeed inserted and modified successfully in Redis, you can perform `DELETE` operations to delete the corresponding data from Redis.

```
MySQL [test]> insert into alantest values(1001,'alan1');
Query OK, 1 row affected (0.00 sec)

MySQL [test]> update alantest set name='alan2' where id=1001;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

------------------------
127.0.0.1:6379> get 1001
"alan2"


MySQL [test]> update alantest set name='alan3' where id=1001;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

------------------------
127.0.0.1:6379> get 1001
"alan3"

MySQL [test]> delete from alantest where id=1001;
Query OK, 1 row affected (0.00 sec)

-----------------------

127.0.0.1:6379> get 1001
(nil)

```
