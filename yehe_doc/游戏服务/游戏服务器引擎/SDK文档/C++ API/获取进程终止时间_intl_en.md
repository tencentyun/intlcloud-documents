
### API Description
This API is used to get the estimated process end time. If `-1` is returned, it indicates that reduction can be performed at any time.	

### Parameter Description

No parameters.

### Returned Value Description

End time in [LongOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) type.



### Use Cases
```
TencentCloud::Gse::LongOutcome TermTimeOutcome = 
	TencentCloud::Gse::Server::GetTerminationTime();
```
