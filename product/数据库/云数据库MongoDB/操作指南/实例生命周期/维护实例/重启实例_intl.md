## Description ##
Due to the architecture of TencentDB for MongoDB, when you restart your instance, you need to go through Mongos and Mongod processes. Because restarting an instance might cause instant disconnection, even rollback when data is written into Mongod,  resulting in data loss. Therefore, please make sure you fully prepare for the service unavailability before you restart the instance. Starting Mongod processes currently are whitelisting, contact us if needed. Please note that restarting TencentDB for MongoDB instances is a high-risk operation, so proceed with caution.

## Steps ##
Log in to Tencent Cloud's official website, and go to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb). Specify the instance on the list of the replica set or the sharding instance and click **Restart**, as shown below:
![](https://main.qcloudimg.com/raw/f9970b086c8d84dee900e72e320f2fbf.png)

Alternatively, click **Operation** -> **More** -> **Restart** for each instance, as shown below:
![](https://main.qcloudimg.com/raw/712e6bc5b00ede03cccf0855affe0d22.png)

After you click the **Restart**, use a pop-up box to specify the components to restart, and click **OK**, as shown below:
![](https://main.qcloudimg.com/raw/b6331e32eb64212ceb7fc4bed98ddff7.png)

