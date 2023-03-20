### Does COS limit the upload and download bandwidth?

15 Gbps of upstream and downstream bandwidth for each bucket in a public cloud region in the Chinese mainland, or 10 Gbps for each bucket in other regions. If this threshold is reached, traffic throttling will be triggered. For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### How can I directly preview a file in my browser without downloading it?

You need to specify a correct `Content-Type` header for this file. In addition, the value of `Content-Disposition` cannot be `attachment`. If the browser supports the current file format, it will directly open the file instead of downloading it. For detailed directions, see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).

### How do I directly download a file in my browser without previewing it?

You can go to the [COS console](https://console.cloud.tencent.com/cos5) and set the value of `Content-Disposition` in the custom object headers to `attachment`. For detailed directions, see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).

You can also let your browser pop up a window for the file to be downloaded by setting the value of the request parameter `response-content-disposition` in the GET Object API to `attachment`. For more information, see [GET Object](https://www.tencentcloud.com/document/product/436/7753).

>! To use the `response-*` parameter in a request, the request must be signed.
>

### How do I determine if I am accessing COS over a private network?

The access endpoints of COS use intelligent DNS resolution. For COS access via the Internet (including different ISPs), we will detect and select the optimal linkage for you to access COS. If you have deployed a service in Tencent Cloud to access COS, access within the same region will be automatically directed to a private network address. Cross-region access is not supported in a private network and the COS endpoint is resolved to a public network address by default.

>! The private networks of public cloud regions do not interconnect with those of finance cloud regions.
>

#### How to determine access over a private network

Tencent Cloud products within the same region access each other over a private network by default, incurring no traffic fees. Therefore, we recommend choosing the same region when you purchase different Tencent Cloud products to save on costs.

The following shows how to determine access over a private network:

For example, when a CVM accesses COS, to determine whether a private network is used for access, use the `nslookup` command on the CVM to resolve the COS endpoint. If a private IP is returned, access between the CVM and COS is over a private network; otherwise, it is over a public network.

>? Generally, a private IP address takes the form of `10.*.*.*` or `100.*.*.*`, and a VPC IP address takes the form of `169.254.*.*`.
>

Assume that `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com` is the address of the destination bucket; the `Address: 10.148.214.13` below indicates access is over a private network.

```shell
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com

Server:         10.138.224.65
Address:        10.138.224.65  #53

Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.13
Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.14
```

For more information on private and public network access and connectivity testing, see [COS Access via Private Network and Public Network](https://www.tencentcloud.com/document/product/436/30613).

For the private DNS server addresses of CVM, see [Private Network DNS](https://www.tencentcloud.com/document/product/213/5225).

>! The private IPs of Tencent Cloud BM instances may be different from those of CVM instances, and their formats are usually `9.*.*.*` or `10.*.*.*`. If you have any queries, [contact us](https://intl.cloud.tencent.com/contact-sales).
>

### How do I download a folder?

You can log in to [COSBrowser](https://intl.cloud.tencent.com/document/product/436/11366), select the folder to be downloaded, and click **Download** to download the folder or files in batches. You can also download a folder using the COSCMD tool. For more information, see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).

### What should I do if the error "403 Forbidden" occurs or access permission is rejected when I perform upload/download and other operations?

You can troubleshoot by referring to [403 Error for COS Access](https://www.tencentcloud.com/document/product/436/40105).


### How do I upload or download multiple files using COS?

COS allows you to upload or download multiple files through various methods such as the console, APIs/SDKs, and tools.

- Console: For detailed directions, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321) and [Downloading Objects](https://intl.cloud.tencent.com/document/product/436/13322).
- APIs/SDKs: COS allows you to operate on multiple files by repeatedly calling an API or SDK. For more information, see [Action List](https://intl.cloud.tencent.com/document/product/436/10111) and [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).
- Tools: Use [COSBrowser](https://intl.cloud.tencent.com/document/product/436/11366), [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976), or [COSCLI](https://intl.cloud.tencent.com/document/product/436/43249) for batch operations.


### When I upload a new file to a bucket in which another file of the same name exists, will the old file be overwritten or will the new file be saved with a different version name?

The versioning feature is now available in COS. If versioning is not enabled for the bucket, when you upload a new file to a bucket in which another file of the same name already exists, the older one will be directly overwritten; if versioning is enabled, multiple versions of the object will co-exist.

### What is the minimum part size of a multipart upload in COS?

1 MB. For more information, see [Specifications and Limits](https://www.tencentcloud.com/document/product/436/14518).

### When uploading large files using multipart upload, can I replace an invalid signature to continue the multipart upload?

Yes.

### How do I generate a temporary URL for files in COS?

For more information, see [Download via Pre-Signed URL](https://www.tencentcloud.com/document/product/436/14116).


### I have set a validity period for a signature, but why can it still be used to download objects after it has expired?

By default, the browser will cache objects that have been loaded successfully. Therefore, if you access the same URL, the cached object will be returned without requesting the server again. Therefore, we recommend that you use the `Cache-Control: no-cache` header during object upload to prevent browser caching (see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) or [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) for details). Alternatively, you can specify the `response-cache-control=no-cache` request header during object download to prevent browser caching (see [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) for details).


### What should I do if I upload a file on the console and "Failed to upload. System error." is displayed?
This error may occur due to an unstable local network environment. You can try the upload again in a different network environment.


### How do I prevent others from downloading my COS files?

To do so, you can set your bucket permission to private read/write. For more information, see [Setting Access Permission](https://www.tencentcloud.com/document/product/436/13315). You can also configure a hotlink protection whitelist on your bucket to block any access from domain names not in the list. For more information, see [Setting Hotlink Protection](https://www.tencentcloud.com/document/product/436/13319).

### Can I use case-insensitive download URLs?

No. COS filenames are case-sensitive, and thus so are the download URLs. If you have enabled CDN acceleration for your bucket, you can go to the CDN console to configure [Cache Ignore URL Case](https://www.tencentcloud.com/document/product/228/35316), which will increase the hit rate to some extent.


### What should I do if the error "your policy or acl has reached the limit (Status Code: 400; Error Code: PolicyFull)" occurs when I am uploading files or creating a bucket?

COS allows each root account to have up to 1,000 bucket ACLs. If more bucket ACLs have been configured, this error will occur. Therefore, you can delete unnecessary bucket ACLs.
>? We recommend that you not use object-level ACLs or policies. When you call APIs or SDKs, if you don't need ACL control over a file, we recommend that you leave the ACL-related parameters (such as x-cos-acl and ACL) empty to inherit the bucket permissions.
>


