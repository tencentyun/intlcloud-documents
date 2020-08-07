
## Configuration Scenario
Generally, contents delivered over CDN are public resources by default, which can be accessed by users with URLs. To prevent malicious users from hotlinking your content for profit, you can configure advanced timestamp authentication in addition to access control policies such as referer blocklist/allowlist, IP blocklist/allowlist, and IP access frequency limit.

> !After timestamp hotlink protection is configured, the client needs to calculate the signature as configured and carry it to the server when initiating a request. The CDN node will authenticate the signature on the server, which will pass only after successful authentication.

## Configuration Guide
### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to access its configuration page. Under the **Security Configuration** tab, find the authentication configuration, which is disabled by default:
![](https://main.qcloudimg.com/raw/77831beaa25a77dd26b60e1f401c8dd3.png)

### Modifying configuration
#### 1. Modify the configuration
CDN provides four authentication signature calculation models of your choice. You can use the **Authentication Calculator** provided to view these models. For more information on the configuration effect and algorithms, please see the specific algorithm documents for [TypeA](https://intl.cloud.tencent.com/document/product/228/35222), [TypeB](https://intl.cloud.tencent.com/document/product/228/35223), [TypeC](https://intl.cloud.tencent.com/document/product/228/35224), and [TypeD](https://intl.cloud.tencent.com/document/product/228/35225):
![](https://main.qcloudimg.com/raw/ffd60184fa759b4c7a82a5a49634b8c3.png)

#### 2. Disable the configuration
You can toggle the authentication configuration switch to disable this feature. When the switch is off, any existing configuration will not take effect in the production environment. If you toggle the switch on, a message will be displayed asking for your confirmation before the configuration takes effect across the entire network.
![](https://main.qcloudimg.com/raw/5bb10025c5887793807e6b41dbea48a6.png)

#### 3. Add a region-specific configuration
If your acceleration domain name is configured for global acceleration and you want acceleration in and outside mainland China to have different authentication configurations, you can click **Add Special Configuration** under the configuration.
![](https://main.qcloudimg.com/raw/391372dbf734e813c45640dace716793.png)

> !Currently, an added region-specific configuration item cannot be deleted but can only be disabled.

## Configuration Sample
Suppose the domain name `cloud.tencent.com` is configured for global acceleration and the authentication configuration is as follows:
![](https://main.qcloudimg.com/raw/6f432b21603b61e4a1d9c17048a675bf.png)
The actual effect will be as follows:

1. A user in mainland China can access the resource `http://cloud.tencent.com/1.jpg` by directly initiating a request.
2. A user outside Mainland China can access the resource `http://cloud.tencent.com/1.jpg` by initiating a request with a URL in the format of `http://cloud.tencent.com/509301d10da7b862052927ed7a947f43/5e561139/1.jpg`.


## Sample Code

The following is the authentication calculation method with the Demo for Python as an example:

```
import requests
import json
import sys
import time
import hashlib

def generate_url(category, ts=None):
    url = 'http://www.test.com'              # Test domain name
    path = '/1.txt'                                     # Access path
    suffix = '?a=1&b=2'                                 # URL parameter
    key = 'abc123456789'                                # Authentication key
    now = int(time.mktime(time.strptime(ts, "%Y%m%d%H%M%S")) if ts else time.time())                # If a `ts` is entered, it will be used; otherwise, the current `ts` will be used
    sign_key = 'key'                                    # URL signature field
    time_key = 't'                                      # URL time field
    ttl_format = 10                                     # Time format. Valid values: 10, 16. This is supported only for type D
    if category == 'A':                                 # Type A
        ts = now
        rand_str = '123abc'
        sign = hashlib.md5('%s-%s-%s-%s-%s' % (path, ts, rand_str, 0, key)).hexdigest()
        request_url = '%s%s?%s=%s' % (url, path, sign_key, '%s-%s-%s-%s' % (ts, rand_str, 0, sign))
        print(request_url)
    elif category == 'B':                               # Type B
        ts = time.strftime('%Y%m%d%H%M', time.localtime(now))
        sign = hashlib.md5('%s%s%s' % (key, ts, path)).hexdigest()
        request_url = '%s/%s/%s%s%s' % (url, ts, sign, path, suffix)
        print(request_url)
    elif category == 'C':                               # Type C
        ts = hex(now)[2:]
        sign = hashlib.md5('%s%s%s' % (key, path, ts)).hexdigest()
        request_url = '%s/%s/%s%s%s' % (url, sign, ts, path, suffix)
        print(request_url)
    elif category == 'D':                               # Type D
        ts = now if ttl_format == 10 else hex(now)[2:]
        sign = hashlib.md5('%s%s%s' % (key, path, ts)).hexdigest()
        request_url = '%s%s?%s=%s&%s=%s' % (url, path, sign_key, sign, time_key, ts)
        print(request_url)


if __name__ == '__main__':
    if len(sys.argv) == 1:
        print('usage: python generate_url.py A 20200501000000')
    args = sys.argv[1:]
    generate_url(*args)
```
