This document describes how to apply for a certificate and enter the information for review.

## Certificate Application Process

The process for purchasing a certificate is as shown below:
![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100023397743/b67b3c0b398e11ed8088525400463ef7.png?q-sign-algorithm=sha1&q-ak=AKIDd2WHer59yXTd_a_JJDkcyZ1SHi9Wf9PX43L_4V5Lj9VowvyHxxy5ko8yzSM6Vuhq&q-sign-time=1677228325;1677231925&q-key-time=1677228325;1677231925&q-header-list=&q-url-param-list=&q-signature=bd2a87217d1e6b62fb3f5cf64fd36be3b3978aff&x-cos-security-token=6hMEYRM6EVK7wQVx1850tcGp3oXIcQLa7d0f59e280aa92cc99fda2265cc99ddclq4GrbYk_Xrb8oMoMGYe5GnqBBwAmi6wx9HfvSJ82dm5blzxcEXv2P9BMB95ym8UW3BkD9HKIk5Zft9m_q99iyS6o6SaWLPHEA17EMLN9CyfBospWfLdAj-f9dr1aT8HEXpIxxkdSODRCEmH8tlR_JF8RE2x_Wunz1PzpvyKAz3z1R71omtu0pBE5p-FFJcwURRkyx7bxnazbQJviqblccStlqlWRKo1raKXz8EwPyk6l2GhRoDwV2MIc_nZTawwp_bCZd-g8OWjOvkSg2kg0j8ANnbEsAZmFs3QJOstZ9oH-QizOZCBgnDZeBseGlr-gOiG8P0M_ZYaAC82EavJTr7XyM40jABG92fEZBs4yVMqUjJr71P5Xy5EELZ6LeCD)

### Step 1. Purchase a certificate
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), go to the certificate list management page, and click **Purchase Certificate** as shown below:
   

> **Notes**
>   - You can also purchase a certificate on the [SSL certificate purchase page](https://intl.cloud.tencent.com/pricing/ssl).
>   - If you are not familiar with certificate types and brands, click **Quick Configuration** to quickly purchase a certificate recommended by the system.
>   - After you pay the order, a certificate ID will be generated. During certificate issue, a domain is bound, after which the domain cannot be modified or another domain cannot be added.


2. Select the target certificate type, brand, and validity period as well as domain type as instructed in [Purchasing Process](https://intl.cloud.tencent.com/document/product/1007/30159).


### Step 2. Submit the information for verification

#### Method 1

**Free DV SSL certificates:**
After applying for the certificate, complete the domain ownership verification. The CA will then issue the certificate.

#### Method 2

**OV and EV SSL certificates from other brands:**
After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and select **Pending Submission** to enter the management page. Then, submit the information and upload the confirmation letter to apply for the certificate. After your application is submitted, manual approval is needed, after which the CA will issue the certificate. For more information, see [Information Submission Process for SSL Certificates of Other Brands](https://intl.cloud.tencent.com/document/product/1007/30160).

> **Notes**
> 
> - If you use the approved organization and administrator information in [**My Profile**](https://console.cloud.tencent.com/ssl/info), the confirmation letter is not required.
> - For GlobalSign certificates, the confirmation letter still needs to be uploaded when you submit the information.


#### Method 3
- **DV SSL certificates:**
After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and select **Pending Submission** to enter the management page. Then, submit the information and complete the domain identity verification, after which the CA will issue the certificate.

- **WoTrus OV and EV SSL certificates:**
After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and select **Pending Submission** to enter the management page. Then, submit the information to pre-apply for the certificate. After your pre-application is approved, domain identity verification is required. After your domain is validated, manual approval is needed, after which the CA will issue the certificate. For more information, see [Information Submission Process for Wotrus OV and EV SSL Certificates](https://intl.cloud.tencent.com/document/product/1007/40206).

- **DNSPod Chinese SM (SM2) OV and EV SSL certificates:**
After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and select **Pending Submission** to enter the management page. Then, submit the information, upload the confirmation letter, and complete the domain identity verification to apply for the certificate. After your application is submitted, manual approval is needed, after which the CA will issue the certificate.


### Step 3. Issue the certificate

After your certificate application is approved, the CA will issue the certificate.

### Step 4. Install the certificate
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) again and go to the **My Certificates** page.

2. Select the target certificate and click **Download** in the **Operation** column.

3. After downloading the certificate, decompress and install it to your Tencent Cloud service as instructed in [Selecting an Installation Type for an SSL Certificate](https://intl.cloud.tencent.com/document/product/1007/30173).
