The global acceleration feature provided by Tencent Cloud Object Storage (COS) utilizes a load balancing system based on Tencent's global traffic scheduling to intelligently route and parse user requests and select the optimal network linkage for nearby access. Backed by globally deployed Tencent Cloud data centers, it allows users across the world to quickly access buckets and improves application access success rate, allowing for greater business stability and a smoother user experience. In addition, COS's global acceleration also speeds up uploads and downloads.

> !
> - The global acceleration feature is now generally available and supported in all public cloud regions.
> - Using this feature incurs fees as request data transfers are accelerated via Direct Connect lines in the Tencent Cloud private network. For more pricing information, see [Product Pricing](https://intl.cloud.tencent.com/pricing/cos).


## Directions

You can enable global acceleration on the COS Console or through APIs.

#### Using the COS console
You can enable global acceleration for your buckets in the COS console. For more information, see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406) in the console documentation.

#### Using RESTful APIs
You can directly use the following APIs to enable global acceleration:

- [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)
- [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)

## Access Endpoint Domain Names

After enabling global acceleration, you can access your COS files through two types of endpoint domain names:

- **Default bucket endpoint domain name:** Format: `<BucketName-APPID>.cos.<Region>.myqcloud.com`. For more information, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
- **Global acceleration endpoint domain name:** Format: `<BucketName-APPID>.cos.accelerate.myqcloud.com`.

Take the bucket `examplebucket-1250000000` in Guangzhou as an example. If you have enabled global acceleration for it, when you need to upload the file `exampleObject.txt` from Beijing to it, you can do so in the following two ways:

- **Use the global acceleration endpoint domain name for access**: when uploading the object, you need to set the endpoint domain name to `exampleBucket-1250000000.cos.accelerate.myqcloud.com`. When you upload the object through this endpoint domain name, COS will intelligently parse your request based on your network conditions and implement nearby access. For example, it will forward your request to the Beijing access layer and then transmit it to the Guangzhou storage layer via a private network Direct Connect line to accelerate data transfer.
- **Use the default bucket endpoint domain name for access**: when uploading the object, you need to set the endpoint domain name to `examplebucket-125000000.cos.ap-guangzhou.myqcloud.com`. When you upload the object through this endpoint domain name, your request will be directly forwarded to the Guangzhou access layer and then the Guangzhou storage layer. In this case, long public network linkage may lead to unstable transfer.

>! If you use global acceleration, fees will be incurred. Therefore, we recommend that you carefully evaluate whether to use this feature with your actual business needs in mind:
> 1. If your business has more writes (e.g., `PUT Object`, `POST Object`, and `Multipart Upload`) than reads and uploads data to Tencent Cloud data centers from a remote region, we recommend using a global acceleration endpoint domain name.
> 2. If your business has more reads (e.g., GET Object) than writes and mainly involves file download, we recommend that you perform a comprehensive evaluation of the [CDN-based access acceleration](https://intl.cloud.tencent.com/document/product/436/18668) solution and select the option with the best cost performance.
> 3. If your business mainly involves configuration operations or file extraction, we recommend using the default bucket endpoint domain name.
> 4. If your business needs to access buckets over a private network or through a Direct Connect line within the same region, we recommend using the default bucket endpoint domain name.
> 

## Notes

We have outlined below some important factors to note when using a global acceleration endpoint domain name:

- The global acceleration domain name will take effect 15 minutes after being enabled.
- After the global acceleration domain name is enabled, the maximum bandwidth for a bucket will be allocated based on the business volume of the entire network.
- After the global acceleration domain name is enabled, only requests using that domain name will be accelerated. However, the default bucket domain name can still be used.
- When using a global acceleration domain name, fees will be incurred only for requests for which linkage is accelerated. For example, if you use a global acceleration domain name to upload data from Beijing to a bucket in Beijing, the request will not incur acceleration fees as the linkage was not accelerated.
- When using a global acceleration domain name, you can specify the HTTP or HTTPS transfer protocol. However, if the request is transmitted via a private network Direct Connect line, COS will choose to use the HTTPS protocol to guarantee data transfer security.

## Billing Example

Uploading data or accessing a bucket by using a global acceleration endpoint domain name will incur fees calculated by the **day**. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) and [Product Pricing](https://intl.cloud.tencent.com/pricing/cos). The following example compares billing between a global acceleration endpoint domain name and a default endpoint domain name:

**Business scenario 1**

A user uses COS mainly to upload video files which require a high transmission success rate. If he/she uploads 1 GB of video data daily from his/her offices in Xinjiang and Singapore to his/her bucket in Guangzhou, then 30-day fees will be charged as follows:

- Upload traffic fees for using an **acceleration endpoint domain name**: 30 x 1 GB x (0.07 USD/GB + 0.18 USD/GB) = 7.5 USD
- Upload traffic fees for using a **default bucket endpoint domain name**: 30 x 1 GB x （0 USD/GB） = 0 USD

> ?Upload traffic fees within the Chinese mainland are charged at 0.07 USD/GB, while those outside the Chinese mainland are charged at 0.18 USD/GB when an acceleration endpoint domain name is used. Uploads with a default bucket endpoint domain name do not incur fees.

**Business scenario 2**

A user uses COS mainly to download video files that require a high transmission success rate. If he/she downloads 1 GB of video data daily from his/her office in Singapore to his/her bucket in Guangzhou, then 30-day fees will be charged as follows:

- Download traffic fees for using an acceleration domain name: 30 x 1 GB x 0.18 USD/GB = 5.4 USD
- Public downstream traffic fees for using an acceleration domain name: 30 x 1 GB x 0.1 USD/GB = 3 USD

To sum up, the total download traffic fee is 8.4 USD (5.4 + 3 = 8.4).

>? The unit price for cross-border download acceleration is 0.18 USD/GB. If you use a global acceleration domain name to download files, **public downstream traffic fees** and **global acceleration downstream traffic fees** will be charged.
>



