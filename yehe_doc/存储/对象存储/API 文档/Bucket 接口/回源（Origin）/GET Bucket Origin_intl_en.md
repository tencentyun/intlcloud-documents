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
> - This request should be used with a request body.



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
    <OriginType>Redirect|Proxy</OriginType>
    <OriginCondition>
    	<HTTPStatusCode>404</HTTPStatusCode>
    	<Prefix></Prefix>
    </OriginCondition>
    
    <OriginParameter>
    	<Protocol>HTTP|HTTPS|FOLLOW</Protocol>
    	<!--The query parameter is optional only when the origin-pull type is `Proxy`. Otherwise, a parameter error is reported.-->
    	<FollowQueryString>true|false</FollowQueryString>
    	<!--The request header parameter is optional only when the origin-pull type is `Proxy`. Otherwise, a parameter error is reported.-->
    	<HttpHeader>
    		<!--The header can be passed in or not passed in.-->
    		<FollowAllHeaders>true|false</FollowAllHeaders>
    		<!--At most 10 headers can be set. A key-value pair in a custom header counts as one header.-->
            <!--If there is a value, add a header. If the value is null, do not add a header.-->
    		<NewHttpHeaders>
                <Header>
                    <Key>x-cos|oss|amz-ContentType|CacheControl|ContentDisposition|ContentEncoding|HttpExpiresDate|UserMetaData</Key>
                    <Value>string</Value>
    			</Header>
    			...
    		</NewHttpHeaders>
			<FollowHttpHeaders>
                <Header>
                    <Key>x-cos|oss|amz-ContentType|CacheControl|ContentDisposition|ContentEncoding|HttpExpiresDate|UserMetaData</Key>
    			</Header>
    			...
    		</FollowHttpHeaders>
    	</HttpHeader>
    	<!--The follow3xx parameter is optional only when the origin-pull type is `Proxy`. Otherwise, a parameter error is reported.-->
    	<FollowRedirection>true|false</FollowRedirection>
    	<!--The redirect code parameter is optional only when the origin-pull type is `Redirect`. Otherwise, a parameter error is reported.-->
    	<HttpRedirectCode>301|302|307</HttpRedirectCode> 
    	
    </OriginParameter>
    
    <OriginInfo>
    	<HostInfo>
			<HostName>bucketname-appid.cos.region.myqcloud.com</HostName>
		</HostInfo>
    </OriginInfo>
  </OriginRule>
  ...
</OriginConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :------------------ | :----- | :-------------- | :-------- | :--- |
| OriginConfiguration | None | Origin-pull configuration | Container | Yes |

Content of `OriginConfiguration`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------------ | :-------------------------- | :-------- | :--- |
| OriginRule | OriginConfiguration | Currently, only one OriginRule needs to be supported. | Container | Yes |

Content of `OriginRule`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| OriginType         | OriginConfiguration.OriginRule | Origin-pull type. Enumerated values: `Proxy` (async origin-pull), `Mirror` (sync origin-pull), `Redirect` (redirection-based origin-pull)                       | Container |
| OriginCondition | OriginConfiguration.OriginRule | Origin-pull conditions, such as the HTTP protocol | Container | Yes |
| OriginParameter  | OriginConfiguration.OriginRule | Origin address configuration | Container | Yes |
| OriginInfo | OriginConfiguration.OriginRule | Information about the origin, such as its domain name or IP | Container | Yes |

Content of `OriginCondition`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HTTPStatusCode | OriginConfiguration.OriginRule.OriginCondition | HTTP status code that triggers origin-pull. Default value: `404` | String | Yes |
| Prefix | OriginConfiguration.OriginRule.OriginCondition | Filename prefix that triggers origin-pull. By default, this parameter is left empty, meaning that any file can trigger origin-pull. | String | No   |

Content of `OriginParameter`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Protocol | OriginConfiguration.OriginRule.OriginParameter | Protocol used for origin-pull. Enumerated values: `HTTP`, `HTTPS`, `FOLLOW` (default, meaning to follow the user protocol) | String | Yes |
| FollowQueryString | OriginConfiguration.OriginRule.OriginParameter | Whether to pass through the HTTP request string in `Proxy` mode. Enumerated values: `true` (default), `false` | Boolean | No |
| HttpHeader | OriginConfiguration.OriginRule.OriginParameter | Whether to transfer HTTP headers in `Proxy` mode | Container | No  |
| FollowRedirection | OriginConfiguration.OriginRule.OriginParameter | Redirection policy for 3xx responses in `Proxy` mode. Enumerated values: <br>`true` (default): Pulls resources from the origin and saves the resources to COS for 3xx responses. <br>`false`: Passes through 3xx responses without requesting the resources. | Boolean | No |
| HttpRedirectCode | OriginConfiguration.OriginRule.OriginParameter | Return code in `Redirect` mode. Enumerated values: `301`, `302` (default), `307` | String | No |
| CopyOriginData         | OriginConfiguration.OriginRule.OriginParameter | Whether to copy a piece of origin data to the origin when redirecting to the origin in `Redirect` mode. Enumerated values: `true`, `false` (default)                      | Boolean | No  |

Content of `HttpHeader`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| FollowAllHeaders | OriginConfiguration.OriginRule.OriginParameter.HttpHeader | Whether to transfer all request headers in `Proxy` mode. Enumerated values: `true`, `false` (default) | Boolean | No  |
| NewHttpHeaders | OriginConfiguration.OriginRule.OriginParameter.HttpHeader | Request headers to set in `Proxy` mode | Container | No |
| FollowHttpHeaders | OriginConfiguration.OriginRule.OriginParameter.HttpHeader | Request headers to transfer in `Proxy` mode | Container | No |

Content of `NewHttpHeaders` and `FollowHttpHeaders`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Header | OriginConfiguration.OriginRule.OriginParameter.HttpHeader.NewHttpHeader | Custom headers to add or transfer during origin-pull. This parameter is left empty by default. | Container | No  |


Content of `Header`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| Key | OriginConfiguration.OriginRule.OriginParameter.HttpHeader.NewHttpHeader.UserMetaData | Name of the custom header. This parameter is left empty by default. Example: `x-cos|oss|amz-ContentType|CacheControl|ContentDisposition|ContentEncoding|HttpExpiresDate|UserMetaData` | String | No  |
| Value | OriginConfiguration.OriginRule.OriginParameter.HttpHeader.NewHttpHeader.UserMetaData | Value of the custom header. This parameter is left empty by default. | String | No |

Content of `OriginInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HostInfo | OriginConfiguration.OriginRule.OriginInfo | Information about the origin | Container | Yes |
| FileInfo  | OriginConfiguration.OriginRule.OriginInfo | Information about the pulled file | Container | Yes |

Content of `HostInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| HostName | OriginConfiguration.OriginRule.OriginInfo.HostInfo | Domain name/IP of the origin | String | Yes   |

Content of `FileInfo`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| PrefixDirective | OriginConfiguration.OriginRule.OriginInfo.FileInfo | Whether to redirect a file to another file with a different suffix for origin-pull. Enumerated values: `true`, `false` (default)  | Boolean | No |
| Prefix | OriginConfiguration.OriginRule.OriginInfo.FileInfo | Prefix of the files to pull. This parameter is left empty by default. | String | No |
| Suffix | OriginConfiguration.OriginRule.OriginInfo.FileInfo | Suffix of the files to pull. This parameter is left empty by default. | String | No |

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
