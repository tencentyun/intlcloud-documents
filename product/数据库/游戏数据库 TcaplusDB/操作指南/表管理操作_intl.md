[//]: # (chinagitpath:XXXXX)

## Scenario
This document describes the detailed process of managing Protobuf tables.
## Procedure
Common table management operations in TcaplusDB include batch creation, batch modification, batch deletion, batch scaling and batch rollback.
### Batch Creation
TcaplusDB supports batch creation of tables. Follow the steps below:  
1. Click **Add tables** to enter the table creation page.
![](https://main.qcloudimg.com/raw/dcd146329f21bf57a47bda3e8484f2b9.png)

2. Select the deployment unit. If there is no deployment unit, you can create one. Click **New Deployment Unit** and enter the name as needed.
![](https://main.qcloudimg.com/raw/a176ad01272429d75cebc6ab272233c2.png)


3. Click **Local File** to select local files to upload. If you have uploaded a file, click **Import From History File** to add a file, and then click **Next**.
>The file only supports Proto format and cannot exceed 2 MB.
> 
![](https://main.qcloudimg.com/raw/95a183b83475debbeb0d63b2202c63ab.png)

4. Set the table information. Select the table to be set, set **Storage**, **Reserved Read** and **Reserved Write** as needed, and click **Next**.
![](https://main.qcloudimg.com/raw/43ab6bca9d9fbd1d45c568d157f5bec3.png)

5. Confirm the table information, and then click **Create**.
![](https://main.qcloudimg.com/raw/8e7cc073421c3d28fee0c1f54c37875f.png)

6. The system will return a success message when the table is successfully created. 
![](https://main.qcloudimg.com/raw/edc84d8d88fb754eef6cdfd595b7259c.png)



### Batch modification
TcaplusDB supports batch modification of tables. Follow the steps below:

1. On the **Table Management** page, select the table to be modified, and click **Batch Modification** to enter the modification page.
![](https://main.qcloudimg.com/raw/81989a4df973ce7f360d9598cb84dbe0.png)

2. In the file upload step, add a file by clicking **Local File** or **Import from History File**, and then click **Next**.
![](https://main.qcloudimg.com/raw/015f751d6ce29c117d9a7db997d6de4a.png)
> 1\. The key fields labeled with required cannot be deleted.
>  2\. The names and types of the key fields cannot be changed.
>  3\. The value fields labeled with required cannot be deleted.
>  4\. The names and types of the fields with the same tagid cannot be changed.
>  5\. No new key fields can be added.
>  6\. New value fields should conform to the value name rule.
>  7\. The names of new value fields cannot be the same with those of the existing key/value fields.



3. Confirm the table information, and then click **Complete**.
![](https://main.qcloudimg.com/raw/258ee0155764e05672d7999611a2e9e1.png)

4. The message indicating a successful modification is returned. The modification process is completed.
![](https://main.qcloudimg.com/raw/f696cfa0cebed654e976aba609b87de6.png)

### Batch deletion
1. On the **Table Management** page, select the table to be deleted, and click **Batch Deletion**. The **Delete Table** dialog box pops up.

![](https://main.qcloudimg.com/raw/a3dfc8889feb8a22333be9ca8b666dcb.png)

2. Confirm the table information, and then click **OK**. The deletion process is completed.

![](https://main.qcloudimg.com/raw/2eaf1354fa096c07cc579fbfd8840d00.png)

### Batch scaling
1. On the **Table Management** page, select the table to be scaled, and click **Batch Scaling** to enter the scaling page.
![](https://main.qcloudimg.com/raw/acbf433bfc0d540e3995c1e9e5efc786.png)
2. Set the table information. Select the table to be scaled, set **Capacity**, **Reserved Read** and **Reserved Write** as needed, and click **Next**.
![](https://main.qcloudimg.com/raw/68e83934d95ab7564db765d95df3778e.png)
3. Confirm the table information, and then click **Submit**.
![](https://main.qcloudimg.com/raw/fd0a4619397346fc3b4bebe7deecc3c1.png)
4. If the request is submitted successfully, a message indicating a successful submission is returned. After the table is scheduled, the batch scaling operation is completed.
![](https://main.qcloudimg.com/raw/b46cff256db192ea952877a2f4ddf177.png)

### Batch rollback
1. On the **Table Management** page, select the table to be rolled back, and click **Batch Rollback** to enter the rollback page.
![](https://main.qcloudimg.com/raw/8b527a2bcfe95ddfdd8586b9f7ccbed8.png)
2. On the rollback page, click **Local File** to upload the key file (only txt file is supported), then select a time point in the past 15 days for rollback, and click **Batch Rollback**. The rollback operation is completed.
![](https://main.qcloudimg.com/raw/1c262280d6047ff5b1a3fe2c71d32d57.png)

### Table monitoring
1. On the **Table Management** page, click the name of the table to be monitored to display its details.
![](https://main.qcloudimg.com/raw/ac10899d4015f14dc1f9832dd7522eae.png)
2. On the table details page, you can find the table's information such as creation time, modification time, key information and value information. Click **Monitor** to display the table monitoring page.
![](https://main.qcloudimg.com/raw/c343bb0d83ea80a28ed7f637b2e11e23.png)
3. On the table monitoring page, you can monitor the metrics for a specified time range, including **Actual Capacity**, **Actual Read**, **Actual Write**, **Average Write Latency**, **General Error Rate**, **System Error Rate**, and **Error Rate**.
![](https://main.qcloudimg.com/raw/7d609ebf3b72c2c2e5ba38e88c14507a.png)
4. Click the icon of each metric to view larger image.
![](https://main.qcloudimg.com/raw/406f7274dc84d61e11ebe5b6b5307fc2.png)

