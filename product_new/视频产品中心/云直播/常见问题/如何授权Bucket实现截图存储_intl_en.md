This document describes how to store LVB screenshots or porn detection data in a COS bucket. You need to create a COS bucket, authorize LVB to store data in it, and then configure LVB screencapturing and porn detection settings in the LVB Console. After doing so, LVB screenshots and porn detection data can be stored in the bucket. (This feature is available in the new version of console.)
### Creating a COS bucket
1. Log in to the COS Console and select [Bucket List](https://console.cloud.tencent.com/cos5/bucket).
2. Click **Create Bucket**, enter the corresponding information on the pop-up page, and click **OK**.
 ![](https://main.qcloudimg.com/raw/423beefad19658e0cec8cdd28d6d25e1.png)
>!
> - The bucket name is "examplebucket" (excluding numbers on the right).
> - The above information can be configured based on the actual needs of your business.
3. You can enable CDN acceleration for the COS bucket as needed. Click the name of the bucket or **Configuration Management** to enter its details page. Select **Domain and transmission management** -> **Default CDN Acceleration Domain** on the left, and click **Edit** to enable **Status** and complete the other configurations. Click **Save** to enable the CDN acceleration. For more information about the configurations, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/zh/document/product/436/31505).
![](https://main.qcloudimg.com/raw/097144cf7c6d1df5923d406b0301f93e.png)

### Authorizing LVB to Store Screenshots
1. Grant the root account (ID: 3508645126) permission to store LVB screenshots.

	i. Add a user for the bucket in **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)** > **Permission Management** > **Bucket Access Permission**, select root account as user type , **and enter the root account ID `3508645126`**
	> **You need to enter the root account ID `3508645126` in the account ID field for authorization. (This root account is the LVB service, so it is sufficient to directly enter `3508645126`).**
	![](https://main.qcloudimg.com/raw/37362cc7a0b945e79899e24f84f33dab.png)
	
	ii. For more information on the bucket access permission setting API, please see [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737).
2. Get the information of the authorized COS bucket.
	(1) You can view all the information of COS in the **Basic Configuration** section of the bucket. The access domain name (i.e., origin server domain name) contains bucket name, cos appid, and bucket region.
	![](https://main.qcloudimg.com/raw/b84d288cf37b40ed548ca4a25863742a.png)
	 - bucket name: examplebucket
	 - cos appid: 125****900
	 - bucket region: ap-chengdu
	(2) After submitting the above 3 fields, and the system will store LVB screenshots in the authorized COS bucket.
