## Description of the Feature 
Tencent Cloud COS has hotlink protection, and it is recommended that you configure the blacklist/whitelist in Hotlink Protection Settings in the console for security protection purpose.
<span id="Case of Hotlinking"></span>
## Case of Hotlinking
User A uploaded the image resource `1.jpg` in COS, got the access link `http://test-1250000000.cosgz.myqcloud.com/1.jpg`, and embedded the image in his web page `http://a.com/a.html`, which can be accessed normally.
User B saw the image on `a.com` and embedded the link of `1.jpg` in his web page `http://b.com/b.html` which can also display the image normally.
In the above case, A's image `1.jpg` was hotlinked by B. A was not aware of its COS resource was continuously used by B's web page and A paid for the extra traffic cost. 

## How to Determine Hotlink Protection
Hotlink protection is determined by Referer in the request Header:
-  Referer is part of the Header. Referer is generally added when the browser sends a request to the Web server to indicate the page from which the request is linked, and the server can allow or deny access to resources by websites from certain sources.
-  If you directly open the file link `http://test-1250000000.cosgz.myqcloud.com/1.jpg` in the browser, the request Header will not contain Referer.

In the following figure, for example, `1.jpg` is embedded in `http://127.0.0.1/test/test.html`, and the Referer that points to the access source is added when you access `test.html`:
![referer_1](//mc.qcloudimg.com/static/img/f000c8ee64ae569f08680c495ddb1b7b/image.png)
## How to Set Hotlink Protection in the Console
### Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos4/index), click **Bucket List** in the left sidebar, and click the bucket for which you want to set hotlink protection to enter the bucket. 
2. In the bucket details page, click **Basic Configuration**, find Hotlink Protection Settings, and click **Edit**.
![](//mc.qcloudimg.com/static/img/3d76b7e130d8917a41c4b2b7e8b1a730/image.png)
3. Set the current status to Enabled, select a list type (blacklist or whitelist), enter applicable domain names, and then click **Save**. After enabling Hotlink Protection, you must enter applicable domain names.
![](//mc.qcloudimg.com/static/img/14919513b487b1bac4a6617618e6de78/image.png)

### Setting rules
-  Select blacklist or whitelist:
    * Blacklist: Domain names on this list are not allowed to access the default access address of the bucket. 403 is returned if any domain name on the list accesses such address.
    * Whitelist: Only domain names on this list are allowed to access the default access address of the bucket. 403 is returned if any domain name not on the list accesses such address.
- Examples
    * Domain names and IPs with ports are supported, such as `test.com:8080` and `10.10.10.10:8080`.
    * Configuring `test.com` will hit addresses prefixed with `test.com`, such as `test.com/123` and `test.com.cn`.
    * Configuring `test.com` will hit addresses prefixed with `test.com`, such as `https://test.com` and `http://test.com`.
    * Configuring `test.com` will hit its domain name with port `test.com:8080`. 
    * Configuring `test.com:8080` will not hit the domain name `test.com`.
    * Configuring `test.com` will limit its second-level and third-level domain names `test.com`, `b.test.com`, and `a.b.test.com`.
- A maximum of 10 addresses including domain names and IPs are supported. Wildcard `*` in addresses is allowed and domain names with the same prefix are also subject to the list. One address per line.

## Configuration Example
We use the [Case of Hotlinking](https://intl.cloud.tencent.com/document/product/436/6226) above as an example to introduce how user A can set hotlink protection and prevent user B from hotlinking images:
1. User A sets hotlink protection rules for the bucket "test". You can use one of the following methods to prevent `b.com` from hotlinking based on the actual situation:
 - Method 1: Configure the blacklist by entering the domain name `*.b.com`, and save it.

 - Method 2: Configure the whitelist by entering the domain name `*.a.com`, and save it.
2. After hotlink protection is enabled:
 - The image is displayed normally when `http://a.com/a.html` is accessed.

 - The image cannot be displayed when `http://b.com/b.html` is accessed, as shown below.
![referer_4](//mc.qcloudimg.com/static/img/e58fab402a31ccc903ee3941dbb08eee/image.png)

## FAQs
Why the hotlink protection still did not work after I enabled the CDN acceleration for the bucket and used CDN domain name to access resources?
> Since you are using a CDN domain name, the resources will be cached in the CDN, resulting in unstable performance. You need to configure hotlink protection in the [CDN Console](https://console.cloud.tencent.com/cdn).

Can I set a whitelist to allow access and access resources when I open a link in the browser?
> When you directly open a link in the browser, Referer is empty. Referer cannot be configured separately.

The whitelist of hotlink protection for the bucket "test" is set to allow access to `a.com`, but the Web Player under `a.com` cannot play video files under the bucket "test".
> When you open a video link and use Windows Media Player, Flash Player and other players to play the video on the web page, the Referer in the request is empty, in which case its domain name on the whitelist is not hit. It is recommended to configure a blacklist to ensure normal access when Referer is empty.

