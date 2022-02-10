
## Error Description
When you apply for a free DV SSL certificate, the following message is displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/897f9d3bd2391144b73a916d4a28a59c.png)

## Common Causes
Due to CA’s anti-phishing mechanism, sensitive words contained in domain names, such as “bank” and “pay”, can cause security verification failures. Specific sensitive words are defined by CAs. Some less commonly used root domain names may also result in verification failures. For example, root domain names with .pw suffix, such as `www.qq.pw` and `www.qcloud.pw`, will fail to pass the verification.

## Solution
You can:
- Purchase a non-DV SSL certificate to bind to your domain.
- Apply for a domain that does not contain sensitive words.

