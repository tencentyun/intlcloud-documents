To protect your site resources from being downloaded or stolen by unauthorized users, you can choose an authentication method from Types A, B, C, and D as needed. This document describes parameter fields and their purposes in TypeC authentication.

## Algorithm Description

**Access URL format**
`http://DomainName/FileName?sign=md5hash&t=timestamp`
>! The access URL cannot contain any Chinese characters.
>
-  **Description of authentication fields**
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>DomainName</td>
<td>CDN domain.</td>
</tr>
<tr>
<td>filename</td>
<td>Resource access path. During authentication, `Filename` must start with a slash (<code>/</code>).</td>
</tr>
<tr>
<td>timestamp</td>
<td>The time when the server generates the authentication URL. It is a positive hex integer Unix timestamp, which is the total number of seconds between 00:00:00, January 1, 1970, UTC time and the URL generation time. Its definition is irrelevant to the time zone.</td>
</tr>
<tr>
<td>md5hash</td>
<td>A string containing 32 characters calculated based on the MD5 algorithm. It is calculated as follows: <br>•  There are no symbols between parameters in `md5hash = md5sum(pkeytimestampuri)`. <br>•  pkey: It can contain 6–40 letters and digits. It should be kept private and disclosed to only the client and server. <br>•   uri: It is the resource access path and must start with a slash (/). <br>•  timestamp: Its value is the above `timestamp`.</td>
</tr>
</tbody></table>
-  **Authentication logic description**
After the CDN server receives a user request, it parses the `timestamp` parameter in the URL and the validity period of the authentication URL and compares it with the current time.
  1. If the sum of `timestamp` and the validity period of the authentication URL is before the current time, the server judges that the URL has expired and is invalid and returns the HTTP error code 403.
  2. If the sum of `timestamp` and the validity period of the authentication URL is after the current time, the server uses the MD5 algorithm to calculate the value of `md5hash` and it with the `md5hash` value passed in by the URL. If they are the same, the request will pass the authentication; otherwise, the HTTP error code 403 will be returned.

## Directions 

**Taking the configuration of TypeC authentication as an example, the parameters and console configuration items are configured as follows:** 

- **Field configuration**
  - Authentication key: dimtm5evg50ijsx2hvuwyfoiu65
  - Validity period of the authentication URL: 1s   
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/FsKK054_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16715089128415.png" width="600" />
  -    The time when the signature calculation server generates the authentication URL: 2020-02-27 16:10:32 (UTC+8). Its decimal integer value after conversion is `1582791032` (timestamp).
  -    Requested origin address: `http://cloud.tencent.com/test.jpg`
- Generation process
  - Get authentication parameters:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Value</th>
</tr>
</thead>
<tbody><tr>
<td>URI</td>
<td>Resource access path, which is `/test.jpg`.</td>
</tr>
<tr>
<td>timestamp</td>
<td>1582791032</td>
</tr>
<tr>
<td>pkey</td>
<td>dimtm5evg50ijsx2hvuwyfoiu65</td>
</tr>
</tbody></table>
   - Concatenate the signature string: dimtm5evg50ijsx2hvuwyfoiu651582791032/test.jpg
   - Calculate the MD5 value of the signature string: md5hash = md5sum(pkeytimestampuri) =md5sum(dimtm5evg50ijsx2hvuwyfoiu651582791032/test.jpg) = ea68b93ac23ebbc6eebf7f163c6e9c4c
-   **Generate the authentication URL:**

When the client uses the encryption URL for access, if the `md5hash` value calculated by the CDN server is the same as the `md5hash` value carried by the access request, which are both `ea68b93ac23ebbc6eebf7f163c6e9c4c` in this example, the request will pass the authentication; otherwise, the authentication will fail.

## Limits

**Cache hit rate**
If you have enabled the TypeD authentication mode for a domain name, the access URL will carry the authentication parameter. When a CDN node caches the resource, it will automatically ignore the corresponding parameter and thus will not affect the cache hit rate.

>!
>!As the authentication parameter will be automatically ignored, the cache keys of the files to be authenticated will be affected, and the priority here is higher than the cache key rules in **Cache Configuration** -> **Cache Key Rule Configuration**.
For example, the TypeD configuration here is as: "Authentication Parameter: `sigh`"; "Timestamp Parameter: `t`"; "Authentication Scope: `jpg`"; then the `sign` and `t` parameters will be automatically filtered for JPG files even though the configuration is as "All Files: Do Not Filter" in **Cache Configuration** -> **Cache Key Rule Configuration**.

**Origin-pull policy** 
The access format of a domain name with TypeD authentication mode enabled is as follows:
 `http://DomainName/FileName?sign=md5hash&t=timestamp` 

If the CDN node is not hit after successful authentication, it will initiate an origin-pull request, **which is in the same format as the access request with the `sign/t` parameter retained**. The origin server can ignore it or perform authentication again as needed.
