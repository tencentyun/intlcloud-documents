## Overview

This document describes how to use the application-enabled authentication mode for the authentication management of your APIs in Python.

## Operation Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as **App authentication**. To learn more about the authentication types, please find the documentation for different types of backends in [Creating API - Overview](https://intl.cloud.tencent.com/document/product/628/11795).
2. Release the service where the API resides to an environment. See [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page in the console.
4. Select the created application in the application list, click **Bind API**, select the service and API, and click **Submit** to bind the application to the API.
5. Generate signing information in Python by referring to the [Sample Code](#Sample-Code).

## Environmental Dependencies

API Gateway provides sample codes for Python 2.7 and Python 3 with the request body in JSON format and form-data format. Please select as needed.

## Note

- For more information on operations such as application lifecycle management, authorizing an app to access the API, and binding an app with an API, please see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For the application signature generation process, please see [Application Authentication](https://intl.cloud.tencent.com/document/product/628/40304).


## Sample Code[](id:Sample-Code)

### Sample code for Python 2.7 with the request body in JSON format
<dx-codeblock>
:::  python
# -*- coding: utf-8 -*-
import base64
import datetime
import hashlib
import hmac
import json
import requests
from urlparse import urlparse

# Application's `ApiAppKey`
ApiAppKey = 'Your ApiAppKey'
# Application's `ApiAppSecret`
ApiAppSecret = 'Your ApiAppSecret'

# apigw access address
Url = 'http://service-xxx-xxx.gz.apigw.tencentcs.com/'
HTTPMethod = 'GET'  # method
Accept = 'application/json'
ContentType = 'application/json'

urlInfo = urlparse(Url)
Host = urlInfo.hostname
Path = urlInfo.path

# Environment information is not included in the signature path
if Path.startswith(('/release', '/test', '/prepub')) :
    Path = '/' + Path[1:].split('/',1)[1]
Path = Path if Path else '/'

# Splice query parameters. The query parameters need to be sorted in lexicographical order.
if urlInfo.query :
    queryStr = urlInfo.query
    splitStr = queryStr.split('&')
    splitStr = sorted(splitStr)
    sortStr = '&'.join(splitStr)
    Path = Path + '?' + sortStr 

ContentMD5 = ''
GMT_FORMAT = '%a, %d %b %Y %H:%M:%S GMT'
xDate = datetime.datetime.utcnow().strftime(GMT_FORMAT)

# Modify body content
if HTTPMethod == 'POST' :
    body = { "arg1": "a", "arg2": "b" }
    body_json = json.dumps(body)
    ContentMD5 = base64.b64encode(hashlib.md5(body_json).hexdigest())

# Obtain the signature string
signing_str = 'x-date: %s\n%s\n%s\n%s\n%s\n%s' % (
    xDate, HTTPMethod, Accept, ContentType, ContentMD5, Path)

# Compute the signature
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
if(HTTPMethod == 'GET'):
    ret = requests.get(Url, headers=headers)
if(HTTPMethod == 'POST'):
    ret = requests.post(Url, headers=headers, data=body_json)

print(ret.headers)
print(ret.text)
:::
</dx-codeblock>




### Sample code for Python 2.7 with the request body in form-data format
<dx-codeblock>
:::  python
# -*- coding: utf-8 -*-
import base64
import datetime
import hashlib
import hmac
import json
import requests
import urllib
from urlparse import urlparse

# Application's `ApiAppKey`
ApiAppKey = 'Your ApiAppKey'
# Application's `ApiAppSecret`
ApiAppSecret = 'Your ApiAppSecret'

# apigw access address
Url = 'http://service-xxx-xxx.gz.apigw.tencentcs.com/'
HTTPMethod = 'POST'  # method
Accept = 'application/json'
ContentType = 'application/x-www-form-urlencoded'

urlInfo = urlparse(Url)
Host = urlInfo.hostname
Path = urlInfo.path

# Environment information is not included in the signature path
if Path.startswith(('/release', '/test', '/prepub')) :
    Path = '/' + Path[1:].split('/',1)[1]
Path = Path if Path else '/'

ContentMD5 = ''
GMT_FORMAT = '%a, %d %b %Y %H:%M:%S GMT'
xDate = datetime.datetime.utcnow().strftime(GMT_FORMAT)

# Modify body content
body = { "arg1": "a", "arg2": "b" }
argBody = urllib.urlencode(body)

# When signing, the form parameters are spliced with the query parameters. The parameters need to be sorted in lexicographical order.
if urlInfo.query :
    argBody = argBody + '&' + urlInfo.query

splitStr = argBody.split('&')
argBody = sorted(splitStr)
sortStr = '&'.join(argBody)
Path = Path + '?' + sortStr

# Obtain the signature string
signing_str = 'x-date: %s\n%s\n%s\n%s\n%s\n%s' % (
    xDate, HTTPMethod, Accept, ContentType, ContentMD5, Path)

# Compute the signature
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
if(HTTPMethod == 'GET'):
    ret = requests.get(Url, headers=headers)
if(HTTPMethod == 'POST'):
    ret = requests.post(Url, headers=headers, data=body)

print(ret.headers)
print(ret.text)
:::
</dx-codeblock>



### Sample code for Python 3 with the request body in form-data format
<dx-codeblock>
:::  python
# -*- coding: utf-8 -*-
import base64
import datetime
import hashlib
import hmac
import json
import requests
from urllib.parse import urlparse
from urllib.parse import urlencode

# Application's `ApiAppKey`
ApiAppKey = 'Your ApiAppKey'
# Application's `ApiAppSecret`
ApiAppSecret = 'Your ApiAppSecret'

# apigw access address
Url = 'http://service-xxx-xxx.gz.apigw.tencentcs.com/'
HTTPMethod = 'POST'  # method
Accept = 'application/json'
ContentType = 'application/x-www-form-urlencoded'

urlInfo = urlparse(Url)
Host = urlInfo.hostname
Path = urlInfo.path

# Environment information is not included in the signature path
if Path.startswith(('/release', '/test', '/prepub')) :
    Path = '/' + Path[1:].split('/',1)[1]
Path = Path if Path else '/' 

ContentMD5 = ''
GMT_FORMAT = '%a, %d %b %Y %H:%M:%S GMT'
xDate = datetime.datetime.utcnow().strftime(GMT_FORMAT)

# Modify body content
body = { "arg1": "a", "arg2": "b" }
argBody = urlencode(body)

# When signing, the form parameters are spliced with the query parameters. The parameters need to be sorted in lexicographical order.
if urlInfo.query :
    argBody = argBody + '&' + urlInfo.query

splitStr = argBody.split('&')
argBody = sorted(splitStr)
sortStr = '&'.join(argBody)
Path = Path + '?' + sortStr

# Obtain the signature string
signing_str = 'x-date: %s\n%s\n%s\n%s\n%s\n%s' % (
    xDate, HTTPMethod, Accept, ContentType, ContentMD5, Path)

# Compute the signature
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

if HTTPMethod == 'GET' :
    ret = requests.get(Url, headers=headers)
if HTTPMethod == 'POST' :
    ret = requests.post(Url, headers=headers, data=body)

print(ret.headers)
print(ret.text)
:::
</dx-codeblock>



