### API Description
This API is used to end a server process, change the process status to `TERMINATED`, and repossess resources related to the process.

### Parameter Description

No parameters.

### Returned Value Description
- True: success.
- False: failure.

A generic result in [GenericOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) type containing an error message will be returned.

### Use Cases
```
 TencentCloud::Gse::GenericOutcome outcome = TencentCloud::Gse::Server::ProcessEnding();   
```
