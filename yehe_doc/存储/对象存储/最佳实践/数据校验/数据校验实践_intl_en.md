## Overview

Errors may occur when data is being transmitted between the client and the server. COS can guarantee the integrity of the uploaded data through MD5 verification. Only when the MD5 checksum received by the COS server is the same as that you set can the data be successfully uploaded.

Each object in COS has a corresponding ETag, which is the information identifier of the object content when the object is created. However, the ETag is not necessarily equivalent to the MD5 checksum of the object content. Therefore, the ETag cannot be used to verify whether the downloaded object is the same as the original object. In this case, you can use custom object metadata (x-cos-meta-\*) to verify the object consistency.

## Data Verification Methods

- Verify an uploaded object
If you need to verify whether the object uploaded to COS is the same as the local object, you can set the [Content-MD5](https://intl.cloud.tencent.com/document/product/436/7728) field in the HTTP upload request to the Base64-encoded MD5 checksum of the object content. After that, the COS server will verify the uploaded object. Only when the MD5 checksum received by the COS server is the same as the Content-MD5 value you set can the object be successfully uploaded.
- Verify a downloaded object
If you need to verify whether the downloaded object is the same as the original object, you can use a verification algorithm to calculate the checksum of the object when it is uploaded, set the checksum of the object through custom metadata, recalculate the checksum of the object after downloading the object, and then verify it against the custom metadata. In this mode, you can choose the verification algorithm as you wish, but for the same object, the algorithm used during upload should be the same as that used during download.   



## API Samples

#### Simple Upload Request

Below is a sample request for object upload. When uploading the object, set the Content-MD5 to the Base64-encoded MD5 checksum of the object content and set the custom metadata "x-cos-meta-md5" to the checksum of the object. Only when the MD5 checksum received by the COS server is the same as the Content-MD5 value you set can the object be successfully uploaded.
> In the sample, the checksum of the object is obtained through the MD5 checksum algorithm, and you can choose other algorithms as you wish.  

```url
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:28 GMT
Content-Type: image/jpeg
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
x-cos-meta-md5: b62e10bcab55a88240bd9c436cffdcf9
Connection: close

[Object Content]
```

#### Multipart Upload Request

Below is a sample request to initialize a multipart upload. When uploading object parts, you can set the custom metadata of the object by initializing the multipart upload. Here, set the custom metadata "x-cos-meta-md5" as the checksum of the object.   

```url
POST /exampleobject?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:45:12 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
x-cos-meta-md5: b62e10bcab55a88240bd9c436cffdcf9
```

#### Object Download Response

Below is a sample response obtained after you send an object download request. You can get the custom metadata "x-cos-meta-md5" of the object from the response and then check it against the recalculated checksum of the object to verify whether the downloaded object is the same as the original object.   

```url
HTTP/1.1 200 OK
Content-Type: application/octet-stream
Content-Length: 13
Connection: close
Accept-Ranges: bytes
Cache-Control: max-age=86400
Content-Disposition: attachment; filename=example.jpg
Date: Thu, 04 Jul 2019 11:33:00 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Thu, 04 Jul 2019 11:32:55 GMT
Server: tencent-cos
x-cos-request-id: NWQxZGUzZWNfNjI4NWQ2NF9lMWYyXzk1NjFj****
x-cos-meta-md5: b62e10bcab55a88240bd9c436cffdcf9

[Object Content]
```

## SDK Sample

The following uses the Python SDK as an example to demonstrate how to verify an object. The complete sample code is as follows.

> The code is based on Python 2.7. For more information on how to use the Python SDK, see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31546) for Python SDK..

#### 1. Initial configuration

Set user attributes, including SecretId, SecretKey, and region, and create a client object.

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

# Set user attributes, including SecretId, SecretKey, and region
# APPID has been removed from the configuration. Please add the APPID to the `Bucket` parameter in the format of BucketName-APPID.
secret_id = COS_SECRETID           # Replace with your own SecretId
secret_key = COS_SECRETKEY         # Replace with your own SecretKey
region = 'ap-beijing'      # Replace with your own region (which is Beijing in this sample)
token = None               # If a temporary key is used, Token needs to be passed in, which is null by default. This can be left blank
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # Get the configured object
client = CosS3Client(config)
```

#### 2. Verify an object uploaded using simple upload

#### (1) Calculate the checksum of the object

Get the checksum of the object through the MD5 checksum algorithm (you can choose other algorithms as you wish).

```python
object_body = 'hello cos'
# Get the MD5 checksum of the object
md5 = hashlib.md5()
md5.update(object_body)
md5_str = md5.hexdigest()
```

#### (2) upload objects using simple upload 

EnableMD5=True in the code indicates the enablement of MD5 verification for object upload. The SDK for Python will calculate the Content-MD5. Enabling this will increase the time it takes to upload the object. Only when the MD5 checksum of the object received by the COS server is the same as the Content-MD5 can the object be successfully uploaded.
x-cos-meta-md5 is a custom parameter (in the name format of x-cos-meta-\*), which represents the MD5 checksum of the object.

```python
# Upload the object using simple upload and enable MD5 verification
response = client.put_object(
    Bucket='examplebucket-1250000000',      # Replace with your own bucket name. Here, examplebucket is a sample bucket, and 1250000000 is a sample APPID
    Body='hello cos',                 # Content of the uploaded object
    Key='example-object-1',           # Replace with the key value of your uploaded object 
    EnableMD5=True,                   # Enable MD5 verification for upload
    Metadata={                        # Set the custom parameter and save the MD5 checksum of the object to the COS server as the parameter value
        'x-cos-meta-md5' : md5_str
    }
)
print 'ETag: ' + response['ETag']     # Etag value of the object
```

#### (3) Download the object

Download the object and get the custom parameter.

```python
# Download the object
response = client.get_object(
    Bucket='examplebucket-1250000000',      # Replace with your own bucket name. Here, examplebucket is a sample bucket, and 1250000000 is a sample APPID
    Key='example-object-1'                  # Key value of the download object
)
fp = response['Body'].get_raw_stream()
download_object = fp.read()                 # Get the object content
print "get object body: " + download_object
print 'ETag: ' + response['ETag']               
print 'x-cos-meta-md5: ' + response['x-cos-meta-md5']   # Get the custom parameter "x-cos-meta-md5"
```

#### (4) Verify the object

After successfully downloading the object, you can recalculate the checksum of the object (the verification algorithm should be the same as that used for upload) and check it against the custom parameter "x-cos-meta-md5" to verify whether the downloaded object is the same as the uploaded object.

```python
# Calculate the MD5 checksum of the downloaded object
md5 = hashlib.md5()                 
md5.update(download_object)
md5_str = md5.hexdigest()
print 'download object md5: ' + md5_str

# Verify object consistency by checking the MD5 checksum of the downloaded object against that of the uploaded object
if md5_str == response['x-cos-meta-md5']:
    print 'MD5 check OK'
else:
    print 'MD5 check FAIL'
```

#### 3. Verify an object uploaded in parts

#### (1) Calculate the checksum of the object

Simulate object parts and calculate the checksum of the entire object. The MD5 checksum algorithm is used to obtain the checksum of the object in the sample below, and you can choose other algorithms as you wish.

```python
OBJECT_PART_SIZE = 1024 * 1024      # Size of each simulated part
OBJECT_TOTAL_SIZE = OBJECT_PART_SIZE * 1 + 123      # Total size of the object
object_body = '1' * OBJECT_TOTAL_SIZE       # Object content

# Calculate the MD5 checksum of the entire object content
md5 = hashlib.md5()
md5.update(object_body)
md5_str = md5.hexdigest()
```

#### (2) Initialize the multipart upload

When initializing the multipart upload, set the custom parameter "x-cos-meta-md5" and use the MD5 checksum of the entire object as the parameter value.

```python
# Initialize the multipart upload
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',      # Replace with your own bucket name. Here, examplebucket is a sample bucket, and 1250000000 is a sample APPID
    Key='exampleobject-2',              # Replace with the key value of the uploaded object 
    StorageClass='STANDARD',            # Storage class of the object
    Metadata={
        'x-cos-meta-md5' : md5_str      # Set the custom parameter to the MD5 checksum
    }
)
# Get the UploadId of the multipart upload
upload_id = response['UploadId']
```

#### (3) Upload the object in parts

During a multipart upload, an object is divided into multiple (up to 10,000) parts for the upload. The size of each part can range from 1 MB to 5 GB, and the last part can be less than 1 MB. When uploading the parts, you need to set the PartNumber of each part. EnableMD5=True indicates enabling the part check, which increases the time it takes to upload the object. The Python SDK will calculate the Content-MD5 of each part. Only when the MD5 checksum of the object received by the COS server is the same as the Content-MD5 can the parts be successfully uploaded. After the upload succeeds, the ETag of each part will be returned.     

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

    # Upload parts
    response = client.upload_part(
        Bucket='examplebucket-1250000000',      # Replace with your own bucket name. Here, examplebucket is a sample bucket, and 1250000000 is a sample APPID
        Key='exampleobject-2',              # Key value of the object 
        Body=body,
        PartNumber=part_number,
        UploadId=upload_id,
        EnableMD5=True       # Enable part verification and the COS server will perform MD5 verification on each part
    )
    etag = response['ETag']     # ETag represents the MD5 checksum of each part
    part_list.append({'ETag' : etag, 'PartNumber' : part_number})
    print etag + ', ' + str(part_number)
```

#### (4) Complete the multipart upload

After all parts are uploaded, you need to complete the multipart upload operation. The ETag and PartNumber of each part should be in one-to-one correspondence which will be used by the COS server to verify the part accuracy. After the multipart upload completes, the returned ETag represents the unique tag value of the merged object but not the MD5 checksum of the entire object content. As a result, you can use the custom parameter to verify the object when downloading it.

```python
# Complete the multipart upload
response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',      # Replace with your own bucket name. Here, examplebucket is a sample bucket, and 1250000000 is a sample APPID
    Key='exampleobject-2',              # Key value of the object 
    UploadId=upload_id,
    MultipartUpload={       # Requires one-to-one correspondence between ETag and PartNumber for each part
        'Part' : part_list    
    },
)

# ETag represents the unique tag value of the merged object, which is not the MD5 checksum of the object content and can only be used to verify the object's uniqueness
print "ETag: " + response['ETag']   
print "Location: " + response['Location']   #URL
print "Key: " + response['Key'] 
```

#### (5) Download the object

Download the object and get the custom parameter.

```python
# Download the object
response = client.get_object(
    Bucket='examplebucket-1250000000',      # Replace with your own bucket name. Here, examplebucket is a sample bucket, and 1250000000 is a sample APPID
    Key='exampleobject-2'               # Key value of the object 
)
print 'ETag: ' + response['ETag']                        # The ETag of the object is not the MD5 checksum of the object content
print 'x-cos-meta-md5: ' + response['x-cos-meta-md5']    # Get the custom parameter "x-cos-meta-md5"
```

#### (6) Verify the object

After successfully downloading the object, you can recalculate the MD5 checksum of the object and check it against the custom parameter "x-cos-meta-md5" to verify whether the downloaded object is the same as the uploaded object.

```python
# Calculate the MD5 checksum of the downloaded object
fp = response['Body'].get_raw_stream()
DEFAULT_CHUNK_SIZE = 1024*1024
md5 = hashlib.md5()
chunk = fp.read(DEFAULT_CHUNK_SIZE)     
while chunk:
    md5.update(chunk)
    chunk = fp.read(DEFAULT_CHUNK_SIZE)
md5_str = md5.hexdigest()
print 'download object md5: ' + md5_str

# Verify object consistency by checking the MD5 checksum of the downloaded object against that of the uploaded object
if md5_str == response['x-cos-meta-md5']:
    print 'MD5 check OK'
else:
    print 'MD5 check FAIL'
```
