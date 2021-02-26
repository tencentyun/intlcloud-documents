You can connect to CDN to deliver contents on your origin server to service nodes closest to end users, which directly respond to user requests to effectively reduce user access latency and improve availability. 
To configure CDN, you must sign up for a Tencent Cloud account, activate CDN, add a domain name, and configure CNAME. The steps are detailed in this document.

## Step 1. Sign up for a Tencent Cloud account
If you already have a Tencent Cloud account, you can ignore this step.
<div style="background-color:#00A4FF; width: 270px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn1">Sign up for a Tencent Cloud account</a></div>

## Step 2. Activate the CDN service
#### 1. Complete identity verification
Registered users must first complete identity verification in order to activate CDN. You can verify your identity in the CDN console or Account Center. For more information on the verification process, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/cdn" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn2">Go to CDN console</a></div><br>

![](https://main.qcloudimg.com/raw/e593cf6199d64fbcc5c6f50089778cf9.png)
#### 2. Activate the CDN service
After completing identity verification, you can activate the CDN service.
(1) Select the billing mode
Tencent Cloud CDN has two billing regions, namely the **Chinese mainland** and **outside the Chinese mainland**. For users who activate CDN after December 7, 2020 21:30, **bill-by-hourly-traffic** is the only billing option. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949).
![](https://main.qcloudimg.com/raw/5f75a3047566df1413233c2c0ac2736f.png)
(2) Activate CDN
Indicate your consent to the Terms of Service, click **Activate CDN**, and start using the acceleration service.
![](https://main.qcloudimg.com/raw/4b1997247ae88641d1c2af0289b7ad2a.png)

## Step 3. Connect a domain name
You need to connect your business domain name for the acceleration service. CDN caches resources from your business origin server to CDN cache nodes via an acceleration domain name to achieve resource access acceleration, thus end users can request resources from the nearest nodes. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/228/5734" hotrep="document.guide.3149.linkdomain">Adding Domain Names</a>.

## Step 4. Configure CNAME
Once your domain name is connected to CDN, you need to complete the CNAME configuration at your domain name service provider. After the configuration takes effect, CDN can be used properly. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/228/3121" hotrep="document.guide.3149.linkcname">CNAME Configuration</a>.
