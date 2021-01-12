### Does COS limit the upload and download bandwidth?

Yes. By default, the bandwidth limit on each account is 15 Gbit/s in each public cloud region in the Chinese mainland, and 10 Gbit/s in any other regions. If this threshold is exceeded, traffic throttling will be triggered for requests. To increase the threshold, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### How can I directly preview a file in my browser without downloading it?

Bucket endpoints in the format of `<BucketName-APPID>.cos.<Region>.myqcloud.com` are in XML format. You can directly preview file types supported by your browser by accessing the object URL using this endpoint format.


#### Sample:

Take the picture.jpg file in the root directory of the bucket `examplebucket-1250000000` in the Beijing region as an example:

If the object endpoint is in the format of `https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/picture.jpg`, you can directly access it to preview the picture.jpg file via your browser.

### How do I directly download a file in my browser without previewing it?

You can go to the [COS console](https://console.cloud.tencent.com/cos5) and set the value of the `Content-Disposition` in the custom object headers to `attachment`. For detailed directions, please see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).

You can also set the value of the request parameter `response-content-disposition` in the GET Object API to `attachment` so that your browser can pop up a window for the file to be downloaded. For more information, please see [GET Object](https://intl.cloud.tencent.com/document/product/436/7753).

>! To use the `response-*` parameter in a request, the request must be signed.

### How do I determine if I am accessing COS over a private network?

The access endpoints of COS use intelligent DNS resolution. For COS access via the Internet (including different ISPs), we will detect and select the optimal linkage for you to access COS. If you have deployed a service in Tencent Cloud to access COS, access within the same region will be automatically directed to a private network address. Cross-region access is not supported in a private network and the COS endpoint is resolved to a public network address by default.

#### How to determine access over a private network

Tencent Cloud products within the same region access each other over a private network by default, incurring no traffic fees. Therefore, we recommend choosing the same region when you purchase different Tencent Cloud products to save on costs.

The following shows how to determine access over a private network:

For example, when a CVM accesses COS, to determine whether a private network is used for access, use the `nslookup` command on the CVM to resolve the COS endpoint. If a private network IP is returned, access between the CVM and COS is over a private network; otherwise, it is over a public network.

>?Generally, a private IP address takes the form of `10.*.*.*` or `100.*.*.*`, and a VPC IP address takes the form of `169.254.*.*`.

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

For more information about private and public network access and connectivity testing, please see [COS Access via Private Network and Public Network](https://intl.cloud.tencent.com/document/product/436/30613).

For the private DNS server addresses of CVM, please see [Private Network DNS](https://intl.cloud.tencent.com/document/product/213/5225).

>!There are differences between the private IP address of a CPM (common format: `9.*.*.*`) and the IP address of a CVM (common format: `10.*.*.*`). If you have any questions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### How do I download a folder?

You can log in to [COSBrowser](https://intl.cloud.tencent.com/document/product/436/11366), select the folder to be downloaded, and click **Download** to download the folder or files in batches. You can also download a folder using the COSCMD tool. For more information, please see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).

### What should I do if the error "403 Forbidden" occurs or access permission is rejected when I perform upload/download and other operations?

Troubleshoot the problems by following the steps below:

1. Check whether the following configuration is correct:
   `BucketName`, `APPID`, `Region`, `SecretId`, `SecretKey`, etc.
2. If the configuration above is correct, check whether a sub-account is used for the operation. If yes, check whether the sub-account has been authorized by the root account. If it has not yet been authorized, log in using the root account to authorize the sub-account. For more information about authorization, please see [Cases of Permission Settings](https://intl.cloud.tencent.com/document/product/436/12514).
3. If a temporary key is used, check whether the current operation is in the policy set when the temporary key is obtained; if not, modify the relevant policy settings. For more information, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
4. If the problem persists, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1).


### How do I upload or download multiple files using COS?

COS allows you to upload or download multiple files through various methods such as the console, APIs/SDKs, and tools.

- Console: For detailed directions, please see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).
- APIs/SDKs: COS allows you to operate on multiple files by repeatedly calling an API or SDK. For more information, please see [APIs for object uploads](https://intl.cloud.tencent.com/document/product/436/10111) and [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).
- Tools: Use [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) and [COSBrowser](https://intl.cloud.tencent.com/document/product/436/11366) for batch operations.


### When I upload a new file to a bucket in which another file of the same name exists, will the old file be overwritten or will the new file be saved with a different version name?

The versioning feature is now available in COS. If versioning is not enabled for the bucket, when you upload a new file to a bucket in which another file of the same name already exists, the older one will be directly overwritten; if versioning is enabled, multiple versions of the object will co-exist.

### What is the minimum part size of a multipart upload in COS?

1 MB. For more information, please see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### When uploading large files using multipart upload, can I replace an invalid signature to continue the multipart upload?

Yes.


### What should I do if I upload a file on the console and "Failed to upload. System error." is displayed?
This error may occur due to an unstable local network environment. You can try the upload again in a different network environment.


### How do I prevent others from downloading my COS files?

You can set your bucket permission to private read/write. For more information, please see [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315). You can also configure a hotlink protection allowlist on your bucket to block any access from endpoints that are not in the list. For more information, please see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319).


### What should I do if the error "your policy or acl has reached the limit (Status Code: 400; Error Code: PolicyFull)" occurs when I am uploading files or creating a bucket?

COS allows each root account to have up to 1,000 bucket ACLs. If more bucket ACLs have been configured, this error will occur. Therefore, you can delete unnecessary bucket ACLs.

>?You are not advised to use object-level ACLs or policies. When calling APIs or SDKs, if you do not need ACL control over a file, we recommend leaving the ACL-related parameters (such as x-cos-acl and ACL) empty to inherit the bucket permissions.