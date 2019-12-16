The global acceleration feature of Tencent Cloud COS utilizes a load balancing system based on Tencent's global traffic scheduling to intelligently route and parse user requests and select the optimal network linkage for nearby access. Backed by globally deployed Tencent Cloud data centers, it allows users across the world to quickly access your buckets and improves your business access success rate for a higher business stability and smoother user experience.


>Currently, the global acceleration feature of COS is in beta test. To try it out, [please submit an application for beta test eligibility](https://cloud.tencent.com/apply/p/j5u6h2ibpi8).

## Directions

You can enable global acceleration in the COS Console or through APIs.

#### Via the COS Console
You can enable global acceleration for your buckets in the COS Console. For more information, please see [Enabling Global Acceleration](https://cloud.tencent.com/document/product/436/38864) in console documentation.

#### Via REST API
You can directly use the following APIs to enable global acceleration:

- [PUT Bucket Accelerate](https://cloud.tencent.com/document/product/436/38869)
- [GET Bucket Accelerate](https://cloud.tencent.com/document/product/436/38868)

## Access domain name

After enabling global acceleration, you can access your COS files through two types of domain names:

- **Default bucket domain name:** The format is `<BucketName-APPID>.cos.<Region>.myqcloud.com`. For more information, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
- **Global acceleration domain name:** The format is `<BucketName-APPID>.cos.accelerate.myqcloud.com`.

Take the bucket `examplebucket-125000000` in Guangzhou as an example. If you have enabled global acceleration for it, when you need to upload the file `exampleObject.txt` from Beijing to it, you can do so in the following two ways:

- **Use the global acceleration domain name for access**: When uploading the object, you need to set the domain name to `exampleBucket-125000000.cos.accelerate.myqcloud.com`. When you upload the object through this domain name, COS will intelligently parse your request based on your network conditions and implement nearby access. For example, it will forward your request to the Beijing access layer and then transmit it to the Guangzhou storage layer via a private network Direct Connect line to accelerate data transfer.
- **Use the default bucket domain name for access**: When uploading the object, you need to set the domain name to `examplebucket-125000000.cos.ap-guangzhou.myqcloud.com`. When you upload the object through this domain name, your request will be directly forwarded to the Guangzhou access layer and then the Guangzhou storage layer. In this case, long public network linkage may lead to unstable transfer.

>If you use global acceleration, fees will be incurred. Therefore, it is recommended that you carefully evaluate this feature based on your actual business needs:
>
> 1. If your business has more writes (e.g., PUT Object, POST Object, and Multipart Upload) than reads and uploads data from a remote region to Tencent Cloud data centers, you are recommended to use a global acceleration domain name.
> 2. If your business has more reads (e.g., GET Object) than writes and mainly involves file download, you are recommended to perform a comprehensive evaluation on the [CDN-based access acceleration](https://intl.cloud.tencent.com/zh/document/product/436/18669) solution and select the option with the best cost performance.
> 3. If your business mainly involves configuration operations or file extraction, you are recommended to use a default bucket domain name.
> 4. If your business needs to access buckets over the private network or a Direct Connect line in the same region, you are recommended to use a default bucket domain name.

## Notes

Below are precautions for using a global acceleration domain name:

- The global acceleration domain name will take effect in 15 minutes after being enabled. Please wait patiently.
- After the global acceleration domain name is enabled, the maximum bandwidth for a bucket through it will be allocated based on the business volume on the entire network.
- After the global acceleration domain name is enabled, only requests with it will be accelerated. However, the default bucket domain name can still be used.
- When the global acceleration domain name is used, fees will be incurred only for the accelerated linkage of requests. For example, if you use the global acceleration domain name to upload data from Beijing to a bucket in Beijing, as the linkage is not accelerated, the request will not incur acceleration fees.
- When using the global acceleration domain name, you can specify the HTTP or HTTPS transfer protocol. If the request is transmitted via a private network Direct Connect line, COS will choose to use the HTTPS protocol to guarantee data transfer security as appropriate.


