## Overview
This document describes how to automatically purge the cached files specified in CDN using Serverless Cloud Function (SCF) when you upload objects to COS, so that CDN can automatically obtain the updated resources.

> You need to follow CDN's API request rate limit when using this feature. For more information, see [Cache Purge](https://intl.cloud.tencent.com/document/product/228/6299#url-.E5.88.B7.E6.96.B0).

## Background

When any static content needs to be updated, the old resource in COS will be overwritten by the updated one or deleted. If the configured CDN cache validity period is too long, some edge servers of CDN may still cache the old resource. If the validity period is too short, acceleration may be affected. For more information, see [Cache Expiration Configuration](https://intl.cloud.tencent.com/document/product/228/6290).

For this reason, you need to use the [cache purge](https://intl.cloud.tencent.com/document/product/228/6299) feature in the CDN Console to manually purge the specified URL to delete the invalid cached files or update the resource.

This document describes how to automatically purge cached content in CDN by combining COS with SCF when a file is updated to COS.

## Prerequisites

1. Your Tencent Cloud account needs to have access to COS, CDN, and SCF.
2. Follow [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309) and bound the bucket to a CDN accelerated domain name.
3. Ensure the region of the COS bucket supports the SCF feature. Cross-region calls are not supported at the moment.
4. Prepare the TencentCloud API key for calling the API used to purge cached content in CDN and download the [sample code for purging cached content in CDN with SCF](https://main.qcloudimg.com/raw/757b646eb68e9b9a5b2fc4bf0fed2492/scf_about_cdn_refresh.zip).

## Directions

This practical case uses Node.js sample code as an example. Follow the steps below: [create an SCF function](#step1) > [configure the function](#step2) > [test](#step3).


<span id="step1"></span>
### Creating an SCF Function
> The region​ to which your function belongs must be the same as that of the COS bucket.

1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/) and click **Function Service** on the left sidebar.
2. Select the same region as for the static content and click **Create** to create a function.
3. On the **Create a Function** page, select **Blank Function**, enter the function name (such as refresh_cdn), and then set the runtime environment (the sample code is written in Node.js, so the runtime environment should be set to Nodejs 6.10 here), as shown below:
![](https://main.qcloudimg.com/raw/48d8a30d738a5cdde8d5dc989e1fbebb.png)
4. After confirming that the configuration is correct, select **Next** > **Finish** to create the SCF function.

<span id="step2"></span>
### Configuring the Function

After the blank function is created, you need to add the function code and set the trigger, so that the function can work.

1. Configure the function code
 1. Download the [sample code for purging cached content in CDN with SCF](https://main.qcloudimg.com/raw/757b646eb68e9b9a5b2fc4bf0fed2492/scf_about_cdn_refresh.zip).
 2. Extract all files and then find and open the index.js file.
 3. In the following code, replace the strings in red boxes with your SecretId and SecretKey (which should have the permission to call the API used for purging cached content in CDN) and the domain name where you want to purge the cached content.
![](https://main.qcloudimg.com/raw/87d4efa184484e2e64441791d42e296a.png)
 4. To purge the cached content at a domain name bound to Tencent Cloud CDN outside Mainland China, change `RefreshCdnUrl` in the code to `RefreshCdnOverSeaUrl`.
2. Upload the function code
	1. Compress the modified code and other files into a .zip file.
	2. In the [SCF Console](https://console.cloud.tencent.com/scf/), select the **Function Code** tab, set the "Submission Method" to "Local Zip Package Upload", click **Upload**, and select the compressed .zip file as shown below:
![](https://main.qcloudimg.com/raw/4404e739459ec5d72679fb3bb8d7145a.png)
3. Add a trigger
 1. In the [SCF Console](https://console.cloud.tencent.com/scf/), select the **Triggers** tab and click **Add a Trigger**.
 2. Set **Trigger** to **COS trigger** and select the COS bucket where the resource needs to be updated. Below are the configuration items. For more information, see [COS Trigger](https://intl.cloud.tencent.com/document/product/583/9707). 
    **COS Bucket**: Select the COS bucket to be used as the event source, which must be in the same region as for the function.
    **Event Type**: Select under what conditions the COS bucket will trigger the function. For each COS bucket, only one event type can be set.
If you only want to automatically purge CDN to access the objects uploaded to COS in an overwriting manner, you need to set the "Event Type" to an upload operation, such as creation in the PUT or POST method.
If you also want to automatically purge CDN when a deletion operation occurs, add another trigger and set the "Event Type" to "File Deletion".
    **Prefix Filtering**: prefix filtering is usually used to filter file events in the specified directory. For example, if the prefix to be filtered is `test/`, only file events in the `test/` directory can trigger the function, while those in the `hello/` directory cannot.
    **Suffix Filtering**: suffix filtering is usually used to filter file events in the specified type or with the specified suffix. For example, if the suffix to be filtered is `.jpg`, only file events of the `.jpg` type can trigger the function, while those of the `.png/` type cannot.
![](https://main.qcloudimg.com/raw/8d0b04ec9c7971f79bbf25671cc7762b.png)
 3. Select "Enable Now".
 4. After confirming that the configuration information is correct, click **Save**.


<span id="step3"></span>
### Test
> As a CDN operation takes a few minutes to take effect, please wait a moment before you perform a query operation.

After completing the configuration, you can upload a new file with the same object key to the corresponding bucket for verification.
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and upload a new file with the same object key. For directions, see [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/13321).
2. After uploading, log in to the [SCF Console](https://console.cloud.tencent.com/scf/) and select **Function Service** > **Function Name** > **Execution Logs** to query the log of successful call.
3. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and select **Cache Purge** > **Operation Records** to query the record of the automatic call of cache purge.
4. If the above test is successful, you can access the CDN-accelerated URL to get the latest resource.

