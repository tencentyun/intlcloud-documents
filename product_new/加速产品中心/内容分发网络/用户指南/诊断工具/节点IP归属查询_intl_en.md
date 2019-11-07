## Features
CDN offers a tool for querying IP ownership. This tool can be used to verify whether a specified IP is of a CDN global cache node, and check the IP’s acceleration service region, district, and ISP.
## Applicable Scenarios
This tool can be used for troubleshooting. When there is access exception, you can query the IP accessed in the following ways:
- If the IP is not of a CDN node, domain name resolution may be exceptional. Please go to your DNS service provider and check whether the CNAME configuration is correct;
- If the IP is of a CDN node, you can check the node service status to see whether node activation/deactivation operations have led to request interruptions.

## Operation Guide
### Query Method
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and select **Inspect Tool** > **Verify Tencent IP Tool** on the left sidebar.
![](https://main.qcloudimg.com/raw/2cef9ef14588bf79841e072d5eecc04a.png)
### Usage Constraints
- Enter the IP addresses to be verified in the text box (one address per line).
- Up to 20 IP addresses can be verified at a time.
- Verification of IPv4 and IPv6 addresses is supported.
- Verification is supported for global cache nodes. For nodes in Mainland China, data of the ISP in the corresponding district will be returned; for nodes outside Mainland China, data of the corresponding country/region will be returned.
- You can view the node service status **for the past 3 hours**. If there were online/offline status changes, the corresponding operation time will be displayed.

## Use Cases
### Nodes in Mainland China
![](https://main.qcloudimg.com/raw/8b6d72d95c45a1ddc3a5f7fe47f0a189.png)
### Nodes Outside Mainland China
![](https://main.qcloudimg.com/raw/df019c3d710a6a206e1eefa90338403d.png)
### IPv6 Ownership Query
>! IPv6 acceleration is currently in beta. [Submit an application](https://cloud.tencent.com/apply/p/own2eu41dg8) if you want to use this feature.
>
![](https://main.qcloudimg.com/raw/d6489b1f3f74ae740873f50a2fd42c3b.png)







