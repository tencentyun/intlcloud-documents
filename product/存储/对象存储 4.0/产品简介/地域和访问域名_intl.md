Tencent Cloud's Cloud Object Storage (COS) supports multi-region storage, and different regions have different default access domain names. The region selected when you create a bucket cannot be modified. It is recommended to choose the nearest storage region according to your own business scenarios, so as to improve the object upload and download speed.

## Available Regions and Access Domain Names
>!
>- After the bucket is created, the default domain name can be viewed through the bucket **Domain Name Management** of [COS Console](https://console.cloud.tencent.com/cos5).
>- bucketname is the name given upon creating a bucket, and it can be viewed through the bucket **Basic Configuration** of [COS Console](https://console.cloud.tencent.com/cos5).
>- APPID is one of the account identifiers assigned by the system after the successful application of a Tencent Cloud account, which can be viewed through **Account Information** of [Tencent Cloud Console](https://console.cloud.tencent.com).
>- For more information on available regions for historical versions, see [List of Regions for Historical Versions](https://cloud.tencent.com/document/product/436/7777).
>- For more information on access from private network and public network, see [Creating Requests](https://cloud.tencent.com/document/product/436/31315).

| Region | Abbreviation | Default Domain Name (Upload/Download/Management) |
| -------- | ------------ | ---------------------------------------- |
| Beijing Zone 1 (North China) | ap-beijing-1 | &lt;bucketname-APPID&gt;.cos.ap-beijing-1.myqcloud.com |
| Beijing | ap-beijing   | &lt;bucketname-APPID&gt;.cos.ap-beijing.myqcloud.com |
| Shanghai (East China) | ap-shanghai  | &lt;bucketname-APPID&gt;.cos.ap-shanghai.myqcloud.com |
| Guangzhou (South China) | ap-guangzhou | &lt;bucketname-APPID&gt;.cos.ap-guangzhou.myqcloud.com |
| Chengdu (West China) | ap-chengdu   | &lt;bucketname-APPID&gt;.cos.ap-chengdu.myqcloud.com |
| Chongqing | ap-chongqing | <bucketname-APPID&gt;.cos.ap-chongqing.myqcloud.com |
| Singapore | ap-singapore | &lt;bucketname-APPID&gt;.cos.ap-singapore.myqcloud.com |
| Hong Kong | ap-hongkong  | &lt;bucketname-APPID&gt;.cos.ap-hongkong.myqcloud.com |
| Toronto | na-toronto   | &lt;bucketname-APPID&gt;.cos.na-toronto.myqcloud.com |
| Frankfurt | eu-frankfurt | &lt;bucketname-APPID&gt;.cos.eu-frankfurt.myqcloud.com |
| Mumbai | ap-mumbai    | <bucketname-APPID&gt;.cos.ap-mumbai.myqcloud.com |
| Seoul | ap-seoul     | <bucketname-APPID&gt;.cos.ap-seoul.myqcloud.com |
| Silicon Valley | na-siliconvalley     | <bucketname-APPID&gt;.cos.na-siliconvalley.myqcloud.com |
| Virginia | na-ashburn     | <bucketname-APPID&gt;.cos.na-ashburn.myqcloud.com |
| Bangkok | ap-bangkok     | <bucketname-APPID&gt;.cos.ap-bangkok.myqcloud.com |
| Moscow | eu-moscow     | <bucketname-APPID&gt;.cos.eu-moscow.myqcloud.com |
| Tokyo |ap-tokyo  |     <bucketname-APPID&gt;.cos.ap-tokyo.myqcloud.com |

> Example:
> A user created a bucket in Guangzhou where he/she resides. The user-defined string of the bucket name is "example", and the system-generated APPID is "1250000000", so the default access domain name of the bucket is:
```
example-1250000000.cos.ap-guangzhou.myqcloud.com
```

