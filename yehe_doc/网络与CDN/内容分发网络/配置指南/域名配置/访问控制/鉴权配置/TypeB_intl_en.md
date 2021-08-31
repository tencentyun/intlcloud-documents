## Algorithm Description
**Access URL format**
`http://DomainName/timestamp/md5hash/FileName`

**Algorithm description**
- timestamp: A timestamp in the format of `YYYYMMDDHHMM`.
- md5hash: MD5 (custom key + timestamp + file path).

**Sample request**
`http://cloud.tencent.com/202003032017/b91bad39a0f9c885ddebd6b6164de3c4/test.jpg`

> !When the MD5 value is calculated, if the request path is `http://cloud.tencent.com/test.jpg`, then the path used for MD5 calculation will be `/test.jpg`.

## Configuration Guide

### Parameter description
TypeB requires the following configurations:
![](https://main.qcloudimg.com/raw/d0cd00305ed4911a500995628bd45cfd.png)
**Custom Authentication Key**: it can contain 6 to 40 digits, uppercase and lowercase letters. It should be kept private and disclosed to only the client and server.
**Custom Validity Period**: the `timestamp` value in the request path plus the configured validity period is compared with the current time to determine whether the request has expired; if so, a 403 error will be directly returned.

### Object
After configuring the key, parameter name, and validity period, you can specify the authentication object as needed. The following three authentication modes are supported:
![](https://main.qcloudimg.com/raw/13ccf23f34aaa9963e2ca36ea48b36f0.png)
- All files under a specified domain name need to be authenticated.
- All files except those of a specified type need to be authenticated.
- Only files of a specified type need to be authenticated.

## Notes:
**Cache hit rate**
If you have enabled TypeB authentication for a domain name, the signature and timestamp will be carried in the access URL path. When a CDN node caches a resource, it will automatically ignore the fields in the path and thus not affect the cache hit rate.
**Origin-pull policy**
The access format of a domain name with TypeB authentication mode enabled is as follows:
`http://DomainName/timestamp/md5hash/FileName`

If no hits are found on the CDN node after successful authentication, the node will initiate an origin-pull request, **in which the `md5hash` and `timestamp` will be removed from the path.** The origin server does not require any configuration.

