## When do I need to verify my domain name?
1. When you access a third-level domain name (e.g., a.example.com) for the first time, the same-level domain names (e.g., b.example.com) and subdomain names can be accessed directly without verification, while to access the second-level domain names (e.g., example.com), ownership verification is needed.
2. The subdomain names that have been accessed under another account need to be verified. If you pass the verification, you can access them under the current account.
3. The same-level wildcard domain names to access need to be verified. Supposing you have accessed a third-level domain name, e.g., a.example.com, any same-level wildcard domain name requires verification, while a subdomain name such as *.a.example.com can be accessed directly.

## Method 1: DNS Verification (Recommended)
1. When a domain name that you’re adding requires ownership verification, you’ll be asked to do so. In this case, click **Verification Method**.
![](https://qcloudimg.tencent-cloud.cn/raw/1c6915b095d74f4358923be2ec7740dd.png)
2. Use the default verification method, DNS verification.
To start DNS verification, add a host record of type TXT "_cdnauth" for the domain name at your DNS provider.
>!
When you add a subdomain name, the host record value to the main domain name. Assuming that the added subdomain name is c.b.a.example.com, you need to add a resolution record as _cdnauth.example.com.
![](https://qcloudimg.tencent-cloud.cn/raw/e1da0524ad0781544052fd65195d9798.png)
Then wait for the TXT record value to take effect before clicking **Verify** below to start verification. If the domain name fails to be verified, make sure that the TXT record value is valid, and it has taken effect at the DNS provider.

## Method 2: File Verification
1. When a domain name that you’re adding requires ownership verification, you’ll be asked to do so. In this case, click **Verification Method**.
![](https://qcloudimg.tencent-cloud.cn/raw/140a8b980bd0c30c0336dcd8f8e3607e.png)
2. Choose **File verification**.
![](https://qcloudimg.tencent-cloud.cn/raw/8883258277fef3bf2e42ceffb489324a.png)
3. Click **verification.html** to download the file.
4. Upload the file to the root directory of your domain name’s server (such as Tencent Cloud CVM or COS, and Alibaba Cloud ECS or OSS). Assuming your domain name is test.example.com, then you need to upload the file to the root directory example.com.
5. Make sure the file is accessible via http://example.com/verification.html before clicking **Verify**. Your domain will get successfully verified if the record value you added is consistent with the file. If it can’t be verified, check the above file link and the file uploaded.

## FAQs
### How do I know whether TXT record values take effect?
Windows:
Suppose your accessed domain name is test.example.com. Open the Command Prompt and enter `nslookup -qt=txt _cdnauth.example.com`. Based on the output, you can determine whether the TXT record value is effective or correct.
![](https://qcloudimg.tencent-cloud.cn/raw/1728c7c311e4db18fc28287299ab2068.png)

Linux/Mac:
Supposing your accessed domain name is test.example.com, enter `dig _cdnauth.example.com txt` in the command interface. Based on the output, you can determine whether the resolution record is effective or correct.
![](https://qcloudimg.tencent-cloud.cn/raw/d07ca2df386f12185af00abe813d4b60.png)

### Why do I get an error that the VOD domain name cannot be accessed?
It’s because your domain name has already been added to the VOD console. If you want to manage the domain name in the CDN console, it must be deleted from the VOD console and wait about 1 minute before adding it to the CDN console, or access other subdomain names.

