
## Error Description
When you apply for a free DV SSL certificate, the following message is displayed:
![](https://main.qcloudimg.com/raw/89a308c1e2dfa481aba018db2869beb0.png)

## Possible Causes
Due to CA's anti-phishing mechanism, sensitive words contained in domain names, such as "bank" and "pay", can cause security review failure. Specific sensitive words are defined by the CA. Some less commonly used root domain names may also result in review failure. For example, root domain names suffixed with .pw, such as `www.qq.pw` and `www.qcloud.pw`, will not pass the review.

## Solutions
You can:
- Purchase a paid SSL certificate to bind to your domain.
- Apply for another domain that does not contain sensitive words.
