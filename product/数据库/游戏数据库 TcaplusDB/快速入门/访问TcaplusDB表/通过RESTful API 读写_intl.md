[//]: # (chinagitpath:XXXXX)

This document describes the steps on how to access the TcaplusDB table through RESTful API.

After cluster creation, table group creation, and table creation, a TcaplusDB App data table is created. You can perform read and write operations on the App data table through the obtained access point information. This example shows how to use SetRecord and GetRecord APIs to perform read and write operations on the destination table.

>Operations must be performed in the CVM under your Tencent Cloud account.

In the following example, you received the following access point information and created a table tb_online in the table group with the TableGroupID  of 1.

* AccessID:2
* AppKey:3aa84dd773826cd655e9f24a249d68bb
* RESTful Access Point:10.123.9.70:31002
* TableGroupID:1

## Write Operation

Write a data to the table through the following HTTP requests. The corresponding request URL, HTTP request header, request data and response packet are as follows:

```
HTTP Method: POST
req_url:
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_online/records
Http header:
[
 "x-tcaplus-target:Tcaplus.SetRecord", 
 "x-tcaplus-version:Tcaplus3.32.0", 
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82", 
 "x-tcaplus-result-flag:1", 
 "x-tcaplus-data-version-check:1", 
 "x-tcaplus-data-version:-1", 
 "x-tcaplus-idl-type:Protobuf"
]
Data:
{
 "ReturnValues": "user define data", 
 "Record": {
  "name": "tcaplus_user", 
  "lockid": [
   50, 
   60, 
   70, 
   80, 
   90, 
   100
  ], 
  "pay": {
   "pay_times": 184, 
   "total_money": 100000, 
   "pay_id": 12000, 
   "auth": {
    "pay_keys": "njaklhewunfasdjnuonawef", 
    "update_time": 1544018596
   }
  }, 
  "region": 10, 
  "uin": 1024, 
  "is_available": true, 
  "gamesvrid": 5000, 
  "logintime": 100
 }
}
----------------------------------------
Resp Status 200
cost:9 ms
Response
{
 "ReturnValues": "aaaaaaaaaa", 
 "RecordVersion": 1, 
 "ErrorMsg": "Succeed", 
 "ErrorCode": 0, 
 "Record": {
  "name": "tcaplus_user", 
  "lockid": [
   50, 
   60, 
   70, 
   80, 
   90, 
   100
  ], 
  "pay": {
   "pay_times": 184, 
   "total_money": 100000, 
   "pay_id": 12000, 
   "auth": {
    "pay_keys": "njaklhewunfasdjnuonawef", 
    "update_time": 1544018596
   }
  }, 
  "region": 10, 
  "uin": 1024, 
  "is_available": true, 
  "gamesvrid": 5000, 
  "logintime": 100
 }
}
```

## Read Operation

Read the written data through the following HTTP requests. The corresponding request URL, HTTP request header, and response packet are as follows:

```
HTTP Method: GET
req_url:
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_online/records?keys=%7B%22region%22%3A%2010%2C%20%22name%22%3A%20%22tcaplus_user%22%2C%20%22uin%22%3A%201024%7D
HTTP request header:
[
 "x-tcaplus-target:Tcaplus.GetRecord", 
 "x-tcaplus-version:Tcaplus3.32.0", 
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82", 
 "x-tcaplus-idl-type:protobuf"
]
----------------------------------
Response status 200
Response:
{
 "RecordVersion": 2, 
 "Record": {
  "name": "tcaplus_user", 
  "lockid": [
   50, 
   60, 
   70, 
   80, 
   90, 
   100
  ], 
  "pay": {
   "pay_times": 184, 
   "total_money": 100000, 
   "pay_id": 12000, 
   "auth": {
    "pay_keys": "njaklhewunfasdjnuonawef", 
    "update_time": 1544018596
   }
  }, 
  "region": 10, 
  "uin": 1024, 
  "is_available": true, 
  "gamesvrid": 5000, 
  "logintime": 100
 }, 
 "ErrorMsg": "Succeed", 
 "ErrorCode": 0
}
```

## Example Program

The following section shows how to implement the two features in the above example through Python. For more information about table operations, see [Tcaplus RESTful API Documentation](https://intl.cloud.tencent.com/document/product/1016/30290).

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# author : tcaplus
# created : 2018.11.12
##########################
import sys
import time
import os
import json
import pycurl
import StringIO
import hashlib
from urllib import unquote, quote 

############################################
# User's app and table information
CGI_URL = "http://xx.xx.xx.xx:xxxxx/ver1.0"
APP_ID_INT = 2
ZONE_ID_INT = 1
GAME_KEY_STR = "xxxxxxxxxxxx"
TABLE_NAME_STR = "tb_online"
############################################

def op_get(url, header):
    '''Send Http Get request'''
    ret = None
    curl_fp = None

    try:  
        curl = pycurl.Curl()
        curl.setopt(pycurl.HTTPHEADER, header)
        curl.setopt(pycurl.CONNECTTIMEOUT, 60)
        curl.setopt(pycurl.TIMEOUT, 300)
        curl.setopt(pycurl.CUSTOMREQUEST, "GET")
        curl_fp = StringIO.StringIO()
        curl.setopt(pycurl.URL, url.encode('utf-8'))
        curl.setopt(curl.WRITEFUNCTION, curl_fp.write)
        curl.perform()
        ret = json.loads(curl_fp.getvalue())
        print "Resp Status %d" %(curl.getinfo(pycurl.RESPONSE_CODE))
        return ret
    except pycurl.error, err_msg:
        print err_msg
    finally:
        if curl_fp:
            curl_fp.close()
        curl.close()

def op_put(url, header, content):
    '''Send Http Put request'''
    ret = None
    try:
        curl = pycurl.Curl()
        curl.setopt(pycurl.HTTPHEADER, header)
        curl.setopt(pycurl.FOLLOWLOCATION, 1)
        curl.setopt(pycurl.MAXREDIRS, 5)
        curl.setopt(pycurl.CONNECTTIMEOUT, 60)
        curl.setopt(pycurl.TIMEOUT, 300)
        curl.setopt(pycurl.HTTPPROXYTUNNEL, 1)
        curl_fp = StringIO.StringIO()
        curl.setopt(pycurl.CUSTOMREQUEST, "PUT")
        curl.setopt(curl.POSTFIELDS, content)
        curl.setopt(pycurl.URL, str(url))
        curl.setopt(curl.WRITEFUNCTION, curl_fp.write)
        curl.perform()

        ret = json.loads(curl_fp.getvalue())
        print "Resp Status %d" %(curl.getinfo(pycurl.RESPONSE_CODE))
    except pycurl.error, err_msg:
        print err_msg
    finally:
        if curl_fp:
            curl_fp.close()
        curl.close()
    return ret

def test_GetRecord():
    # Enter key field
    keys ={"uin":1024,
           "name":"tcaplus_user",
           "region":10}

    # Enter http header
    header = []
    header.append("x-tcaplus-target:Tcaplus.GetRecord")
    header.append("x-tcaplus-version:Tcaplus3.32.0")
    header.append("x-tcaplus-pwd-md5:%s" %(hashlib.md5(GAME_KEY_STR).hexdigest()))
    header.append("x-tcaplus-idl-type:protobuf")

    # Set request URL
    # The select attribute must be URL-encoded.
    req = '%s/apps/%d/zones/%d/tables/%s/records?keys=%s' \
                    %(CGI_URL, APP_ID_INT, ZONE_ID_INT, TABLE_NAME_STR, quote(json.dumps(keys)))

    print "req_url:\n%s" %req
    print "Http header:"
    print header
    # Send Get request
    ret = op_get(req, header)
    print "Response:"
    print ret

def test_SetRecord():
    # Enter http header
    header = []
    header.append("x-tcaplus-target:Tcaplus.SetRecord")
    header.append("x-tcaplus-version:Tcaplus3.32.0")
    header.append("x-tcaplus-pwd-md5:%s" %(hashlib.md5(GAME_KEY_STR).hexdigest()))
    header.append("x-tcaplus-result-flag:1")
    header.append("x-tcaplus-data-version-check:1")
    header.append("x-tcaplus-data-version:-1")
    header.append("x-tcaplus-idl-type:Protobuf")

    str_user_buff = "test user buff"
    print "user buff len:%s" %(len(str_user_buff))

    # Data records to be set
    data = {}
    data["Record"] = {}
    data["Record"]["uin"] = 1024
    data["Record"]["name"] = "tcaplus_user"
    data["Record"]["region"] = 10
    data["Record"]["gamesvrid"] = 5000
    data["Record"]["logintime"] = 100
    data["Record"]["lockid"] = [50, 60, 70, 80, 90, 100]
    data["Record"]["is_available"] = True
    data["Record"]["pay"] = {}
    data["Record"]["pay"]["pay_id"] = 12000
    data["Record"]["pay"]["pay_times"] = 184
    data["Record"]["pay"]["total_money"] = 100000
    data["Record"]["pay"]["auth"] = {}
    data["Record"]["pay"]["auth"]["pay_keys"] = "njaklhewunfasdjnuonawef"
    data["Record"]["pay"]["auth"]["update_time"] = 1544018596
    data["ReturnValues"] = str_user_buff

    # Enter request
    req = '%s/apps/%d/zones/%d/tables/%s/records' \
                    %(CGI_URL, APP_ID_INT, ZONE_ID_INT, TABLE_NAME_STR)
    req_data_str = json.dumps(data)
    print "req_url:\n %s" %req
    print "Http header:"
    print header
    print "Data:"
    print '-' * 40
    print data
    print '-' * 40
    ret = op_put(req, header, req_data_str)
    print "Response"
    print ret

if __name__=='__main__':
    test_SetRecord()
    print '*' * 40
    test_GetRecord()
```

