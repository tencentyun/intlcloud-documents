## Introduction

Errors may occur when data is transferred between the client and the server. COS can not only verify data integrity through [MD5 and custom attributes](https://intl.cloud.tencent.com/document/product/436/32467), but also the CRC64 check code.

COS will calculate the CRC64 of the newly uploaded object and store the result as object attributes. It will carry x-cos-hash-crc64ecma in the returned response header, which indicates the CRC64 value of the uploaded object calculated according to [ECMA-182 standard](https://www.ecma-international.org/publications/standards/Ecma-182.htm). If an object already has a CRC64 value stored before this feature is activated, COS will not calculate its CRC64 value, nor will it be returned when the object is obtained.

## Steps

APIs that currently support CRC64 are:

- Multipart upload APIs
	- Upload Part: Users can compare and verify the CRC64 value returned by COS with the value calculated locally.
	- Complete Multipart Upload: If each part has a CRC64 attribute, the CRC64 value of the entire object is returned. It is not returned if some parts do not have the CRC64 value.
	- When executing on Upload Part-Copy, the corresponding CRC64 value is returned.
- When executing on PUT Object-Copy, if the source object has a CRC64 value, CRC64 is returned, otherwise it is not returned.
- When executing on HEAD Object and GET Object, if the object has a CRC64 value, it is returned. Users can compare and verify the CRC64 value returned by COS with the locally calculated CRC64.

> Currently, PUT Object and POST Object APIs of COS do not support CRC64.

## API Samples

#### Multipart upload response

The following is an example of the response obtained after a user sends an Upload Part request. The x-cos-hash-crc64ecma header indicates the CRC64 value of the part, and the user can compare the value with the locally calculated CRC64 value to verify the integrity of the part.

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Thu, 08 Aug 2019 09:15:29 GMT
etag: "358e8c8b1bfa35ee3bd44cb3d2cc416b"
Server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0MmJfMjBiNDU4NjRfNjkyZl80ZjZi****
```

#### Completing the multipart upload response

The following is an example of the response obtained after a user sends a Complete Multipart Upload request. The x-cos-hash-crc64ecma header indicates the CRC64 value of the part, and the user can compare the value with the locally calculated CRC64 value to verify the integrity of the part.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Transfer-Encoding: chunked
Connection: close
Date: Thu, 08 Aug 2019 09:15:29 GMT
Server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0ZWRfMjNiMjU4NjRfOGQ4Ml81MDEw****

[Object Content]
```

## SDK Sample

The following uses the Python SDK as an example to demonstrate how to verify an object. The complete sample code is as follows.

> The code is based on Python 2.7. For more information on how to use the Python SDK, see [Object Operations] for Python SDK.(https://intl.cloud.tencent.com/document/product/436/31546).

#### 1. Initial configuration

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

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# Configure user attributes, including SecretId, SecretKey, and region
# APPID has been removed from the configuration. Please add the APPID to the `Bucket` parameter in the format of BucketName-APPID.
secret_id = COS_SECRETID           # Replace with your own SecretId
secret_key = COS_SECRETKEY         # Replace with your own SecretKey
region = 'ap-beijing'      # Replace with your own region (which is Beijing in this sample)
token = None               # If a temporary key is used, Token needs to be passed in, which is null by default. This can be left blank
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

# 1. Initialize multipart upload

```python
# Initialize the multipart upload
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000', # Replace with your own bucket name, examplebucket is a sample bucket, and 1250000000 is a sample APPID
    Key='exampleobject-2',              # Replace with the key value of the uploaded object 
    StorageClass='STANDARD',            # Storage class of the object
)
# Get the UploadId of the multipart upload
upload_id = response['UploadId']
```

#### 4. Upload the object via multipart upload

During a multipart upload, an object is divided into multiple (up to 10,000) parts for upload. The size of each part can range from 1 MB to 5 GB, and the last part can be less than 1 MB. When uploading parts, configure the PartNumber of each part and its corresponding CRC64 value. After the parts are successfully uploaded, check the returned CRC64 value with the locally calculated value to verify the integrity of each part.

```python
# Upload an object in parts where the size of each part is OBJECT_PART_SIZE except the last part which may be smaller
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
    	print 'MD5 check FAIL'
    	exit(1);
    etag = response['ETag']
    part_list.append({'ETag' : etag, 'PartNumber' : part_number})
```

# 3. Complete Multipart Upload

After all parts are successfully uploaded, you need to complete the multipart upload. The CRC64 returned by COS and the CRC64 of the local object can be used for comparison and verification.

```python
# Complete the multipart upload
response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',      # Replace with your own bucket name, examplebucket is a sample bucket, and 1250000000 is a sample APPID
    Key='exampleobject-2',              # Key value of the object 
    UploadId=upload_id,
    MultipartUpload={       # Requires one-to-one correspondence between ETag and PartNumber for each part
        'Part' : part_list    
    },
)
crc64ecma = response['x-cos-hash-crc64ecma']
if crc64ecma != local_crc64:# Data Check
    print 'MD5 check FAIL'
    exit(1);
```

