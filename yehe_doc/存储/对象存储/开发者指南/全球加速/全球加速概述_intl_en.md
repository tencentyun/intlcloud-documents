The global acceleration feature of Tencent Cloud COS utilizes a load balancing system based on Tencent's global traffic scheduling to intelligently route and parse user requests and select the optimal network linkage for nearby access. Backed by globally deployed Tencent Cloud data centers, it allows users across the world to quickly access your buckets and improves your business access success rate for a higher business stability and smoother user experience.

> !
> - The global acceleration feature is now generally available and supported in all public cloud regions. It is not supported in finance cloud regions due to network isolation.
> - Using this feature incurs fees as request data is transferred with the Direct Connect of Tencent Cloud private network. For more pricing information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).


## Directions

You can enable global acceleration in the COS Console or through APIs.

#### Using the COS Console
You can enable global acceleration for your buckets in the COS Console. For more information, please see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406) in console documentation.

#### Using REST API
You can directly use the following APIs to enable global acceleration:

- [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)
- [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)

## Access Domain Names

After enabling global acceleration, you can access your COS files through two types of domain names:

- **Default bucket domain name:** the format is `<BucketName-APPID>.cos.<Region>.myqcloud.com`. For more information, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
- **Global acceleration domain name:** the format is `<BucketName-APPID>.cos.accelerate.myqcloud.com`.

Take the bucket `examplebucket-125000000` in Guangzhou region as an example. If you have enabled global acceleration for it, when you need to upload the file `exampleObject.txt` from Beijing region to it, you can do so in the following two ways:

- **Use the global acceleration domain name for access**: when uploading the object, you need to set the domain name to `exampleBucket-125000000.cos.accelerate.myqcloud.com`. When you upload the object through this domain name, COS will intelligently parse your request based on your network conditions and implement nearby access. For example, it will forward your request to the Beijing access layer and then transmit it to the Guangzhou storage layer via a private network Direct Connect line to accelerate data transfer.
- **Use the default bucket domain name for access**: when uploading the object, you need to set the domain name to `examplebucket-125000000.cos.ap-guangzhou.myqcloud.com`. When you upload the object through this domain name, your request will be directly forwarded to the Guangzhou access layer and then the Guangzhou storage layer. In this case, long public network linkage may lead to unstable transfer.

> !If you use global acceleration, fees will be incurred. Therefore, it is recommended that you carefully evaluate this feature based on your actual business needs:
>
> 1. If your business has more writes (e.g., PUT Object, POST Object, and Multipart Upload) than reads and uploads data from a remote region to Tencent Cloud data centers, you are recommended to use a global acceleration domain name.
> 2. If your business has more reads (e.g., GET Object) than writes and mainly involves file download, you are recommended to perform a comprehensive evaluation on the [CDN-based access acceleration](https://intl.cloud.tencent.com/document/product/436/18669) solution and select the option with the best cost performance.
> 3. If your business mainly involves configuration operations or file extraction, you are recommended to use a default bucket domain name.
> 4. If your business needs to access buckets over the private network or a Direct Connect line in the same region, you are recommended to use a default bucket domain name.

## Notes

Below are precautions for using a global acceleration domain name:

- The global acceleration domain name will take effect in 15 minutes after being enabled.
- After the global acceleration domain name is enabled, the maximum bandwidth for a bucket through it will be allocated based on the business volume on the entire network.
- After the global acceleration domain name is enabled, only requests with it will be accelerated. However, the default bucket domain name can still be used.
- When the global acceleration domain name is used, fees will be incurred only for the accelerated linkage of requests. For example, if you use the global acceleration domain name to upload data from Beijing to a bucket in Beijing, as the linkage is not accelerated, the request will not incur acceleration fees.
- When using the global acceleration domain name, you can specify the HTTP or HTTPS transfer protocol. If the request is transmitted via a private network Direct Connect line, COS will choose to use the HTTPS protocol to guarantee data transfer security as appropriate.

## Billing Example

Uploading data or accessing a bucket using a global acceleration domain name will incur fees billed by the **day**. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) and [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239). The following example compares the bills between a global acceleration domain name and a custom default domain name:

**Scenario**

A user uses COS mainly to upload video files which demand a high transmission success rate. If he uploads 1 G of video data daily from his offices in Xinjiang and Singapore respectively to his bucket in Guangzhou region, then the 30-day fees will be charged as follows:

- Upload traffic fees for using an **acceleration domain name**: 30 x 1 GB x (0.07 USD/GB + 0.18 USD/GB) = 7.5 USD
- Upload traffic fees for using a **default bucket domain name**: 30 x 1 GB x （0 USD/GB） = 0 USD

> ?Upload traffic fees are charged at 0.07 USD/GB and 0.18 USD/GB for uploads inside and outside Mainland China respectively using an acceleration domain name, and free for uploads using a default bucket domain name.

