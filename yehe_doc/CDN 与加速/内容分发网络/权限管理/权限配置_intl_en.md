CDN allows you to configure query and management policies for domain names at a fine granularity. You can grant permissions at the domain name level through custom policy statements.	

>?As the support for CDN API 2.0 has been ended, please choose **Create by Policy Generator** or **Authorize by Tag** to create new policies. The **Create by Product Feature or Project Permission** is not recommended. 

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) and click **Policies** to enter the policy management page. Click **Create Custom Policy**:
![img](https://main.qcloudimg.com/raw/b986334f0d3acde5eb9526fe01d669bb.png)

2. Select **Create by Policy Generator**:
![img](https://main.qcloudimg.com/raw/55a2e3b5b0011b2a8e520df6fc37ff57.png)

3. Select **CDN** in the service drop-down list and select the actions to be authorized. If you want to grant full read/write permission, check **All actions**. To map specific actions with console features, please see [Console Permissions](https://intl.cloud.tencent.com/document/product/228/35229).
![img](https://main.qcloudimg.com/raw/43b88d53d2beb2b2c167a4a732dc6ded.png)

4. Enter the domain name to be authorized as the resource:
	- For all domain names: check **All resources** and click **Confirm**.
	![img](https://main.qcloudimg.com/raw/9ddd4b97828faeadd0063d0ede3283a0.png)
	- For specific domain names: check **Specific Resources** and click **Add a 6-segment resource description**.
	![img](https://main.qcloudimg.com/raw/05dd24c7e96e3ae6cd6aa2b9ee64641d.png)
	In the pop-up window on the right, enter a domain name and click **Confirm**. You can repeat the operation to add multiple domain names.
	![img](https://main.qcloudimg.com/raw/68715dd7708d3b79aac0d64ae713ae85.png)

5. After the configuration is completed, click **Confirm** and **Next**. Associate the created policy with existing users or user groups, and finally click **Done** to grant them the permissions.
![img](https://main.qcloudimg.com/raw/1232f5b90fa612ee32b560c83dd36c08.png)
