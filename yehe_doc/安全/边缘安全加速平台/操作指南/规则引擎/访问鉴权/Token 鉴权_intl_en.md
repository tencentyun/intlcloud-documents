
## About Bill Subscription
As an access control policy, token authentication verifies access requests according to the configured authentication rules to filter out unauthorized access requests. This effectively prevents your site resources from being maliciously hotlinked and thus protects your business content.

**How does token authentication implement access control?**

When the client initiates a request, an authentication URL needs to be generated based on the access request URL according to authentication rules. The request will be considered authorized, and the node will respond normally only when the authentication information such as timestamp in the authentication URL passes node verification (i.e., successful authentication). If the verification fails, the node will reject the request and directly return 403.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the rule engine page, select the target site and click ![](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to configure token authentication rules as needed.
>?Currently, you can configure token authentication only if the match condition is **All (any request)** or **Host**.

Parameter description:
<table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Authentication method</td>
<td>Currently, three authentication signature calculation methods are supported. Select an appropriate one based on the access URL format. For more information, see <a href="#jqfs">Authentication Methods</a>.</td>
</tr>
<tr>
<td>Primary key</td>
<td>A primary key must be between 6-40 characters and contains letters and numbers.</td>
</tr>
<tr>
<td>Secondary key</td>
<td>A secondary key must be between 6-40 characters and contains letters and numbers.</td>
</tr>
<tr>
<td>Authentication parameter</td>
<td>An authentication parameter must be between 1-100 characters and contains letters, numbers and underscores. The parameter value will be authenticated by nodes.</td>
</tr>
<tr>
<td>Validity period</td>
<td>Validity period of the configured authentication URL, which is used to check whether the client access request expires. If the current time exceeds the time of "timestamp + validity period", the request will be considered expired, and 403 will be directly returned. If it hasn't expired, verification will continue.<br>Unit: Second.<br>Value range: 1–630720000.</td>
</tr>
</tbody></table>


## Notes
1. After the authentication is passed, the node will automatically ignore the URL after the authentication parameters and use it as the cache key to improve the cache hit rate and reduce the origin-pull traffic.
2. After the authentication is passed, if no node cache is hit, origin-pull will be performed, and the actual origin-pull URL will be in the same format as the authentication URL to retain the authentication parameters. You can configure the origin server to ignore authentication parameters or perform secondary verification as needed.
3. The access URL cannot contain any Chinese characters.

## Authentication Methods[](id:jqfs)

### Method A

#### Authentication URL format
```
http://Hostname/Filename?sign=timestamp-rand-uid-md5hash
```

#### Parameter description

| Field       | Description                                                         |
| --------- | ------------------------------------------------------------ |
| Hostname  | Site acceleration domain                                                 |
| Filename  | Actually accessed URL in origin-pull, which must start with `/`                              |
| sign      | Custom name of the authentication parameter                                   |
| timestamp | Timestamp carried in the access URL<br/>Format: Decimal (UNIX timestamp)      |
| rand      | Random string, which can contain 0–100 letters and digits                 |
| uid       | User ID. Default value: 0                                              |
| md5hash   | The string calculated with the MD5 algorithm: MD5(/Filename-timestamp-rand-uid-custom key)<br/>If the request hasn't expired, the node will compare this string value with the `md5hash` value carried in the access request:<li>If they are the same, the authentication will succeed, and the request will be responded to.</li><li>If they are different, the authentication will fail, and 403 will be returned.</li> |

### Method B

#### Authentication URL format
```
http://Hostname/timestamp/md5hash/Filename
```

#### Parameter description

| Field       | Description                                                         |
| --------- | ------------------------------------------------------------ |
| Hostname  | Site acceleration domain                                                 |
| Filename  | Actually accessed URL in origin-pull, which must start with `/`                              |
| timestamp | Timestamp carried in the access URL<br/>Format: YYYYMMDDHHMM               |
| md5hash   | The string calculated with the MD5 algorithm<br/>Algorithm: MD5(custom key + timestamp + /Filename)<br/><br/>If the request hasn't expired, the node will compare this string value with the `md5hash` value carried in the access request:<li>If they are the same, the authentication will succeed, and the request will be responded to.</li><li>If they are different, the authentication will fail, and 403 will be returned.</li> |

### Method C

**Authentication URL format**

```
http://Hostname/md5hash/timestamp/Filename
```

#### Parameter description

| Field       | Description                                                         |
| --------- | ------------------------------------------------------------ |
| Hostname  | Site acceleration domain                                                 |
| Filename  | Actually accessed URL in origin-pull, which must start with `/`                              |
| timestamp | Timestamp carried in the access URL<br/>Format: Hexadecimal (UNIX timestamp)    |
| md5hash   | The string calculated with the MD5 algorithm<br/>Algorithm: MD5(custom key + /Filename + timestamp)<br/><br/>If the request hasn't expired, the node will compare this string value with the `md5hash` value carried in the access request:<li>If they are the same, the authentication will succeed, and the request will be responded to.</li><li>If they are different, the authentication will fail, and 403 will be returned.</li> |
