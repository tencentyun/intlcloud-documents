## Introduction
This document describes how to automatically purge the cached files specified on the CDN using Serverless Cloud Function (SCF) when you upload objects with Tencent Cloud's COS, so that the CDN can automatically obtain updated resources.

>!You need to follow CDN’s API request rate limit when using this feature. For information, see [Purge Cache](https://cloud.tencent.com/document/product/228/6299#url-.E5.88.B7.E6.96.B0).

## Background

When any static content needs to be updated, the old resource in the COS is overwritten by the updated one or is deleted. If the CDN cache validity period you set is very long, some edge servers in the CDN may still cache old resources. If the validity period is too short, the acceleration will be affected. For more information, see [Cache Expiration Configuration](https://cloud.tencent.com/document/product/228/6290).

For this reason, you need to use [Purge Cache](https://cloud.tencent.com/document/product/228/6299) feature in the CDN Console to manually purge the specified URL to delete the invalid cached files or update the resource.

This document describes how to automatically purge cached content in CDN by combining COS with SCF features when a file is updated in COS.

## Preparations

1. Your Tencent Cloud account needs to have the access to such products as COS, CDN, and SCF.
2. Create a bucket and bind a CDN accelerated domain name to the bucket.
3. Ensure the region of the COS bucket supports the SCF feature. Cross-region calls are not supported.
4. Prepare the cloud API keys for calling the API used for purging cached content in CDN and download the [sample code for purging cached content in CDN with SCF](https://main.qcloudimg.com/raw/757b646eb68e9b9a5b2fc4bf0fed2492/scf_about_cdn_refresh.zip).

## Directions

> The following example is based on the same code in Node.js.

### 1. Create SCF function
>!The region​to which your function belongs must be the same as that of the COS bucket.

(1) Log in to the [SCF Console](https://console.cloud.tencent.com/scf/), click **Function Service**, select the region to which the static content belongs, and then create a function, as shown below:
![](https://main.qcloudimg.com/raw/332edc2828575a4c802a9af9cb233b08.png)
2) On the **New Function** page, select **Blank Function**, enter the function name (such as refresh_cdn), and then set the runtime environment (the sample code is written in Node.js, so the runtime environment is set to Nodejs 6.10). After confirming that the configuration is correct, click **Finish**, as shown below:
![](https://main.qcloudimg.com/raw/70e9dbae0471dd8cd50ffa724eb089f4.png)

### 2. Configure function

After the blank function is created, you need to add the function code and set the trigger mode so that the function can work normally.

### 2.1. Configure function code

(1) Download the [sample code for purging cached content in CDN with SCF](https://main.qcloudimg.com/raw/757b646eb68e9b9a5b2fc4bf0fed2492/scf_about_cdn_refresh.zip).
(2) Decompress all files, and then find and open the file index.js.
(3) In the following code, replace the strings in red boxes with your SecretId and SecretKey (they should have the permission to call the API used for purging cached content in CDN), and with the domain name from which you want to purge the cached content.
![](https://main.qcloudimg.com/raw/b2b0eba560e3229fc402490f0737712b.png)
(4) To purge the cached content from a domain name bound to Tencent Cloud's CDN outside Mainland China, modify the `RefreshCdnUrl` in the code to RefreshCdnOverSeaUrl`.

#### 2.2 Upload function code

(1) Compress the modified code and other files into a .zip file.
(2) In the SCF Console, select the **Function Code** tab, set the **Submit Method** to **Upload .Zip Package Locally**, select the .zip file you just created, and then click **Upload**, as shown below:
![](https://main.qcloudimg.com/raw/9672da05b98748a5ef06da393ec64d04.png)

#### 2.3 Add trigger mode

(1) In the SCF Console, select the **Trigger Mode** tab and click **Add Trigger Mode**.
(2) Set the **Trigger Mode** to **Trigger by COS**, and select the bucket for which you want to purge the COS resources, as shown below:
![](https://main.qcloudimg.com/raw/8f3b5efab6a30b008fd1b8e12eafb1e0.png)
(3) Set the event type as needed.
- If you only need to automatically purge the cached files in CDN to access the objects uploaded to COS, set the **Event Type** to **File Upload**.
-  If you also want to automatically purge the deletion action, add another trigger mode and set the **Event Type** to **File Deletion**.

(4) Select **Enable Now**.
(5) Confirm that the information you configured is correct, and then click **Save**.

### 3. Test
>!A CDN operation takes a few minutes to take effect. Please wait a moment after performing a Query operation.

After completing the configuration, upload a new object for verification in the bucket.
(1) In the COS Console, upload an updated file with the same name, as shown below:
For more information, see [Upload Objects](https://cloud.tencent.com/document/product/436/13321).
![](https://main.qcloudimg.com/raw/66ba3a7ea298f2f4e240f76ebe76df03.png)
(2) After the upload is completed, you can find the log indicating the call is successful in the **Run Log** in the SCF Console, as shown below:
![](https://main.qcloudimg.com/raw/99b84dec0d0d3599fbffecef2d8e4d95.png)
(3) Go to **Purge Cache** -> **Operation Records** in the CDN Console to find the record indicating the API for purging has been called automatically.

(4) If the above test is successful, you can access the CDN-accelerated URL to get the latest resources.

