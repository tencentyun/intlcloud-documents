
Spot instances may be repossessed by Tencent Cloud due to price or inventory reasons. To enable users to perform custom operations before instance repossession, we provide an API for obtaining information about repossession status via an internal metadata mechanism.

## Metadata
Instance metadata refers to data relevant to an instance. It can be used for configuring or managing a running instance. You can log in to the instance to access and obtain instance metadata. For more information, see [Querying Instance Metadata](https://intl.cloud.tencent.com/document/product/213/4934).


## Querying the Termination Information of a Spot Instance using Metadata
Run the following command using the cURL tool. You can also send an HTTP GET request.
```
curl metadata.tencentyun.com/latest/meta-data/spot/termination-time
```
- If the instance has been terminated, the termination time of the spot instance is returned, as shown below.
>?The termination time refers to the OS time of the spot instance when it’s terminated (in UTC+8).
>
```
2018-08-18 12:05:33
```
- If the error code 404 is returned, the instance is not a spot instance or it’s not terminated.

For more information, see [Querying Instance Metadata](https://intl.cloud.tencent.com/document/product/213/4934).

