## Symptoms

- **Symptom 1**: <span id="FaultPhenomenon1"></span>
 - The upload speed is slow (below 8 Mbps) over a home network, while it is normal over a corporate network.
 - The upload speed is slow (below 8 Mbps) over a corporate network, while it is normal using a 4G network.
- **Symptom 2**: <span id="FaultPhenomenon2"></span>The upload is slow using a custom endpoint.

## Possible Causes

- Symptom 1
 1. The speed slow due to your ISP and networking condition.
 2. CORS is used and thus the speed is slow.
- Symptom 2: CNAME maps the custom endpoint to other products (e.g., Content Delivery Network (CDN), Cloud Virtual Machine (CVM), or Anti-DDoS) before mapping to COS.

## Solutions

- [Symptom 1](#FaultPhenomenon1): Check the network condition of your client. For detailed directions, please see [Troubleshooting Client-Side Network](#SearchTheClientNetwork).
- [Symptom 2](#FaultPhenomenon2): Reduce the intermediate links by modifying the DNS record for your custom endpoint to improve the transfer efficiency. For detailed directions, please see [Modifying custom endpoint’s DNS record](#ModifyCustomDomainNameResolution).

## Troubleshooting Procedure

<span id="SearchTheClientNetwork"></span>
### Checking the client-side network

1. Run the following command to check whether the IPS of the IP address is the same as that of the client:
```
ping COS endpoint
```
Example:
```
ping examplebucket-1250000000.cos.ap-beijing.mqcloud.com
```
 - If yes, skip to [Step 3](#step03).
 - If not, perform [Step 2](#step02).
2. <span id="step02"></span>Check whether a proxy is enabled in the browser (Chrome is taken as an example).
    1. Open Chrome and click <img src="https://main.qcloudimg.com/raw/41a048f92c3d6160faff7e211bacce76.png"/> > **Settings**.
    2. Click **Advanced**. In the **System** area, click **Open your computer’s proxy settings** to open the configuration window of your OS.

    Check whether a proxy is enabled.
     - If yes, disable the proxy.
     - If not, perform [Step 3](#step03).
3. <span id="step03"></span>Check whether your Wi-Fi router limits the speed.
 - If yes, allocate the bandwidth as needed.
 - If not, perform [Step 4](#step04).
4. <span id="step04"></span>Test the performance of the upload to COS using the current network.
The following example uses a 20 MB object and COS’s COSCMD to test the upload and download speeds:
```
coscmd probe -n 1 -s 20
```
A message similar to the following will be displayed, from which you can get the Average/Min/Max speeds:
![](https://main.qcloudimg.com/raw/2fcecb96df04acc6b0c32c120ccb3c39.png)
5. Browse [Speed Test](https://www.speedtest.net/) to test the speed and compare the tested speed with data obtained in [Step 4](#step04) to determine whether the client has used the maximum bandwidth.
 - If the speeds obtained in Step 4 are slower than the client bandwidth, please [contact us](https://intl.cloud.tencent.com/support).
 - If the speeds obtained in Step 4 equal to the client bandwidth but have not reached the speed promised by your ISP, please contact your ISP.
 - If the speeds obtained in Step 4 equal to the client bandwidth and reached the bandwidth promised by your ISP, please perform [Step 6](#step06).
6. <span id="step06"></span>Check whether the client is accessing a bucket residing in a region in another country.
 - If yes, you are advised to enable COS’s Global Acceleration feature.
 - If not, please [contact us](https://intl.cloud.tencent.com/support).

<span id="ModifyCustomDomainNameResolution"></span>
### Modifying DNS record for your custom endpoint

1. Check whether the custom endpoint is mapped to a COS endpoint.
 - If yes, please [contact us](https://intl.cloud.tencent.com/support).
 Common COS endpoints are as follows:
```
XXX.cos.ap-beijing.myqcloud.com  (default COS endpoint)
XXX.cos.accelerate.myqcloud.com (COS global acceleration endpoint)
XXX.cos-website.ap-beijing.myqcloud.com (COS static website endpoint)
XXX.picbj.myqcloud.com (COS’s default CI endpoint)
```
 - If not, perform [Step 2](#2_step02).
Common non-COS endpoints are as follows: 
```
XXX.file.myqcloud.com or XXX.cdn.dnsv1.com (Tencent Cloud’s CDN default endpoint)
XXX.w.kunlungr.com (aliyunCDN default endpoint)
```
2. <span id="2_step02"></span>Map the custom endpoint to the desired COS endpoint in the CNAME and upload data.
Example: `upload.mydomain.com  cname XXX.cos.ap-beijing.myqcloud.com`. For detailed directions, please see [Enabling Custom Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/31507).
3. Modify the default COS endpoint of the client.
The following uses C# as an example:
```
CosXmlConfig config = new CosXmlConfig.Builder()
.SetConnectionTimeoutMs(60000)  // Set the connection timeout in milliseconds. Defaults to 45000.
.SetReadWriteTimeoutMs(40000)  // Set the read/write timeout period in milliseconds, which is 45,000 ms by default
.IsHttps(true)  // Set HTTPS as default request method 
.SetAppid(appid)  // Sets the APPID of your Tencent Cloud account
.SetRegion(region)  // Sets the default bucket region
.SetHost("XXXXXX.com") // Enter the custom endpoint.
.SetDebugLog(true) .Build(); // Create the CosXmlConfig object.
```
For more information about how to call other SDKs, please see [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).
