## Overview

This API is used to set origin-pull for a bucket.

## Request

#### Sample request

```shell
PUT /?origin HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 


#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body is an origin-pull rule.

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :------------------ | :----- | :-------------- | :-------- | :--- |
| OriginConfiguration | None | Origin-pull configuration | Container | Yes |

Content of `OriginConfiguration`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------------ | :-------------------------- | :-------- | :--- |
| OriginRule | OriginConfiguration | Origin-pull rule. More than one `OriginRule` are supported, which are applied in order of priority. | Container | Yes |

Content of `OriginRule`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
|  RulePriority | OriginConfiguration.OriginRule | Priority of the rule | Integer | Yes |
| OriginType | OriginConfiguration.OriginRule | Origin-pull type. Enumerated values: `Mirror` (sync origin-pull), `Proxy` (async origin-pull)  | Enum | Yes |
| OriginCondition | OriginConfiguration.OriginRule | Origin-pull conditions, such as the HTTP protocol | Container | Yes |
| OriginParameter  | OriginConfiguration.OriginRule | Origin address configuration | Container | Yes |
| OriginInfo | OriginConfiguration.OriginRule | Information about the origin server, such as its domain name or IP | Container | Yes |

Content of `OriginCondition`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HTTPStatusCode | OriginConfiguration.OriginRule.<br/>OriginCondition | HTTP status code that triggers origin-pull. Default value: `404` | String | Yes |
| Prefix | OriginConfiguration.OriginRule.<br/>OriginCondition | Filename prefix that triggers origin-pull. By default, this parameter is left empty, meaning that any file can trigger origin-pull. | String | No   |

Content of `OriginParameter`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Protocol | OriginConfiguration.OriginRule.<br/>OriginParameter | Protocol used for origin-pull. Enumerated values: `HTTP`, `HTTPS`, `FOLLOW` (default, meaning to follow the user protocol) | String | Yes |
| FollowQueryString | OriginConfiguration.OriginRule.<br/>OriginParameter | Whether to pass through the HTTP request string in proxy mode. Enumerated values: `true` (default), `false` | Boolean | No |
| HttpHeader | OriginConfiguration.OriginRule.<br/>OriginParameter | Whether to transfer HTTP headers in proxy mode | Container | No  |
| FollowRedirection | OriginConfiguration.OriginRule.<br/>OriginParameter | Redirection policy for 3xx responses in proxy mode. Enumerated values: <br>`true` (default): pulls resources from the origin server and saves the resources to COS for 3xx responses <br> `false`: passes through 3xx responses without requesting the resources | Boolean | No |
| HttpRedirectCode | OriginConfiguration.OriginRule.<br/>OriginParameter | Return code in proxy mode. Enumerated values: `301`, `302` (default) | String | No |

Content of `HttpHeader`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| FollowHttpHeader | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader | Whether to transfer request headers in proxy mode. Enumerated values: `true`, `false` (default) | Boolean | No  |
| NewHttpHeader | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader | Request headers to transfer in proxy mode | Container | No |

Content of `NewHttpHeader`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Header | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader.NewHttpHeader | Custom headers to add during origin-pull. This parameter is left empty by default. | Container | No  |

Content of `Header`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Key | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader.NewHttpHeader.Header | Name of the custom header. This parameter is left empty by default. Examples: `x-cos`, `oss`, `amz-ContentType`, `CacheControl`, `ContentDisposition`, `ContentEncoding`, `HttpExpiresDate`, `UserMetaData` | String | No  |
| Value | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader.NewHttpHeader.Header | Value of the custom header. This parameter is left empty by default. | String | No |

Content of `OriginInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HostInfo | OriginConfiguration.OriginRule.OriginInfo | Information about the origin server | Container | Yes |
| FileInfo  | OriginConfiguration.OriginRule.OriginInfo | Information about the pulled file | Container | Yes |

Content of `HostInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HostName | OriginConfiguration.OriginRule.<br/>OriginInfo.HostInfo | Domain name/IP of the origin server | String | Yes   |

Content of `FileInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| PrefixConfiguration | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo | Prefix configuration for the files to pull | Container | No  |
| Prefix | OriginConfiguration.OriginRule.OriginInfo.<br/>FileInfo.PrefixConfiguration | Prefix of the files to pull. This parameter is left empty by default. | String | No |
| SuffixConfiguration | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo | Suffix configuration for the files to pull | Container | No |
| Suffix | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo.SuffixConfiguration | Suffix of the files to pull. This parameter is left empty by default. | String | No |
| FixedFileConfiguration | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo.FixedFileRedirection | Whether to redirect a file to another file with a different suffix for origin-pull. Enumerated values: `TRUE`, `FALSE` (default)  | Boolean | No |
| FixedFilePath | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo.FixedFileConfiguration | A fixed file to pull. This parameter is left empty by default. | String | No |

## Response

**Response headers**

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Response body**

The response body of this API is empty.

**Error codes**

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Example

**Request (`Mirror` mode)**

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
