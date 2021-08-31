## Operation Scenarios
This document describes how to get a subdomain name for service access in the service details in the API Gateway Console.

## Prerequisites
A [service has been created](https://intl.cloud.tencent.com/document/product/628/11787).

## Directions
1. Log in to the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1) and select **Service** on the left sidebar.
2. In the service list, click the target service name to enter the service details page.
3. On the **Service Info** tab, view the subdomain name for accessing the service.
![](https://main.qcloudimg.com/raw/bbd7e5499899f304074de93255acb9e3.png)

## Service Domain Name Description
* Sample service domain name: `service-a1b2c3d4-1234567890.gz.apigw.tencentcs.com`.
* A service subdomain name contains your service name, `APPID`, and region, such as `http://{your-unique-id}.{region}.apigw.tencentcs.com`.
* If both private network VPC and public network are selected as the access method, two subdomain names will be obtained for private network VPC access and public network access, respectively. Private network VPC access is made available through an allowlist. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
* API Gateway has also enabled the wildcard domain name SSL certificate feature; therefore, the subdomain name of a service can be accessed through the HTTPS protocol at an access address in the format of `https://{your-unique-id}.{region}.apigw.tencentcs.com`.
