[//]: # (chinagitpath:XXXXX)

## Scenario
This document describes the detailed process of managing Protobuf tables.
## Procedure
Common table management operations in TcaplusDB include batch creation, batch modification, batch deletion, batch scaling and batch rollback.
### Batch Creation
TcaplusDB supports batch creation of tables. Follow the steps below:  
1. Click **Batch Creation** to enter the table creation page.
![](https://main.qcloudimg.com/raw/0dac0d2464958af8c66072e2ab15da1a.png)

2. Select the deployment unit. If there is no deployment unit, you can create one. Click **New Deployment Unit** and enter the name as needed.
![](https://main.qcloudimg.com/raw/50e7aababcc964d9b644e632e2ea9e86.png)


3. Click **Local File** to select local files to upload. If you have uploaded a file, click **Import from History File** to add a file, and then click **Next**.
> ! The file only supports Proto format and cannot exceed 2 MB.
> 
![](https://main.qcloudimg.com/raw/0b67458d1b199958cf1f61c0f3f9a904.png)

4. Set the table information. Select the table to be set, set **Capacity**, **Reserved Reads** and **Reserved Writes** as needed, and click **Next**.
![](https://main.qcloudimg.com/raw/957a1d777638e0aee662e8d334ccf4f2.png)

5. Confirm the table information, and then click **Create**.
![](https://main.qcloudimg.com/raw/96c3d9b289eae15d436df12da7449377.png)

6. If the table is created, a message indicating a successful creation is returned.
![](https://main.qcloudimg.com/raw/8fe0a4f0ab12fc8672dcd3026b0ab704.png)



### Batch modification
TcaplusDB supports batch modification of tables. Follow the steps below:

1. On the **Table Management** page, select the table to be modified, and click **Batch Modification** to enter the modification page.
![](https://main.qcloudimg.com/raw/dcb4e25ba626c01fdd1a7892c62f20b9.png)

2. In the file upload step, add a file by clicking **Local File** or **Import from History File**, and then click **Next**.
![](https://main.qcloudimg.com/raw/803f79a8dcab9e4874bcf22d28a668e4.png)
> ! 1\. The key fields labeled with required cannot be deleted.
>  2\. The names and types of the key fields cannot be changed.
>  3\. The value fields labeled with required cannot be deleted.
>  4\. The names and types of the fields with the same tagid cannot be changed.
>  5\. No new key fields can be added.
>  6\. New value fields should conform to the value name rule.
>  7\. The names of new value fields cannot be the same with those of the existing key/value fields.

The corresponding relationship between key and value fields is shown below:
![](https://mc.qcloudimg.com/static/img/09325a3f7eba4b5a938656bcdca36fed/key-value.png)



3. Confirm the table information, and then click **Complete**.
![](https://mc.qcloudimg.com/static/img/edfd149ef2865603bba6c00a7d8a57c2/image.png)

4. The message indicating a successful modification is returned. The modification process is completed.
![](https://mc.qcloudimg.com/static/img/6f2022f870f890a6f83ecafad49dc578/image.png)

### Batch deletion
1. On the **Table Management** page, select the table to be deleted, and click **Batch Deletion**. The **Delete Table** dialog box pops up.
![](https://main.qcloudimg.com/raw/5146eaf3d4fe4fee9f4b0848f2848fff.png)
2. Confirm the table information, and then click **OK**. The deletion process is completed.
![](https://mc.qcloudimg.com/static/img/4bf588feede44297c199de7d01555ffd/image.png)

### Batch scaling
1. On the **Table Management** page, select the table to be scaled, and click **Batch Scaling** to enter the scaling page.
![](https://main.qcloudimg.com/raw/401a42e3982a024d3fedcbad854e24e4.png)
2. Set the table information. Select the table to be scaled, set **Capacity**, **Reserved Read** and **Reserved Write** as needed, and click **Next**.
![](https://mc.qcloudimg.com/static/img/b670d09409f7bfb3ec536aa77646d717/image.png)
3. Confirm the table information, and then click **Submit**.
![](https://mc.qcloudimg.com/static/img/cda5868697a7c01a38cdd0d481b891e3/image.png)
4. If the request is submitted successfully, a message indicating a successful submission is returned. After the table is scheduled, the batch scaling operation is completed.
![](https://mc.qcloudimg.com/static/img/f7ae7b37c1436b6d5db0917eb943629c/image.png)

### Batch rollback
1. On the **Table Management** page, select the table to be rolled back, and click **Batch Rollback** to enter the rollback page.
![](https://main.qcloudimg.com/raw/753affc0548e3abd368ef6495015cc41.png)
2. On the rollback page, click **Local File** to upload the key file (only txt file is supported), then select a time point in the past 15 days for rollback, and click **Batch Rollback**. The rollback operation is completed.
![](https://mc.qcloudimg.com/static/img/aa5f4d4e9fae4ff7be1577312c6f76be/image.png)

### Table monitoring
1. On the **Table Management** page, click the name of the table to be monitored to display its details.
![](https://main.qcloudimg.com/raw/ea97219919aa2daeca3d0fb638700f1d.png)
2. On the table details page, you can find the table's information such as creation time, modification time, key information and value information. Click **Monitor** to display the table monitoring page.![](https://main.qcloudimg.com/raw/7819ce138b94888b5f02bcd44fde91fb.png)
3. On the table monitoring page, you can monitor the metrics for a specified time range, including **Actual Capacity**, **Actual Read**, **Actual Write**, **Average Write Latency**, **General Error Rate**, **System Error Rate**, and **Error Rate**.![](https://main.qcloudimg.com/raw/7ca9aab6f230bd86e2046897bafb6501.png)
4. Click the icon of each metric to view larger image.![](https://main.qcloudimg.com/raw/5610f091ffe1ccf663c9be63e3bdabbc.png)

