## Introduction

Tencent Cloud's Cloud Infinite (CI) supports multi-region storage, and different regions have different default access domain names. The region that you select when creating a bucket cannot be changed. We recommend that you select the nearest storage region according to your own business scenarios for efficient object uploading and downloading.


>
> - After a bucket is created, you can view the default domain name on the bucket’s **Domain Management** page in the [CI Console](https://console.cloud.tencent.com/ci/bucket).
> - BucketName is the custom name that you enter when creating the bucket, which can be viewed on the bucket’s **Bucket Configuration** page in the [CI Console](https://console.cloud.tencent.com/ci/bucket).
> - APPID is one of the account identifiers assigned by the system after successful application for a Tencent Cloud account. It can be viewed in **Account Information** in the [Tencent Cloud Console](https://console.cloud.tencent.com/developer).


## Regions in Mainland China
| Region | Processing Domain Name |
| ------------ | ----------|
| Beijing | &lt;BucketName-APPID&gt;.cos.ap-beijing.myqcloud.com | 
| Nanjing | &lt;BucketName-APPID&gt;.cos.ap-nanjing.myqcloud.com | 
| Shanghai | &lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com |
| Guangzhou | &lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com | 
| Chengdu | &lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com | 
| Chongqing | &lt;BucketName-APPID&gt;.cos.ap-chognqing.myqcloud.com |


## Hong Kong (China) and Other Regions Outside Mainland China
| Region | Upload Domain Name | Download Domain Name |
| :------- | :----------------------------------------------- | :------------------------------------- |
| Hong Kong (China) | &lt;BucketName-APPID&gt;.pic.ap-hongkong.myqcloud.com | &lt;BucketName-APPID&gt;.pichk.myqcloud.com |
| Moscow | &lt;BucketName-APPID&gt;.pic.eu-moscow.myqcloud.com | &lt;BucketName-APPID&gt;.picru.myqcloud.com |
| Singapore | &lt;BucketName-APPID&gt;.pic.ap-singapore.myqcloud.com | &lt;BucketName-APPID&gt;.picsgp.myqcloud.com |
| Toronto | &lt;BucketName-APPID&gt;.pic.na-toronto.myqcloud.com | &lt;BucketName-APPID&gt;.picca.myqcloud.com |
| Mumbai | &lt;BucketName-APPID&gt;.pic.ap-mumbai.myqcloud.com | &lt;BucketName-APPID&gt;.picin.myqcloud.com |

**Example**:
Assume a user created a bucket in the Guangzhou region where the user resides. The user-defined string of the bucket name is examplebucket, and the system-generated APPID is 1250000000.
Its default processing domain name for CI is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`.

