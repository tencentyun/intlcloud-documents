
## Returned Result Type
It indicates the returned result of an API call, which is in the template type.

```
template<typename R, typename E> // Result, Error
class Outcome{ }
```



#### Attributes

|Parameter Name|Type|Description|
|---|---|---|
|success|bool| It indicates whether the result is a success or failure, which is a private parameter and will be returned through `IsSuccess()` |
|result|Template R| It is a private parameter and can be obtained through `GetResult()` |
|error|Template E| It is a private parameter, which will be returned for a failure and can be obtained through `GetError()` |



#### Methods

| Method Name      | Parameter | Returned Value Type   | Description                        |
| ----------- | ---- | ---------- | --------------------------- |
| IsSuccess() | None   | bool       | Whether the call of the corresponding API succeeds |
| GetResult() | None   | Template R | Returned result of API call           |
| GetError()  | None   | Template E | Specific information on API call error       |


<span id="jtlx">

#### Specific types

| Type Name                        | Definition                                                         | Description                |
| ----------------------------- | ------------------------------------------------------------ | ------------------- |
| DescribePlayerSessionsOutcome | `typedef Outcome<TencentCloud::Gse::Server::Model::DescribePlayerSessionsResult, GseError><br>DescribePlayerSessionsOutcome` | Player session information        |
| GenericOutcome                | `typedef Outcome<void*, GseError> GenericOutcome;`             | Generic returned result        |
| InitSDKOutcome                | `typedef TencentCloud::Gse::Outcome<TencentCloud::Gse::Internal::GseServerState*, GseError> <br>InitSDKOutcome;` | Class object implemented inside GSE |
| LongOutcome                   | `typedef Outcome<long, GseError> LongOutcome;`                 | Data in `long` type        |
| StringOutcome            | `typedef Outcome<std::string, GseError> StringOutcome;`        | Data in `string` type      |



## LogParameters

It is the path of logs to be uploaded by a game process.

#### Attributes

| Parameter Name     | Type                       | Description                 |
| ---------- | -------------------------- | -------------------- |
| m_logPaths | `std::vector<<std::string>>` | It is the log path vector, which is a private parameter |



#### Methods

| Method Name      | Parameter | Returned Value Type                   | Description         |
| ----------- | ---- | -------------------------- | ------------ |
| getLogPaths | None   | `std::vector<<std::string>>` |  Returns log path |



## PlayerSessionCreationPolicy

It is the policy used to allow players to join a game session, which is in enumeration type.

#### Valid values

| Value         | Description         |
| ---------- | ------------ |
| NOT_SET    | Not set       |
| ACCEPT_ALL | Allows players to join |
| DENY_ALL   | Prohibits players to join |

