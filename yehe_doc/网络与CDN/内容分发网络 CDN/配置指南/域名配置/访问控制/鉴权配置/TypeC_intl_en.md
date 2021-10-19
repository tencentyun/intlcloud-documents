## Algorithm Description
**Access URL format**
`http://DomainName/md5hash/timestamp/FileName`

**Algorithm description**
- timestamp: A hex timestamp in UNIX format.
- md5hash: MD5 (custom key + file path + timestamp).

**Sample request**
`http://cloud.tencent.com/8fe9b5597c809d7ace147468c7c7eadb/5e577978/test.jpg`

> !When the MD5 value is calculated, if the request path is `http://cloud.tencent.com/test.jpg`, then the path used for MD5 calculation will be `/test.jpg`.

## Configuration Guide
### Parameter description
TypeC requires the following configurations:
![](https://main.qcloudimg.com/raw/d7b8d589f8690f1e4c33985d6bcd3f09.png)
**Custom Authentication Key**: it can contain 6 to 40 digits, uppercase and lowercase letters. It should be kept private and disclosed to only the client and server.
**Custom Validity Period**: the `timestamp` value in the request path plus the configured validity period is compared with the current time to determine whether the request has expired; if so, a 403 error will be directly returned.

### Object
After configuring the key, parameter name, and validity period, you can specify the authentication object as needed. The following three authentication modes are supported:
![](https://main.qcloudimg.com/raw/34d27c8908808cacddfde94c8a3f1d81.png)
+ All files under a specified domain name need to be authenticated.
+ All files except those of a specified type need to be authenticated.
+ Only files of a specified type need to be authenticated.

## Notes:
**Cache hit rate**
If you have enabled TypeC authentication for a domain name, the signature and timestamp will be carried in the access URL path. When a CDN node caches a resource, it will automatically ignore the authentication path and thus not affect the cache hit rate.
**Origin-pull policy**
The access format of a domain name with TypeC authentication mode enabled is as follows:
`http://DomainName/md5hash/timestamp/FileName`

If no hits are found on the CDN node after successful authentication, the node will initiate an origin-pull request, **in which the `md5hash` and `timestamp` will be removed from the path.** The origin server does not require any configuration.
