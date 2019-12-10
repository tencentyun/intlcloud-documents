This document describes how to store LVB screenshots or porn detection data in a COS bucket. You need to create a COS bucket, authorize LVB to store data in it, and then configure LVB screencapturing and porn detection settings in the LVB Console. After doing so, LVB screenshots and porn detection data can be stored in the bucket. (This feature is available in the new version of console.)
### Creating a COS bucket
1. Log in to the COS Console and select [Bucket List](https://console.cloud.tencent.com/cos5/bucket).
2. Click **Create Bucket**, enter the corresponding information on the pop-up page, and click **OK**.
 ![](https://main.qcloudimg.com/raw/31b306873ac7f72aa96d86b0ba91a948.png)
>!
> - The bucket name is examplebucket (excluding -1271775094).  
> - The above information can be configured based on the actual needs of your business.
3. You can enable CDN acceleration for the COS bucket according to your business needs. Click the name of the created bucket or **Configuration Management**, select "Domain Name Management", click **Edit** to set the acceleration, and click **Save**.

### Authorizing LVB to Store Screenshots
1. Grant the root account (ID: 3508645126) permission to store LVB screenshots.
	(1) Add a user for the bucket in **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)** > **Permission Management** > **Bucket Access Permission**, select root account as user type , **and enter the root account ID `3508645126`**
	>! **You need to enter the root account ID `3508645126` in the account ID field for authorization. (This root account is the LVB service, so it is sufficient to directly enter `3508645126`).**
	![](https://main.qcloudimg.com/raw/2417cd97ea3ae2f3ebf57ff1f8834ba1.png)
	(2) For more information on the bucket access permission setting API, please see [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737).
2. Get the information of the authorized COS bucket.
	(1) You can view all the information of COS in the **Basic Configuration** section of the bucket. The access domain name (i.e., origin server domain name) contains bucket name, cos appid, and bucket region.
	![](https://main.qcloudimg.com/raw/f442ced48355a2c94b858cebd8928cb5.png)
	 - bucket name: buckettest123
	 - cos appid: 1259200900
	 - bucket region: ap-chengdu
	(2) After submitting the above 3 fields, and the system will store LVB screenshots in the authorized COS bucket.
