## Overview

Tencent Cloud Enterprise Content Delivery Network (ECDN) integrates static edge caching and dynamic origin-pull route optimization. Through Tencent's global nodes and based on more than ten years of technical practice on the QQ platform, ECDN provides one-stop acceleration service with high reliability and low latency.

Connecting the API Gateway with ECDN can help you solve problems such as slow response, high packet loss and unstable service caused by cross-ISP, cross-boarder and cross-network data transfer.

## Relevant Products

- [API Gateway](https://console.cloud.tencent.com/apigateway/service)
- [ECDN](https://console.cloud.tencent.com/ecdn)

<img src="https://qcloudimg.tencent-cloud.cn/raw/22c2e5a8781a7b820e9db25ffb49dd1e.png" width="450px">     

## Directions

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/service). Create an API Gateway service. A default access address is generated.
2. Configure a custom domain name in the ECDN console.

	- Enter the custom domain name in the "Add acceleration domain name" field.
	- Select "Origin server domain name" as the origin server type.
	- Select "Optimal origin-pull" as the origin-pull policy.
	- Enter the default access address generated in step 1 (without the protocol and port number) as the origin-pull address.
	- Select the origin-pull protocol and acceleration region as needed.
	
Click **Save** to complete the configuration. A CNAME domain name will be generated in the CDN console after a while.
                
3. Modify the origin server Host.                      
Select the just configured domain name in the domain name list in ECDN console. Click it to go to the details page.
Change the origin server Host to the default public network access address generated in step 1.

4. Configuring CNAME.
Configure the CNAME domain name for the connected domain name.
![](https://qcloudimg.tencent-cloud.cn/raw/4ce80b56098ea1d99503078675f4c86a.png)

5. Initiate a call, and you can see that they are already connected.

