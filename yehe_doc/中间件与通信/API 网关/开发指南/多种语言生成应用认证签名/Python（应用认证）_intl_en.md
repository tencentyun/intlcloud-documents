## Overview

This document describes how to use the application-enabled authentication mode for the authentication management of your APIs in Python.

## Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as **App Authentication**. To learn more about the authentication types, please find the documentation for different types of backends in [Creating API - Overview](https://intl.cloud.tencent.com/document/product/628/11795).
2. Publish the service where the API resides to an environment. See [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page in the console.
4. Select the created application in the application list, click **Bind API**, select the service and API, and click **Submit** to bind the application to the API.
5. Generate signing information in Python by referring to the [Sample Code](#sample-code).

## Environmental Dependencies

API Gateway provides sample codes for Python 2.7 and Python 3 and provides code samples for JSON request mode and form request mode. Please select an appropriate mode according to your business needs.

## Notes

- For more information on operations such as application lifecycle management, authorizing an app to access the API, and binding an app with an API, please see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For the application signature generation process, please see [Application Authentication](https://intl.cloud.tencent.com/document/product/628/40304).


## Sample Code[](id:sample-code)
### Sample code for Python 2.7 JSON request mode
<dx-codeblock>
:::  python
# -*- coding: utf-8 -*-
import base64
import datetime
import hashlib
import hmac
import json
import requests


Url = 'http://service-xxxxxxxx-1234567890.cq.apigw.tencentcs.com/app'
Host = 'service-xxxxxxxx-1234567890.cq.apigw.tencentcs.com'
#Application ApiAppKey
ApiAppKey = 'APIDkva7jni5ihyaaaaaaaaavyz7scdnxdhhba9'
#Application ApiAppSecret
ApiAppSecret = '5rbMhtz2Q44ZxyaaaaaaaaaNBeWjnO9Qgwz537wv'


# Obtain the signature string
GMT_FORMAT = '%a, %d %b %Y %H:%M:%S GMT'
xDate = datetime.datetime.utcnow().strftime(GMT_FORMAT)
HTTPMethod = "POST"
Accept = 'application/json'
ContentType = 'application/json'
body = {
    "arg1": "a",
    "arg2": "b"
}
body_json = json.dumps(body)
ContentMD5 = base64.b64encode(hashlib.md5(body_json).hexdigest())
signing_str = 'x-date: %s\n%s\n%s\n%s\n%s\n/app' % (
    xDate, HTTPMethod, Accept, ContentType, ContentMD5)


# Calculate the signature
sign = hmac.new(ApiAppSecret, msg=signing_str, digestmod=hashlib.sha1).digest()
sign = base64.b64encode(sign)
auth = "hmac id=\"" + ApiAppKey + "\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\""
sign = auth + sign + "\""


# Send the request
headers = {
    'Host': Host,
    'Accept': Accept,
    'Content-Type': ContentType,
    'x-date': xDate,
    'Authorization': sign
}

ret = requests.post(Url, headers=headers, data=body_json)
print(ret.text)
:::
</dx-codeblock>



### Sample code for Python 2.7 form request mode
<dx-codeblock>
:::  python
# -*- coding: utf-8 -*-
import base64
import datetime
import hashlib
import hmac
import requests


Url = 'http://service-xxxxxxxx-1234567890.hk.apigw.tencentcs.com/app'
Host = 'service-xxxxxxxx-1234567890.hk.apigw.tencentcs.com'
#Application ApiAppKey
ApiAppKey = 'APID4I7Ic3DPy83aaaaaaaaan2fwtwe1ywl64fof'
#Application ApiAppSecret
ApiAppSecret = '42A6S7ZUpK2UL6Faaaaaaaa1rz2qe22RU6h4mT5'


# Obtain the signature string
GMT_FORMAT = '%a, %d %b %Y %H:%M:%S GMT'
xDate = datetime.datetime.utcnow().strftime(GMT_FORMAT)
HTTPMethod = "POST"
Accept = 'application/json'
ContentType = 'application/x-www-form-urlencoded'
ContentMD5 = ''
body = {
    "arg1": "a",
    "arg2": "b"
}
sorted_body = sorted(body)
signing_str = 'x-date: %s\n%s\n%s\n%s\n%s\n/app?%s=%s&%s=%s' % (
    xDate, HTTPMethod, Accept, ContentType, ContentMD5, sorted_body[0], body[sorted_body[0]], sorted_body[1],
    body[sorted_body[1]])


# Calculate the signature
sign = hmac.new(ApiAppSecret, msg=signing_str, digestmod=hashlib.sha1).digest()
sign = base64.b64encode(sign)
auth = "hmac id=\"" + ApiAppKey + "\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\""
sign = auth + sign + "\""


# Send the request
headers = {
    'Host': Host,
    'Accept': Accept,
    'Content-Type': ContentType,
    'x-date': xDate,
    'Authorization': sign
}

ret = requests.post(Url, headers=headers, data=body)
print(ret.text)
:::
</dx-codeblock>



### Sample code for Python 3 JSON request mode
<dx-codeblock>
:::  python
# -*- coding: utf-8 -*-
import base64
import datetime
import hashlib
import hmac
import json
import requests


Url = 'http://service-xxxxxxxx-1234567890.cq.apigw.tencentcs.com/app'
Host = 'service-xxxxxxxx-1234567890.cq.apigw.tencentcs.com'
#Application ApiAppKey
ApiAppKey = 'APIDkva7jni5ihyaaaaaaaaavyz7scdnxdhhba9'
#Application ApiAppSecret
ApiAppSecret = '5rbMhtz2Q44ZxyaaaaaaaaaNBeWjnO9Qgwz537wv'


# Obtain the signature string
GMT_FORMAT = '%a, %d %b %Y %H:%M:%S GMT'
xDate = datetime.datetime.utcnow().strftime(GMT_FORMAT)
HTTPMethod = "POST"
Accept = 'application/json'
ContentType = 'application/json'
body = {
    "arg1": "a",
    "arg2": "b"
}
body_json = json.dumps(body)
body_md5 = hashlib.md5(body_json.encode()).hexdigest()
ContentMD5 = base64.b64encode(body_md5.encode()).decode()
signing_str = 'x-date: %s\n%s\n%s\n%s\n%s\n/app' % (
    xDate, HTTPMethod, Accept, ContentType, ContentMD5)


# Calculate the signature
sign = hmac.new(ApiAppSecret.encode(), msg=signing_str.encode(), digestmod=hashlib.sha1).digest()
sign = base64.b64encode(sign).decode()
auth = "hmac id=\"" + ApiAppKey + "\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\""
sign = auth + sign + "\""


# Send the request
headers = {
    'Host': Host,
    'Accept': Accept,
    'Content-Type': ContentType,
    'x-date': xDate,
    'Authorization': sign
}

ret = requests.post(Url, headers=headers, data=body_json)
print(ret.text)
:::
</dx-codeblock>



### Sample code for Python 3 form request mode
<dx-codeblock>
:::  python
# -*- coding: utf-8 -*-
import base64
import datetime
import hashlib
import hmac
import requests


Url = 'http://service-xxxxxxxx-1234567890.hk.apigw.tencentcs.com/app'
Host = 'service-xxxxxxxx-1234567890.hk.apigw.tencentcs.com'
#Application ApiAppKey
ApiAppKey = 'APID4I7Ic3DPy83aaaaaaaaan2fwtwe1ywl64fof'
#Application ApiAppSecret
ApiAppSecret = '42A6S7ZUpK2UL6Faaaaaaaa1rz2qe22RU6h4mT5'


# Obtain the signature string
GMT_FORMAT = '%a, %d %b %Y %H:%M:%S GMT'
xDate = datetime.datetime.utcnow().strftime(GMT_FORMAT)
HTTPMethod = "POST"
Accept = 'application/json'
ContentType = 'application/x-www-form-urlencoded'
ContentMD5 = ''
body = {
    "arg1": "a",
    "arg2": "b"
}
sorted_body = sorted(body)
signing_str = 'x-date: %s\n%s\n%s\n%s\n%s\n/app?%s=%s&%s=%s' % (
    xDate, HTTPMethod, Accept, ContentType, ContentMD5, sorted_body[0], body[sorted_body[0]], sorted_body[1],
    body[sorted_body[1]])


# Calculate the signature
sign = hmac.new(ApiAppSecret.encode(), msg=signing_str.encode(), digestmod=hashlib.sha1).digest()
sign = base64.b64encode(sign).decode()
auth = "hmac id=\"" + ApiAppKey + "\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\""
sign = auth + sign + "\""


# Send the request
headers = {
    'Host': Host,
    'Accept': Accept,
    'Content-Type': ContentType,
    'x-date': xDate,
    'Authorization': sign
}

ret = requests.post(Url, headers=headers, data=body)
print(ret.text)
:::
</dx-codeblock>

