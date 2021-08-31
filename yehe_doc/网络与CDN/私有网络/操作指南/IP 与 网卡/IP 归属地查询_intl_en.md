The IP location query feature helps you obtain the information about the geographic location and ISP of a public IP address.
For example, the query shows that the `123.123.123.123` IP address is located in Beijing and provided by China Unicom.
>?  
>- Currently, the IP location query feature is in beta test. To try it out, please apply for beta eligibility.
>- This feature is now available for free, and no SLA can be provided. It will be billed after commercialization.

## Use Cases
- You can query the location and ISP of a destination CVM IP address and choose the source CVM to connect. 
- You can query the actual location of a public IP you purchased from Tencent Cloud or other cloud platforms.

## Restrictions
Currently, the IP location query is only available to IPv4 addresses.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **IP and Interface** > **IP Location Query** on the left sidebar.
3. Enter an IP address to query and click <img src="https://main.qcloudimg.com/raw/38242f38a7e37d681899fe37dfbc6423.png" style="margin:-3px 0px">.
>? You can also call the [`DescribeIpGeolocationInfos`](https://intl.cloud.tencent.com/document/product/215/39094) or [`DescribeIpGeolocationDatabaseUrl`](https://intl.cloud.tencent.com/document/product/215/38901) API to query the IP location.

