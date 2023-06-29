You can add authentication to prevent hotlinking of your website. Tencent Cloud supports Type A, B, C and D authentication. This document describes details of Type A authentication.

## Algorithm Description

-  **Access URL format**
`http://DomainName/Filename?sign=timestamp-rand-uid-md5hash` 
>! The access URL cannot contain any Chinese characters.

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
<td>Filename</td>
<td>Resource access path. During authentication, `Filename` must start with a slash (<code>/</code>).</td>
</tr>
<tr>
<td>timestamp</td>
<td>The time when the server generates the authentication URL. It is a positive hex integer Unix timestamp, which is the total number of seconds between 00:00:00, January 1, 1970, UTC time and the URL generation time. Its definition is irrelevant to the time zone.</td>
</tr>
<tr>
<td>rand</td>
<td>A random string consisting 0-100 characters ([0-9], [a-z], [A-Z]).</td>
</tr>
<tr>
<td>uid</td>
<td>User ID (not in use), which defaults to 0. </td>
</tr>
<tr>
<td>md5hash</td>
<td>A string containing 32 characters calculated based on the MD5 algorithm. It is calculated as follows: <br>• `md5hash = md5sum(uri-timestamp-rand-uid-pkey)`.<br>• `uri`: It is the resource access path and must start with a slash (/).<br>• `timestamp`: Its value is the above `timestamp`.<br>• `rand`: Its value is the above `rand`.<br>• `uid`: Its value is the above `uid`.<br>• `pkey`: It can contain 6 to 40 letters and digits. It should be kept private and disclosed to only the client and server.</td>
</tr>
</tbody></table>
-  **Authentication logic description** 
After the CDN server receives a user request, it parses the `timestamp` parameter in the URL and the validity period of the authentication URL and compares it with the current time.
	1. If the sum of `timestamp` and the validity period of the authentication URL is before the current time, the server judges that the URL has expired and is invalid and returns the HTTP error code 403.
	2. If the sum of `timestamp` and the validity period of the authentication URL is after the current time, the server uses the MD5 algorithm to calculate the value of `md5hash` and it with the `md5hash` value passed in by the URL. If they are the same, the request will pass the authentication; otherwise, the HTTP error code 403 will be returned.

## Configuration Directions 

Here we take Type-A authentication as an example. 

- **Field configuration** 
	- Authentication key: dimtm5evg50ijsx2hvuwyfoiu65
	- Signature parameter: sign
	- Validity period of the authentication URL: 1s   
	<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/sR8D244_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423152051.png" width="80%">
	-  The time when the signature calculation server generates the authentication URL: 2020-02-27 16:10:32 (UTC+8). Its decimal integer value after conversion is `1582791032` (timestamp).
	-  Requested origin address: `http://www.mixcre.com/test/1.jpg`
- **Generation process**
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
<td>rand</td>
<td>Generate a random string: im1acp76sx9sdqe601v</td>
</tr>
<tr>
<td>uid</td>
<td>Set it to `0`</td>
</tr>
<tr>
<td>pkey</td>
<td>dimtm5evg50ijsx2hvuwyfoiu65</td>
</tr>
</tbody></table>
 - Concatenate the signature string: /test.jpg-1582791032-im1acp76sx9sdqe601v-0-dimtm5evg50ijsx2hvuwyfoiu65
 - Calculate the MD5 value of the signature string: md5hash =md5sum(uri-timestamp-rand-uid-pkey)= md5sum(/test.jpg-1582791032-im1acp76sx9sdqe601v-0-dimtm5evg50ijsx2hvuwyfoiu65) = 3fbb88382c9356b6faaf9d68c7b2ae3a

-   **Generate the authentication URL:** `http://www.mixcre.com/test/1.jpg?sign=1682234383-YES3WZ57u91G3zA1YYzh5Y3aIy6U2i0K-0-57b80424b3e6f9da4027fe13c00c44a7`
When the client uses the encryption URL for access, if the `md5hash` value calculated by the CDN server is the same as the `md5hash` value carried by the access request, which are both `3fbb88382c9356b6faaf9d68c7b2ae3a` in this example, the request will pass the authentication; otherwise, the authentication will fail.

## Notes

**Cache hit rate**

 For domain names using TypeA authentication mode, the access URL will carry the authentication parameter. When a CDN node caches the resource, the corresponding parameter will be ignored and thus will not affect the cache hit rate.

>!As the authentication parameter will be automatically ignored, the cache keys of the files to be authenticated will be affected, and the priority here is higher than the cache key rules in **Cache Configuration** -> **Cache Key Rule Configuration**.
For example, the Type A configuration here is as: "Authentication Parameter: `sign`"; "Authentication Scope: `jpg`"; then the `sign` parameter will be automatically ignored for JPG files even though the configuration is as "All Files: Not Ignore" in **Cache Configuration** -> **Cache Key Rule Configuration**.

**Origin-pull policy**

The access format of a domain name with Type A authentication mode enabled is as follows:
 `http://DomainName/Filename?sign=timestamp-rand-uid-md5hash` 

If the CDN node is not hit after successful authentication, it will initiate an origin-pull request, **which is in the same format as the access request with the `sign` parameter retained**. The origin server can ignore it or perform authentication again as needed.
