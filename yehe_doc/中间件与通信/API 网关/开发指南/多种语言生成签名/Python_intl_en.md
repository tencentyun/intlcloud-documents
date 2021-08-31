## Operation Scenarios

This document describes how to authenticate and manage your APIs through key pair authentication in Python.

## Directions
1. In the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as "key pair authentication" (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create a key pair on the key management page in the console.
4. Create a usage plan on the usage plan page in the console and bind it to the created key pair (for more information, please see [Sample Usage Plan](https://intl.cloud.tencent.com/document/product/628/11816)).
5. Bind the usage plan to the API or the service where the API resides.
6. Generate signing information in Python by referring to the [Sample Code](#example).

## Environment Dependencies
API Gateway provides sample code for Python v2.7 and v3. Please select one according to the version of your Python.

## Notes
- The eventually delivered HTTP request contains at least two headers: `Date` or `X-Date` and `Authorization`. More optional headers can be added in the request. If `Date` is used, the server will not check the time; if `X-Date` is used, the server will check the time.
- The value of `Date` header is the construction time of the HTTP request in GMT format, such as Fri, 09 Oct 2015 00:00:00 GMT.
- The value of `X-Date` header is the construction time of the HTTP request in GMT format, such as Mon, 19 Mar 2018 12:08:40 GMT. It cannot deviate from the current time for more than 15 minutes.
- If it is a microservice API, you need to add two fields in the header: `X-NameSpace-Code` and `X-MicroService-Name`. They are not needed for general APIs and are included in the demo by default.

<span id="example"></span>
### Sample code for Python v2.7
```python
# -*- coding: utf-8 -*-
import requests
import datetime
import hashlib
from hashlib import sha1
import hmac
import base64


GMT_FORMAT = '%a, %d %b %Y %H:%M:%S GMT'

def getSimpleSign(source, SecretId, SecretKey) :
    dateTime = datetime.datetime.utcnow().strftime(GMT_FORMAT)
    auth = "hmac id=\"" + SecretId + "\", algorithm=\"hmac-sha1\", headers=\"date source\", signature=\""
    signStr = "date: " + dateTime + "\n" + "source: " + source
    sign = hmac.new(SecretKey, signStr, hashlib.sha1).digest()
    sign = base64.b64encode(sign)
    sign = auth + sign + "\""
    return sign, dateTime

SecretId = 'your SecretId' # `SecretId` in key pair
SecretKey = 'your SecretKey' # `SecretKey` in key pair
url = 'http://service-xxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com/release/xxx' # API access path

#header = {}
header = { 'Host':'service-xxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com', # Service domain name of API
            'Accept': 'text/html, */*; q=0.01',
            'X-Requested-With': 'XMLHttpRequest',
            'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.89 Safari/537.36',
            'Accept-Encoding': 'gzip, deflate, sdch',
            'Accept-Language': 'zh-CN,zh;q=0.8,ja;q=0.6'
}

Source = 'xxxxxx' # Arbitrary signature watermark value
sign, dateTime = getSimpleSign(Source, SecretId, SecretKey)
header['Authorization'] = sign
header['Date'] = dateTime
header['Source'] = Source

# If it is a microservice API, you need to add two fields in the header: 'X-NameSpace-Code' and 'X-MicroService-Name'. They are not needed for general APIs.
header['X-NameSpace-Code'] = 'testmic'
header['X-MicroService-Name'] = 'provider-demo'

print header

r = requests.get(url, headers=header)
print r
print r.text
```

### Sample code for Python v3

```
# -*- coding: utf-8 -*-
import base64
import datetime
import hashlib
import hmac

import requests

GMT_FORMAT = '%a, %d %b %Y %H:%M:%S GMT'


def getSimpleSign(source, SecretId, SecretKey):
    dateTime = datetime.datetime.utcnow().strftime(GMT_FORMAT)
    auth = "hmac id=\"" + SecretId + "\", algorithm=\"hmac-sha1\", headers=\"date source\", signature=\""
    signStr = "date: " + dateTime + "\n" + "source: " + source
    sign = hmac.new(SecretKey.encode(), signStr.encode(), hashlib.sha1).digest()
    sign = base64.b64encode(sign).decode()
    sign = auth + sign + "\""
    return sign, dateTime


SecretId = 'your SecretId'  # SecretId in key pair
SecretKey = 'your SecretKey'  # SecretKey in key pair
url = 'http://service-xxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com/release/xxx'  # API access path

header = {'Host': 'service-xxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com',  # Service domain name of API
          'Accept': 'text/html, */*; q=0.01',
          'X-Requested-With': 'XMLHttpRequest',
          'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.89 Safari/537.36',
          'Accept-Encoding': 'gzip, deflate, sdch',
          'Accept-Language': 'zh-CN,zh;q=0.8,ja;q=0.6'
          }
Source = 'xxxxxx'  # Arbitrary signature watermark value
sign, dateTime = getSimpleSign(Source, SecretId, SecretKey)
header['Authorization'] = sign
header['Date'] = dateTime
header['Source'] = Source


r = requests.get(url, headers=header)
print(r.text)
```

