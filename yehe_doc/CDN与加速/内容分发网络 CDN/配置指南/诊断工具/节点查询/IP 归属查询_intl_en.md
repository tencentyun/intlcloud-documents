## Feature Overview
CDN offers a tool for querying IP ownership. This tool can be used to verify whether a specified IP is of a CDN global cache node, and check the IP's acceleration service region, district, and ISP.
## Overview
This tool can be used for troubleshooting. When there is an access exception, you can query the IP accessed in the following ways:
- If the IP is not of a Tencent Cloud CDN node, the problem may be caused by domain name resolution exception. Please go to your DNS service provider and check whether the CNAME configuration is correct;
- If the IP is of a Tencent Cloud CDN node, you can check the node service status to see whether requests are interrupted by node activation/deactivation.

## Operation Guide
### Query Method
Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and select **Inspect Tool** -> **Verify Tencent Cloud CDN IP** on the left sidebar.
![](https://main.qcloudimg.com/raw/7c72a39a1c0f33e633057d02af9c3a6f.png)
### Use Limits
- Enter the IP addresses to be verified in the text box (one address per line).
- Up to 20 IP addresses can be verified at a time.
- Verification of IPv4 and IPv6 addresses is supported.
- Verification is supported for global cache nodes. For nodes in the Chinese mainland, data of the ISP in the corresponding district will be returned; for nodes outside the Chinese mainland, data of the corresponding country/region will be returned.
- You can view the node service status **for the last 3 hours**. If there were activation/deactivation status changes, the corresponding operation time will be displayed.

## Use Cases
### Nodes in the Chinese mainland
![](https://main.qcloudimg.com/raw/92a04bfdc0905c9be0465d3dc4825dd3.png)
### Nodes outside the Chinese mainland
![](https://main.qcloudimg.com/raw/6a2e1b6f94362d5508ed98a52bd2d125.png)







