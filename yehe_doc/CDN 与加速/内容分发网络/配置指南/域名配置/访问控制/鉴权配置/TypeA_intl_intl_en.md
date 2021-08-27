## Algorithm Description
**Access URL format**
`http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`

>! The access URL cannot contain any Chinese characters.

**Algorithm description**
- `timestamp`: a decimal timestamp in UNIX format.
- `rand`: a random string consisting of 0 to 100 digits, uppercase and lowercase letters.
- `uid`: 0.
- `md5hash`: MD5 (file path-timestamp-rand-uid-custom key).

**Request sample**
`http://cloud.tencent.com/test.jpg?sign=1582791032-im1acp76sx9sdqe601v-0-dd63f95e739ed4b47427a129d21ef4e3`

> ! Supposing that you are calculating the MD5 for the request path `http://cloud.tencent.com/test.jpg`, then the path used for MD5 calculation will be `/test.jpg`.

## Directions
### Parameter description
TypeA requires the following configurations:
![](https://main.qcloudimg.com/raw/b7da5881cba4ad972aa11f43bc2bc2ca.png))
**Authentication Key**: supports 6–40 uppercase and lowercase letters and digits. The key must be kept private and known only to the client and server.
**Signature Parameter Name**: the `sign` in the example can be replaced with a parameter name containing 1 to 100 uppercase and lowercase letters, digits, and underscores. After CDN receives the request, it will read the value of the specified signature parameter and calculate the MD5 value. If the result matches the `md5hash` value passed in, the signature will be successfully verified. If not, a 403 error will be directly returned.
**Valid Time**: decides whether the request has expired by comparing the `timestamp` value in the request plus the configured validity period with the current time. If expired, a 403 error will be directly returned. The validity period can be up to 630720000 seconds.

### Object
After configuring the key, parameter name, and validity period, you can specify the authentication object as needed. The following three authentication modes are supported:
![](https://main.qcloudimg.com/raw/148f6319984b1f3d99ccb186666cb425.png)

+ All files under a specified domain name need to be authenticated.
+ All files except those in a specified type need to be authenticated.
+ Only files in a specified type need to be authenticated.

## Notes
**Cache hit rate**
For domain names using TypeA authentication mode, the access URL will carry the authentication parameter. When a CDN node caches the resource, the corresponding parameter will be ignored and thus will not affect the cache hit rate.
>!As the authentication parameter will be automatically ignored, the cache keys of the files to be authenticated will be affected, and the priority here is higher than the cache key rules in **Cache Configuration** -> **Cache Key Rule Configuration**.
For example, the Type A configuration here is as: "Authentication Parameter: `sign`"; "Authentication Scope: `jpg`"; then the `sign` parameter will be automatically ignored for JPG files even though the configuration is as "All Files: Not Ignore" in **Cache Configuration** -> **Cache Key Rule Configuration**.


**Origin-pull policy**
The access format of a domain name with Type A authentication mode enabled is as follows:
`http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`

If the CDN node is not hit after successful authentication, it will initiate an origin-pull request, **which is in the same format as the access request with the `sign` parameter retained**. The origin server can ignore it or perform authentication again as needed.
