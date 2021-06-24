## Overview

This document describes how to use the application-enabled authentication mode for the authentication management of your APIs in Python.

## Directions

1. Create an API in the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), and select “Application-Enabled” as the authentication type. For details, see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795).
2. Publish the service to which the API belongs to the release environment. For details, see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page.
4. Select the application you created in the application list and click **Bind API**. In the pop-up window, select a service and an API, and click **Submit**. Then you can bind the selected API to the application.
5. Generate signing information in Python by referring to the [Sample Code](#sample code).

## Environmental Dependencies

API Gateway provides sample codes for Python 2.7 and Python 3. Please select as needed.

## Notes

- For information on application lifecycle management, API authorization, and how to bind an API to an application, please see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For information on signature generation, please see [Application-Enabled Authentication](https://intl.cloud.tencent.com/document/product/628/40304).

[](id: sample code)
## Sample Code

### Sample codes for Python 2.7
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



### Sample codes for Python 3

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

