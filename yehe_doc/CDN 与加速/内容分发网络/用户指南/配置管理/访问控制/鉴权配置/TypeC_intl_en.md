## Algorithm Description
**Access URL format**
`http://DomainName/md5hash/timestamp/FileName`

**Algorithm description**
- timestamp: a hex timestamp in UNIX format.
- md5hash: MD5 (custom key + file path + timestamp).

**Sample request**
`http://cloud.tencent.com/8fe9b5597c809d7ace147468c7c7eadb/5e577978/test/test.jpg`

>When the MD5 value is calculated, if the request path is `http://cloud.tencent.com/test.jpg`, then the path used for MD5 calculation will be `/test.jpg`.

## Configuration Guide
### Parameter description
TypeC requires the following configuration:
![](https://main.qcloudimg.com/raw/396248d32cc6b09760d60cad3fd9412d.png)
**Custom Authentication Key**: it contains 6–32 uppercase and lowercase letters and digits. The key should be kept private and known only to the client and server.
**Custom Validity Period**: the `timestamp` value in the request path, plus the configured validity period, is compared with the current time to determine whether the request has expired. If yes, a 403 error will be directly returned.

### Object
After configuring the key, parameter name, and validity period, you can specify the authentication object as needed. The following three modes are supported:
![](https://main.qcloudimg.com/raw/df138e80a34d1c6cb98c9caadaef3cf5.png)
+ All files under a specified domain name need to be authenticated.
+ All files except those in a specified type need to be authenticated.
+ Only files in a specified type need to be authenticated.

## Notes
**Cache hit rate**
If you have enabled TypeC authentication for a domain name, it will be carried in the access URL path. When a CDN node caches the resource, it will automatically ignore the authentication path and thus not affect the cache hit rate.
**Origin-pull policy**
The access format of a domain name with TypeC authentication mode enabled is as follows:
`http://DomainName/md5hash/timestamp/FileName`

If the CDN node is not hit after successful authentication, it will initiate an origin-pull request, **in which the `md5hash` and `timestamp` will be removed from the path.** The origin server does not need to process the authentication information.
