## Feature Description

This API is used to consume the read logs. It gets the log data on the corresponding topic partition based on `cursor` and `count`.

## Request

#### Sample request

```shell
GET /pulllogs?topic_id=xxxxxxxx-xxxx-xxxx-xxxx&partition_id=1&cursor=xxxxxxxxx&count=10 HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Parameter Name | Type | Location | Required | Description |
| ------------ | ------ | ----- | -------- | ------------------------------------------------------------ |
| topic_id       | string            | query | Yes       | Log topic ID            |
| partition_id   | int    | query | Yes       | Consumed topic partition number                                        |
| cursor       | string | query | Yes       | Base64-encoded cursor value, which indicates to read data from the current position             |
| count        | int    | query | Yes       | Number of `LogGroup` consumed at a time, which can be up to 1,000 (one `LogGroup` contains multiple logs. For the `LogGroup` definition, please see [Uploading Structured Logs](https://intl.cloud.tencent.com/document/product/614/16873)) |



## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/x-protobuf
Content-Length: 23
x-cls-cursor: xxxxxx
x-cls-count: 10

<Packaged content of `LogGroupList` in pb format>
```

#### Response header

| Header Name | Description |
| ------------ | ------------------------------------------------------------ |
| x-cls-cursor | Base64-encoded cursor value, which indicates to read data from the current position next time and is used for continued consumption            |
| x-cls-count  | Number of `LogGroup` returned in the current request (one `LogGroup` contains multiple logs. For the `LogGroup` definition, please see [Uploading Structured Logs](https://intl.cloud.tencent.com/document/product/614/16873)) |

#### Response parameters

The packaged content of the `LogGroupList` object is returned. For the pb file description, please see [Uploading Structured Logs](https://intl.cloud.tencent.com/document/product/614/16873).

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
