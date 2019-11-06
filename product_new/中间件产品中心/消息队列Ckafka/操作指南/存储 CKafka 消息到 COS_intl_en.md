## Operation Scenarios
CKafka allows you to store messages to COS and download them for analysis.

## Prerequisites
This feature is currently under beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=335&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97CMQ/CKAFKA/IoT%20MQ&step=1) for application.

## Directions
1. Log in to the [CKafka Console](https://console.cloud.tencent.com/ckafka).
2. On the instance list page, click the target instance ID to enter the **Topic Management** tab.
3. On the Topic Management tab, click **Store messages to COS** in the "Operation" column.
4. Click the "Enable" icon to enable this feature.
![](https://main.qcloudimg.com/raw/04d60a7d3ad31482b97d777d0525c521.png)
 - Time Granularity: You need to select the time interval for aggregating messages based on the number of messages, which ranges from 5 to 60 minutes.
 - Bucket: Select a COS bucket for the specific topic, where a folder named "instance id + topic id" will be automatically created for the request messages. Then, click the bucket address to redirect to the file download page.

If you haven't created a COS bucket yet, create one on [Create Bucket](https://console.cloud.tencent.com/cos/bucket) and then select the corresponding storage location.

## Postconditions
After you enable the **Store messages to COS** feature, CKafka will add a **cosCkafka_QCSRole** role in **CAMt** > **Role** to authorize this feature.
- If you no longer need this feature, go to [CKafka Console](https://console.cloud.tencent.com/ckafka/index?rid=1) > **Instance List** > **Topic Management**, click **Store messages to COS** in the "Actions" column, disable it, and delete its role.
![](https://main.qcloudimg.com/raw/ffc5692c9accc5a6f209c832e125121e.png)

- If you need to use this feature all the time but delete the **cosCkafka_QCSRole** role by mistake, messages cannot be stored to COS properly, and you should create that role again timely.

The specific steps are as follows:
1. Log in to the **[CAM Console](https://console.cloud.tencent.com/cam/overview)**, select **Role** > **Create Role** > **Tencent Cloud Account** on the left sidebar, and enter the account ID 91000000031.
![](https://main.qcloudimg.com/raw/a1d1804eb487adfa7a871d52fb536336.png)
2. Select for the `QcloudCOSAccessForCkafkaRole` policy, select it, and click **Next**.
![](https://main.qcloudimg.com/raw/6f14c065bceb3c21438ecb4a2df70663.png)
3. Enter the role name and description.
Role Name: cosCkafka_QCSRole
Role Description: 	Cross-service access of CKafka to COS
![](https://main.qcloudimg.com/raw/193a3d01b247ba38b5da51fda96a0efb.png)
4. Click **Complete** and the created role will appear in the role list.
![](https://main.qcloudimg.com/raw/d7d1c233b9271d08d999fd7d67366a11.png)
5. In the CKafka Console, check whether the consumer group consumes data normally.
![](https://main.qcloudimg.com/raw/349f6814ebcce445c751d23dba93d291.png)

## Restrictions and Billing
- This feature is suitable for scenarios where a small amount of data is backed up to COS. It cannot be guaranteed that the data will be 100% successfully synced to COS.
- Currently, the granularity for aggregation of COS files can be customized in the range of 5-60 minutes
- Data transfer may experience a delay.
- Currently, you can only store messages to a COS bucket in the same region as the CKafka instance. For the sake of latency, cross-region storage is not supported.
- The default private read/write permission in COS is used as the permission for the objects.
- The transfer-and-storage service will occupy a group ID.
- The filename is the timestamp of the storage operation, and the storage path is `instance id/topic id`.
- The file content is composed by serializing the values in CKafka messages with strings.
- Currently, the storage of CKafka messages to COS is provided **free of charge**. You are eligible to [free tier](https://intl.cloud.tencent.com/document/product/436/6240) of 50 GB storage capacity. If you have higher numbers of messages, clean them up timely.
- The operator who enables "Store messages to COS" must have write permission to the destination COS bucket.
- Accumulated CKafka messages is not stored to COS before enabling the forwarding feature.
- Storing messages to COS will be interrupted after the instance expires and will be automatically resumed after the instance is renewed.
