You can connect to CDN to deliver contents on your origin server to service nodes closest to end users, which directly respond to user requests to effectively reduce user access latency and improve availability. 
To configure CDN, you must sign up for a Tencent Cloud account, activate CDN, add a domain name, and configure CNAME. The steps are detailed in this document.

## Step 1. Sign up for a Tencent Cloud account
If you already have a Tencent Cloud account, you can ignore this step.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;">Click here to sign up for a Tencent Cloud account</a></div>

## Step 2. Activate the CDN service
#### 1. Complete identity verification
Registered users must first complete identity verification in order to activate CDN. You can verify your identity in the CDN Console or Account Center. For more information on the verification process, please see [Identity verification guide](https://intl.cloud.tencent.com/document/product/378/3629).
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;">Click here to go to the Account Center</a></div><br>

![](https://main.qcloudimg.com/raw/e71557f3118bf3579d551bb2ae2e2e9e.png)
#### 2. Provide additional service information
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), confirm your identity verification information, select the service, and click **Next**.
![](https://main.qcloudimg.com/raw/087a21d256d40282127396a63b67c7b4.png)
#### 3. Select a billing method
CDN provides two billing methods: bill-by-traffic and bill-by-bandwidth. You can choose according to your business type. For more information, please see [Billing Descriptions](https://cloud.tencent.com/doc/product/228/2949).
Accept the terms of service and click **Activate CDN** to start using the acceleration service.
![](https://main.qcloudimg.com/raw/03c8c19ce7c7c73c956c23dc1c36dd3f.png)

## Step 3. Connect a domain name
You need to add an accelerated domain name for your acceleration service. Through accelerated domain name, CDN caches resources on an origin server into a CDN cache node closest to the client to accelerate resource access. For more information, please see [Connecting a domain name](https://intl.cloud.tencent.com/document/product/228/5734). 

## Step 4. Configure CNAME
After connecting your domain name to CDN, you need to configure the CNAME with your domain name provider. The CDN service will be available after the configuration takes effect. For more information, please see [Configuring CNAME](https://intl.cloud.tencent.com/document/product/228/3121).
