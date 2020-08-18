The Tencent Cloud COS global acceleration feature utilizes a load balancing system based on Tencent's global traffic scheduling to intelligently route and parse user requests and select the optimal network linkage for nearby access. Backed by globally deployed Tencent Cloud data centers, it allows users across the world to quickly access buckets and improves application access success rate, allowing for greater business stability and a smoother user experience. In addition, it can also accelerate data uploads and downloads.

> !
> - The global acceleration feature is now generally available and supported in all public cloud regions. However, it is not supported in finance cloud regions due to network isolation.
> - Using this feature incurs fees as request data transfers are accelerated through Direct Connect lines in the Tencent Cloud private network. For more pricing information, please see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).


## Directions

You can enable global acceleration on the COS Console or through APIs.

#### Through the COS Console
You can enable global acceleration for your buckets on the COS Console. For more information, please see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406) in the console documentation.

#### Through RESTful APIs
You can directly use the following APIs to enable global acceleration:

- [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)
- [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)

## Access Endpoint Domain Names

After enabling global acceleration, you can access your COS files through two types of endpoint domain names:

- **Default bucket endpoint domain name:** Format: `<BucketName-APPID>.cos.<Region>.myqcloud.com`. For more information, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
- **Global acceleration endpoint domain name:** Format: `<BucketName-APPID>.cos.accelerate.myqcloud.com`.

Take the bucket `examplebucket-125000000` in the Guangzhou region as an example. If you have enabled global acceleration, you can upload the file `exampleObject.txt` from the Beijing region to your current bucket in the Guangzhou region in the following two ways:

- **Use the global acceleration endpoint domain name for access**: when uploading the object, you need to set the endpoint domain name to `exampleBucket-125000000.cos.accelerate.myqcloud.com`. When you upload the object through this endpoint domain name, COS will intelligently parse your request based on your network conditions and implement nearby access. For example, it will forward your request to the Beijing access layer and then transfer it to the Guangzhou storage layer through a private network Direct Connect line to accelerate data transfer.
- **Use the default bucket endpoint domain name for access**: when uploading the object, you need to set the endpoint domain name to `examplebucket-125000000.cos.ap-guangzhou.myqcloud.com`. When you upload the object through this endpoint domain name, your request will be directly forwarded to the Guangzhou access layer and then the Guangzhou storage layer. In this case, long public network linkage may lead to unstable transfer.

> !If you use global acceleration, fees will be incurred. Therefore, we recommend you carefully evaluate whether to use this feature with your actual business needs in mind:
>
> 1. If your business has more writes (e.g., `PUT Object`, `POST Object`, and `Multipart Upload`) than reads and uploads data to Tencent Cloud data centers from a remote region, we recommend using a global acceleration endpoint domain name.
> 2. If your business has more reads (e.g., `GET Object`) than writes and mainly involves file download, we recommend you perform a comprehensive evaluation of the [CDN-based access acceleration](https://cloud.tencent.com/document/product/436/18668) solution and select the option with the best cost performance.
> 3. If your business mainly involves configuration operations or file extraction, we recommend using the default bucket endpoint domain name.
> 4. If your business needs to access buckets over a private network or through a Direct Connect line within the same region, we recommend using the default bucket endpoint domain name.

## Notes

We have outlined below some important factors to note when using a global acceleration endpoint domain name:

- The global acceleration endpoint domain name will take effect 15 minutes after being enabled.
- After the global acceleration endpoint domain name is enabled, the maximum bandwidth for a bucket will be allocated based on the business volume of the entire network.
- After the global acceleration endpoint domain name is enabled, only requests using that endpoint domain name will be accelerated. However, the default bucket endpoint domain name can still be used.
- When using a global acceleration endpoint domain name, fees will be incurred only for requests for which linkage is accelerated. For example, if you use a global acceleration endpoint domain name to upload data from Beijing to a bucket in Beijing, the request will not incur acceleration fees as the linkage was not accelerated.
- When using a global acceleration endpoint domain name, you can specify to use HTTP or HTTPS transfer protocol. However, if the request is transferred through a private network Direct Connect line, COS will choose to use HTTPS protocol to guarantee data transfer security.

## Billing Samples

Uploading data or accessing a bucket by using a global acceleration endpoint domain name will incur fees calculated by the **day**. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) and [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239). The following example compares billing between a global acceleration endpoint domain name and a default endpoint domain name:

**Scenario**

You use COS mainly to upload video files which require a high transfer success rate. If you upload 1 GB of video data daily from your offices in Xinjiang and Singapore to your bucket in Guangzhou, then 30-day fees will be charged as follows:

- Upload traffic fees for using an acceleration endpoint domain name: 30 x 1 GB x (0.07 USD/GB + 0.18 USD/GB) = 7.5 USD
- Upload traffic fees for using a default bucket endpoint domain name: 30 x 1 GB x (0 USD/GB) = 0 USD

> ?Upload traffic fees within the Chinese mainland are charged at 0.07 USD/GB, while those outside the Chinese mainland are charged at 0.18 USD/GB when an acceleration endpoint domain name is used. Uploads with a default bucket endpoint domain name do not incur fees.