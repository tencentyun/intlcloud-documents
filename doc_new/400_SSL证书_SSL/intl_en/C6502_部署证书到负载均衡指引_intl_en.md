## Scenario
This document guides you through how to deploy an SSL certificate to CLB.

## Prerequisites
You have logged in to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) and successfully applied for a certificate (see [DV Certificate Application](https://intl.cloud.tencent.com/document/product/1007/30167).

## Directions
1. Select the certificate to be deployed, click **More**, and select **Deploy to CLB**, as shown below:
![](https://main.qcloudimg.com/raw/e59be48a8f0db68680611e4a9e40159f.png)
2. Filter the CLB instances by project and region and select one as shown below:
>Currently, South China (Shenzhen Finance) is not supported.

![](https://main.qcloudimg.com/raw/ef50fc5201e6e863dd409f101836dde9.png)
3. Go to the CLB Console and select the **Listener Management** tab.
4. Click **Create** in **HTTP/HTTPS Listeners** and the **Create a Listener** window will pop up.
5. Switch the **Listening Protocol Port** to HTTPS, select the server certificate, and configure the remaining basic items as shown below:
![](https://main.qcloudimg.com/raw/b09b40de147452e036a4d2e9b8d6ac16.png)
6. Go on to complete other configurations to create a listener, and then you can get a load balancer with HTTPS.
