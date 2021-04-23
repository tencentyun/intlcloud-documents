## FAQs about Access and Acceleration

### How do I access objects with my own domain name?

This can be achieved by binding a custom domain name. For more information, see [Custom Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

### Does COS support HTTPS access?

Yes. COS allows SSL transport for all access nodes in the [available regions](https://intl.cloud.tencent.com/document/product/436/6224), and HTTPS is enabled by default in the SDK and console. **COS strongly recommends you use HTTPS to protect the data linkage for transport. If you use unencrypted HTTP, the linkage may be monitored or the data may be stolen.**

### How do I enable CDN for COS?

For more information, see [Enabling Default CDN Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/436/31505) and [Enabling Custom CDN Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

### Does COS support CDN origin-pull with HTTPS?

Yes. For more information, see [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508).

### How to configure HTTPS access for a custom domain name?

If you have bound the bucket to your own domain name, and enabled CDN acceleration, you can configure HTTPS access in the [CDN Console](https://console.cloud.tencent.com/cdn). For more information, see [HTTPS Acceleration Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213).
If you haven’t used CDN, you can alternatively configure a reverse proxy for the domain name and resolve it to the server. For more information, see [Configuring Custom Domain Names to Support HTTPS Access](https://intl.cloud.tencent.com/document/product/436/11142).

### How do I generate a temporary URL for files in COS?

For more information, see [Download via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14116).

### Can I access private-read buckets via CDN acceleration?

Yes, if you set permissions configuration as required. For specific configuration, see the “Private-read buckets” section in [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).

### Can overseas acceleration GCD be used to accelerate domestic COS?

Yes. However, due to policies, the public ISP's network must be used when the overseas acceleration platform GCD pulls the data in Mainland China from the origin server or the Mainland Chinese users access overseas nodes. The access speed may be unsatisfactory and even the website cannot be accessed. You are suggested to use the URL prefetch feature of overseas acceleration GCD to cache hotspot files in advance.


### What should I do if COS denies my access request with allowed headers after I configured CORS?

To find the reason for the deny:
1. Check if your configuration is consistent with the headers you include, especially for the presence of invisible characters, such as spaces.
2. Check the domain name with which you initiate the request. If you use a CDN acceleration domain name, you need to configure CORS in the CDN console. See [Custom Response Header Configuration](https://intl.cloud.tencent.com/document/product/228/35320).
3. Check the permissions of your bucket and determine whether your access will be granted.
4. Check if any error is reported due to your browser's cache. To fix this, you can use Ctrl + F5 to forcibly refresh your browser, or select “Disable cache” in the **Network** tab of your browser.


## FAQs about Domain Names and Other Issues


### When I manage domain names on the console, I am always prompted to ""Enable at least one available key"". What should I do?

Log in to the [CAM Console](https://console.cloud.tencent.com/cam/capi) to check if the cloud API key is enabled.

- If the cloud API key is not enabled, create and enable a key before managing domain names.
- If the cloud API key is enabled and you are still prompted, check whether the account you are operating with is a sub-account (collaborator's or sub-user's account):
  - If it is a sub-account, log in using the root account and confirm that the cloud API key is enabled;
  - If it is a root account, purge the browser cache and log in to the Tencent Cloud account again.

### Must the custom domain name be ICP filed by Tencent Cloud if I use it?
Currently, you need to enable CDN service to use a custom domain name in COS.

- For domain names connected to a CDN node in Mainland China, you need to complete ICP filing. You are not required to do so through Tencent Cloud though.
- If your domain name is connected to a CDN node outside Mainland China, you don't need to obtain an ICP filing for it.

### When the origin server is changed in the CDN Console, why does the original custom domain name disappear in the COS Console?

>If you use the Console V5 configured with JSON domain name, the COS V5 Console cannot display the new domain name.

Check whether the JSON domain name is configured in your bucket, and modify the JSON domain name to XML domain name.

<a id="gcd"></a>
### Can I access the overseas acceleration GCD platform via unfiled domain names?

ICP filing is not required for GCD. However, it should be noted that your data and operations in Tencent Cloud should comply with local laws and regulations as well as [Tencent Cloud Terms of Service](https://intl.cloud.tencent.com/document/product/301/12905).

### When a file is updated (re-uploaded or deleted) on COS, its cached content remains unchanged in CDN, resulting in inconsistency with the origin server. Can the cache in CDN be purged automatically when the file on COS is updated?

COS itself does not support automatic purging of CDN cache, a feature you should use with the help of Serverless Cloud Function (SCF). For more information, see Using SCF to Automatically Purge COS Resources Cached in CDN.
