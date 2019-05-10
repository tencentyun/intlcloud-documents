### When a file is updated (re-uploaded or deleted) on COS, its cached content remains unchanged in CDN, resulting in inconsistency with the origin server. Can the cache in CDN be refreshed automatically when the file on COS is updated?

COS itself does not support automatic refresh of cache in CDN. You can set up automatic refresh of cache in CDN with Serverless Cloud Function (SCF). For more information, see [Automatically Refresh COS Resources Cached in CDN Using SCF](https://cloud.tencent.com/document/product/436/30434).

### When I manage domain names on the console, I am always prompted to "Enable at least one available key". What should I do?

Log in to the [CAM Console](https://console.cloud.tencent.com/cam/capi) to check if the cloud API key is enabled.

- If the cloud API key is not enabled, create and enable a key before managing domain names.
- If the cloud API key is enabled and you are still prompted, check whether the account you are operating with is a sub-account (collaborator's or sub-user's account):
  - If it is a sub-account, log in using the primary account and confirm that the cloud API key is enabled;
  - If it is a primary account, refresh the browser cache and log in to the Tencent Cloud account again.

### How do I access objects with my own domain name?

This can be achieved by binding a custom domain name. For more information, see [Custom Acceleration Domain Name](https://cloud.tencent.com/document/product/436/18424#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.8A.A0.E9.80.9F.E5.9F.9F.E5.90.8D).

### Does COS support HTTPS access?

Yes. COS allows SSL transport for all access nodes in the [available regions](https://cloud.tencent.com/document/product/436/6224), and HTTPS is enabled by default in the SDK and console. **COS strongly recommends you use HTTPS to protect the data linkage for transport. If you use unencrypted HTTP, the linkage may be monitored or the data may be stolen.**

### Does COS support CDN origin-pull with HTTPS?

Yes.

### Must the custom domain name be ICP filed by Tencent Cloud if I use it?

At present, domain names for accessing COS need to be filed, both at home and abroad, but Tencent Cloud ICP filing is not required.

### How do I generate a temporary URL for files in COS?

For more information, see [Pre-signed Authorization Download](https://cloud.tencent.com/document/product/436/14116).

### Can I access private-read buckets via CDN acceleration?

Yes, but you need to be authorized with related configurations first. For more information, see [Private-Read Bucket](https://cloud.tencent.com/document/product/436/18669#.E7.A7.81.E6.9C.89.E8.AF.BB.E5.AD.98.E5.82.A8.E6.A1.B6) in the CDN Acceleration Overview documentation.

### When the origin server is changed in the CDN Console, why does the original custom domain name disappear in the COS Console ?
>!If you use the Console V5 configured with JSON domain name, the COS V5 Console cannot display the new domain name.

Check whether the JSON domain name is configured in your bucket, and modify the JSON domain name to XML domain name.


<a id="gcd"></a>
### Can I access the overseas acceleration GCD platform via unfiled domain names?

Filing is not required for overseas acceleration, but note that the data and operations on Tencent Cloud still need to comply with the laws and regulations of relevant countries/regions and [Tencent Cloud Service Agreement](https://cloud.tencent.com/document/product/301/1967).

### Can overseas acceleration GCD be used to accelerate domestic COS?

Yes. However, due to policies, the public ISP's network must be used when the overseas acceleration platform GCD pulls the data in Mainland China from the origin server or the Mainland Chinese users access overseas nodes. The access speed may be unsatisfactory and even the website cannot be accessed. You are suggested to use the URL prefetch feature of overseas acceleration GCD to cache hotspot files in advance.


