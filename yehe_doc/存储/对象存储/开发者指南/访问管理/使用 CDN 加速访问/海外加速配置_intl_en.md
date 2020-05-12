## Overview

Tencent Cloud Global Content Delivery (GCD) distributes Tencent's high-performance cache nodes globally, which accelerate worldwide static content, content download and delivery, audio/video on-demand services.
Tencent Cloud GCD is under open beta test and the quota is limited. Submit an application if you want to have a try. The following describes how to configure GCD for CDN.

>You need to apply for activating GCD before you can use this feature.

## Use Cases

- The end users outside Mainland China need to be reached and accelerating access and reducing access delay are required.
- Cross-region, cross-border or cross-continent data transfer reaching GB or TB-level is required.
- The same content needs to be downloaded frequently.

## Description

When your application for activating GCD is approved, go to Tencent Cloud's [GCD Console](https://console.cloud.tencent.com/cdn/open_oversea) to add COS's XML access domain name for acceleration.
You need to set the content to be accessed to **Public** in COS console in order to bind and use the GCD accelerated domain name to access the content on COS.

## Directions
Configure GCD by following the steps below: **Configure Policy Permissions** -> **Configure GCD** -> **Configure CNAME**.

### Configure policy permissions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click to enter the bucket for which you want to configure policy permissions.
3. Click **Permission Management**, and find the **Permission Policy Settings** section to add a public access policy.
4. Click **Add Policy**, and then set **User**, **Resource** and **Operation** as follows:
 - Effect: Allow
 - User: All Users
 - Resource: Entire Bucket
 - Actions: Read Operation.
![](https://main.qcloudimg.com/raw/3b29c902ad3ea3b64ef07485b813bf53.png)
5. Click **OK** to save the policy configuration.

### Configure GCD

1. Obtain the COS domain name.
In the [COS Console](https://console.cloud.tencent.com/cos5), obtain the access domain name of the bucket for which you want to accelerate access.
```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```
If you want to accelerate the delivery of content for a bucket for which the static website feature is enabled, and use the features of a static website, use a static website domain name, for example:
```shell
examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```
2. Bind a domain name to GCD
Log in to Tencent Cloud's [GCD Console](https://console.cloud.tencent.com/cdn/open_oversea), and then add a domain name by using COS as your self-owned origin. The configuration items are as follows:
 - Domain: Enter the access domain name you want to bind to GCD.
 - Service Type: The data in COS is mostly unstructured data. It is recommended to select **Static Content**.
 - Origin Type: Select **External** (self-owned origin).
 - Origin Domain: Enter COS's XML API domain name or static website domain name.
 - **Host header (origin-pull Host) : This should be same as the origin server's domain name**.
![](https://main.qcloudimg.com/raw/691da49e660fb3a5675d371821e702d9.png)
Set other options as needed.

### Configure CNAME
Go to your DNS service provider to add the CNAME record. For more information on how to configure CNAME, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121) in CDN documentation.

## FAQs
- For questions about whether a domain name without ICP-filing in Mainland China can access GCD, see COS [FAQs](https://intl.cloud.tencent.com/document/product/436/30590).
