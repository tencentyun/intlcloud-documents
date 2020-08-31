## API Description

**Request method**: POST.

The API request address corresponds to the service access point one by one; therefore, please select the request address corresponding to your application service access point.

Service access point in Guangzhou:
```shell
https://api.tpns.tencent.com/v3/push/package/upload
```
Service access point in Hong Kong (China):
```shell
https://api.tpns.hk.tencent.com/v3/push/package/upload
```
Service access point in Singapore:
```shell
https://api.tpns.sgp.tencent.com/v3/push/package/upload
```

**Feature**: the user needs to upload account package files to batch accounts as files. The files in the account package must then be pushed. The account package push APIs mainly include the account package upload API and the account package push API.

>
- Request files are uploaded in form-data format, and the key is the `file`.
- The uploaded file must have a zip file extension, and only contains UTF-8-encoded txt files.
- Each line in a txt file represents one account, and the account length is limited to [2, 100].

## Parameter Description

#### Request parameters  

| Parameter Name | Type | Required | Description |
| --- | --- | --- | --- |
| file  | form-data | Yes  | Uploaded files must be zip files less than 100 MB. Each .zip file only contains UTF-8-encoded txt files, without any nested folders. Each line in a txt file represents one account, and the account length is limited to [2, 100].

#### Response parameters

| Parameter Name | Type | Required | Description |
| --- | --- | --- | --- |
| retCode   | Integer   | Yes   | Error code   |
| errMsg   | String   | Yes   | Error message when an error occurs in the request   |
| uploadId    | Integer   | Yes   | When a file upload succeeds, a positive integer uploadId will be provided, which represents the ID of the uploaded file. It is provided for the push of the subsequent account package API.   |


## Samples


Curl example
``` xml
curl -X POST 
https://api.tpns.tencent.com/v3/push/package/upload 
   
-H 'Authorization: basic application authorization information' 
-H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' 
-F 'file=@C:\File upload with absolute path'
  
```

Python example
``` python

import requests

url = "https://api.tpns.tencent.com/v3/push/package/upload"

boundary='----WebKitFormBoundary7MA4YWxkTrZu0gW'
data=[]
data.append('--%s' % boundary)
data.append('Content-Disposition: form-data; name="file"; filename="File name"\r\n')
fr=open('File address')
content=fr.read()
data.append(content)
fr.close()

data.append('\r\n')
data.append('--%s--\r\n' % boundary)
httpBody = '\r\n'.join(data)

headers = {
'content-type': "multipart/form-data,boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW",
    'Authorization': "Basic application authorization information",
    }
response = requests.request("POST", url, data=httpBody, headers=headers, verify=False)
print(response.text.encode('utf-8'))

```

>For application authorization information, please see [Basic Auth Authentication](https://intl.cloud.tencent.com/document/product/1024/34672).
