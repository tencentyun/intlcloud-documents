## Use Cases
This operation is applicable to clusters for which you want to activate COS based on your business needs.

## Directions
### Step 1. View COS access key
Get `SecretId` and `SecretKey` in [Key Management](https://console.cloud.tencent.com/cam/capi).
![](https://main.qcloudimg.com/raw/7de96fc8624694cfdd8ef24b450d53c8.png)

### Step 2. Get the file download path in the bucket
In the [COS Console](https://console.cloud.tencent.com/cos5/bucket), create or select a bucket and enter the bucket file management page. To manually activate COS in the EMR Console, you need to provide an authentication address to check whether the `SecretId` and `SecretKey` are correct. Therefore, you should make sure that there is at least one downloadable file under the account corresponding to the entered `SecretId` and `SecretKey`.

For example, if there is a file `t1.txt` in the root directory of the bucket, you can enter its object address as the authentication address. In the bucket file list, click **Details** of the file to enter the file details page, and copy the file object address.
![](https://main.qcloudimg.com/raw/8a308284db105fa01c701ebfdd474454.png)![](https://main.qcloudimg.com/raw/83f7e2e435ddfd10246de4865fc3258c.png)

### Step 3. Set COS in the cluster
1. Enter the [EMR Console](https://console.cloud.tencent.com/emr) and click a cluster ID in **Cluster List** to enter the cluster details page.
![](https://main.qcloudimg.com/raw/c1555c479499b401cf8f55d346fd3297.png)
2. In **Software Info** > **COS Access**, click **Set**.
![](https://main.qcloudimg.com/raw/110d1ee209f59db7079ecbbe8ef9cfa0.png)
3. In the pop-up window, enter the `SecretId` and `SecretKey` and authentication address obtained in the previous steps and click **OK**.
![](https://main.qcloudimg.com/raw/9fa2354b0c282d1f00893d75ebad2bd6.png)

### Step 4. Conduct a test
On the command line of the master node, run the following commands to view bucket files.
```
[root@172 ~]# su hadoop
[hadoop@172 root]$ hadoop fs -ls cosn://{bucket-name}/
Found 8 items
-rw-rw-rw-   1 hadoop hadoop       1366 2019-07-17 18:51 cosn://{bucket-name}/README.txt
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/emr
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/flume
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/hive
-rw-rw-rw-   1 hadoop hadoop   95169691 2019-06-25 20:28 cosn://{bucket-name}/spark-test.jar
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/test
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/test2
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/usr
```
