## Features
CDN offers a tool for querying IP ownership. This tool can be used to verify whether a specified IP is of a CDN global cache node, and check the IP’s acceleration service region, district, and ISP.
## Applicable Scenarios
This tool can be used for troubleshooting. When there is access exception, you can query the IP accessed in the following ways:
- If the IP is not of a CDN node, domain name resolution may be exceptional. Please go to your DNS service provider and check whether the CNAME configuration is correct;
- If the IP is of a CDN node, you can check the node service status to see whether node activation/deactivation operations have led to request interruptions.

## Operation Guide
### Query Method
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and select **Inspect Tool** > **Verify Tencent IP Tool** on the left sidebar.
![](https://main.qcloudimg.com/raw/7c72a39a1c0f33e633057d02af9c3a6f.png)
### Usage Constraints
- Enter the IP addresses to be verified in the text box (one address per line).
- Up to 20 IP addresses can be verified at a time.
- Verification of IPv4 and IPv6 addresses is supported.
- Verification is supported for global cache nodes. For nodes in Mainland China, data of the ISP in the corresponding district will be returned; for nodes outside Mainland China, data of the corresponding country/region will be returned.
- You can view the node service status **for the past 3 hours**. If there were online/offline status changes, the corresponding operation time will be displayed.

## Use Cases
### Nodes in Mainland China
![](https://main.qcloudimg.com/raw/dc8780895ef36d9e1676e35a12b21726.png)
### Nodes Outside Mainland China
![](https://main.qcloudimg.com/raw/83950ca0bfc7ecce0cf4bd8172dd8ba9.png)
### IPv6 Ownership Query
> IPv6 acceleration is currently in beta. [Submit an application](https://cloud.tencent.com/apply/p/own2eu41dg8) if you want to use this feature.
>
![](https://main.qcloudimg.com/raw/73bf5aab29c934452a97984527cd945f.png)







