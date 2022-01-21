### API Description
This API is used to terminate a game session, change the status of `GameServerSession` to `TERMINATED`, and save the relevant log.

### Parameter Description
No parameters.

### Returned Value Description
- True: success.
- False: failure.

A generic result in [GenericOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) type containing an error message will be returned.

### Use Cases
```
TencentCloud::Gse::GenericOutcome outcome = 
	TencentCloud::Gse::Server::TerminateGameSession();

if (outcome.IsSuccess())
{
       // Subsequent processing
}
```
