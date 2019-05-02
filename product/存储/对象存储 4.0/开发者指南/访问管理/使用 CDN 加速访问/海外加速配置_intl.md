## Overview

Tencent Cloud's Global Content Delivery (GCD) allows the worldwide acceleration of static content, content download and delivery, audio/video on-demand service, and other services using Tencent's globally distributed high-performance cache nodes.
Tencent Cloud's GCD is on trial with limited quota for applicants. Submit a trail application if you need to use this feature. For more information, see [How to apply for trial](https://cloud.tencent.com/document/product/673/30415). The following describes how to configure GCD for CDN.

>!You need to apply for activating GCD before you can use this feature.

## Use Cases

- The end users outside Mainland China need to be reached and accelerating access and reducing access delay are required.
- Cross-region, cross-border or cross-continent data transfer reaching GB or TB-level is required.
- The same content needs to be downloaded frequently.

## Description

When your application for activating GCD is approved, go to Tencent Cloud's [GCD Console](https://console.cloud.tencent.com/cdn/open_oversea) to add COS's XML access domain name for acceleration.
You need to set the content to be accessed to **Public** in COS in order to bind and use the GCD accelerated domain name to access the content on COS.

## Directions
Configure GCD by following the steps below: **Configure Policy Permissions** -> **Configure GCD** -> **Configure CNAME**.

### Configure policy permissions

1. Log in to Tencent Cloud's [COS Console](https://console.cloud.tencent.com/cos5) to go to the management page. Click the **Permission Management** tab to add a public access policy.
![](https://main.qcloudimg.com/raw/b1c0862f797da9d1447bc6a13929a927.png)
2. Click **Add Policy**, and then set **User**, **Resource** and **Operation** as follows:
 - Effect: Allow
 - User: All Users
 - Resource: Entire Bucket
 - Operation: Read Access
![](https://main.qcloudimg.com/raw/953311e15a9ca272dc5fece6a87ac6b7.png)

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
Set other options as needed. For more information, see [Getting Started](https://cloud.tencent.com/document/product/673/14422) in GCD documentation.

### Configure CNAME
Go to your DNS service provider to add the CNAME record. For more information on how to configure CNAME, see [CNAME Configuration](https://cloud.tencent.com/document/product/228/3121) in CDN documentation.

## FAQs
For the question whether a domain name that has not gone through filing procedure with MIIT can be bound to GCD and other questions, see [FAQs](https://cloud.tencent.com/document/product/436/30737#.E5.B0.9A.E6.9C.AA.E5.A4.87.E6.A1.88.E7.9A.84.E5.9F.9F.E5.90.8D.E5.8F.AF.E4.BB.A5.E6.8E.A5.E5.85.A5.E6.B5.B7.E5.A4.96.E5.8A.A0.E9.80.9F-gcd-.E5.B9.B3.E5.8F.B0.E5.90.97.EF.BC.9F) in COS documentation.
For more questions about CDN acceleration, see [FAQs](https://cloud.tencent.com/document/product/673/31673) in GCD documentation.

