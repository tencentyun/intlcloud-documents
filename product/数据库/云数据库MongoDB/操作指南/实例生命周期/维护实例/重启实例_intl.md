## Description ##
Due to the architecture of TencentDB for MongoDB, you need to go through Mongos and Mongod processes when you restart your instance. Restarting an instance might cause instant disconnection, and rollback may occur if data is written into Mongod when Mongod is being restarted. So data may be lost as a result. So, make sure you are fully prepared for service unavailability before restarting the instance. Starting Mongod process is now being whitelisted, and you can submit a ticket to us if needed. Please note that restarting TencentDB for MongoDB instances is a highly risky, so operate carefully.

## Steps ##
Log in to Tencent Cloud's official website, and go to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb). Specify the instance on the list of the replica set or the sharding instance and click **Restart**, as shown below:
![](https://main.qcloudimg.com/raw/f9970b086c8d84dee900e72e320f2fbf.png)

Alternatively, click **Operation** -> **More** -> **Restart** for each instance, as shown below:
![](https://main.qcloudimg.com/raw/712e6bc5b00ede03cccf0855affe0d22.png)

After you click the **Restart**, use a pop-up box to specify the components to restart, and click **OK**, as shown below:
![](https://main.qcloudimg.com/raw/b6331e32eb64212ceb7fc4bed98ddff7.png)

