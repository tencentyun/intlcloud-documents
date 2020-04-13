## Algorithm Description
**Access URL format**
`http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`

**Algorithm description**
- timestamp: a decimal timestamp in UNIX format.
- rand: a random string consisting of 0–100 uppercase and lowercase letters and digits.
- uid: 0.
- md5hash: MD5 (file path-timestamp-rand-uid-custom key).

**Sample request**
`http://cloud.tencent.com/test/test.jpg?sign=1582791032-im1acp76sx9sdqe601v-0-dd63f95e739ed4b47427a129d21ef4e3`

>When MD5 value is calculated, if the request path is `http://cloud.tencent.com/test.jpg`, then the path used for MD5 calculation will be `/test.jpg`.

## Configuration Guide
### Parameter description
TypeA requires the following configuration:
![](https://main.qcloudimg.com/raw/242bbc36baa0225e38d854714f2296c1.png)
**Custom Authentication Key**: it contains 6–32 uppercase and lowercase letters and digits. The key should be kept private and known only to the client and server.
**Custom Authentication Parameter Name**: the `sign` in the example can be replaced with a parameter name containing 1–100 uppercase and lowercase letters, digits, and underscores. After CDN receives the request, it will read the value of the specified signature parameter and calculate the MD5 value. If the result matches the `md5hash` value passed in, the signature will be successfully verified. If not, a 403 error will be directly returned.
**Custom Validity Period**: the `timestamp` value in the request, plus the configured validity period, is compared with the current time to determine whether the request has expired. If yes, a 403 error will be directly returned. 

### Object
After configuring the key, parameter name, and validity period, you can specify the authentication object as needed. The following three modes are supported:
![](https://main.qcloudimg.com/raw/656f4ff6cef0e6b2a3022348a8293d4e.png)

+ All files under a specified domain name need to be authenticated.
+ All files except those in a specified type need to be authenticated.
+ Only files in a specified type need to be authenticated.

## Notes
**Cache hit rate**
If you have enabled the TypeA authentication mode for a domain name, the access URL will carry the authentication parameter. When a CDN node caches the resource, it will automatically ignore the authentication parameter and thus not affect the cache hit rate.
**Origin-pull policy**
The access format of a domain name with TypeA authentication mode enabled is as follows:
`http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`

If the CDN node is not hit after successful authentication, it will initiate an origin-pull request, **which is in the same format as the access request with the `sign` parameter retained.** The origin server can ignore it or perform authentication again as needed.
