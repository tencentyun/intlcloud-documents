The Tencent Cloud COS global acceleration feature utilizes a load balancing system based on Tencent's global traffic scheduling to intelligently route and parse user requests and select the optimal network linkage for nearby access. Backed by globally deployed Tencent Cloud data centers, it allows users across the world to quickly access buckets and improves application access success rate, allowing for greater business stability and a smoother user experience.

> !
> - The global acceleration feature is now generally available and supported in all public cloud regions. However, it is not supported in finance cloud regions due to network isolation.
> - Using this feature incurs fees as request data transfers are accelerated via Direct Connect lines in the Tencent Cloud private network. For more pricing information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).


## Directions

You can enable global acceleration on the COS Console or through APIs.

#### Using the COS Console
You can enable global acceleration for your buckets on the COS Console. For more information, please see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406) in the console documentation.

#### Using the REST API
You can directly use the following APIs to enable global acceleration:

- [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)
- [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)

## Access Endpoint Domain Names

After enabling global acceleration, you can access your COS files through two types of endpoint domain names:

- **Default bucket endpoint domain name:** the format is `<BucketName-APPID>.cos.<Region>.myqcloud.com`. For more information, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
- **Global acceleration endpoint domain name:** the format is `<BucketName-APPID>.cos.accelerate.myqcloud.com`.

Take the bucket `examplebucket-125000000` in the Guangzhou region as an example. If you have enabled global acceleration, you can upload the file `exampleObject.txt` from the Beijing region to your current bucket in the Guangzhou region in the following two ways:

- **Use the global acceleration endpoint domain name for access**: when uploading the object, you need to set the endpoint domain name to `exampleBucket-125000000.cos.accelerate.myqcloud.com`. When you upload the object through this endpoint domain name, COS will intelligently parse your request based on your network conditions and implement nearby access. For example, it will forward your request to the Beijing access layer and then transmit it to the Guangzhou storage layer via a private network Direct Connect line to accelerate data transfer.
- **Use the default bucket endpoint domain name for access**: when uploading the object, you need to set the endpoint domain name to `examplebucket-125000000.cos.ap-guangzhou.myqcloud.com`. When you upload the object through this endpoint domain name, your request will be directly forwarded to the Guangzhou access layer and then the Guangzhou storage layer. In this case, long public network linkage may lead to unstable transfer.

> !If you use global acceleration, fees will be incurred. Therefore, we recommend that you carefully evaluate whether to use this feature with your actual business needs in mind:
>
> 1. If your business has more writes (e.g., PUT Object, POST Object, and Multipart Upload) than reads and uploads data to Tencent Cloud data centers from a remote region, we recommend that you use a global acceleration endpoint domain name.
> 2. If your business has more reads (e.g., GET Object) than writes and mainly involves file download, we recommend that you perform a comprehensive evaluation of the [CDN-based access acceleration](https://intl.cloud.tencent.com/document/product/436/18669) solution and select the option with the best cost performance.
> 3. If your business mainly involves configuration operations or file extraction, we recommend that you use the default bucket endpoint domain name.
> 4. If your business needs to access buckets over the private network or via a Direct Connect line in the same region, we recommend that you use the default bucket endpoint domain name.

## Notes

We have outlined below some important factors to note when using a global acceleration endpoint domain name:

- The global acceleration endpoint domain name will take effect 15 minutes after being enabled.
- After the global acceleration endpoint domain name is enabled, the maximum bandwidth for a bucket will be allocated based on the business volume of the entire network.
- After the global acceleration domain name is enabled, only requests with it will be accelerated. However, the default bucket domain name can still be used.
- When using a global acceleration endpoint domain name, fees will be incurred only for requests for which linkage is accelerated. For example, if you use a global acceleration endpoint domain name to upload data from Beijing to a bucket in Beijing, the request will not incur acceleration fees as the linkage was not accelerated.
- When using a global acceleration endpoint domain name, you can specify to use HTTP or HTTPS transfer protocol. However, if the request is transmitted via a private network Direct Connect line, COS will choose to use HTTPS protocol to guarantee data transfer security.

## Billing Example

Uploading data or accessing a bucket using a global acceleration endpoint domain name will incur fees calculated by the **day**. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) and [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239). The following example compares billing between a global acceleration domain name and a custom default endpoint domain name:

**Scenario**

A user uses COS mainly to upload video files which require a high transmission success rate. If he/she uploads 1 G of video data daily from his/her offices in Xinjiang and Singapore to his/her bucket in Guangzhou, then 30-day fees will be charged as follows:

- Upload traffic fees for using an **acceleration endpoint domain name**: 30 x 1 GB x (0.07 USD/GB + 0.18 USD/GB) = 7.5 USD
- Upload traffic fees for using a **default bucket endpoint domain name**: 30 x 1 GB x （0 USD/GB） = 0 USD

> ?Upload traffic fees within the Chinese mainland are charged at 0.07 USD/GB, while those outside the Chinese mainland are charged at 0.18 USD/GB when using an acceleration endpoint domain name. Uploads using a default bucket endpoint domain name do not incur fees.

