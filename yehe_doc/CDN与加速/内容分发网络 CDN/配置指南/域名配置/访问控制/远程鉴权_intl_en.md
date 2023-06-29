## Remote Authentication

### Overview

To prevent unauthorized access, Tencent Cloud supports remote authentication in addition to [advanced timestamp authentication](https://intl.cloud.tencent.com/document/product/228/35237) at the CDN edge.

The following describes how remote authentication works:

![](https://qcloudimg.tencent-cloud.cn/raw/8f8d75de26e96ebaf58676eee0ca084a.png)

1. The end user initiates a request.
2. CDN forwards the request to the remote authentication server.
3. The authentication server returns a status code as the authentication result.
4. The CDN node responds to the requester according to the return code.

> !
> - When the return code is `200`/`206`/`304`, the authentication succeeded. For a successful authentication, the request is allowed with 200 returned; for an authentication failure, it is blocked with 403 returned.
> - For now, only synchronized remote authentication is supported, which means that CDN responds after receiving the authentication result from the remote authentication server.
> - Note that remote authentication is NOT supported in some regions outside the Chinese mainland.
> - Remote authentication is not available for audio and video resources



### Directions

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar. Click **Manage** on the right of the domain name to enter its configuration page. Configure remote authentication on the **Access Control** tab.

- **Server Address**: enter an HTTP/HTTPS domain name or an IP address.
- **Request Method**: select a request method. You can choose to follow client request or specify a request method (GET/POST/HEAD).
- **File Type**: set the authentication scope. You can choose **All content**/**Specified File Extension**/**Specified File**.
- **Timeout Period**: set the amount of response timeout period for the remote authentication server. The maximum value is 30,000 ms.
- **Timeout Action**: the action taken after the response timed out. The default value is **Allow**.

<img src="https://qcloudimg.tencent-cloud.cn/raw/02def6deb735b7defbbd26a86be9b022.png" width="60%">



### Sample

Assume the acceleration domain name is `www.example.com` and its remote authentication is configured as follows:

- **Server Address**: `www.remoteauth.com`
- **Request Method**: Follow client request
- **File Type**: All content
- **Timeout Period**: 1,500 ms
- **Timeout Action**: Block

CDN will respond to the user request as follows:
1. The user initiates a GET request: `http://www.example.com/v001/test.txt?token=Gf6Gq04ymjdSTXusvTmh8yalO82YsuKUQb63ToXOFc&e=1467565695283&sign=854124740723b575a7cfa4fc40f0be30`
2. CDN receives the request and forwards it to the remote authentication server: `http://www.remoteauth.com/v001/test.txt?token=Gf6Gq04ymjdSTXusvTmh8yalO82YsuKUQb63ToXOFc&e=1467565695283&sign=854124740723b575a7cfa4fc40f0be30`
3. The remote authentication server returns a status code.
4. CDN responds normally with 200 if the returned status code is 200 (i.e., the authentication passed).


