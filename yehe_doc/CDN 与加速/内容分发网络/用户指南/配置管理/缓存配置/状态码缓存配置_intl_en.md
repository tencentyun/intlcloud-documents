
## Configuration Overview
Normally, when a CDN node successfully pulls a requested resource from the origin server (with a 2XX status code returned), the node will process the resource based on the rules in the node cache validity configuration.
If the origin server cannot immediately process the non-2XX status codes and you do not want that all requests pass through the origin server, you can configure the status code cache validity period so the CDN node will directly respond to non-2XX status code, helping reduce pressure on the origin server.
Currently supported status codes are as follows:
- 4XX: 400, 401, 403, 404, 405, 407, 414
- 5XX: 500, 501, 502, 503, 504, 509, 514

>! Some platforms are being upgraded and only support status codes 404 and 403.


## Configuration Guide

### Viewing configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Cache Configuration** tab to find the **Status Code Cache** section.
There is a default rule: Status Code: 404; Cache Time: 10 seconds.
![](https://main.qcloudimg.com/raw/4584bfd2e219918025199968bfaa9d81.png)

### Adding rules
You can click **Add Rule** to add status code cache rules as needed.

![](https://main.qcloudimg.com/raw/6bb67eb1ad2be9744d8af289ad289111.jpg)


Configuration limitations:
- Each status code can only have one unique rule.
- The cache time `0` means not to cache content.
