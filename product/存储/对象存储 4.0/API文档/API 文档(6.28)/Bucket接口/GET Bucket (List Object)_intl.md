## Description
This API (Get Bucket) is used to list partial or all Objects under a Bucket. The permission to read the Bucket is required to initiate this request. It is equivalent to List Object request.

## Request
### Request example

```shell
GET / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

### Request headers
#### Common headers
Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special request headers
This request operation does not use any special request header.

#### Request parameters

Name | Type | Description | Required
---|---|---|---
prefix | string | Prefix match. It is used to specify the prefix address of the returned file. | No
delimiter | string | Delimiter is a sign. If Prefix exists, the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix, and then all Common Prefixes are listed. If Prefix does not exist, the listing process starts from the beginning of the path. | No
encoding-type|string | Indicates the encoding method of the returned value. Available value: url | No
marker | string | Entries are listed in UTF-8 binary order by default, starting from marker. | No
max-keys | string | Maximum number of entries returned at a time. It defaults to 1000. The maximum is 1000. | No

### Request body
The request body is empty.

## Response
### Response headers

#### Common response headers
This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special response headers
This response does not use any special response header.

### Response body
If the request is successful, application/xml data is returned, which contains the information of the Objects in the Bucket.

```shell
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
    <Name>examplebucket-1250000000</Name>
    <Encoding-Type>url</Encoding-Type>
    <Prefix>ela</Prefix>
    <Marker/>
    <MaxKeys>1000</MaxKeys>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <NextMarker>exampleobject.txt</NextMarker>
    <Contents>
        <Key>photo</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"79f2a852fac7e826c9f4dbe037f8a63b\"</ETag>
        <Size>10485760</Size>
        <Owner>
           <ID>1250000000</ID>
        </Owner>
        <StorageClass>STANDARD</StorageClass>
    </Contents>
    <CommonPrefixes>
      <Prefix>example</Prefix>
    </CommonPrefixes>
</ListBucketResult>
```

The detailed data are described as follows:

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
ListBucketResult | None | Stores all the information returned by Get Bucket request. | Container

**Content of Container node ListBucketResult:**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
Name | ListBucketResult | Bucket information | string
Encoding-Type | ListBucketResult | Encoding format | string
Prefix | ListBucketResult | Prefix match. It is used to specify the prefix address of the returned file. | string
Marker | ListBucketResult | Entries are listed using UTF-8 binary order by default, starting from the marker. | string
MaxKeys | ListBucketResult | Maximum number of entries of the result returned for response request each time. | string
Delimiter | Delimiter is a sign. If Prefix exists, the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix, and then all Common Prefixes are listed. If Prefix does not exist, the listing process starts from the beginning of the path. | string
IsTruncated | ListBucketResult | Indicates whether the response entry is truncated. Boolean: true and false | boolean
NextMarker | upload_id_marker | If the returned entry is truncated, the returned NextMarker indicates the beginning of the next entry. | string
Contents | ListBucketResult | Metadata information | Container
CommonPrefixes | ListBucketResult | The same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix. | Container


**Content of Container node Contents:**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|--
Key | ListBucketResult.Contents | Key of the Object | string
LastModified | ListBucketResult.Contents | The time when the Object was last modified | string
ETag | ListBucketResult.Contents | The MD-5 algorithm check value of the file | string
Size | ListBucketResult.Contents | File size (in Byte) | string
Owner | ListBucketResult.Contents | Information of the Bucket owner | Container
StorageClass | ListBucketResult.Contents | The storage class of the Object. Enumerated values: STANDARD, STANDARD_IA, and ARCHIVE | string

**Content of Container node Owner:**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
ID | ListBucketResult.Contents.Owner | AppID of the Bucket | string


**Content of Container node CommonPrefixes:**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
Prefix | ListBucketResult.CommonPrefixes | Single Common prefix | string


### Error codes
No special error message is returned for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

### Request

```shell
GET / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213451;32557109451&q-key-time=1484213451;32557109451&q-header-list=host&q-url-param-list=&q-signature=0336a1fc8350c74b6c081d4dff8e7a2db9007dc
```

### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1132
Connection: keep-alive
Vary: Accept-Encoding
Date: Wed, 18 Oct 2014 22:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRjY2VfYmRjMzVfMTc5M182MmIyNg==

<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
    <Name>examplebucket-1250000000</Name>
    <Encoding-Type>url</Encoding-Type>
    <Prefix>ela</Prefix>
    <Marker/>
    <MaxKeys>1000</MaxKeys>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <NextMarker>exampleobject.txt</NextMarker>
    <Contents>
        <Key>photo</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"79f2a852fac7e826c9f4dbe037f8a63b\"</ETag>
        <Size>10485760</Size>
        <Owner>
            <ID>1250000001</ID>
        </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <Contents>
        <Key>picture</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"3f9a5dbff88b25b769fa6304902b5d9d\"</ETag>
        <Size>10485760</Size>
        <Owner>
            <ID>1250000002</ID>
        </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <Contents>
        <Key>file</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"39bfb88c11c65ed6424d2e1cd4db1826\"</ETag>
        <Size>10485760</Size>
        <Owner>
            <ID>1250000003</ID>
        </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <Contents>
        <Key>world</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"fb31459ad10289ff49327fd91a3e1f6a\"</ETag>
        <Size>4</Size>
        <Owner>
            <ID>1250000004</ID>
        </Owner>
        <StorageClass>STANDARD</StorageClass>
    </Contents>
</ListBucketResult>
```



