### Delivering configuration histories on resource timelines

Click **Settings** > **Delivery service**. On the displayed page, toggle on to **enable** and create a delivery service to deliver the scheduled configuration histories on the resource timelines to the specified COS bucket, so that you can analyze resource configuration information more precisely and retain it for a longer time.
![](https://qcloudimg.tencent-cloud.cn/raw/85f4b40754ca9e992eacc3fa63d60afb.png)
![](https://qcloudimg.tencent-cloud.cn/raw/b3347143ed82a4bc21b779b49bb1b0bc.png)
After the delivery service is activated, Config will deliver the resource configuration change history to the specified COS bucket at 00:30 AM every day when a timeline is updated. If you **deactivate** the delivery service, updates to the timeline will not be stored in the bucket.
![](https://qcloudimg.tencent-cloud.cn/raw/753fdf6ae5d0bb7dc596036ebda49e7f.png)
![](https://qcloudimg.tencent-cloud.cn/raw/570f9d8479e7224f7400cb0a2f50a23c.png)
Due to a large data volume, it takes about 15 minutes to pull resource configuration snapshots and deliver them to the COS bucket, after which the data will be updated in the bucket.

