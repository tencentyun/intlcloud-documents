We have completely upgraded CDN permission polices. Users can now grant permissions at a domain name level via custom policy statements. This enables users to configure domain name queries and manage permissions at a more granular level. 

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and click **Policies** to enter the policy management page. Click **Create Custom Policy**:
![](https://main.qcloudimg.com/raw/b986334f0d3acde5eb9526fe01d669bb.png)
2. Select **Create by Policy Generator**:
![](https://main.qcloudimg.com/raw/55a2e3b5b0011b2a8e520df6fc37ff57.png)
3. Select **CDN** from the service drop-down list and select the actions to be authorized. If you want to grant full read/write permission, check **All** to select all actions. To map specific actions with console features, please see [Console Permissions](https://cloud.tencent.com/document/product/228/41867).
![](https://main.qcloudimg.com/raw/43b88d53d2beb2b2c167a4a732dc6ded.png)
4. Enter the domain name to be authorized as the resource. You can use `*` to represent all domain names. After the configuration is completed, click **Add Statement** and **Next** to create a policy. Associate the created policy with existing users and user groups to grant them the needed permissions:
![](https://main.qcloudimg.com/raw/54865bb0305e1f4e5ae5b662dab27cc9.png)

