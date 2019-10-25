### Does COS have a limit on the upload and download bandwidth?

No. The upload and download speed depends on your local bandwidth.

### How can I directly preview a file in my browser without downloading it?

A bucket domain name in the format of `<BucketName-APPID>.cos.<Region>.myqcloud.com` is an XML domain name. As long as the file type can be directly previewed in your browser, you can preview the file in your browser by accessing the object link in this domain name format.

A bucket domain name in the format of `<BucketName-APPID>.<region>.myqcloud.com` is a JSON domain name. If you access the object link in this domain name format in your browser, a download window will pop up, and there are two ways to preview the file in the browser:

1. Upgrade your COS Console to [the latest version](https://console.cloud.tencent.com/cos5) and use the object link in the XML domain name format for access (strongly recommended).
2. Bind a custom domain name, enable static website, and access the file with the custom domain name.

#### Sample

Take the picture.jpg file in the root directory of the bucket examplebucket-1250000000 in Beijing for example:

- If the object address is in the format of `https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/picture.jpg`, you can directly access the address to preview the picture.jpg file in your browser.
- If the object address is in the format of `https://examplebucket-1250000000.cosbj.myqcloud.com/picture.jpg`, there are two ways to directly preview the object in your browser:
  1. Upgrade your COS Console to [the latest version](https://console.cloud.tencent.com/cos5) and use the object link in the XML domain name format for access (strongly recommended).
  2. Bind a custom domain name, enable static website, and access the file with the custom domain name.

### How can I directly download a file in my browser without previewing it?

You can set the value of the Content-Disposition parameter in the custom object headers to "attachment" in the console. For more information on how to do so in the console, see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).

You can also let your browser pop up a window for the file to be downloaded by setting the value of the request parameter `response-content-disposition` in the GET Object API to "attachment". For more information, see [GET Object](https://intl.cloud.tencent.com/document/product/436/7753).

>To use the response-* parameter in a request, the request must be signed.

### How to determine if I am accessing COS over the private network?

The access domain names of COS use intelligent domain name resolution, so that you requests to COS can be routed through the optimal linkage in case of cross-ISP access. If you deploy a service in Tencent Cloud to access COS, intra-region access requests will be automatically directed to a private network address. Cross-region requests do not support private network access for the time being and will be resolved to a public network address by default.

### How to identify private network access?

In the same region, Tencent Cloud products automatically communicate with one another over the private network and no traffic fees will be incurred. Therefore, it is recommended to choose the same region for cost reduction when you purchase different Tencent Cloud products.

The following shows how to determine whether it is private network access:

For example, to determine whether CVM accesses COS over the private network, run the `nslookup` command on the CVM instance to resolve the COS domain name. If a private network IP is returned, the access is over the private network; otherwise, it is over the public network.

>Generally, a private IP address is in the format of `10.*.*.*` or `100.*.*.*`, while a VPC IP address `169.254.*.*`.

If `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com` is the destination bucket address, the `Address: 10.148.214.13` below it indicates that the access is over the private network.

```shell
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com

Server:         10.138.224.65
Address:        10.138.224.65  #53

Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.13
Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.14
```

For more information on private and public network access and connectivity testing, see [COS Access via Private Network and Public Network](https://intl.cloud.tencent.com/document/product/436/30613#.E5.86.85.E7.BD.91.E4.B8.8E.E5.A4.96.E7.BD.91.E8.AE.BF.E9.97.AE).

For the private DNS server addresses of CVM, see [Private Network DNS](https://intl.cloud.tencent.com/document/product/213/5225#.E5.86.85.E7.BD.91-dns).

### How to download a folder?

You can log in to the [COSBrowser](https://intl.cloud.tencent.com/document/product/436/11366), select the folder to be downloaded, and click **Download** to download the folder or files in batches. You can also download the folder using the COSCMD tool. For more information, see [COSCMD tool](https://intl.cloud.tencent.com/document/product/436/10976).

### What should I do if the error "403 Forbidden" occurs or the access is denied when I perform upload/download and other operations?

Troubleshoot the problem by following the steps below:

1. Check whether the following configuration information is correct:
   BucketName, APPID, Region, SecretId, SecretKey, etc.
2. If the above information is correct, check whether a sub-account is used for operation, and if yes, check whether the sub-account has been authorized by the root account. If it hasn't yet, log in using the root account to authorize the sub-account. For more information on authorization, see [Cases of Permission Settings](https://intl.cloud.tencent.com/document/product/436/12514).
3. If a temporary key is used, check whether the current operation is in the policy set when the temporary key is obtained, and if no, modify the relevant policy settings. For more information, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
4. If the problem persists after all the above steps are completed, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1).


### How can I upload or download files in batches using COS?

COS allows you to perform batch operations on files through APIs or SDK. Plus, it offers the command line tool [COSCMD tool](https://intl.cloud.tencent.com/document/product/436/10976) and graphical program [COSBrowser](https://intl.cloud.tencent.com/document/product/436/11366) for batch operations.


### When I upload a new file to the bucket where another file with the same name exists, will it be overwritten or will the new file be saved with a different version number?

The versioning feature is now available in COS. If versioning is not enabled for the bucket, when you upload a new file to the bucket where another file with the same name already exists, the latter will be directly overwritten; if versioning is enabled, multiple versions of the object will co-exist.

### What is the lower limit of part size for multipart upload COS?

1 MB. For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### When uploading a large file using multipart upload, can I change the signature to continue the multipart upload if the signature expires?

Yes.

