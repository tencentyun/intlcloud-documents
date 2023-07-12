## Overview

This API is used to query the origin-pull configuration of a bucket.

## Request

#### Sample request

```plaintext
GET /?origin HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
>- This request should be used with a request body.



#### Request parameters

This API has no request parameter.


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).



#### Request body

The request body of this request is empty.



## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

The response body is an origin-pull rule, with its structure shown below:

```plaintext
<OriginConfiguration>
    <OriginRule>
        <RulePriority>Integer</RulePriority>
        <OriginType>Redirect|Proxy|Mirror</OriginType>
        <OriginCondition>
            <!--The setting of the HTTP status code for origin-pull is determined based on the origin-pull type. If the type is `Proxy` or `Mirror`, the HTTP status code is set to `404`. If the type is `Redirect`, the HTTP status code is set to `4XX` or `5XX`.-->
            <HTTPStatusCode>404</HTTPStatusCode>
            <Prefix></Prefix>
        </OriginCondition>
        <OriginParameter>
            <Protocol>HTTP|HTTPS|FOLLOW</Protocol>
            <!--Whether to retain the error code of the origin for origin-pull-->
            <TransparentErrorCode>true|false</TransparentErrorCode>
            <!--Whether to retain the raw query parameter for origin-pull. Valid values: `true`, `false`-->
            <FollowQueryString>true|false</FollowQueryString>
            <!--Origin-pull request header parameter-->
            <HttpHeader>
                <!--Whether to transfer all request headers for origin-pull. Valid values: `true`, `false`-->
                <FollowAllHeaders>true|false</FollowAllHeaders>
                <!--Add specified headers for origin-pull. At most 10 headers can be added. A key-value pair in a custom header counts as one header.-->
                <!--If there is a value, add a header. If the value is null, do not add a header.-->
                <NewHttpHeaders>
                    <Header>
                        <Key>x-cos|oss|amz-ContentType|CacheControl|ContentDisposition|ContentEncoding|HttpExpiresDate|UserMetaData</Key>
                        <Value>string</Value>
                    </Header>
                </NewHttpHeaders>
                <!--Pass through the specified headers of the raw request for origin-pull.-->
                <FollowHttpHeaders>
                    <Header>
                        <Key>x-cos|oss|amz-ContentType|CacheControl|ContentDisposition|ContentEncoding|HttpExpiresDate|UserMetaData</Key>
                    </Header>
                </FollowHttpHeaders>
                <!--Do not pass through the specified headers of the raw request for origin-pull.-->
                <ForbidFollowHeaders>
                    <Header>
                        <Key>String</Key>
                    </Header>
                </ForbidFollowHeaders>
            </HttpHeader>
            <!--Follow3xx parameter-->
            <FollowRedirection>true|false</FollowRedirection>
            <!--The redirect code parameter is optional only when the origin-pull type is `Redirect` or `Proxy`. Otherwise, a parameter error is reported.-->
            <HttpRedirectCode>301|302|307</HttpRedirectCode>
        </OriginParameter>
	<!--Error code that triggers a switchover to the secondary origin. By default, a switchover is triggered if a 5XX status code is returned. After this field is added, a switchover is triggered if a 4XX status code is returned.-->
        <HTTPStandbyCode>                        
            <StatusCode>404</StatusCode>
            <StatusCode>403</StatusCode>
        </HTTPStandbyCode>
        <OriginInfo>
            <!--In the `Mirror` mode, multiple origins can be set to perform origin-pull based on the ratio, so that these origins can share the origin-pull traffic of a single origin. At most 10 origin addresses are supported, and the ratio is set by weight. In the `Proxy` or `Redirect` mode, only one origin can be set.-->
            <HostInfo>
                <HostName>bucketname-appid.cos.region.myqcloud.com</HostName>
                <!--Weight set for the origins. Origin-pull is performed based on the ratio.-->
		<Weight>4</Weight> 
                <!--Secondary origin address. At most 10 secondary origin addresses are supported, and the node names are numbered from 1 to 10.-->
                <StandbyHostName_1>bucketname2-appid.cos.region.myqcloud.com</StandbyHostName_1>
                <StandbyHostName_2>bucketname3-appid.cos.region.myqcloud.com</StandbyHostName_2>
            </HostInfo>
            <HostInfo>
                <HostName>bucketname4-appid.cos.region.myqcloud.com</HostName>
                <!--Weight set for the origins. Origin-pull is performed based on the ratio.-->
                <Weight>2</Weight> 
                <!--Secondary origin address. At most 10 secondary origin addresses are supported, and the node names are numbered from 1 to 10.-->
                <StandbyHostName_1>bucketname5-appid.cos.region.myqcloud.com</StandbyHostName_1>
                <StandbyHostName_2>bucketname6-appid.cos.region.myqcloud.com</StandbyHostName_2>
            </HostInfo>
            <FileInfo>
                <!--A specified file to pull-->
                <FixedFileConfiguration>
                    <FixedFilePath>String</FixedFilePath>
                </FixedFileConfiguration>
                <!--New prefix of the origin-pull filename-->
				<PrefixConfiguration>
					<Prefix></Prefix>
				</PrefixConfiguration>
                <!--New suffix of the origin-pull filename-->
				<SuffixConfiguration>
					<Suffix></Suffix>
				</SuffixConfiguration>
            </FileInfo>
        </OriginInfo>
    </OriginRule>
</OriginConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :----- | :-------------- | :-------- |
| OriginConfiguration | None | Origin-pull configuration | Container |

Content of `OriginConfiguration`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :-------------------------- | :-------- |
| OriginRule | OriginConfiguration | Origin-pull rule. More than one `OriginRule` are supported, which are applied in order of priority. | Container |

Content of `OriginRule`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
|  RulePriority | OriginConfiguration.OriginRule | Priority of the rule | Integer |
| OriginType         | OriginConfiguration.OriginRule | Origin-pull type. Three modes are supported: async origin-pull (Proxy), sync origin-pull (Mirror), redirection-based origin-pull (Redirect). Enumerated values: `Proxy`, `Mirror`, `Redirect`.                       | String |
| OriginCondition | OriginConfiguration.OriginRule | Origin-pull conditions, such as the HTTP protocol | Container |
| OriginParameter  | OriginConfiguration.OriginRule | Origin address configuration | Container |
| OriginInfo | OriginConfiguration.OriginRule | Information about the origin, such as its domain name or IP | Container |

Content of `OriginCondition`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| HTTPStatusCode | OriginConfiguration.OriginRule.<br/>OriginCondition | HTTP status code that triggers origin-pull. Set this parameter to `404` for the origin-pull of the `Proxy` or `Mirror` type and to `4XX` or `5XX` for the origin-pull of the `Redirect` type. | String |
| Prefix | OriginConfiguration.OriginRule.<br/>OriginCondition | Filename prefix that triggers origin-pull. By default, this parameter is left empty, meaning that any file can trigger origin-pull. | String |

Content of `OriginParameter`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| Protocol | OriginConfiguration.OriginRule.<br/>OriginParameter | Protocol used for origin-pull. Enumerated values: `HTTP`, `HTTPS`, `FOLLOW` (default, meaning to follow the user protocol) | String |
| FollowQueryString         | OriginConfiguration.OriginRule.OriginParameter | Whether to pass through the HTTP request string for origin-pull. Enumerated values: `true` (default), `false` | Boolean |
| HttpHeader | OriginConfiguration.OriginRule.OriginParameter | Whether to set HTTP header transferring | Container |
| FollowRedirection         | OriginConfiguration.OriginRule.OriginParameter | Redirection policy for 3xx responses. Enumerated values: <br>`true` (default): pulls resources from the origin and saves the resources to COS for 3xx responses <br> `false`: passes through 3xx responses without requesting the resources | Boolean |
| HttpRedirectCode | OriginConfiguration.OriginRule.OriginParameter | Return code set only for the `Redirect` or `Proxy` mode. Enumerated values: `301`, `302` (default), `307` | String |

Content of `HttpHeader`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| FollowAllHeaders         | OriginConfiguration.OriginRule.OriginParameter.HttpHeader | Whether to transfer all request headers. Enumerated values: `true`, `false` (default) | Boolean |
| NewHttpHeaders | OriginConfiguration.OriginRule.OriginParameter.HttpHeader | Specified headers to add during origin-pull. At most 10 headers are supported. | Container |
| FollowHttpHeaders         | OriginConfiguration.OriginRule.OriginParameter.HttpHeader | Headers in the raw request that are to pass through during origin-pull | Container |
| ForbidFollowHeaders         | OriginConfiguration.OriginRule.OriginParameter.HttpHeader | Headers in the raw request that are not to pass through during origin-pull | Container |

Content of `NewHttpHeaders`, `FollowHttpHeaders`, and `ForbidFollowHeaders`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| Header         | OriginConfiguration.OriginRule.OriginParameter.<br/>HttpHeader.NewHttpHeaders | Custom headers to add or transfer during origin-pull. This parameter is left empty by default. | Container |

Content of `Header`:


| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| Key         | OriginConfiguration.OriginRule.OriginParameter.<br/>HttpHeader.NewHttpHeader.UserMetaData | Name of the set header in the format of `x-A-B`. Valid values for A: `cos`, `oss`, `amz`; valid values for B: `ContentType`, `CacheControl`, `ContentDisposition`, `ContentEncoding`, `HttpExpiresDate`, `UserMetaData`.                        | String |
| Value         | OriginConfiguration.OriginRule.OriginParameter.<br/>HttpHeader.NewHttpHeader.UserMetaData | Value of the custom header. This parameter is left empty by default.                        | String |

Content of `OriginInfo`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| HostInfo         | OriginConfiguration.OriginRule.OriginInfo | Origin information. In the `Mirror` mode, multiple origins can be set to perform origin-pull based on the ratio, so that these origins can share the origin-pull traffic of a single origin. At most 10 origin addresses are supported, and the ratio is set by weight. In the `Proxy` or `Redirect` mode, only one origin can be set.                        | Container |
| FileInfo  | OriginConfiguration.OriginRule.OriginInfo | Information about the pulled file | Container |

Content of `HostInfo`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| HostName | OriginConfiguration.OriginRule.<br/>OriginInfo.HostInfo | Domain name/IP of the origin | String |
|Weight         | OriginConfiguration.OriginRule.OriginInfo.HostInfo | Origin weight. If multiple origins are configured in the `Mirror` mode, the origins will perform origin-pull according to the weight ratio.                       |Integer |
| StandbyHostName_N         | OriginConfiguration.OriginRule.OriginInfo.HostInfo | Secondary origin address. At most 10 secondary origin addresses are supported, and the node names are numbered from 1 to 10, for example, `StandbyHostName_1`, `StandbyHostName_2`, ..., and `StandbyHostName_10`.                        | String |

Content of `FileInfo`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| PrefixConfiguration         | OriginConfiguration.OriginRule.OriginInfo.FileInfo | Prefix configuration for the files to pull.                     | Container |
| SuffixConfiguration         | OriginConfiguration.OriginRule.OriginInfo.FileInfo | Suffix configuration for the files to pull.                        | Container |
| FixedFileConfiguration         | OriginConfiguration.OriginRule.OriginInfo.FileInfo | A fixed file to pull. This parameter is left empty by default. | Container |

Content of `FixedFileConfiguration`:


| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| FixedFilePath         | OriginConfiguration.OriginRule.OriginInfo.<br/>FileInfo.FixedFileConfiguration | Path of a fixed file to pull.                        |  String |


Content of `PrefixConfiguration`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| Prefix       | OriginConfiguration.OriginRule.OriginInfo.<br/>FileInfo. PrefixConfiguration | New prefix of the files to pull. This parameter is left empty by default.                   |  String |

Content of `SuffixConfiguration`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- |
| Suffix         | OriginConfiguration.OriginRule.OriginInfo.<br/>FileInfo. SuffixConfiguration | New suffix of the files to pull. This parameter is left empty by default.                        |  String |

## Examples

#### Request

```plaintext
GET /?origin= HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization: Auth String
Date: Sun, 28 Apr 2019 12:02:24 GMT
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Sun, 28 Apr 2019 12:02:25 GMT
Server: tencent-cos
x-cos-request-id: NWNjNTk2NTFfMmM4OGY3MGFfNTI1****

<?xml version="1.0" encoding="UTF-8"?>
<OriginConfiguration>
    <OriginRule>
        <OriginType>Proxy</OriginType>
        <OriginCondition>
            <HTTPStatusCode>404</HTTPStatusCode>
            <Prefix></Prefix>
        </OriginCondition>
        <OriginParameter>
            <Protocol>FOLLOW</Protocol>
            <FollowQueryString>true</FollowQueryString>
            <HttpHeader>
                <FollowAllHeaders>true</FollowAllHeaders>
                <NewHttpHeaders>
                    <Header>
                        <Key>x-cos-ContentType</Key>
                        <Value>csv</Value>
                    </Header>
                </NewHttpHeaders>
                <FollowHttpHeaders>
                    <Header>
                        <Key>Content-Type</Key>
                    </Header>
                </FollowHttpHeaders>
            </HttpHeader>
            <FollowRedirection>true</FollowRedirection>
        </OriginParameter>
        <OriginInfo>
            <HostInfo>
                <HostName>examplebucket-1250000000.cos.ap-shanghai.myqcloud.com</HostName>
            </HostInfo>
        </OriginInfo>
    </OriginRule>
</OriginConfiguration>
```

