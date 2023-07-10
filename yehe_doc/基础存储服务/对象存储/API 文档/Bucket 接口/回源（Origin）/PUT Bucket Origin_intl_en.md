## Overview

This API is used to set origin-pull for a bucket.

## Request

#### Sample request

```plaintext
PUT /?origin HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - This request should be used with a request body.



#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body is an origin-pull rule.

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
            <!--follow3xx parameter-->
            <FollowRedirection>true|false</FollowRedirection>
            <!--The redirect code parameter is optional only when the origin-pull type is `Redirect` or `Proxy`. Otherwise, a parameter error is reported.-->
            <HttpRedirectCode>301|302|307</HttpRedirectCode>
        </OriginParameter>
	<!--Error code that triggers a switchover to the secondary origin. By default, a switchover is triggered if a 5xx status code is returned. After this field is added, a switchover is triggered if a 4xx status code is returned.-->
        <HTTPStandbyCode>                        
            <StatusCode>404</StatusCode>
            <StatusCode>403</StatusCode>
        </HTTPStandbyCode>
        <OriginInfo>
            <!--In the `Mirror` mode, multiple origins can be set to perform origin-pull based on the ratio, so that they can share the origin-pull traffic of a single origin. At most 10 origin addresses are supported, and the ratio is set by weight. In the `Proxy` or `Redirect` mode, only one origin can be set.-->
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
                <Prefix></Prefix>
                <!--New suffix of the origin-pull filename-->
                <Suffix></Suffix>
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
| OriginType         | OriginConfiguration.OriginRule | Origin-pull type. Enumerated values: `Proxy` (async origin-pull), `Mirror` (sync origin-pull), `Redirect` (redirection-based origin-pull)                       | Container | Yes |
| OriginCondition | OriginConfiguration.OriginRule | Origin-pull conditions, such as the HTTP protocol | Container | Yes |
| OriginParameter  | OriginConfiguration.OriginRule | Origin address configuration | Container | Yes |
| OriginInfo | OriginConfiguration.OriginRule | Information about the origin, such as its domain name or IP | Container | Yes |

Content of `OriginCondition`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HTTPStatusCode | OriginConfiguration.OriginRule.<br/>OriginCondition | HTTP status code that triggers origin-pull. Set this parameter to `404` for the origin-pull of the `Proxy` or `Mirror` type and to `4XX` or `5XX` for the origin-pull of the `Redirect` type. | String | Yes |
| Prefix | OriginConfiguration.OriginRule.<br/>OriginCondition | Filename prefix that triggers origin-pull. By default, this parameter is left empty, meaning that any file can trigger origin-pull. | String | No   |

Content of `OriginParameter`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Protocol | OriginConfiguration.OriginRule.<br/>OriginParameter | Protocol used for origin-pull. Enumerated values: `HTTP`, `HTTPS`, `FOLLOW` (default, meaning to follow the user protocol) | String | Yes |
| FollowQueryString | OriginConfiguration.OriginRule.<br/>OriginParameter | Whether to pass through the HTTP request string for origin-pull. Enumerated values: `true` (default), `false` | Boolean | No |
| HttpHeader | OriginConfiguration.OriginRule.OriginParameter | Whether to set HTTP header transferring | Container | No  |
| FollowRedirection | OriginConfiguration.OriginRule.OriginParameter | Redirection policy for 3xx responses. Enumerated values: <br>`true` (default): Pulls resources from the origin and saves the resources to COS for 3xx responses. <br> `false`: Passes through 3xx responses without requesting the resources. | Boolean | No |
| HttpRedirectCode | OriginConfiguration.OriginRule.OriginParameter | Return code set only for the `Redirect` or `Proxy` mode. Enumerated values: `301`, `302` (default), `307` | String | No |

Content of `HttpHeader`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| FollowHttpHeader | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader | Whether to transfer all request headers. Enumerated values: `true`, `false` (default) | Boolean | No  |
| NewHttpHeaders | OriginConfiguration.OriginRule.OriginParameter.HttpHeader | Specified headers to add during origin-pull. At most 10 headers are supported. | Container | No  |
| NewHttpHeader | OriginConfiguration.OriginRule.<br/>OriginParameter.HttpHeader | Headers in the raw request that are to pass through during origin-pull | Container | No |
| ForbidFollowHeaders         | OriginConfiguration.OriginRule.OriginParameter.HttpHeader | Headers in the raw request that are not to pass through during origin-pull | Container | No |

Content of `NewHttpHeaders`, `FollowHttpHeaders`, and `ForbidFollowHeaders`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Header | OriginConfiguration.OriginRule.OriginParameter.HttpHeader.NewHttpHeader | Custom headers to add or transfer during origin-pull. This parameter is left empty by default. | Container | No  |

Content of `Header`:


| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Key | OriginConfiguration.OriginRule.OriginParameter.HttpHeader.NewHttpHeader.UserMetaData | Name of the custom header. This parameter is left empty by default. Example: `x-cos\|oss\|amz-ContentType\|CacheControl\|ContentDisposition\|ContentEncoding\|HttpExpiresDate\|UserMetaData` | String | No  |
| Value | OriginConfiguration.OriginRule.OriginParameter.HttpHeader.NewHttpHeader.UserMetaData | Value of the custom header. This parameter is left empty by default. | String | No |

Content of `OriginInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HostInfo         | OriginConfiguration.OriginRule.OriginInfo | Origin information. In the `Mirror` mode, multiple origins can be set to perform origin-pull based on the ratio, so that they can share the origin-pull traffic of a single origin. At most 10 origin addresses are supported, and the ratio is set by weight. In the `Proxy` or `Redirect` mode, only one origin can be set.                        | Container | Yes   |
| FileInfo  | OriginConfiguration.OriginRule.OriginInfo | Information about the pulled file | Container | Yes |

Content of `HostInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HostName | OriginConfiguration.OriginRule.<br/>OriginInfo.HostInfo | Domain name/IP of the origin | String | Yes   |
|Weight         | OriginConfiguration.OriginRule.OriginInfo.HostInfo | Origin weight. If multiple origins are configured in the `Mirror` mode, they will perform origin-pull according to the weight ratio.                       |Integer | No   |
| StandbyHostName_N         | OriginConfiguration.OriginRule.OriginInfo.HostInfo | Secondary origin address. At most 10 secondary origin addresses are supported, and the node names are numbered from 1 to 10, for example, `StandbyHostName_1`, `StandbyHostName_2`, ..., and `StandbyHostName_10`.                        | String | Yes   |

Content of `FileInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Prefix | OriginConfiguration.OriginRule.OriginInfo.<br/>FileInfo.PrefixConfiguration | New prefix of the files to pull. This parameter is left empty by default. | String | No |
| Suffix | OriginConfiguration.OriginRule.<br/>OriginInfo.FileInfo.SuffixConfiguration | New suffix of the files to pull. This parameter is left empty by default. | String | No |
| FixedFileConfiguration         | OriginConfiguration.OriginRule.OriginInfo.FileInfo | A fixed file to pull. This parameter is left empty by default. | String | No |

Content of `FixedFileConfiguration`:


| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| FixedFilePath         | OriginConfiguration.OriginRule.OriginInfo.FileInfo.FixedFileConfiguration | Path of a fixed file to pull | String | No |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Examples

#### Example 1: Common `Mirror` mode


#### Request

```plaintext
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

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Sun, 28 Apr 2019 12:02:45 GMT
Server: tencent-cos
x-cos-request-id: NWNjNTk2NTFfMmM4OGY3MGFfNadfadsfY2****
```


#### Example 2: `Mirror` mode with weight

In the following example, all headers except `x-cos-example-header` in the raw request will be passed through during origin-pull. The rule specifies two origins: origin 1 `bucketname1-appid.cos.region.myqcloud.com` and origin 2 `bucketname2-appid.cos.region.myqcloud.com`. Origins 1 and 2 are configured with weights 8 and 2, respectively. To be specific, 80% origin-pull requests will be sent to origin 1 and 20% to origin 2.


#### Request

```plaintext
PUT /?origin= HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization:Authstring
Content-Length:Content-Length
DATE:Sun, 28 Apr 2019 12:02:24 GMT

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
            <Protocol>HTTPS</Protocol>
            <FollowQueryString>true</FollowQueryString>
            <HttpHeader>
                <FollowAllHeaders>true</FollowAllHeaders>
                <ForbidFollowHeaders>
                    <Header>
                        <Key>x-cos-example-header</Key>
                    </Header>
                </ForbidFollowHeaders>
            </HttpHeader>
        </OriginParameter>
        <OriginInfo>
            <HostInfo>
                <HostName>bucketname1-appid.cos.region.myqcloud.com</HostName>
                <Weight>8</Weight>
            </HostInfo>
            <HostInfo>
                <HostName>bucketname2-appid.cos.region.myqcloud.com</HostName>
                <Weight>2</Weight>
            </HostInfo>
        </OriginInfo>
    </OriginRule>
</OriginConfiguration>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Sun, 28 Apr 2019 12:02:25 GMT
Server: tencent-cos
x-cos-request-id: NWNjNTk2NTFfMmM4OGY3MGFfNTI1****
```

#### Example 3: `Proxy` mode


#### Request

```plaintext
PUT /?origin= HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization:Authstring
Content-Length: 347
DATE:Sun, 28 Apr 2019 12:02:24 GMT

<?xml version="1.0" encoding="UTF-8"?>
<OriginConfiguration>
  <OriginRule>
    <RulePriority>1</RulePriority>
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
    		</NewHttpHeader>
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

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Sun, 28 Apr 2019 12:02:45 GMT
Server: tencent-cos
x-cos-request-id: NWNjNTk2NTFfMmM4OGY3MGFfNadfadsfY****
```


#### Example 4: `Redirect` mode


#### Request

```plaintext
PUT /?origin= HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization:Authstring
Content-Length: 347
DATE:Sun, 28 Apr 2019 12:02:24 GMT

<?xml version="1.0" encoding="UTF-8"?>
<OriginConfiguration>
  <OriginRule>
    <RulePriority>1</RulePriority>
    <OriginType>Redirect</OriginType>
    <OriginCondition>
    	<HTTPStatusCode>403</HTTPStatusCode>
    	<Prefix></Prefix>
    </OriginCondition>
    <OriginParameter>
    	<HttpRedirectCode>301</HttpRedirectCode>
    </OriginParameter>
    <OriginInfo>
    	<HostInfo>
    	<HostName>examplebucket-1250000000.cos.ap-shanghai.myqcloud.com</HostName>
    	</HostInfo>
    </OriginInfo>
  </OriginRule>
</OriginConfiguration>
```


#### Response


```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Sun, 28 Apr 2019 12:02:25 GMT
Server: tencent-cos
x-cos-request-id: NWNjNTk2NTFfMmM4OGY3MGFfNTI1****
```


