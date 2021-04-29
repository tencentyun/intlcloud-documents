## Algorithm Description
**Access URL format**
`http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`

**Algorithm description**
- `timestamp`: a decimal timestamp in UNIX format.
- `rand`: a random string consisting of 0 to 100 digits, uppercase and lowercase letters.
- `uid`: 0.
- `md5hash`: MD5 (file path-timestamp-rand-uid-custom key).

**Sample request**
`http://cloud.tencent.com/test.jpg?sign=1582791032-im1acp76sx9sdqe601v-0-dd63f95e739ed4b47427a129d21ef4e3`

> !When the MD5 value is calculated, if the request path is `http://cloud.tencent.com/test.jpg`, then the path used for MD5 calculation will be `/test.jpg`.

## Configuration Guide
### Parameter Description
TypeA requires the following configurations:
![](https://main.qcloudimg.com/raw/b7da5881cba4ad972aa11f43bc2bc2ca.png)
**Custom authentication key**: it contains 6 to 40 digits and uppercase and lowercase letters. The key should be kept private and known only to the client and server.
**Custom authentication parameter name**: the `sign` in the example can be replaced with a parameter name containing 1 to 100 uppercase and lowercase letters, digits, and underscores. After CDN receives the request, it will read the value of the specified signature parameter and calculate the MD5 value. If the result matches the `md5hash` value passed in, the signature will be successfully verified. If not, a 403 error will be directly returned.
**Custom validity period**: the `timestamp` value in the request, plus the configured validity period, is compared with the current time to determine whether the request has expired. If yes, a 403 error will be directly returned. The validity period is in seconds.

### Object
After configuring the key, parameter name, and validity period, you can specify the authentication object as needed. The following three authentication modes are supported:
![](https://main.qcloudimg.com/raw/148f6319984b1f3d99ccb186666cb425.png)

+ All files under a specified domain name need to be authenticated.
+ All files except those in a specified type need to be authenticated.
+ Only files in a specified type need to be authenticated.

## Notes
**Cache hit rate**
If you have enabled the TypeA authentication mode for a domain name, the access URL will carry the authentication parameter. When a CDN node caches the resource, it will automatically ignore the corresponding parameter and thus will not affect the cache hit rate.
>!As the corresponding parameter will be automatically ignored after the configuration, i.e., the configured authentication parameter will be filtered, the cache keys of the files to be authenticated will be affected, and the priority here is higher than the cache key rules in **Cache Configuration** -> **Cache Key Rule Configuration**.
For example, the TypeA configuration here is as: "Authentication Parameter: `sigh`"; "Authentication Scope: `jpg`"; then the `sign` parameter will be automatically filtered for JPG files even though the configuration is as "All Files: Do Not Filter" in **Cache Configuration** -> **Cache Key Rule Configuration**.


**Origin-pull policy**
The access format of a domain name with TypeA authentication mode enabled is as follows:
`http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`

If the CDN node is not hit after successful authentication, it will initiate an origin-pull request, **which is in the same format as the access request with the `sign` parameter retained**. The origin server can ignore it or perform authentication again as needed.
