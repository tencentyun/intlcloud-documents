## Overview

You can add a domain and validate it for approved certificate administrator information, so that you can skip domain validation during certificate application to accelerate the process.

> **Notes**
> 
> No domain can be added for certificate administrator information that has not been approved.
> 


## Prerequisites
- Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and click **My Profile** on the left sidebar to enter the management page.

- The administrator information has been approved.


## Directions
1. On the **My Profile** page, click the target organization name to view the information of administrators that have been applied for.

2. Click the target administrator name to enter the **Review Information** page.

3. Click **Domain Information** > **Add Domain** to enter the management page.

4. In the **Domain Information** module, enter the target domain and click **Next**.
5. In the **Domain validation** module, enable automatic validation and select the validation method as needed.

  - Automatic validation: It is enabled by default. After validation parameters are configured, this option avoids repeated validation operations during certificate renewal.

  - Validation method: It is subject to the status of **Automatic validation**.

    - **Enable automatic validation**: You can select either of the following validation methods as needed:

      - **Automatic DNS validation**: Configuring CNAME records can ensure continuous domain validation. For detailed directions, see [Automatic DNS Validation](https://www.tencentcloud.com/document/product/1007/53635).

      - **Automatic file validation**: Configuring reverse proxies can ensure continuous domain validation. For detailed directions, see [Automatic File Validation](https://intl.cloud.tencent.com/document/product/1007/44061).

    - **Disable automatic validation**: You can select one of the three validation methods as needed:

      - **Automatic DNS addition**: Tencent Cloud will automatically add DNS records for you.
            

            > **Notes**
            > 
            > This option is available only for [DNSPod](https://console.cloud.tencent.com/cns) domains.
            > 

      - **DNS validation**: You need to manually add a DNS record for the domain as instructed in [DNS Validation](https://intl.cloud.tencent.com/document/product/1007/45895).

      - **File validation**: You need to create the specified file in the root directory of the domain to verify your ownership as instructed in [File Validation](https://intl.cloud.tencent.com/document/product/1007/43542).

6. Click **Next** and complete domain validation as prompted. Here, **Automatic DNS validation** is selected as an example.

7. After adding the corresponding DNS record, click **Validate** to check whether the configuration is correct and has taken effect.
   

   > **Notes**
   > 
   > The domain identity verification will be completed after the CA scans and approves the record.
   > 
