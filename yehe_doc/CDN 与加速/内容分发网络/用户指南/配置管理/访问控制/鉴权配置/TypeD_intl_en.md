## Algorithm Description
**Access URL format**
`http://DomainName/FileName?sign=md5hash&t=timestamp`

**Algorithm description**
- `timestamp`: a decimal or hexadecimal timestamp in UNIX format.
- `md5hash`: MD5 (custom key + file path + timestamp).

**Sample request**
`http://cloud.tenloud.tencent.com/test.jpg?sign=0f8201d814dfaf64cf54e74c5f7dbcb0&t=1582791032`

> !When the MD5 value is calculated, if the request path is `http://cloud.tencent.com/test.jpg`, then the path used for MD5 calculation will be `/test.jpg`.

## Configuration Guide
### Parameter Description
TypeD requires the following configurations:
![](https://main.qcloudimg.com/raw/6caae33f26a263699003ccb2e4e562c5.png)
**Custom authentication key**: it contains 6 to 40 digits and uppercase and lowercase letters. The key should be kept private and known only to the client and server.
**Custom authentication parameter name and timestamp parameter name**: the `sign` in the example can be replaced with a parameter name containing 1 to 100 uppercase and lowercase letters, digits, and underscores. After CDN receives the request, it will read the value of the specified signature parameter and calculate the MD5 value. If the result matches the `md5hash` value passed in, the signature will be successfully verified. If not, a 403 error will be directly returned.
**Custom validity period**: the `timestamp` value in the timestamp parameter, plus the configured validity period, is compared with the current time to determine whether the request has expired. If yes, a 403 error will be directly returned. The validity period is in seconds. 

### Object
After configuring the key, parameter name, and validity period, you can specify the authentication object as needed. The following three authentication modes are supported:
![](https://main.qcloudimg.com/raw/8a9b8c36cfc91a31cf96b31f0e6553c2.png)

+ All files under a specified domain name need to be authenticated.
+ All files except those in a specified type need to be authenticated.
+ Only files in a specified type need to be authenticated.

## Notes
**Cache hit rate**
If you have enabled the TypeD authentication mode for a domain name, the access URL will carry the authentication parameter. When a CDN node caches the resource, it will automatically ignore the corresponding parameter and thus will not affect the cache hit rate.
>!As the corresponding parameter will be automatically ignored after the configuration, i.e., the configured authentication and timestamp parameters will be filtered, the cache keys of the files to be authenticated will be affected, and the priority here is higher than the cache key rules in **Cache Configuration** -> **Cache Key Rule Configuration**.
For example, the TypeD configuration here is as: "Authentication Parameter: `sigh`"; "Timestamp Parameter: `t`"; "Authentication Scope: `jpg`"; then the `sign` and `t` parameters will be automatically filtered for JPG files even though the configuration is as "All Files: Do Not Filter" in **Cache Configuration** -> **Cache Key Rule Configuration**.

**Origin-pull policy**
The access format of a domain name with TypeD authentication mode enabled is as follows:
`http://DomainName/FileName?sign=md5hash&t=timestamp`

If the CDN node is not hit after successful authentication, it will initiate an origin-pull request, **which is in the same format as the access request with the `sign/t` parameter retained**. The origin server can ignore it or perform authentication again as needed.
