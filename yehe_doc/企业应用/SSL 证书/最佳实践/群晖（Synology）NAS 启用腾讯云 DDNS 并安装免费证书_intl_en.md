## Overview

This document describes how to enable Tencent Cloud's dynamic DNS (DDNS) in Synology NAS, so as to access Synology NAS with a public IP over the public network by using a domain.

> **Notes**
> 
>  In the process, fees may be incurred by domain purchase, but enabling DDNS and applying for a certificate are free of charge.
> 


## Prerequisites
- You have a Synology NAS account with admin permissions.

- You have a DNSPod account and have completed [identity verification](https://docs.dnspod.cn/account/5f3c8dffab35dc34f5791414/).

- The Synology NAS has a public IP.

- You have an available domain hosted with [DNSPod](https://console.dnspod.cn/dns/list).
  


## Directions

### Step 1. Get the API key information

On the [TencentCloud API key](https://console.dnspod.cn/account/token/apikey) page, get the **SecretId** and **SecretKey**.

> **Notes**
> 
> - Your API key represents your account identity and granted permissions, with which all Tencent Cloud resources under your account can be manipulated.
> - For the security of your assets and services, store your keys safely and change them regularly. Do not upload or share them via any method (such as GitHub).


### Step 2. Configure DDNS in the Synology NAS
1. Log in to your Synology NAS with an admin account and click **Control Panel** > **External Access** > **DDNS** > **Add**.

2. In the **Add DDNS** pop-up window, enter the information.

  - **Service Provider**: Select **Tencent Cloud**.

  - **Hostname**: Enter your **domain**.

  - **Username/Email**: Enter the obtained **SecretId**.

  - **Password/Key**: Enter the obtained **SecretKey**.

  - **Get a certificate from Tencent Cloud and set it as default**: After this option is selected, the system will automatically apply for a free TrustAsia SSL certificate for you and replace the default NAS SSL certificate with it.
    

      > **Notes**
      > 
      > Click **Test Connection** to test the connection. If the **Status** is **Normal**, the connection is established successfully.
      > 

3. Click **OK**. Wait for the DNS record to take effect. Then, you can use the domain to access your Synology NAS.
   

   > **Notes**
   > 
   > The DNS record usually takes 10 minutes to take effect. 
   > 


### Step 3. Manually update the DDNS (optional)
1. After configuring the settings, click **Update Now**, and the system will update the DDNS record. Then, check whether the **Status** is **Normal**.

2. Go back to the [**My Domains**](https://console.dnspod.cn/dns/list) page and click your domain to check whether the record value has changed to your public IP.

  - If so, the settings are successfully applied.

  - If not, troubleshoot according to the following FAQs.


## FAQs

### What should I do if the domain cannot be accessed after the settings are configured?
- Check whether your IP is a public IP. Specifically, access the IP obtained by the Synology NAS via the browser in the public network environment. If the access succeeds, the IP is a public IP.

- After configuring the settings, you need to wait for the DNS record to take effect (which usually takes 10 minutes) before access. Then, run the `ping domain` command to check whether the returned IP is your public IP.


### What should I do if the record value does not change after the manual update?

 Check whether the **SecretId** and **SecretKey** are entered correctly.