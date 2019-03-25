## Description ##
Restarting Mongos or Mongod depends on the architecture of TencentDB for MongoDB. Restarting an instance will lead to an instant disconnection. Especially when data is written to Mongod as it is restarted, which may cause rollback and thus result in data loss. During the restart, TencentDB for MongoDB instances will be unable to provide normal services, so make sure to prepare in advance to avoid impact on your business. Restarting Mongod is implemented based on the whitelist, contact us if you need it. Restarting is a high-risk operation, so proceed with caution.
## Operation Instructions ##
Log in to Tencent Cloud's official website, and go to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb). Go to the replica set or the sharding instance list, select the instance to be restarted, and click **Restart**, as shown below:
![](https://main.qcloudimg.com/raw/f9970b086c8d84dee900e72e320f2fbf.png)
Alternatively, click **Operation** -> **More** -> **Restart** for each instance, as shown below:
![](https://main.qcloudimg.com/raw/712e6bc5b00ede03cccf0855affe0d22.png)
After the **Restart** button is clicked, a pop-up box displays, as shown below:
![](https://main.qcloudimg.com/raw/b6331e32eb64212ceb7fc4bed98ddff7.png)
Select the components to be restarted, and click **OK**.

