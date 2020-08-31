## Overview

Errors may occur when data is transferred between the client and the server. COS can verify data integrity using [MD5 and custom attributes](https://intl.cloud.tencent.com/document/product/436/32467), or the CRC64 check code.

COS calculates the CRC64 value according to [ECMA-182 standard](https://www.ecma-international.org/publications/standards/Ecma-182.htm) for each newly uploaded object, and stores it as part of the object attributes. It then includes `x-cos-hash-crc64ecma` in the response headers to represent this CRC64 value. Objects that were created before this CRC64 feature was launched will have no CRC64 value for COS to return when the object is requested.

## Directions

APIs that currently support CRC64 include:

- APIs for simple upload
	- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) and [POST Object](https://intl.cloud.tencent.com/document/product/436/14690): you can get the CRC64 check value for your file from the response headers.
- Multipart upload APIs
	- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750): you can compare and verify the CRC64 value returned by COS against the value calculated locally.
	- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742): returns a CRC64 value for the entire object only if each part has a CRC64 attribute. Otherwise, no value is returned.
- The [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) operation returns a corresponding CRC64 value.
- When you call the [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881), the CRC64 value is returned only if the source object has one.
- The [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) and [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) operations return the CRC64 value provided the object has one. You can compare and verify the CRC64 value returned by COS against that calculated locally.

## API Samples

#### Upload Part response

The following example shows the response to an Upload Part request. The `x-cos-hash-crc64ecma` header represents the CRC64 value of a part, which you can compare against the locally calculated CRC64 value to verify the part integrity.

```shell
HTTP/1.1 200 OK
content-length: 0
connection: close
date: Thu, 05 Dec 2019 01:58:03 GMT
etag: "358e8c8b1bfa35ee3bd44cb3d2cc416b"
server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0MmJfMjBiNDU4NjRfNjkyZl80ZjZi****
```

#### Complete Multipart Upload response

The following example shows the response to a Complete Multipart Upload request. The `x-cos-hash-crc64ecma` header represents the CRC64 value of an entire object, which you can compare against the locally calculated CRC64 value to verify the object integrity.

```shell
HTTP/1.1 200 OK
content-type: application/xml
transfer-encoding: chunked
connection: close
date: Thu, 05 Dec 2019 02:01:17 GMT
server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0ZWRfMjNiMjU4NjRfOGQ4Ml81MDEw****

[Object Content]
```

## SDK Samples

The following example uses the Python SDK to verify object integrity. The complete sample code is as follows.

> ?The code is based on Python 2.7. For more information on how to use the Python SDK, see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31546).

#### 1. Initialization configuration

Configure user attributes, including SecretId, SecretKey, and region, and create a client object.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError
import sys
import logging
import hashlib
import crcmod

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# Configure user attributes, including SecretId, SecretKey, and region
# APPID has been removed from the configuration. Please specify it using the `Bucket` parameter in the format of `BucketName-APPID`.
secret_id = COS_SECRETID           # Replace with your own SecretId
secret_key = COS_SECRETKEY         # Replace with your own SecretKey
region = 'ap-beijing'      # Replace with your own region (which is Beijing in this sample)
token = None               # If a temporary key is used, Token needs to be passed in, which is left empty by default
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # Get the configured object
client = CosS3Client(config)
```

#### 2. Calculate the object checksum

Simulate object parts and calculate the checksum of the entire object.

```python
OBJECT_PART_SIZE = 1024 * 1024      # Size of each simulated part
OBJECT_TOTAL_SIZE = OBJECT_PART_SIZE * 1 + 123      # Total size of the object
object_body = '1' * OBJECT_TOTAL_SIZE       # Object content

#Calculate the checksum of the entire object.
c64 = crcmod.mkCrcFun(0x142F0E1EBA9EA3693L, initCrc=0L, xorOut=0xffffffffffffffffL, rev=True)
local_crc64 =str(c64(object_body))
```

#### 3. Initialize the multipart upload

```python
# Initialize the multipart upload
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',  #Replace with your own bucket name and APPID
    Key='exampleobject',              # Replace with the key value of your uploaded object
    StorageClass='STANDARD',            # Storage class of the object
)
#Get the UploadId of the multipart upload
upload_id = response['UploadId']
```

#### 4. Upload the object using multipart upload

During a multipart upload, an object is divided into multiple (up to 10,000) parts for upload. The size of each part ranges from 1 MB to 5 GB, except the last part that can be less than 1 MB. When uploading parts, configure the PartNumber of each part and calculate its corresponding CRC64 value. After the parts are successfully uploaded, check the returned CRC64 value with the locally calculated value to verify the object integrity.

```python
#Upload an object in parts where the size of each part is OBJECT_PART_SIZE except the last part which may be smaller
part_list = list()
position = 0 
left_size = OBJECT_TOTAL_SIZE
part_number = 0 
while left_size > 0:
    part_number += 1
    if left_size >= OBJECT_PART_SIZE:
        body = object_body[position:position+OBJECT_PART_SIZE]
    else:
        body = object_body[position:]
    position += OBJECT_PART_SIZE
    left_size -= OBJECT_PART_SIZE
    local_part_crc_64 = c64(body)#Calculate CRC64 locally

    response = client.upload_part(
        Bucket='examplebucket-1250000000',
        Key='exampleobject',
        Body=body,
        PartNumber=part_number,
        UploadId=upload_id,
    )   
    part_crc_64 = response['x-cos-hash-crc64ecma']# CRC64 returned by the server
    if local_part_crc64 != part_crc_64:# Data Check
    	print 'crc64 check FAIL'
    	exit(-1)
    etag = response['ETag']
    part_list.append({'ETag' : etag, 'PartNumber' : part_number})
```

#### 5. Complete the multipart upload

After all parts are successfully uploaded, you need to complete the multipart upload. Then, you can verify the CRC64 value returned by COS against that of the local object.

```python
#Complete the multipart upload
response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',  #Replace with your own bucket name and APPID
    Key=‘exampleobject’,             #Key value of the object
    UploadId=upload_id,
    MultipartUpload={       #Require one-to-one correspondence between ETag and PartNumber for each part
        'Part' : part_list    
    },
)
crc64ecma = response['x-cos-hash-crc64ecma']
if crc64ecma != local_crc64:# Data Check
    print 'check crc64 Failed'
    exit(-1)
```

