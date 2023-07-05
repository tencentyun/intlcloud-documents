## When do I need to verify my domain name?
1. When you connect a domain name, such as `a.example.com`, for the first time, the same-level domain names, such as `b.example.com`, and subdomain names can be directly connected without verification. However, if you want to connect second-level domain names, such as `example.com`, ownership verification is required.
2. The subdomain names that are connected under another account must be verified. If the subdomain names pass the verification, you can connect the subdomain names under the current account.
3. The same-level wildcard domain names that you want to connect must be verified. If you connected a domain name, such as a.example.com, any same-level wildcard domain name must be verified before it is connected, whereas a second-level wildcard domain name, such as `*.a.example.com`, can be directly connected.
4. When your domain name is hosted in Tencent Cloud DNSPod under the current account and is not connected under other accounts, you can quickly access Tencent Cloud CDN without verification. (If the domain name has been accessed by other accounts, please retrieve it after manual verification)

## Method 1: DNS Verification (Recommended)

1. When a domain name that you add requires ownership verification, a message appears below the domain name field to inform you of the requirement details. To view the requirements for verification methods, click **Verification Method**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3D9m056_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230320164010.png)
2. Use the default verification method, which is DNS verification.
To start DNS verification, add the "_cdnauth" host record of the TXT type for the domain name at your DNS provider.
>!In scenarios where multi-level domain names are used, host records must be added only for the domain name regardless of the level of the added domain name, such as `c.b.a.example.com`, `*.example.com`, and `test.example.com`. For example, if you add the `c.b.a.example.com` subdomain name, you must add the `_cdnauth.example.com` resolution record.
>

![](https://staticintl.cloudcachetci.com/yehe/backend-news/wG8y738_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230320164127.png)
**To add a resolution record of Tencent Cloud DNS, perform the following operations:**
If your DNS provider is Tencent Cloud, log in to the [DNSPod console](https://console.cloud.tencent.com/cns), find the target domain name, click **DNS**, and add a TXT record. Set the **Host** parameter to `_cdnauth`, the **Record Type** parameter to `TXT`, and the **Record Value** parameter to the record value provided by Tencent Cloud CDN. Use the default settings for other parameters.
**To add a resolution record of Alibaba Cloud DNS, perform the following operations:**
If your DNS provider is Alibaba Cloud, log in to the DNS console of Alibaba Cloud, find the target domain name, and click **DNS Settings** in the **Actions** column. Set the **Record Type** parameter to `TXT`, configure the **Hostname** and **Record Value** parameters, and use the default settings for other parameters.

3. Wait for the TXT record to take effect before you click the verification button to start verification. If the domain name fails to be verified, make sure that the TXT record is valid and has taken effect at the DNS provider. For information on how to check whether the TXT record has taken effect, see the related documentation.
4. After the domain name is verified, check whether the domain name is connected under another account. If yes, click **Retrieve** to retrieve the domain name. After the domain name is retrieved, the settings that are configured for the domain name under another account are cleared.


## Method 2: File Verification
1. When a domain name that you add requires ownership verification, a message appears below the domain name field to inform you of the requirement details. To view the requirements for verification methods, click **Verification Method**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3D9m056_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230320164010.png)
2. Click the **File verification** tab.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/aSWm077_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230320165516.png)
3. Click **verification.html** to download the file for verification.
4. Upload the file to the root directory on the server of your domain name, such as a Tencent Cloud Cloud Virtual Machine (CVM) instance, a Tencent Cloud Object Storage (COS) bucket, an Alibaba Cloud Elastic Compute Service (ECS) instance, or an Alibaba Cloud Object Storage Service (OSS) bucket. For example, if your domain name is `test.example.com`, you must upload the file to the `example.com/` or `test.example.com/` root directory.
>!You can perform verification by uploading the file to a subdomain name only if you use the file verification method.
5. Make sure that the file is accessible via `http://example.com/verification.html` or `http://test.example.com/verification.html` before you click **Verify**. Your domain name will be successfully verified if the record you added is consistent with the content of the file. If the domain name cannot be verified, check whether the record and the content of the file are consistent.
6. After the domain name is verified, check whether the domain name is connected under another account. If yes, click **Retrieve** to retrieve the domain name. After the domain name is retrieved, the settings that are configured for the domain name under another account are cleared.


**Example:**
In this example, the acceleration domain name is `a.test.com` and the origin server is a COS biucket.
1. Upload the verification.html file to the root directory of COS.
2. Add a CNAME record for the acceleration domain name at your DNS provider. Set the **Record value** parameter to the COS domain name.
3. Check whether the verification.html file is accessible via http(https)://Acceleration domain name/verification.html. Click **Verify**.

## Method 3: API Operation Verification
1. Call the CreateVerifyRecord operation to generate a TXT resolution record for an acceleration domain name.
```
{
  "Response":{
    "Record": "202009071516044acd018wf498457628cn75ba018ec9cv",
    "RecordType": "TXT"
    "RequestId": "8518c99c-a8eb-4930-a7d0-eff586d9cc37",
    "SubDomain": "_cdnauth",
   }
}
```
2. Add the TXT resolution record at your DNS provider, such as DNSPod.
3. Call the VerifyDomainRecord operation to check whether the resolution record takes effect.
```
{
  "Response":{
    "RequestId": "b6926bb2-d0b5-42bc-b17f-e4402bdb9e9b",
    "Result": "true"
   }
}
```
4. If the resolution record takes effect, call the [AddCdnDomain](https://www.tencentcloud.com/document/product/228/34015) operation to add the domain name.


## FAQs
[](id:q1)
### How do I know whether a TXT record takes effect?
**Windows:**
If the domain name that you connected is `test.example.com`, open the command prompt and run the `nslookup -qt=txt _cdnauth.example.com` command. Check whether the TXT record takes effect or is valid based on the output.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/7VQU778_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230310151540.png" width="70%">
**Linux or macOS:**
If the domain name that you connected is `test.example.com`, open the command prompt and run the `dig _cdnauth.example.com txt` command. Check whether the TXT record takes effect or is valid based on the output.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6b65e488b8b52745e8a6a4431c112975.png" width="70%">

### Why do I get an error that the VOD domain name cannot be accessed?
It’s because your domain name has already been added to the VOD console. If you want to manage the domain name in the CDN console, it must be deleted from the VOD console and wait about 1 minute before adding it to the CDN console, or access other subdomain names. 
