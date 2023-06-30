
## Overview
Tencent Container Registry (TCR) Enterprise Edition allows you to configure and use custom domain names, which facilitates the use of the domain access service uniformly planned by your company. In addition, you can continue using the original domain name after migrating from another image registry service to TCR, which helps maintain the service continuity.

TCR Enterprise Edition instances with any specifications all support configuring multiple domain names without affecting the normal use of existing default domain names of the instances. To use a custom domain name, you need to provide the SSL certificate associated with the domain name and access the instance over HTTPS. This document describes how to use a custom domain name to access a TCR Enterprise Edition instance.

## Concepts
#### Domain name
A domain name is a string of characters separated by dots. A domain name in TCR Enterprise Edition is used to access the instance service and directly determines the access address of an image repository.

#### SSL certificate
An [SSL certificate](https://intl.cloud.tencent.com/document/product/1007/30152) is used for compliance with the HTTPS protocol, so that TCR Enterprise Edition can implement encrypted transfer and identity verification over the HTTPS protocol, ensuring the transfer security.


#### DNSPod
DNSPod can route the access traffic to a custom domain name to the corresponding IP address of a TCR Enterprise Edition instance.

## Prerequisites
Before configuring and using a custom domain name, you need to complete the following:
- Get a domain name. You can register one in Tencent Cloud Domains.
<dx-alert infotype="notice" title="">
- Get an ICP filing for you domain name if you want to use it in a public network environment.
- You do not need to get an ICP filing if your TCR Enterprise Edition instance is outside the Chinese mainland. 
</dx-alert>
- Get a certificate for the domain name. You can purchase a certificate in [SSL Certificates](https://intl.cloud.tencent.com/zh/product/ssl) and confirm that it has been bound to the custom domain name to be used by the instance.
- Activate DNSPod. For more information, see [Private DNS](https://intl.cloud.tencent.com/zh/product/privatedns).


## Directions
### Creating custom domain name
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Domain Name Management** on the left sidebar.
2. On the **Domain Name Management** page, select the region and ID of the instance for which you want to add a custom domain name.
3. Click **Add Domain Name*. In the **Add Domain Name** pop-up window, configure the domain name and certificate information as prompted as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/df09f04be90748e1c48d2de0f0d8aab5.png)
 - **Domain Name**: enter the custom domain name to be used. We recommend you use a common domain suffix.
 - **Certificate**: select a certificate bound to the custom domain name. Only a certificate managed in SSL Certificates can be selected.
<dx-alert infotype="explain" title="">
If your custom domain name has been filed with MIIT, and a DNS record has been added in the Domains console, you can enter it in the **Domain Name** input box and select a certificate.
</dx-alert>
4. Click **OK**.
After adding a custom domain name successfully, you can view it on the **Domain Name Management** page. Then, you can perform the following operations to manage the custom domain name as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0e19c0c6c8bd7286773112ef93724bc1.png)

### Setting access control and DNS
You can use the custom domain name in the public network or VPC. We recommend you use a VPC to access the instance preferably.
<dx-tabs>
::: Private\snetwork\saccess
#### Configuring private network access control
   Connect a VPC to the instance and confirm that the private network access IP is generated normally as instructed in [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492).
#### Configuring Private DNS
   Go to the [Private DNS](https://console.cloud.tencent.com/privatedns) console, [create a private domain](https://intl.cloud.tencent.com/document/product/1097/40558) with the added custom domain name, and associate it with the connected VPC. Use an A record to configure DNS in the private domain, and use the private network access IP of the created private network access linkage as the record value. For more information, see [Private DNS](https://intl.cloud.tencent.com/zh/document/product/1097).
:::
::: Public\snetwork\saccess
#### Configuring public network access control
   Enable the public network access entry and open the public network access address as instructed in [Public Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35491).
#### Configuring public network DNS
   Go to the DNSPod console, configure a DNS record for the added custom domain name, select **CNAME** as the record type, and enter the default domain name of the instance as the record value.
:::
</dx-tabs>





### Updating domain certificate
If you need to update the certificate bound to your custom domain name for reasons such as certificate expiration or upgrade, go to the **Domain Name Management** page, click **Update Certificate** on the right of the row of the custom domain name and select an SSL certificate again. Certificate update requires redelivery of the SSL certificate information, during which the custom domain name can still be accessed normally.

### Deleting custom domain name
On the **Domain Name Management** page, click **Delete** on the right of the row of the specified custom domain name to delete it. Doing so may invalidate the existing container image pull configuration and thus affect application update. Therefore, do so with caution.
