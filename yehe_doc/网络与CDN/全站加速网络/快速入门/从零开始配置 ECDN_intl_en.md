Tencent Cloud ECDN integrates static edge caching and dynamic origin-pull route optimization. Through Tencent's global nodes, ECDN can solve problems such as slow response, packet loss, and service instability caused by cross-border and cross-ISP data transfer.
To configure ECDN, follow the steps below to sign up for a Tencent Cloud account, activate ECDN, add a domain name, and configure CNAME.
>? If you use ECDN for the first time, consult [Configuring CDN from Scratch](https://intl.cloud.tencent.com/document/product/228/32978).
## Step 1. Sign up for a Tencent Cloud account
If you already have a Tencent Cloud account, you can ignore this step.
<div style="background-color:#00A4FF; width: 380px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn1">Click here to sign up for a Tencent Cloud account</a></div>

## Step 2: Activate the ECDN service
#### 1. Complete identity verification
Registered users must first complete identity verification in order to activate CDN. You can verify your identity in the CDN console or Account Center. For more information on the verification process, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

<div style="background-color:#00A4FF; width: 300px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3149.btn2">Click here to go to the Account Center</a></div><br>

![](https://main.qcloudimg.com/raw/f4f9c571ccbc82912aab084315d36dff.png)

#### 2. Activate the ECDN service
After identity verification is completed, log in to the [ECDN Console](https://console.cloud.tencent.com/ecdn) to activate ECDN service.
![](https://main.qcloudimg.com/raw/df8fead92c1b97f550b83fe94c35b4e5.png)

## Step 3. Connect a domain name
ECDN caches the static resources on the origin server to the cache node through the acceleration domain name, and quickly pulls the dynamic content from the origin server through intelligent routing optimization, protocol optimization, and other dynamic acceleration technologies to achieve resource access acceleration. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/570/10361" hotrep="document.guide.3149.linkdomain">Domain Name Connection</a>

## Step 4. Configure CNAME
After connecting your domain name to ECDN, you need to configure the CNAME with your domain name provider. The ECDN service will be available after the configuration takes effect. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/570/11134" hotrep="document.guide.3149.linkcname">CNAME Configuration</a>.
