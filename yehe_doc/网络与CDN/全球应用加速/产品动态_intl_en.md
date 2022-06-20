<style> 
table th:nth-of-type(1) {width:20%; } 
table th:nth-of-type(2){ width:45%; } 
table th:nth-of-type(3){ width:16%; } 
table th:nth-of-type(4){ width:19%; } 
</style>

## March 2022

| Update             | Description                                                     | Release Date   | Remarks                                                    |
| -------------------- | ------------------------------------------------------------ | -------- | ---------------------------- |
| Released the "GAAP shared acceleration" feature | TCP/UDP monitoring and transmission acceleration are provided based on high-speed lines over the public network (only supported for Tencent Cloud users in the Chinese mainland). | March 2022   | To use this feature, please submit a ticket. |
| Optimized cross-MLC-border connection     | The specification upgrade and auto-renewal of cross-MLC-border connections are supported.                   | March 2022   | This feature is supported by default.                     |

## February 2022

| Update                 | Description                                                    | Release Date | Remarks     |
| ------------------------ | ----------------------------------------------------------- | -------- | -------- |
| SNI configuration for origin-pull  | SNI is sent to the origin server before an SSL connection is established, so that the origin server can return the correct certificate. | February 2022   | This feature is supported by default. |
| Origin domain | In HTTP/HTTPS listeners, the origin domain field of the origin-pull request can be modified.              | February 2022   | This feature is supported by default. |

## January 2022

| Update      | Description                                               | Release Date | Remarks     |
| ------------- | ------------------------------------------------------------ | -------- | -------- |
| HTTP3 | The HTTP3 feature can be enabled according to actual business needs.<br/>When it is enabled, acceleration connections will support HTTP3 (QUIC) transfer. | January 2022   | This feature is supported by default. |

## December 2021

| Update                   | Description                                               | Release Date | Remarks                         |
| -------------------------- | ------------------------------------------------------------ | -------- | ---------------------------- |
| Multiple domain names for the default entry of the unified domain name | The default entry of the unified domain name supports configuring multiple domain names, separated by semicolons. | December 2021 | This feature is supported by default. |
| Domain name dimension for statistics | Statistics support the domain name dimension listened on by HTTP/HTTPS. Data types include request volume and status code. | December 2021 | To use this feature, please submit a ticket. |
| CUCC cross-border leased line          | If your business involves the Chinese mainland, use CUCC cross-MLC-border connections (currently only supported between Chinese mainland and Hong Kong (China)). | December 2021  | This feature is supported by default.                     |

## November 2021

| Update         | Description                                               | Release Date | Remarks                         |
| ---------------- | ------------------------------------------------------------ | -------- | ---------------------------- |
| Notification of primary/secondary origin server switch   | When a primary/secondary origin server switch is triggered, notifications will be sent through Message Center and email.             | November 2021  | To use this feature, please submit a ticket. |
| Non-BGP statistics optimization | Statistics can be displayed for each ISP or all ISPs. Monitoring alarm policy supports alarms for non-BGP connection IPs. | November 2021  | To use this feature, please submit a ticket. |


## October 2021

| Update | Description                                               | Release Date   | Remarks                                                    |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|IPV6 protocol|An IPV6 address can be used as origin server. Unified domain names can be resolved to IPv6 addresses.|October 2021|To use this feature, please submit a ticket.|
|Layer-7 listener|The domain name bound to the layer-7 listener is allowed to be modified and inconsistent with the origin server domain name. |October 2021|This feature is supported by default.|
|Connection status|Connections can be filtered by status in the console.|October 2021|This feature is supported by default.|
|Non-BGP acceleration solution|Over 10 non-BGP acceleration nodes for the Chinese mainland are available for connection, helping reduce costs.|October 2021|To use this feature, please submit a ticket.|
|Server certificate|Automatically verifying whether the server certificate changed for a layer-7 listener matches the domain name is allowed.|October 2021|This feature is supported by default.|

## September 2021

| Update | Description                                               | Release Date   | Remarks                                                    |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Dedicated BGP solution supported in Hong Kong (China)|Dedicated bandwidth for a T1 line between the Chinese mainland and Hong Kong (China) is supported. |September 2021|To use this feature, please submit a ticket.|
|Linux TOA update|CentOS 8.2 and Ubuntu Server 20.04 are now supported. |September 2021|[TOA Module Loading Method](https://intl.cloud.tencent.com/document/product/608/18945)|


## August 2021
| Update | Description                                               | Release Date   | Remarks                                                    |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Statistics optimization|Statistics can be retained for 6 months and exported from the console.|August 2021 |This feature is supported by default.| 
|Certificate expiration alarm| An expiration reminder will be sent by WeChat, Message Center, email and SMS 30 days, 7 days, 3 days, and 1 day before a certificate expires.|August 2021 |This feature is supported by default.| 
|Silver acceleration connection|Cost-effective Silver acceleration connection is provided and supports monthly settlement.|August 2021 |To use this feature, please submit a ticket.|
