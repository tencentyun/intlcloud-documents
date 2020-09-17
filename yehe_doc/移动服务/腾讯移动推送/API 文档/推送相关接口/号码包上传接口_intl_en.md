## API Description

**Request method**: POST

The API request address is corresponding to the service access point. Select the request address corresponding to the service access point of your application.

Service access point in Guangzhou, China:
```plaintext
https://api.tpns.tencent.com/v3/push/package/upload
```
Service access point in Hong Kong, China:
```plaintext
https://api.tpns.hk.tencent.com/v3/push/package/upload
```
Service access point in Singapore:
```plaintext
https://api.tpns.sgp.tencent.com/v3/push/package/upload
```
Service access point in Shanghai:

```plaintext
https://api.tpns.sh.tencent.com/v3/push/package/upload
```

**Feature**: this API is used to batch upload account package files.

>!
- The account package is in `.zip` format and less than 100 MB in size.
- The account package contains only one `.txt` or `.csv` file. Nested folders are not allowed.
- The `.txt` file is encoded using UTF-8. Each row contains only one account, and the account length is limited to [2, 100].
- The `.csv` file can contain only one column. Each row contains only one account, and the account length is limited to [2, 100].

## Parameters

#### Request parameters  

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| file  | form-data | Yes | <li>The uploaded account package must be in `.zip` format and less than 100 MB in size.<li>The account package contains only one `.txt` or `.csv` file. Nested folders are not allowed.<li>The `.txt` file is encoded using UTF-8. Each row contains only one account, and the account length is limited to [2, 100].<li> The `.csv` file can contain only one column. Each row contains only one account, and the account length is limited to [2, 100].

#### Response parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| retCode | Integer | Yes | Error code. |
| errMsg | String | Yes | Error message when an error occurs in the request. |
| uploadId | Integer | Yes | When a file is uploaded, the uploadId is provided as a positive integer, which represents the ID of the uploaded file. It is provided to the account package API for subsequent pushes. |


## Sample


Curl sample
```xml
curl -X POST 
https://api.tpns.tencent.com/v3/push/package/upload 
   
-H 'Authorization: Basic application authorization information' 
-F 'file=@C:\Absolute path of the uploaded file'
```

Python sample
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

>! For more information on the application authorization, please see [Basic Auth Verification](https://intl.cloud.tencent.com/document/product/1024/34672).
