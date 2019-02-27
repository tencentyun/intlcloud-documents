## Processing upon Upload
The processing upon upload function of CI can complete image processing when an image is uploaded. Simply add the Pic-Operations item to the header of the request packet and set the corresponding parameters to process the image accordingly when it is uploaded. Plus, the original image and processing result can be stored in COS. Currently, it supports processing images with a size of less than 20 MB.

### Request Syntax

```
POST /files/v2/<Appid>/<Bucket>/<FileName> HTTP/1.1
Host: <Region>.image.myqcloud.com
Content-Type: multipart/form-data
Authorization: <MultiEffectSignature>
Content-Length: <ContentLength>
Pic-Operations: <PicOperations>
```

For details of the simple file upload API of COS, see [COS documentation](https://cloud.tencent.com/document/product/436/6066).

### Request
Pic-Operations is a string in .json format with specific parameters as follows:

| Parameter name | Type | Required | Description |
| ----------- | ----- | ---- | ---------------------------------------- |
| is_pic_info | Int | No | Whether to return the original image information; 0 - no, 1 - yes, 0 by default |
| rules | Array | No | Processing rules; one rule corresponds to one processing result (currently, up to five rules are supported); if left blank, no image processing will be performed |

The specific parameters in rules (.json array) are as follows:

| Parameter name | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | Name of the destination bucket that stores the result in the form of bucketName-appid; if not specified, the result will be saved to the current bucket by default |
| fileid | String | Yes | File pathname of the processing result; if it starts with '/', the result will be stored in the specified folder; otherwise, the result will be stored in the same directory as the original image file |
| rule | String | Yes | Processing parameter; for details, see CI's image processing API. If it is to process according to the specified style, this parameter should start with "style/" followed by the style name; for example, if the style name is "test", the rule field will be "style/test" |

### Return

| Parameter name | Type | Description |
| ---------- | ------ | ---------------------------------------- |
| code | Number | Server error code; if no error occurred, the value is **0**; if an error occurred, this parameter refers to the specific error code. Error codes related to the COS service can be found in [COS Error Codes](https://cloud.tencent.com/document/product/436/8432) |
| message | String | Server prompt; if an error occurred, this field details the error.           |
| request_id | String | Unique id of the request |
| data | Object | The response data returned by the server, which represents the specific business data returned by the API.           |




 Description of the data parameter
 
 | Parameter name | Type | Description |
| ------------- | ------ | ---------------------------------------- |
| access_url | String | Access the file's resource link via CDN (faster) |
| resource_path | String | The relative pathname of this file in COS, which can be used as its ID. Format: /<APPID>/<BucketName>/<ObjectName>. It is recommended that the business side store the resource_path and then flexibly splice the resource url based on actual business needs (the url for accessing the COS resource via CDN is different from that for directly accessing the COS resource). |
| source_url | String | Directly access the COS resource link without CDN |
| url | String | url of the file to be operated. The business side can perform further operations on the file by using the url as the request address, i.e., the request address in the following APIs: file properties, file update, file deletion and file moving. |
| image_info | Object | Image processing result |
| timecost      | Number | Time consumed in ms                                  |

Description of the image_info parameter

| Parameter name | Type | Description |
| --------------- | ------ | ---------------- |
| original_info   | Object | Original image information; present if it is specified to return the original image information |
| process_results | Array | Image processing result |


 Description of the original_info parameter
 
 | Parameter name | Type | Description |
| ----------- | ------ | ------ |
| format | String | Format |
| width | Number | Image width |
| height | Number | Image height |
| ave | String | Image's main tone |
| orientation | Number | Image's rotation angle |
| quality | Number | Image quality |

 Description of the parameters in the process_results array
 
 | Parameter name | Type | Description |
| ------------- | ------ | ---------------------------------------- |
| file_id | String | Filename |
| format | String | Format |
| width | Number | Image width |
| height | Number | Image height |
| size | Number | Image size |
| quality | Number | Image quality |
| access_url | String | Access the file's resource link via CDN (faster) |
| resource_path | String | The relative pathname of this file in COS, which can be used as its ID. Format: /<APPID>/<BucketName>/<ObjectName>. It is recommended that the business side store the resource_path and then flexibly splice the resource url based on actual business needs (the url for accessing the COS resource via CDN is different from that for directly accessing the COS resource). |
| source_url | String | Directly access the COS resource link without CDN |
| url | String | url of the file to be operated. The business side can perform further operations on the file by using the url as the request address, i.e., the request address in the following APIs: file properties, file update, file deletion and file moving. |

>**Note:**
> Tencent Cloud COS will generate a CDN access link "access_url" for each resource by default. Even if the business side has not activated CDN yet, the link can still be obtained, but it cannot be accessed.

### Example
#### Request

```
POST /files/v2/appid/bucket/sample_file.jpg HTTP/1.1
Host: cd.image.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: cos-python-sdk-v4
Authorization: XXXXXXXXXXXXXXXXXXXXXXXXXX
Content-Length: XXXXX
Pic-Operations: {"is_pic_info":1,"rules":[{"fileid":"test1.png","rule":"imageView2/format/png"}]}
Content-Type: multipart/form-data; boundary=6815dbc897af4706bd5a39f49b157928

--6815dbc897af4706bd5a39f49b157928
Content-Disposition: form-data; name="op"; 

upload
--6815dbc897af4706bd5a39f49b157928
Content-Disposition: form-data; name="filecontent"; filename="filecontent"
```

Return
```
{
"code":0,
"message":"SUCCESS",
"request_id":"NTlhNDBhZGVfOTYyMjViNjRfMTc3Ml8yYWQ5NWU=",
"data":
{
"access_url":"http://bucket-appid.file.myqcloud.com/sample_file.jpg",
"resource_path":"/appid/bucket/sample_file.jpg",
"source_url":"http://bucket-appid.cosgz.myqcloud.com /sample_file.jpg",
"url":"http://gz.file.myqcloud.com/files/v2/appid/bucket/sample_file.jpg",
"timecost":500,
"image_info":
{
      "original_info":
      {
       "format": "JPEG",
        "height": 200,
        "width": 50,
        "ave": "0xa18432",
                 "orientation":1,
                 "quality":100
      },
  "process_results":
  [ 
{
    "access_url":"http://bucket-appid.file.myqcloud.com/test1.png",
"resource_path":"/appid/bucket/test1.png",
"source_url":"http://bucket-appid.cosgz.myqcloud.com/test1.png",
"url":"http://gz.file.myqcloud.com/files/v2/appid/bucket/test1.png",
"vid":"value",
"file_id":"test1.png",
"format":"PNG",
"height":50,
"width":200,
"size":100200,
"quality":100,
}
]
}
}
```

>**Note:**
>Processing upon upload supports the multipart upload function of COS v4. To process the image, simple add the Pic-Operations item to the request packet header for the multipart upload initializing and multipart upload ending APIs.

```
POST /files/v2/<Appid>/<Bucket>/<FileName>  HTTP/1.1
Host: <Region>.image.myqcloud.com
Authorization: <MultiEffectSignature>
Content-Type: multipart/form-data
Content-Length: <ContentLength>
Pic-Operations: <PicOperations>
```

For COS-related APIs, see [COS documentation](https://cloud.tencent.com/document/product/436/6067).



## Cloud Data Processing
The image processing API of CI can process images stored in COS and then save the results to COS.

### Request Syntax
The request packet's header information is as follows:

```
POST /files/v2/<Appid>/<Bucket>/<FileName> HTTP/1.1
Host: <Region>.image.myqcloud.com
Content-Type: multipart/form-data
Authorization: <MultiEffectSignature>
Content-Length: <ContentLength>
Pic-Operations: <PicOperations>
```

New content in the request packet:

| Parameter name | Type | Required | Description |
| ---------- | ------ | ---- | ---------------------------------------- |
| op | String | yes | Operation type, fixed to "image_process" |
| insertOnly | Int | No | Overwrite option for files with the same name; valid values: 0 - overwrite (which is to delete the existing file with the same name and store the newly uploaded file), 1 - no overwrite (if there is already a file with the same name, it will not be overwritten and "Upload failed" will be returned). No overwrite by default. |

 
### Request
Pic-Operations is a string in .json format with specific parameters as follows:

| Parameter name | Type | Required | Description |
| ----------- | ----- | ---- | ---------------------------------------- |
| is_pic_info | Int | No | Whether to return the original image information; 0 - no, 1 - yes, 0 by default |
| rules | Array | No | Processing rules; one rule corresponds to one processing result (currently, up to five rules are supported); if left blank, no image processing will be performed |

The specific parameters in rules (.json array) are as follows:

| Parameter name | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | Name of the destination bucket that stores the result in the form of bucketName-appid; if not specified, the result will be saved to the current bucket by default |
| fileid | String | Yes | File pathname of the processing result; if it starts with '/', the result will be stored in the specified folder; otherwise, the result will be stored in the same directory as the original image file |
| rule | String | Yes | Processing parameter; for details, see CI's image processing API. If it is to process according to the specified style, this parameter should start with "style/" followed by the style name; for example, if the style name is "test", the rule field will be "style/test" |

### Return
| Parameter name | Type | Description |
| ---------- | ------ | ---------------------------------------- |
| code | Number | Server error code; if no error occurred, the value is **0**; if an error occurred, this parameter refers to the specific error code. Error codes related to the COS service can be found in [COS Error Codes](https://cloud.tencent.com/document/product/436/8432) |
| message | String | Server prompt; if an error occurred, this field details the error.           |
| request_id | String | Unique id of the request |
| data | Object | The response data returned by the server, which represents the specific business data returned by the API.           |

 Description of the data parameter
 
 | Parameter name | Type | Description |
| ---------- | ------ | ------- |
| image_info | Object | Image processing result |
| timecost      | Number | Time consumed in ms                                  |

Description of the image_info parameter

| Parameter name | Type | Description |
| --------------- | ------ | ------ |
| original_info   | Object | Original image information |
| process_results | Array | Image processing result |

 
 Description of the original_info parameter
 
 | Parameter name | Type | Description |
| ----------- | ------ | ------ |
| format | String | Format |
| width | Number | Image width |
| height | Number | Image height |
| ave | String | Image's main tone |
| orientation | Number | Image's rotation angle |
| quality | Number | Image quality |

 Description of the parameters in the process_results array
 
 | Parameter name | Type | Description |
| ------------- | ------ | ---------------------------------------- |
| file_id | String | Filename |
| format | String | Format |
| width | Number | Image width |
| height | Number | Image height |
| size | Number | Image size |
| quality | Number | Image quality |
| access_url | String | Access the file's resource link via CDN (faster) |
| resource_path | String | The relative pathname of this file in COS, which can be used as its ID. Format: /<APPID>/<BucketName>/<ObjectName>. It is recommended that the business side store the resource_path and then flexibly splice the resource url based on actual business needs (the url for accessing the COS resource via CDN is different from that for directly accessing the COS resource). |
| source_url | String | Directly access the COS resource link without CDN |
| url | String | url of the file to be operated. The business side can perform further operations on the file by using the url as the request address, i.e., the request address in the following APIs: file properties, file update, file deletion and file moving. |

 ### Example
 #### Request
 
 ```
POST /files/v2/appid/bucket/sample_file.jpg HTTP/1.1
Host: cd.image.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: cos-python-sdk-v4
Authorization: XXXXXXXXXXXXXXXXXXXXXXXXXX
Content-Length: XXXXX
Pic-Operations: {"is_pic_info":1,"rules":[{"fileid":"test1.png","rule":"imageView2/format/png"}]}
Content-Type: multipart/form-data; boundary=6815dbc897af4706bd5a39f49b157928

--6815dbc897af4706bd5a39f49b157928
Content-Disposition: form-data; name="op"; 

image_process 
--6815dbc897af4706bd5a39f49b157928
Content-Disposition: form-data; name=" insertOnly";

0
--6815dbc897af4706bd5a39f49b157928-
```

#### Return
 
```
 {
"code":0,
"message":"SUCCESS",
"request_id":"NTlhNDBhZGVfOTYyMjViNjRfMTc3Ml8yYWQ5NWU=",
"data":
{
"timecost":500,
"image_info":
{
      "original_info":
      {
       "format": "JPEG",
        "height": 200,
        "width": 50,
        "ave": "0xa18432",
                 "orientation":1,
                 "quality":100
      },
  "process_results":
  [ 
{
    "access_url":"http://bucket-appid.file.myqcloud.com/test1.png",
"resource_path":"/appid/bucket/test1.png",
"source_url":"http://bucket-appid.cosgz.myqcloud.com/test1.png",
"url":"http://gz.file.myqcloud.com/files/v2/appid/bucket/test1.png",
"vid":"value",
"file_id":"test1.png",
"format":"PNG",
"height":50,
"width":200,
"size":100200,
"quality":100,
}
]
}
}
```

