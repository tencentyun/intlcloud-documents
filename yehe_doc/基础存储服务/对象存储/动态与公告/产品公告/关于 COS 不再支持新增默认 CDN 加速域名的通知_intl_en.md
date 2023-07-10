Starting from May 9, 2022, COS will stop supporting default CDN acceleration domains for buckets that have never used them. This change will not affect buckets that are using or once used default CDN acceleration domains. However, we recommend you switch to custom CDN acceleration domains instead. To learn more about CDN acceleration, see [Setting CDN Acceleration](https://intl.cloud.tencent.com/document/product/436/18670).

The change will affect users differently.

#### New COS user

COS will not support default CDN acceleration domains for COS users registered after May 9, 2022.

#### Existing COS user

| Bucket                                                       | Support for Default CDN Acceleration Domain                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| New buckets                                                  | COS will not support default CDN acceleration domains for buckets created after May 9, 2022. |
| Existing buckets that have never used default CDN acceleration domains | COS will not support default CDN acceleration domains for buckets that have never used them before May 9, 2022. |
| Existing buckets that once used default CDN acceleration domains | Buckets that used default CDN acceleration domains before May 9, 2022 can continue to use them. |
| Existing buckets that are using default CDN acceleration domains | Buckets that are using default CDN acceleration domains can continue to use them after May 9, 2022. |


#### Viewing default CDN acceleration domains

Buckets that are using or once used default CDN acceleration domains can continue to use them after May 9, 2022. You can view the default CDN acceleration domains under your account via two methods.

#### Method 1: via the COS console

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Go to **Bucket List**, click a bucket, and go to **Domains and Transfer** > **Default CDN Acceleration Domain** to view the enabled default CDN acceleration domain of the bucket. If the domain is disabled, you can view it in the [CDN console](https://console.cloud.tencent.com/cdn/domains).
![](https://qcloudimg.tencent-cloud.cn/raw/6314b96a1e1be3b7b7aeeac5e44d3f25.png)

#### Method 2: via the CDN console

Go to the [CDN console](https://console.cloud.tencent.com/cdn/domains) > **Domain Management** to view the default CDN acceleration domains you used or are using. If a domain is in the format of “<BucketName-APPID>.file.myqcloud.com” and its origin type is “Tencent Cloud COS Origin”, then its corresponding bucket can continue to use the default CDN acceleration domain.

>! Buckets whose default CDN acceleration domains are disabled as of May 9, 2022 can continue to use the domains. However, the CDN console does not keep records of deleted CDN acceleration domains. Therefore, buckets whose default CDN acceleration domains are deleted can no longer use them after May 9, 2022.

![](https://qcloudimg.tencent-cloud.cn/raw/af25652f08d7648b373f447104914d1b.jpg)
