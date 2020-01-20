## Overview
Tencent Cloud VOD offers hotlink protection to control the video playback permissions. After hotlink protection is enabled, a Tencent Cloud CDN node will check key information in the playback requests and return the video data only to approved requests. This scheme has no special requirements for players, that is, it is applicable to both the player SDK of VOD and common players.


## Types and Capabilities
VOD hotlink protection can prevent hotlinking based on referer and key.
<img src="https://main.qcloudimg.com/raw/a92778f479b70f6ff9d0eaa5d65b5589.png" width="450">

### Referer hotlink protection
The referer mechanism based on HTTP identifies the request source through the referer field in the playback request header. You can add specified domain names to a blacklist or whitelist, based on which the CDN node will authenticate to allow or deny the playback requests accordingly.

### Key hotlink protection
It allows you to splice a video's playback control parameters into the video URL in the form of `QueryString`. The CDN node will check the playback control parameters in the URL and control video playback accordingly. At present, key hotlink protection supports controlling "validity period", "viewer quantity", and "video playback duration" through corresponding parameters, i.e., "expiration time", "number of IPs allowed for playback", and "preview duration".

#### Validity period control
It specifies the expiration time of a video URL. If the requested video URL has expired, the video cannot be played back. In this way, you can set a validity period for the video URL to prevent malicious users from transferring the URL to other websites for long-term use.

#### Viewer quantity control
It specifies the number of viewers that can access the video URL. Devices that are not in the same private network generally have different public IPs. You can specify how many viewers are allowed to access an URL by limiting the number of IPs allowed for playback on the URL. This helps prevent malicious users from transferring the URL to other websites for unrestricted distribution.

#### Video playback duration control
It specifies the preview duration in a video URL (e.g., the first five minutes of a video) to implement preview for non-paying users.

>
>- For more information on referer hotlink protection, please see [Referer Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33985).
>- For more information on key hotlink protection, please see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986).
