### API Description
**Request method**: POST.
``` POST   
https://api.tpns.tencent.com/v3/push/package/upload
```
**Description**: The user needs to upload number package files to batch accounts as files. The files in the number package must then be pushed. The number package push APIs mainly include the number package upload API and the number package push API.





>
- Request files are uploaded in form-data format, and the key is the `file`.
- The uploaded file must have a zip file extension, and the compressed contents must be a txt file.
- Each line in a txt file represents one account, and the account length is limited to [2, 100].

## Parameter Descriptions

#### Request Parameters  

| Parameter name | Type | Required | Description |
| --- | --- | --- | --- |
| file  | form-data  | Yes  | Uploaded files must be zip files that are 100M or less in size. The contents of each zip file must be a txt file, and there can be no nested folders. Each line in a txt file represents one account, and the account length is limited to [2, 100].

#### Response Parameters

| Parameter name | Type | Required | Description |
| --- | --- | --- | --- |
| retCode   | int32\_t   | Yes   | Error code   |
| errMsg   | string   | Yes   | Error message when an error occurs in the request   |
| uploadId    | int32   | Yes   | When a file upload succeeds, a positive integer uploadId will be provided, which represents the ID of the uploaded file. It is provided for the push of the subsequent number package API.   |


## Example(s)


Curl example
```xml
curl -X POST 
https://api.tpns.tencent.com/v3/push/package/upload 
   
-H 'Authorization: Basic application authorization information' 
-H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' 
-F 'file=@C:\Uploaded file’s absolute path'
  
```

Python example
```python

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
    'Authorization': "Basic authorization information",
    }
response = requests.request("POST", url, data=httpBody, headers=headers, verify=False)
print(response.text.encode('utf-8'))

```






