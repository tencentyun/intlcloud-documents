### API Description
This API is used to set whether to accept new players, i.e., whether to allow new players to join a game session.

### Parameter Description

| Parameter Name | Type/Value | Description |
|:---|---|---|
|newPlayerSessionPolicy|[TencentCloud::Gse::Server::Model::PlayerSessionCreationPolicy](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx)| Enumerated values: ACCEPT_ALL, DENY_ALL|


### Returned Value Description

- True: success.
- False: failure.

A generic result in [GenericOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) type containing an error message will be returned.



### Use Cases
```
TencentCloud::Gse::GenericOutcome outcome = 
    TencentCloud::Gse::Server::UpdatePlayerSessionCreationPolicy(TencentCloud::Gse::
		Server::Model::PlayerSessionCreationPolicy::ACCEPT_ALL);
```
