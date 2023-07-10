## Description

This API is used to set an origin-pull configuration for a bucket.

## Request

#### Sample request

```shell
PUT /?origin HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

This API does not use any request parameters.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this API request is an origin-pull rule.

```shell
<?xml version="1.0" encoding="UTF-8"?>
<OriginConfiguration>
	<OriginRule>
		<RulePriority>Integer</RulePriority>
		<OriginType>Mirror|Proxy</OriginType>
		<OriginCondition>
			<HTTPStatusCode>404</HTTPStatusCode>
			<Prefix>FilePrefix</Prefix>
		</OriginCondition>
		<OriginParameter>
            <Protocol>HTTP|HTTPS|FOLLOW</Protocol>
            <FollowQueryString>true|false</FollowQueryString>
            <HttpHeader>
                <FollowAllHeaders>true|false</FollowAllHeaders>
                <NewHttpHeaders>
                    <Header>
                        <Key>exampleKey</Key>
                        <Value>exampleValue</Value>
                    </Header>
                </NewHttpHeaders>
                <FollowHttpHeaders>
                    <Header>
                        <Key>x-cos|oss|amz-ContentType|CacheControl|ContentDisposition|ContentEncoding|HttpExpiresDate|UserMetaData</Key>
                    </Header>
                </FollowHttpHeaders>
            </HttpHeader>
            <FollowRedirection>true|false</FollowRedirection>
            <HttpRedirectCode>301|302</HttpRedirectCode>
        </OriginParameter>
        <OriginInfo>
            <HostInfo>
                <HostName><BucketName-APPID>.cos.<region>.myqcloud.com</HostName>
            </HostInfo>
            <FileInfo>
                <FixedFileConfiguration>
                    <FixedFilePath>String</FixedFilePath>
                </FixedFileConfiguration>
                <PrefixConfiguration>
                    <Prefix>String</Prefix>
                </PrefixConfiguration>
                <SuffixConfiguration>
                    <Suffix>String</Suffix>
                </SuffixConfiguration>
        	</FileInfo>
        </OriginInfo>
	</OriginRule>
</OriginConfiguration>
```

The nodes are described in detail below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :------------------ | :----- | :-------------- | :-------- | :--- |
| OriginConfiguration | None | Origin-pull configuration | Container | Yes |

Container node `OriginConfiguration`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------------ | :-------------------------- | :-------- | :--- |
| OriginRule | OriginConfiguration | Allows more than one OriginRule, which apply in priority order  | Container | Yes |

Container node `OriginRule`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
|  RulePriority   |  OriginConfiguration.OriginRule   |  Specifies the priority order in which rules apply  | Integer   |   Yes  |
| OriginType         | OriginConfiguration.OriginRule | Origin-pull type. Enumerated values: Mirror (sync origin-pull), Proxy (async origin-pull)       | Enum |   Yes   |
| OriginCondition             | OriginConfiguration.OriginRule | Origin-pull condition, which contains information such as HTTP protocol | Container    | Yes   |
| OriginParameter  | OriginConfiguration.OriginRule | Origin address | Container | Yes |
| OriginInfo | OriginConfiguration.OriginRule | Origin information, such as the origin’s domain name or IP | Container | Yes |

Container node ` OriginCondition`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HTTPStatusCode         | OriginConfiguration.OriginRule.<br/>OriginCondition | HTTP status code that triggers origin-pull. Default: 404                        | String | Yes   |
| Prefix         | OriginConfiguration.OriginRule.<br/>OriginCondition | File name prefix that triggers origin-pull. It is left empty by default, indicating any file can trigger origin-pull                        | String | No   |

Container node `OriginParameter`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Protocol         | OriginConfiguration.OriginRule.<br/>OriginParameter | Protocol used for origin-pull. Enumerated values: HTTP, HTTPS, FOLLOW (default; meaning following the user protocol)                        | String | Yes   |
| FollowQueryString         | OriginConfiguration.OriginRule.<br/>OriginParameter | Indicates whether to pass through HTTP request string in Proxy mode. Enumerated values: true (default), false                      | Boolean | No   |
| HttpHeader         | OriginConfiguration.OriginRule.<br/>OriginParameter | Indicates whether to forward HTTP headers in Proxy mode        | Container | No  |
| FollowRedirection         | OriginConfiguration.OriginRule.<br/>OriginParameter | Indicates whether to follow 3XX redirects in Proxy mode. Enumerated values: true, false. `true` (default): follows 3XX redirects to request resources from another origin, and then saves them in COS; `false`: passes 3XX responses, but does not request resources                        | Boolean | No  |
| HttpRedirectCode         | OriginConfiguration.OriginRule.<br/>OriginParameter | Status code returned in Proxy mode. Enumerated values: 301, 302 (default)                      | String | No  |

Container node `HttpHeader`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| FollowHttpHeader         | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader |  Indicates whether to forward request headers in Proxy mode. Enumerated values: true, false (default)                        | Boolean | No  |
| NewHttpHeader         | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader | Specifies the request headers to forward in Proxy mode                        | Container | No |

Container node `NewHttpHeader`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Header         | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader.NewHttpHeader | Adds new custom headers when an origin-pull occurs                        | Container | No  |

Container node `Header`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Key         | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader.NewHttpHeader.Header | Name of the user-defined header. This parameter is left empty by default. Valid values: x-cos, oss, amz-ContentType, CacheControl, ContentDisposition, ContentEncoding, HttpExpiresDate, UserMetaData       | String | No  |
| Value         | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader.NewHttpHeader.Header | Value of the user-defined header. It’s left empty by default          | String | No  |

Container node `OriginInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HostInfo | OriginConfiguration.OriginRule.OriginInfo | Origin information | Container | Yes |
| FileInfo  | OriginConfiguration.OriginRule.OriginInfo | Origin-pull file information | Container | Yes |

Container node `HostInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HostName         | OriginConfiguration.OriginRule.<br/>OriginInfo.HostInfo | Domain name or IP of the origin                        | String | Yes   |

Container node `FileInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| PrefixConfiguration         | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo | Configuration information on origin-pull file name prefix                        |  Container | No  |
| Prefix         | OriginConfiguration.OriginRule.OriginInfo.<br/>FileInfo.PrefixConfiguration | Prefix of origin-pull file name. It’s left empty by default                        |  String | No |
| SuffixConfiguration         | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo | Configuration information on origin-pull file name suffix                        |  Container | No  |
| Suffix         | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo.SuffixConfiguration | Suffix of origin-pull file name. It’s left empty by default                        |  String | No  |
| FixedFileConfiguration         | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo.FixedFileRedirection | Indicates whether to redirect a file to another one with a different suffix for origin-pull. Enumerated values: TRUE, FALSE (default)  |  Boolean | No  |
| FixedFilePath         | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo.FixedFileConfiguration | Fixed file for origin-pull. It’s left empty by default                     |  String | No |

## Response

**Response headers**

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Response body**

The response body of this API is empty.

**Error codes**

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Examples

**Request (Mirror mode)**

```shell
PUT /?origin= HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484639384;32557535384&q-key-time=1484639384;32557535384&q-header-list=host&q-url-param-list=&q-signature=5c07b7c67d56497d9aacb1adc19963135b7d****
Content-Length: 347
Date: Sun, 28 Apr 2019 12:02:24 GMT

<?xml version="1.0" encoding="UTF-8"?>
<OriginConfiguration>
  <OriginRule>
    <RulePriority>1</RulePriority>
    <OriginType>Mirror</OriginType>
    <OriginCondition>
      <HTTPStatusCode>404</HTTPStatusCode>
      <Prefix></Prefix>
    </OriginCondition>
    <OriginParameter>
      <Protocol>HTTP</Protocol>
      <FollowQueryString>true</FollowQueryString>
      <HttpHeader>
        <FollowAllHeaders>false</FollowAllHeaders>
        <NewHttpHeaders>
          <Header>
            <Key>x-cos</Key>
            <Value>exampleHeader</Value>
          </Header>
        </NewHttpHeaders>
        <FollowHttpHeaders>
          <Header>
            <Key>exampleHeaderKey</Key>
          </Header>
        </FollowHttpHeaders>
      </HttpHeader>
      <FollowRedirection>true</FollowRedirection>
      <HttpRedirectCode>302</HttpRedirectCode>
    </OriginParameter>
    <OriginInfo>
      <HostInfo>
        <HostName>examplebucket-1250000000.cos.ap-shanghai.myqcloud.com</HostName>
      </HostInfo>
    </OriginInfo>
  </OriginRule>
</OriginConfiguration>
```

**Response**

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Sun, 28 Apr 2019 12:02:45 GMT
Server: tencent-cos
x-cos-request-id: NWNjNTk2NTFfMmM4OGY3MGFfNadfadsfY2****
```
