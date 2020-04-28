## API Description
**Request method**: POST.
``` POST   
https://api.tpns.tencent.com/v3/push/package/upload
```
**Feature**: the user needs to upload number package files to batch accounts via files. The files in the number package must then be pushed. The number package push APIs mainly include the number package upload API and the number package push API.





>
- Request files are uploaded in form-data format, and the key is the `file`.
- The uploaded file must have a zip file extension, and the compressed contents must be a txt file.
- Each line in a txt file represents one account, and the account length is limited to [2, 100].

## Parameter Description

#### Request parameters  

| Parameter Name | Type | Required | Description |
| --- | --- | --- | --- |
| file  | form-data  | Yes  | Uploaded files must be zip files less than 100 MB. The contents of each zip file must be a txt file, and there can be no nested folders. Each line in a txt file represents one account, and the account length is limited to [2, 100].

#### Response parameters

| Parameter Name | Type | Required | Description |
| --- | --- | --- | --- |
| retCode   | int32\_t   | Yes   | Error code   |
| errMsg   | string   | Yes   | Error message when an error occurs in the request   |
| uploadId    | int32   | Yes   | When a file upload succeeds, a positive integer uploadId will be provided, which represents the ID of the uploaded file. It is provided for the push of the subsequent number package API.   |


## Samples


Curl sample
``` xml
curl -X POST 
https://api.tpns.tencent.com/v3/push/package/upload 
   
-H 'Authorization: basic application authorization information' 
-H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' 
-F 'file=@C:\File upload with absolute path'
  
```

Python sample
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

>!For application authorization information, please see [Basic Auth Authentication](https://intl.cloud.tencent.com/document/product/1024/34672).