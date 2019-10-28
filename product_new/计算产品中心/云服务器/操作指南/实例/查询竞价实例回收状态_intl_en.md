
Spot instances may be repossessed by Tencent Cloud due to price or inventory reasons. To enable users to perform custom operations before the instance repossession, we provide an API for obtaining repossession status information through an internal metadata mechanism.

## Metadata
Instance metadata refers to data relevant to an instance. It can be used for configuring or managing an operating instance. You can access and obtain instance metadata inside an instance. For more information, see [Viewing Instance Metadata](http://intl.cloud.tencent.com/document/product/213/4934).


## Obtaining Repossession Status Information of a Spot Instance by Using Metadata
To obtain the repossession status information of a spot instance, you can access the metadata by using the cURL tool or an HTTP GET request.
```
curl metadata.tencentyun.com/latest/meta-data/spot/termination-time
```
- The following returned information indicates the repossession time of the spot instance.
```
2018-08-18 12:05:33
```
- If the error code 404 is returned, the instance is not a spot instance or repossession has not been triggered.

For more information, see [Viewing Instance Metadata](http://intl.cloud.tencent.com/document/product/213/4934).
