This document instructs you to configure advanced features for domain names, such as traffic tagging, remote client address transfer and access logging, to meet your compliance requirements.
>? Only WAF Enterprise, Ultimate, and Exclusive editions support advanced features.


## Enabling Traffic Tagging
Traffic tagging is used to tag a client request forwarded to the origin server by adding a custom field in the request header.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Asset Center** > **Domain Name List** on the left sidebar.
2. On the page that appears, select a domain name and click **More** > **Traffic tagging**.
![](https://qcloudimg.tencent-cloud.cn/raw/e1440591a01d4c4e2e4e41c369e72f25.png)
3. In the pop-up window, click the checkbox ![](https://qcloudimg.tencent-cloud.cn/raw/9098bf8e15ccf6852ef2c0087bd715f0.png) to enable traffic tagging, enter the required parameters, and then click **Save**.


**Field description:**
 - Traffic tag name: Name of the traffic tag.
 - Traffic tag value: Value of the traffic tag.

4. After the configuration is complete, click **Back** to return to the Domain Name List page.

## Enabling Remote Client Address Transfer
Remote client address transfer is used to pass the IP address and source port of the previous hop to the backend when WAF forwards client requests to the origin server.
1. On the Domain Name List page, select a domain name. Click **More** > **Request configuration** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/7865aa6d48effeb656485f5e910fa3d8.png)
2. In the pop-up window, click the checkbox ![](https://qcloudimg.tencent-cloud.cn/raw/4cc9aad2b46575216b596db8654c2b57.png) to enable remote client address transfer. The real client IP and related information will then be recorded.

## Enabling Log Service
On the [Domain Name List](https://console.cloud.tencent.com/guanjia/tea-domain) page, select a domain name and toggle on the access logging switch ![](https://qcloudimg.tencent-cloud.cn/raw/deacc1dd2ca341267f225409e53c3bf9.png). Access logs will then be recorded automatically, and used for quick retrieval and source-tracking analysis.
![](https://qcloudimg.tencent-cloud.cn/raw/70c139d2db2fd38d3d0509cdcec835d5.png)

