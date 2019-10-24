### When a file is updated (re-uploaded or deleted) in COS, its cached content remains unchanged in CDN, resulting in inconsistency with the origin server. Can the cache in CDN be purged automatically when the file in COS is updated?

COS itself does not support automatically purging the cache in CDN. You can set up automatic purge in CDN with Serverless Cloud Function (SCF). For more information, see [Using SCF to Automatically Refresh COS Resources Cached in CDN](https://intl.cloud.tencent.com/document/product/436/30611).

### When I manage domain names in the console, I am always prompted to "Enable at least one available key". What should I do?

Log in to the [CAM Console](https://console.cloud.tencent.com/cam/capi) to check whether the TencentCloud API key is enabled.

- If no, create and enable a key before managing domain names.
- If yes and the error persists, check whether the account you are using is a sub-account (collaborator or sub-user):
  - If it is a sub-account, log in using the root account and confirm that the TencentCloud API key is enabled;
  - If it is a root account, refresh the browser cache and log in to the Tencent Cloud account again.

### How do I access objects with my own domain name?

This can be achieved by binding a custom domain name. For more information, see [Enabling Custom Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/18424#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.8A.A0.E9.80.9F.E5.9F.9F.E5.90.8D).

### Does COS support HTTPS access?

Yes. COS allows SSL transfer for access nodes in all [regions](https://intl.cloud.tencent.com/document/product/436/6224), and HTTPS is enabled by default in the SDK and console. **You are strongly recommended to use HTTPS to protect the data linkage during transfer. If you use unencrypted HTTP, the linkage may be monitored or the data may be stolen.**

### Does COS support CDN origin-pull with HTTPS?

Yes.

### Do I have to obtain an ICP filing for my custom domain name through Tencent Cloud?
Currently, CDN has to be enabled before COS can use a custom domain name. Please note the following points based on your actual situation:

- If your domain name is connected to a CDN node in Mainland China, you need to obtain an ICP filing for it. However, you are not required to do so through Tencent Cloud, and it is okay as long as your domain name has obtained the ICP filing.
- If your domain name is connected to a CDN node outside Mainland China, you don't need to obtain an ICP filing for it.

### How do I generate a temporary URL for a file in COS?

For directions, see [Download via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14116).

### Can I access private-read buckets via CDN acceleration?

Yes, but you need to be authorized with relevant configurations first. For more information, see [Private-Read Bucket](https://intl.cloud.tencent.com/document/product/436/18669#.E7.A7.81.E6.9C.89.E8.AF.BB.E5.AD.98.E5.82.A8.E6.A1.B6) in the CDN Acceleration Overview document.

### After the origin server is changed in the CDN Console, why does the original custom domain name disappear in the COS Console?
>If you use the COS Console v5 configured with a JSON domain name, the console cannot display the new domain name.

Check whether the JSON domain name is configured in your bucket, and if yes, modify the JSON domain name to an XML domain name.


<a id="gcd"></a>
### Can I access the Global Content Delivery (GCD) platform using a domain name without an ICP filing?

ICP filing is not required for GCD. However, it should be noted that your data and operations in Tencent Cloud should comply with local laws and regulations as well as [Tencent Cloud Terms of Service](https://intl.cloud.tencent.com/document/product/301/9248).

### Can Global Content Delivery (GCD) be used to accelerate COS in Mainland China?

Yes. However, for national policy reasons, GCD can pull data in Mainland China and users in Mainland China can access global nodes only over public ISP networks, which means that the access may be slow or fail. Therefore, you are recommended to use the URL prefetch feature of GCD to cache hotspot files in advance.

