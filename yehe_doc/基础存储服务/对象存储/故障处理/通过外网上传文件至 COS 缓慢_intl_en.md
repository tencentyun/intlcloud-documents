## Symptom

- **Symptom 1**: <span id="FaultPhenomenon1"></span>
 - The upload speed is low (below 8 Mbps) over a home network, while it is normal over a corporate network.
 - The upload speed is low (below 8 Mbps) over a corporate network, while it is normal over a 4G network.
- **Symptom 2**: <span id="FaultPhenomenon2"></span>The upload is slow at a custom domain name.

## Possible Causes

- Symptom 1
 1. The speed is low due to your ISP and network conditions.
 2. CORS is used and thus the speed is low.
- Symptom 2: CNAME resolves the custom domain name to other products (e.g., Content Delivery Network (CDN), Cloud Virtual Machine (CVM), or Anti-DDoS) before resolving to COS.

## Solutions

- [Symptom 1](#FaultPhenomenon1): Check the network conditions of your client. For detailed directions, see [Troubleshooting client network issues](#SearchTheClientNetwork).
- [Symptom 2](#FaultPhenomenon2): Reduce the intermediate links by modifying the DNS record for your custom domain name to improve the transfer efficiency. For detailed directions, see [Modifying custom domain name's DNS record](#ModifyCustomDomainNameResolution).

## Troubleshooting

<span id="SearchTheClientNetwork"></span>
### Troubleshooting client network issues

1. Run the following command to check whether the ISP of the IP address is the same as that of the client network:
```
ping COS domain name
```
For example:
```
ping examplebucket-1250000000.cos.ap-beijing.mqcloud.com
```
 - If so, proceed to [step 3](#step03).
 - If not, proceed to [step 2](#step02).
2. <span id="step02"></span>Check whether a proxy is enabled in the browser (with Chrome as an example).
    1. Open Chrome and click <img src="https://main.qcloudimg.com/raw/41a048f92c3d6160faff7e211bacce76.png"/> > **Settings** in the top-right corner.
    2. Click **Advanced**. On the **System** page, click **Open your computer's proxy settings** to open the configuration window of your OS.

    Check whether a proxy is enabled.
     - If so, disable the proxy.
     - If not, proceed to [step 3](#step03).
3. <span id="step03"></span>Check whether your Wi-Fi router limits the speed.
 - If so, allocate the bandwidth as needed.
 - If not, proceed to [step 4](#step04).
4. <span id="step04"></span>Test the performance of the upload to COS over the current network.
The following example uses a 20 MB object and COSCMD to test the upload and download speeds:
```
coscmd probe -n 1 -s 20
```
A message similar to the following will be displayed, from which you can get the average, min, and max speeds:
![](https://main.qcloudimg.com/raw/2fcecb96df04acc6b0c32c120ccb3c39.png)
5. Visit [Speed Test](https://www.speedtest.net/) to test the speed. Then, compare the tested speed with the data obtained in [step 4](#step04) to determine whether the client has used the maximum bandwidth.
 - If the speeds obtained in step 4 are below the client bandwidth, [contact us](https://intl.cloud.tencent.com/contact-sales).
 - If the speeds obtained in step 4 equal to the client bandwidth but don't reach the speed promised by your ISP, contact your ISP.
 - If the speeds obtained in step 4 equal to the client bandwidth and reach the bandwidth promised by your ISP, proceed to [step 6](#step06).
6. <span id="step06"></span>Check whether the client is accessing a bucket residing in another country/region.
 - If so, we recommend you enable COS' global acceleration feature.
 - If not, [contact us](https://intl.cloud.tencent.com/contact-sales).

<span id="ModifyCustomDomainNameResolution"></span>
### Modifying custom domain name's DNS record

1. Check whether the custom domain name is resolved to a COS domain name.
 - If so, [contact us](https://intl.cloud.tencent.com/contact-sales).
 Common COS domain names are as follows:
```
XXX.cos.ap-beijing.myqcloud.com  (default COS domain name)
XXX.cos.accelerate.myqcloud.com (COS global acceleration domain name)
XXX.cos-website.ap-beijing.myqcloud.com (COS static website domain name)
XXX.picbj.myqcloud.com (COS' default CI domain name)
```
 - If not, proceed to [step 2](#2_step02).
Common non-COS domain names are as follows: 
```
XXX.file.myqcloud.com or XXX.cdn.dnsv1.com (Tencent Cloud CDN's default domain names)
XXX.w.kunlungr.com (Alibaba Cloud CDN's default domain name)
```
2. <span id="2_step02"></span>Resolve the custom domain name to the desired COS domain name via the CNAME record and upload data.
For example, `upload.mydomain.com  cname XXX.cos.ap-beijing.myqcloud.com`. For detailed directions, see [Enabling Custom Origin Domains](https://intl.cloud.tencent.com/document/product/436/31507).
3. Modify the default COS domain name of the client.
The following uses C# as an example:
```
CosXmlConfig config = new CosXmlConfig.Builder()
.SetConnectionTimeoutMs(60000) // Set the connection timeout period in milliseconds, which is 45,000 ms by default.
.SetReadWriteTimeoutMs(40000) // Set the read/write timeout period in milliseconds, which is 45,000 ms by default.
.IsHttps(true) // Set HTTPS as the default request method. 
.SetAppid(appid) // Set the APPID of your Tencent Cloud account
.SetRegion(region) // Set the default bucket region.
.SetHost("XXXXXX.com") // Enter the custom domain name.
.SetDebugLog(true) .Build(); // Create the CosXmlConfig object.
```
For more information on how to call other SDKs, see [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).

