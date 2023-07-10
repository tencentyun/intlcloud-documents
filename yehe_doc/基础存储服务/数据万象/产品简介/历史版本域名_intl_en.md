> !As this is a historical version of the region document that is no longer updated and maintained, we recommend you view the new version of [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423).

## Available Regions and Access Domain Names

>!
> - After a bucket is created, the default domain name will be generated, which can be viewed in **Domain Management** in the [CI console](https://console.cloud.tencent.com/ci/bucket).
> - `BucketName` is the name you set for your bucket upon creation. To view its value, you can go to the [CI console](https://console.cloud.tencent.com/ci/bucket) and select **Bucket Configuration**.
> - `APPID` is one of the account identifiers assigned by the system after you successfully applied for the Tencent Cloud account. It can be viewed in [Tencent Cloud console](https://console.cloud.tencent.com/developer) > **Account Information**.
> 

## Regions in the Chinese Mainland

| Region | Upload Domain Name | Download Domain Name |
| ------------ | ------------------------------------------------------ | ------------------------------------------- |
| Beijing (North China) | &lt;BucketName-APPID&gt;.pic.ap-beijing.myqcloud.com   | &lt;BucketName-APPID&gt;.picbj.myqcloud.com |
| Nanjing (East China) | &lt;BucketName-APPID&gt;.pic.ap-nanjing.myqcloud.com   | &lt;BucketName-APPID&gt;.picnj.myqcloud.com |
| Shanghai (East China) | &lt;BucketName-APPID&gt;.pic.ap-shanghai.myqcloud.com  | &lt;BucketName-APPID&gt;.picsh.myqcloud.com |
| Guangzhou (South China) | &lt;BucketName-APPID&gt;.pic.ap-guangzhou.myqcloud.com | &lt;BucketName-APPID&gt;.picgz.myqcloud.com |
| Chengdu (Southwest China) | &lt;BucketName-APPID&gt;.pic.ap-chengdu.myqcloud.com   | &lt;BucketName-APPID&gt;.piccd.myqcloud.com |
| Chongqing (Southwest China) | &lt;BucketName-APPID&gt;.pic.ap-chongqing.myqcloud.com | &lt;BucketName-APPID&gt;.piccq.myqcloud.com |



## Regions in Hong Kong (China) and Outside the Chinese Mainland

| Region | Upload Domain Name | Download Domain Name |
| -------- | ------------------------------------------------------ | -------------------------------------------- |
| Hong Kong (China) | &lt;BucketName-APPID&gt;.pic.ap-hongkong.myqcloud.com  | &lt;BucketName-APPID&gt;.pichk.myqcloud.com  |
| Moscow   | &lt;BucketName-APPID&gt;.pic.eu-moscow.myqcloud.com    | &lt;BucketName-APPID&gt;.picru.myqcloud.com  |
| Singapore   | &lt;BucketName-APPID&gt;.pic.ap-singapore.myqcloud.com | &lt;BucketName-APPID&gt;.picsgp.myqcloud.com |
| Toronto   | &lt;BucketName-APPID&gt;.pic.na-toronto.myqcloud.com   | &lt;BucketName-APPID&gt;.picca.myqcloud.com  |
| Mumbai     | &lt;BucketName-APPID&gt;.pic.ap-mumbai.myqcloud.com    | &lt;BucketName-APPID&gt;.picin.myqcloud.com  |

**Sample:**
A user created a bucket in Guangzhou region. The user-defined string of the bucket name is "examplebucket", and the system-generated `APPID` is "1250000000".
In this case, CI's default upload and download domain names are `examplebucket-1250000000.pic.ap-guangzhou.myqcloud.com` and `examplebucket-1250000000.picgz.myqcloud.com` respectively.
