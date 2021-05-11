
### API Description 	
This API is used to initialize the SDK.


### Parameter Description
No parameters.


### Returned Value Description
If initialization succeeds, the [InitSdkOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) object will be returned.


### Use Cases
```
TencentCloud::Gse::Server::InitSDKOutcome initOutcome =               
                         TencentCloud::Gse::Server::InitSDK();

if (!initOutcome.IsSuccess())
{
	return false;
} 
```
