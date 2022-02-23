StreamLive allows you to output HLS files to COS for archiving, for which you need to create a bucket in COS first and grant StreamLive access to the bucket.

1. Activate the COS service and create a COS bucket.

Before outputting files to COS for archiving, you need to [activate COS](https://console.cloud.tencent.com/cos5). After activating COS, go to the [COS console](https://console.cloud.tencent.com/cos5), choose **Bucket List** on the left sidebar, and click **Create Bucket** to create a COS bucket in your region.

![img](https://main.qcloudimg.com/raw/258a128f8e010886f7bea5b6dac83c72.png)

2. Set the output type to **HLS_ARCHIVE**. Go back to the StreamLive console, and select **HLS_ARCHIVE** for **Output Group Type**.

![img](https://main.qcloudimg.com/raw/5e782e85e27d4f860d9921cc86f1165f.png)

3. Authorize StreamLive to access the COS bucket. As you have not granted StreamLive access to your COS bucket, the COS destination fields are grayed out and cannot be entered. Click **click here** as instructed, and an authorization dialog box will pop up. Click **Authorize Now** to enter the authorization page, and then click **Grant** to complete the authorization.

![img](https://main.qcloudimg.com/raw/5327f143f1fc7482c68225e8abad3c82.png))![img](https://main.qcloudimg.com/raw/3b3a91b1e9053f9ac0b6c9bc2955e12c.png)

After completing the authorization, go back to the StreamLive console and click **Authorization completed**. The COS destination fields are now editable.

![img](https://main.qcloudimg.com/raw/ee8f5a51ec6fb2642e570a9c67f91865.png))![img](https://main.qcloudimg.com/raw/41fc5c9c4a18d04b54f6585241231688.png)

4. Enter the COS URL for archiving based on the COS bucket created, which is in the format of http://.cos..myqcloud.com/path.

5. Complete other channel configuration described in [StreamLive Channel Management](https://intl.cloud.tencent.com/document/product/1048/45214) and save and submit the configuration.




