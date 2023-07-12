## Overview

Tencent Cloud's Cloud Infinite (CI) supports multi-region storage, and different regions have different default access domain names. The region you initially selected for the bucket cannot be modified. You can select a region closest to your business location to speed up object upload and download.


>!
> - After a bucket is created, the default domain will be generated. To view the URL, you can go to the [CI console](https://console.cloud.tencent.com/ci/bucket), click the name of the desired bucket, and click **File Management** > **Details**.
> - Regions and domains in the following table are COS domains. Old users can still use CI domains.
> - `BucketName` is the name you set for your bucket upon creation. To view its value, you can go to the [CI console](https://console.cloud.tencent.com/ci/bucket), click the name of the bucket, and choose the **Bucket Configuration** tab.
> - `APPID` is one of the account identifiers assigned by the system after you successfully applied for the Tencent Cloud account. It can be viewed at [Tencent Cloud console](https://console.cloud.tencent.com/developer) > **Account Information**.


## Regions in the Chinese Mainland
| Region | Abbreviation | Default Domain (Upload/Download/Management) |
| ------------ | ---|-------|
| Beijing |     ap-beijing        |     &lt;BucketName-APPID&gt;.cos.ap-beijing.myqcloud.com   | 
| Nanjing |       ap-nanjing         |    &lt;BucketName-APPID&gt;.cos.ap-nanjing.myqcloud.com   | 
| Shanghai |       ap-shanghai       |   &lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com  |
| Guangzhou |     ap-guangzhou          |   &lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com | 
| Chengdu |     ap-chengdu          |   &lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com   | 
| Chongqing |     ap-chongqing          |      &lt;BucketName-APPID&gt;.cos.ap-chongqing.myqcloud.com  |


## Regions in Hong Kong (China) and Outside the Chinese Mainland


| Region | Abbreviation | Default Domain (Upload/Download/Management) |
| :------- | :------------------------------| :------------------------------------- |
| Hong Kong (China) |  ap-hongkong|   &lt;BucketName-APPID&gt;.cos.ap-hongkong.myqcloud.com |
| Singapore  |  ap-singapore|       &lt;BucketName-APPID&gt;.cos.ap-singapore.myqcloud.com |
| Mumbai  |  ap-mumbai   |  &lt;BucketName-APPID&gt;.cos.ap-mumbai.myqcloud.com |
| Seoul  |   ap-seoul  |     &lt;BucketName-APPID>.cos.ap-seoul.myqcloud.com  |
|  Bangkok  | ap-bangkok  |    &lt;BucketName-APPID>.cos.ap-bangkok.myqcloud.com  |  
| Tokyo   |    ap-tokyo |   &lt;BucketName-APPID>.cos.ap-tokyo.myqcloud.com   |  
| Silicon Valley (US West) | na-siliconvalley |  &lt;BucketName-APPID>.cos.na-siliconvalley.myqcloud.com  |
| Virginia (US East) |  na-ashburn  |    &lt;BucketName-APPID>.cos.na-ashburn.myqcloud.com  |
| Toronto |    na-toronto  |     &lt;BucketName-APPID&gt;.cos.na-toronto.myqcloud.com  |
| Frankfurt  |   eu-frankfurt |  &lt;BucketName-APPID>.cos.eu-frankfurt.myqcloud.com   |
| Moscow  |  eu-moscow  |    &lt;BucketName-APPID&gt;.cos.eu-moscow.myqcloud.com   |



## Example

Assume that you have logged in to the CI console as the root account (`APPID`: `1250000000`), and clicked **Bucket Management** > **Bind Bucket** to create a bucket named `examplebucket` residing in the Guangzhou region. The domain for CI processing will be as follows:
```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

>?
>- examplebucket-1250000000: indicates that the bucket is owned by the user whose `APPID` is `1250000000`. `APPID` is a fixed and unique ID assigned by the system when you successfully applied for the Tencent Cloud account. You can view it at [Account Information](https://console.cloud.tencent.com/developer).
>- cos: indicates COS domains. `pic` and `picgz` indicate CI domains.
>- ap-guangzhou: abbreviation of the region
>- myqcloud.com: indicates Tencent Cloud domain (fixed)



