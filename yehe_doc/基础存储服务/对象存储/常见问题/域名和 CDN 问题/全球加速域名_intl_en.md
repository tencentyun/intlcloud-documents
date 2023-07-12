### What are the precautions for using a global acceleration domain name in COS?

Below are precautions for using a global acceleration domain name:
- The global acceleration domain name will take effect 15 minutes after being enabled.
- After the global acceleration domain name is enabled, the maximum bandwidth for a bucket will be allocated based on the business volume of the entire network.
- After the global acceleration domain name is enabled, only requests using that domain name will be accelerated. However, the default bucket domain name can still be used.
- When using a global acceleration domain name, fees will be incurred only for requests for which linkage is accelerated. For example, if you use a global acceleration domain name to upload data from Beijing to a bucket in Beijing, the request will not incur acceleration fees as the linkage was not accelerated.
- When using a global acceleration domain name, you can specify to use HTTP or HTTPS transfer protocol. However, if the request is transmitted via a private network Direct Connect line, COS will choose to use HTTPS protocol to guarantee data transfer security.

For more information on global acceleration, see [Overview](https://intl.cloud.tencent.com/document/product/436/33409).

### What do I do if the system indicates that the bucket does not exist when I use a global acceleration domain name to access COS via a path containing `/files/v2/appid/bucketname/`?

Global acceleration is a feature of COS V5 but `/files/v2/` is a reserved field of COS V4. Using the reserved field in COS V5 will cause an internal logic conflict. Be sure to use a V5 API to access the global acceleration domain name. For more information, please see [API Overview](https://intl.cloud.tencent.com/document/product/436/7751#api-overview).

### What operations are currently supported by global acceleration domain names?

Currently, global acceleration domain names support file upload and download. Related APIs are APIs that support acceleration domain names as listed below.

| No. | API                    | No. | API                    |
| ---- | ----------------------- | ---- | ----------------------- |
| 1    | PutObject               | 7    | ListParts               |
| 2    | PostObject              | 8    | UploadPart              |
| 3    | GetObject               | 9    | AbortMultipartUpload    |
| 4    | HeadObject              | 10   | CompleteMultipartUpload |
| 5    | OptionsObject           | 11   | ListMultipartUploads    |
| 6    | InitiateMultipartUpload | -     | -                        |


### Under what circumstances will global acceleration be charged?

After global acceleration is enabled, global acceleration traffic will be charged only when a Direct Connect linkage between two Tencent Cloud data centers is used for data transmission, which accelerates the data transmission. For example, if data is uploaded from Tibet to the bucket in Beijing, the Tibet data center will connect to the Chengdu data center first and transmit the data to the storage layer in Beijing through the Direct Connect linkage. In such a case, acceleration fees will be charged. If data is uploaded from Tibet to the bucket in Chengdu, the Tibet data center will directly connect to the Chengdu data center. In this case, the data directly falls on the Chengdu layer, there is no acceleration effect, and there will be no extra charge.
