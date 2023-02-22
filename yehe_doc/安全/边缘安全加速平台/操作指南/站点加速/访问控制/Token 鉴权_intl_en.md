## Overview
As an access control policy, token authentication supports creating rules to validate access and filter out unauthorized access requests. This effectively prevents your site resources from being maliciously hotlinked and thus protects your business.

**How does token authentication implement access control?**
An authentication URL is generated based on the request URL and specified rule settings. When the node receives an access request, it does not serve resources until the authentication URL is validated successfully. Otherwise, the request is denied with a 403 error.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the page that displays, select the target site and create rules for token authentication as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).

<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Method</td>
<td align="left">Choose one of four available authentication methods. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1145/46164">Authentication Methods</a>.</td>
</tr>
<tr>
<td align="left">Primary key</td>
<td align="left">A primary authentication key must be between 6-40 characters and contains letters and numbers.</td>
</tr>
<tr>
<td align="left">Secondary key</td>
<td align="left">A secondary authentication key must be between 6-40 characters and contains letters and numbers.</td>
</tr>
<tr>
<td align="left">Authentication parameter</td>
<td align="left">An authentication parameter must be between 1-100 characters and contains letters, numbers and underscores. The parameter value will be authenticated by nodes.</td>
</tr>
<tr>
<td align="left">Validity period</td>
<td align="left">Validity period of the authentication URL (1-630720000 seconds). It determines whether a client request is valid:<ul><li>If the time "timestamp + validity period" is reached, the request is considered expired and a 403 is returned. </li><li>If it is not reached, the request is considered valid and will be authenticated.</td>
</tr>
</tbody></table>

## Authentication Methods
### Method A
#### Authentication URL format

```js.
http://Hostname/Filename?sign=timestamp-rand-uid-md5hash
```

#### Field description

| Field       | Description                                                         |
| :-------- | :----------------------------------------------------------- |
| Hostname  | Site domain name.                                                 |
| Filename  | Path to access the resource, which must start with "/".                  |
| sign      | Custom name of the authentication parameter.                                   |
| timestamp | Unix timestamp.<br/>Format: A positive decimal integer, indicating the number of seconds elapsed since 00:00:00, January 1, 1970 at UTC. It does not change regardless of your time zone. |
| rand      | Random string, which contains letters and digits. Length: 0–100.                 |
| uid       | User ID (not in use), which defaults to 0.                                    |
| md5hash   | A fixed-length 32-bit string calculated with the MD5 algorithm:<li>Authentication algorithm: MD5 (/Filename-timestamp-rand-uid-key)</li><li>Authentication logic: When receiving a valid request, the node starts comparing this string value with the `md5hash` value in the request URL. If they match, the node will respond to the request after it is authenticated, otherwise it returns a 403.</li> |

### Method B

#### Authentication URL format

```js.
http://Hostname/timestamp/md5hash/Filename
```

#### Field description

| Field       | Description                                                         |
| :-------- | :----------------------------------------------------------- |
| Hostname  | Site domain name.                                                 |
| Filename  | Path to access the resource, which must start with "/".                  |
| timestamp | Timestamp.<br/>Format: YYYYMMDDHHMM (represented in UTC+8), such as 201807301000. |
| md5hash   | A fixed-length 32-bit string calculated with the MD5 algorithm:<li>Authentication algorithm: MD5 (key + timestamp + /Filename)</li><li>Authentication logic: When receiving a valid request, the node starts comparing this string value with the `md5hash` value in the request URL. If they match, the node will respond to the request after it is authenticated, otherwise it returns a 403.</li> |

### Method C

**Authentication URL format**

```js.
http://Hostname/md5hash/timestamp/Filename
```

#### Field description

| Field       | Description                                                         |
| :-------- | :----------------------------------------------------------- |
| Hostname  | Site domain name.                                                 |
| Filename  | Path to access the resource, which must start with "/".                  |
| timestamp | Unix timestamp.<br/>Format: A positive hex integer, indicating the number of seconds elapsed since 00:00:00, January 1, 1970 at UTC. It does not change regardless of your time zone.|
| md5hash   | A fixed-length 32-bit string calculated with the MD5 algorithm:<li>Authentication algorithm: MD5 (key + /Filename + timestamp). Note that you should remove the identifier 0x from a hex timestamp before calculation.</li><li>Authentication logic: When receiving a valid request, the node starts comparing this string value with the `md5hash` value in the request URL. If they match, the node will respond to the request after it is authenticated, otherwise it returns a 403.</li> |

### Method D

#### Authentication URL format

```js.
http://Hostname/Filename?sign=md5hash&t=timestamp
```

#### Field description

| Field       | Description                                                         |
| :-------- | :----------------------------------------------------------- |
| Hostname  | Site domain name.                                                 |
| Filename  | Path to access the resource, which must start with "/".                  |
| sign      | Custom name of the authentication parameter.                                     |
| t         | Custom name of the timestamp parameter.                                 |
| timestamp | Unix timestamp. <br/>Format: A positive decimal/hex integer, indicating the number of seconds elapsed since 00:00:00, January 1, 1970 at UTC. It does not change regardless of your time zone.|
| md5hash   | A fixed-length 32-bit string calculated with the MD5 algorithm:<li>Authentication algorithm: MD5 (key + /Filename + timestamp). Note that you should remove the identifier 0x from a hex timestamp before calculation.</li><li>Authentication logic: When receiving a valid request, the node starts comparing this string value with the `md5hash` value in the request URL. If they match, the node will respond to the request after it is authenticated, otherwise it returns a 403.</li> |

## Configuration Sample

The following configuration sample shows how to authenticate a request for `http://www.example.com/test.jpg` with Method A:

![](https://qcloudimg.tencent-cloud.cn/raw/573aa274a93ffe436fd69c7f62d2000a.png)

#### Getting authentication parameters
- /Filename: `/foo.jpg`
- imestamp: `1647311432`. The timestamp is returned as a 10-digit positive decimal integer indicating that the authentication URL is generated at 10:30:32, March 15, 2022 (UTC+8).
- rand: `J0ehJ1Gegyia2nD2HstLvw`
- uid：`0`
- key: `3C9mxSGzc8ZadmGNzE`
- md5hash: MD5 (/Filename-timestamp-rand-uid-key) = MD5 (`/foo.jpg`-`1647311432`-`J0ehJ1Gegyia2nD2HstLvw`-`0`-`3C9mxSGzc8ZadmGNzE`) = ecce3150cbdaac83b116d937777ca77f

#### Generating an authentication URL
`http://www.example.com/foo.jpg?sign=1647311432-J0ehJ1Gegyia2nD2HstLvw-0-ecce3150cbdaac83b116d937777ca77f`

#### Authenticating the request

After the request is initiated via an encrypted URL, the node parses the value of the "timestamp" parameter from the URL to determine whether the request is valid:
<dx-steps>
- If the time "timestamp + validity period" is reached, the request is considered expired and a 403 is returned.
- If the time "timestamp + validity period" is not reached, the request is considered valid and will be authenticated.
- The node compares the calculated `md5hash` value with the `md5hash` value in the request URL. If they match, the node will respond to the request after it is authenticated, otherwise it returns a 403.
</dx-steps>

## Must-knows
1. If the authentication succeeds, the authentication parameters in the request URL will be ignored during origin-pull and used as the cache key to increase the cache hit rate.
2. If the authenticated request does not hit the node cache, the request will be forwarded to the origin to retrieve resources. The authentication parameters in the authentication URL (which is identical as the origin-pull URL in this case) can either be used to authenticate again or ignored as needed by setting [origin-pull request parameters](https://www.tencentcloud.com/document/product/1145/52036).
3. The origin-pull request URL cannot contain any Chinese characters.
