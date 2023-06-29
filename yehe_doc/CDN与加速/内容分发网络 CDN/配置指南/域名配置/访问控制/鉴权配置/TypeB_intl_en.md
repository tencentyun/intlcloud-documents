To protect your site resources from being downloaded or stolen by unauthorized users, you can choose an authentication method from Types A, B, C, and D as needed. This document describes parameter fields and their purposes in TypeC authentication.

## Algorithm Description

**Access URL format**
`http://DomainName/timestamp/md5hash/FileName`
>! The access URL cannot contain any Chinese characters.

-  **Description of authentication fields**

| Field | Description |
|--|--|

| Filename  | Path to access the resource, which must start with "/".                  |

<td>A string containing 32 characters calculated based on the MD5 algorithm. It is calculated as follows: <br>•  There are no symbols between parameters in `md5hash = md5sum(pkeytimestampuri)`. <br>•  pkey: It can contain 6–40 letters and digits. It should be kept private and disclosed to only the client and server. <br>•   uri: It is the resource access path and must start with a slash (/). <br>•  timestamp: Its value is the above `timestamp`.</td>

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

</tr>
<tr>
<td>pkey</td>
<td>dimtm5evg50ijsx2hvuwyfoiu65</td>
</tr>
</tbody></table>

   - Concatenate the signature string: dimtm5evg50ijsx2hvuwyfoiu65202002271610/test.jpg
   - Calculate the MD5 value of the signature string: md5hash = md5sum(pkeytimestampuri) =md5sum(dimtm5evg50ijsx2hvuwyfoiu651582791032/test.jpg) = ea68b93ac23ebbc6eebf7f163c6e9c4c

-   **Generate the authentication URL:**

When the client uses the encryption URL for access, if the `md5hash` value calculated by the CDN server is the same as the `md5hash` value carried by the access request, which are both `ea68b93ac23ebbc6eebf7f163c6e9c4c` in this example, the request will pass the authentication; otherwise, the authentication will fail.
## Limits 

**Cache hit rate**

If you have enabled TypeB authentication for a domain name, the signature and timestamp will be carried in the access URL path. When a CDN node caches a resource, it will automatically ignore the fields in the path, which does not affect the cache hit rate.

**Origin-pull policy**

The access format of a domain name with TypeB authentication mode enabled is as follows:
 `http://DomainName/timestamp/md5hash/FileName` 

If no hits are found on the CDN node after successful authentication, it will initiate an origin-pull request, **in which the `md5hash` and `timestamp` will be removed from the path.** The origin server does not need to process the authentication information.
