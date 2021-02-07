
## API Description

**Request method**: POST.

```plaintext
Service address/v3/push/package/upload
```

The API service address corresponds to the service access point one by one; therefore, please select the service address corresponding to your application [service access point](https://intl.cloud.tencent.com/document/product/1024/38517).

**Feature**: you can upload a token package file for a batch of device tokens, and messages will be pushed by the tokens in it.

## Request Parameters 

| Parameter | Type | Required | Description |
| ------ | --------- | -------- | ------------------------------------------------------------ |
| file   | form-data | Yes       | <li>Token package format and size: `.zip`, `.txt`, or `.csv` file within 100 MB<li>The `.zip` package can contain a single `.txt` or `.csv` file but not folders.<li>`.txt` file requirements: (1) encoded in UTF-8; (2) one token (36 characters) per row<li>`.csv` file requirements: (1) one column only; (2) one token (36 characters) per row |

## Response Parameters

| Parameter | Type | Required | Description |
| -------- | ------- | -------- | ------------------------------------------------------------ |
| retCode  | Integer | Yes       | Error code                                                       |
| errMsg   | String   | Yes   | Error message when an error occurs in the request   |
| uploadId | Integer | Yes | When a file is uploaded, the `uploadId` is returned as a positive integer, which represents the ID of the uploaded file. It is provided to the push API for `Token` package pushes |


## Sample Request

#### Curl sample

```xml
curl -X POST 
https://api.tpns.tencent.com/v3/push/package/upload 
   
-H 'Authorization: basic application authorization information' 
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

>!For application authorization information, please see [Basic Auth Verification](https://intl.cloud.tencent.com/document/product/1024/34672).

