## Overview
This step shows how to bind the custom domain name to the bucket. You can access the files in the bucket via the custom domain name.

> A maximum of 20 custom domain names can be added on the COS Console. If you need to apply for a higher quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

### Procedure

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5). Click **Bucket List** on the left sidebar to open the Bucket List page.
2. Click the bucket for which you need to set a domain name to go the COS configuration page, as shown below:
![Custom Origin Domain Entry](https://main.qcloudimg.com/raw/41251dd19a92b7492106b7225f0871b1.png)
3. Click **Domain Management** at the top, and click **Add Domain** in the column **Custom Origin Domain**. If your custom domain name has gone through the [filing](https://cloud.tencent.com/product/ba) procedures with MIIT, and resolution has been added on the Domain Name Service, you can enter the custom domain name in the **Domain Name** input box, and click **Save**.
![](https://main.qcloudimg.com/raw/d0c76b2e57cd6a1b6d395bd7d4d21216.png)

### Console Version Differences	
The two console versions differ in terms of bucket domain names. For example, the bucket region abbreviation for Guangzhou is `ap-guangzhou` in the new console version, but `cosgz` in the old one. For more information, see [Regions & Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).	

 Due to domain name differences, you need to configure CNAME while using the custom origin domain. We **recommend** that you use the new-version bucket domain name as CNAME, which allows more operations than the old one.	

 You can modify your CNAME information at the DNS vendor:	
- Configure on the [Tencent Cloud Domain Name Resolution Console](https://console.cloud.tencent.com/domain) if your DNS vendor is Tencent Cloud.	
- Configure on the OSS Domain Console if your DNS vendor is Alibaba Cloud.	
- Configure on the AWS Route53 Console if your DNS vendor is Amazon Cloud.	

>The new and old console versions vary in not only the domain names, but also in the APIs they call. We **recommend** that you use the new version console, as well as the new-version APIs, tools, SDKs, which offers you more stable features. The APIs called to manipulate objects or buckets on the new-version COS Console are XML APIs, while those called on the old version are JSON APIs. For the API differences between the two versions, see [API and SDK](https://intl.cloud.tencent.com/document/product/436/10687).