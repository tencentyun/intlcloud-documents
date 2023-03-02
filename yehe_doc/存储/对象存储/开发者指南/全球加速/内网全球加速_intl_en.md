By leveraging Tencent Cloud's global traffic scheduling capabilities, COS's private network global acceleration routes and resolves user requests intelligently to select the optimal network access linkage, helping you quickly access resources across regions over the private network. It allows you to fully enjoy the stable transfer quality of Tencent Cloud's private network backbone lines, so as to improve the stability and performance of cross-region data transfer.

Many businesses need to pull data across regions over the private network. In the container image distribution scenario, for example, image repositories are usually stored in a region centrally, and the container cluster may be deployed in different regions based on the business needs. During application deployment, the container cluster needs to pull the image from another region, which generates many cross-region requests. In this scenario, a private network global acceleration endpoint can be used to offer a stable private network cross-region Direct Connect line to improve the image distribution stability.

>!Using this feature incurs fees as request data transfers are accelerated via Direct Connect lines in the Tencent Cloud private network. For more pricing information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).

## How to Use

You can enable global acceleration in the COS console or through APIs.

#### Using COS console

You can enable global acceleration for your buckets in the COS console. For more information, see [Enabling Global Acceleration](https://intl.cloud.tencent.com/document/product/436/33406) in the console documentation.

#### Using RESTful APIs

You can directly use the following APIs to enable global acceleration:

- [PUT Bucket Accelerate](https://www.tencentcloud.com/document/product/436/33411)
- [GET Bucket Accelerate](https://www.tencentcloud.com/document/product/436/33412)

## Access Endpoint Domain Names

After enabling the global acceleration feature, you can access COS files in another region over the private network through a private network global acceleration endpoint in the format of `<BucketName-APPID>.cos-internal.accelerate.tencentcos.cn`.

For example, a business' application image is stored in bucket `examplebucket-1250000000` in Guangzhou region, and its container clusters are deployed in Guangzhou, Beijing, and Shanghai regions. To accelerate container image distribution, the business team enables global acceleration for bucket `examplebucket-1250000000`, so container clusters in Beijing, Shanghai, and Guangzhou regions can pull the image package over the private network through the private network global acceleration endpoint `examplebucket-1250000000.cos-internal.accelerate.tencentcos.cn`.

- When the container cluster in Guangzhou region pulls the file through the endpoint, COS will intelligently resolve the request to the private network access layer in Guangzhou region to directly pull the file from the storage cluster in the same region.
- When the container cluster in Beijing/Shanghai region pulls the file through the endpoint, COS will intelligently resolve the request to the private network access layer in Beijing/Shanghai region and use the private network access layer device to pull the file from the storage cluster in Guangzhou region over the cross-region backbone network Direct Connect line.

>!
>- If you use global acceleration, fees will be incurred. Therefore, we recommend that you carefully evaluate whether to use this feature with your actual business needs in mind:
>- The private network global acceleration endpoint can be used in the Tencent Cloud private network environment only. If your request source is not in the Tencent Cloud private network environment, it cannot be connected to. In this case, you can consider using the default endpoint or the default global acceleration endpoint.
>- When you use a private network global acceleration endpoint in another Tencent Cloud product such as CVM, TKE, or SCF, the product must be in a region where COS is available; otherwise, it cannot be used. For more information on regions where COS is available, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

## Limits

We have outlined below some important factors to note when using a global acceleration endpoint domain name:

- The global acceleration domain name will take effect 15 minutes after being enabled.
- After the global acceleration domain name is enabled, the maximum bandwidth for a bucket will be allocated based on the business volume of the entire network.
- After the global acceleration domain name is enabled, only requests using that domain name will be accelerated. However, the default bucket domain name can still be used.
- When using a global acceleration domain name, fees will be incurred only for requests for which linkage is accelerated. For example, if you use a global acceleration domain name to upload data from Beijing to a bucket in Beijing, the request will not incur acceleration fees as the linkage was not accelerated.
- When using a global acceleration domain name, you can specify the HTTP or HTTPS transfer protocol. However, if the request is transmitted via a private network Direct Connect line, COS will choose to use HTTPS protocol to guarantee data transfer security.

