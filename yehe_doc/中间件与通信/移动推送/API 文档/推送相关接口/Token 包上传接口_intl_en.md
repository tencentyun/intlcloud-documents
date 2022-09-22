
## API Description

**Request method**: POST

```plaintext
Service URL/v3/push/package/upload
```

API service URLs correspond to service access points one by one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: you can upload a token package file for a batch of device tokens, and messages will be pushed by the tokens in it.

## Request Parameters 

| Parameter | Type | Required | Description |
| ------ | --------- | -------- | ------------------------------------------------------------ |
| file   | form-data | Yes       | <li>Token package file name: [1, 100] characters</li><li>Token package format and size: `.zip`, `.txt`, or `.csv` file within 100 MB</li><li>`.zip` file requirements: contains a single `.txt` or `.csv` file but not folders</li><li>`.txt` file requirements: encoded in UTF-8; one token (36 characters) per row</li><li>`.csv` file requirements: one column only; one token (36 characters) per row</li> |

## Response Parameters

| Parameter | Type | Required | Description |
| -------- | ------- | -------- | ------------------------------------------------------------ |
| retCode  | Integer | Yes       | Error code                                                       |
| errMsg   | String  | Yes       | Error message when a request error occurs                                        |
| uploadId | Integer | Yes | When a file is uploaded, `uploadId` is provided as a positive integer, which represents the ID of the uploaded file. It is provided to the push API for token package push. |


## Sample Request

#### Curl sample

```xml
curl -X POST 
https://api.tpns.tencent.com/v3/push/package/upload 
   
-H 'Authorization: Basic application authorization information' 
-F 'file=@C:\Absolute path of the uploaded file'
```



#### Python sample

```python
import requests

url = "https://api.tpns.tencent.com/v3/push/package/upload"

files = {'file':open('file name', 'rb')}
upload_data={"fileName": "absolute file address"}

headers = {
    'Authorization': "Basic application authorization information",
    }

response = requests.request("POST", url, data=upload_data, headers=headers, files=files, verify=False)
print(response.text.encode('utf-8'))
```

>!For more information on the application authorization, please see [Basic Auth Verification](https://intl.cloud.tencent.com/document/product/1024/34672).

