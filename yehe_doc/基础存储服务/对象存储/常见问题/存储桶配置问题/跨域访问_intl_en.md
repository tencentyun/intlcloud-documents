### What is CORS and how do I enable it?

Cross-origin resource sharing (CORS) is to request resources over HTTP from a domain for another domain. Two origins that differ in protocol, domain name, or port are treated as different origins. To enable cross-origin access, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318) or the best practice documentation [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/11488).

### What should I do if COS denies my access request with headers in the allowlist after I configure CORS?

If your access request is denied, troubleshoot the issue as follows:
1. Check that your configuration is consistent with the headers your request includes, especially for the presence of invisible characters, such as spaces.
2. Check the domain name with which you initiate the request. If you use a CDN acceleration domain name, you need to configure CORS in the CDN console. For operation details, see [HTTP Response Header](https://intl.cloud.tencent.com/document/product/228/35320).
3. Check the permissions of your bucket and determine whether your access will be granted.
4. Check if any error is reported due to your browser's cache. If such an error exists, press **Ctrl + F5** to forcibly refresh your browser, or select **Disable cache** on the **Network** tab of your browser.


### How do I configure the file headers in the bucket to return "Access-Control-Allow-Origin:* "?

Set the origin to `*` when configuring CORS. For more information, see the best practice documentation [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/11488).

### What should I do if the error "get ETag error, add `ETag` to CORS ExposeHeader setting." occurs during an upload operation?

Configure the CORS rule as shown below and try using a different browser to test whether it works. For more information, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/11488).
![](https://main.qcloudimg.com/raw/e2cb8ce626ceaba0058423bb5eb72327.png)

### What should I do if both COS and CDN are used but CORS does not work in COS?

If you are using a CDN acceleration domain name, configure CORS in the CDN console. For operation details, see [HTTP Response Header](https://intl.cloud.tencent.com/document/product/228/35320).

### Does CORS configuration support fuzzy match of origins?

The console supports fuzzy match of second-level domain names.

### What should I do if COS CORS reports an error?

Troubleshoot the issue as follows:
1. Check that CORS rules are configured in the COS console. For operation details, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
2. Check whether a CDN acceleration domain name is used. If yes, you need to configure CORS rules in the CDN console. For operation details, see [HTTP Response Header](https://intl.cloud.tencent.com/document/product/228/35320).
3. If CORS rules are configured, check whether they are effective by running a command in the format of `curl -Lvo /dev/null "<Object address>" -H "origin:<Domain name>"`, for example, `curl -Lvo /dev/null "https://bucketname-1250000000.cos.ap-guangzhou.myqcloud.com/test.png" -H "origin:https://www.baidu.com"`. If the status code 200 is returned, the CORS rules are effective. In that case, clear the browser cache and try again.
4. If the problem persists, try to configure `max-age=0` in the CORS rules.

### Can I add IP addresses to CORS rules?
CORS rules support IP addresses. For more information, see [Setting Cross-Origin Resource Sharing (CORS)](https://intl.cloud.tencent.com/document/product/436/13318).

### What should I do if a CORS error is reported when I use CDN to access files in COS although CDN has been configured in COS?

Enable CORS in the CDN console. For operation details, see [HTTP Response Header](https://intl.cloud.tencent.com/document/product/228/35320).

### What should I do if a CORS error is reported when I access file URLs?

Check whether CORS is configured properly. If yes, we recommend that you clear the browser cache and try again. If the problem persists, try to configure `max-age=0` in the CORS rules. For CORS configuration details, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318).
