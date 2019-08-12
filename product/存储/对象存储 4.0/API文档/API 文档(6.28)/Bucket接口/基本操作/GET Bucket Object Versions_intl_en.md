## Description

The GET Bucket Object Versions API is used to query all objects in a bucket and their historical version information. You can also filter certain objects and their version information by specifying relevant parameters.

>  If you use a sub-account to initiate this request, you need to be granted the permission to `GET Bucket Object Versions` by the root account. If you initiate it as a root account, you have this permission by default.

## Request

### Sample Request

```http
GET /?versions HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Parameter

<table>
   <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>prefix</td>
      <td>Prefix match, used to specify the prefix address of the file returned</td>
      <td>string</td>
      <td>No</td>
   </tr>
   <tr>
      <td>delimiter</td>
      <td>The delimiter is a symbol. If there is a prefix, the identical paths between prefix and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. If there is no prefix, it starts at the beginning of the path</td>
      <td>string</td>
      <td>No</td>
   </tr>
   <tr>
      <td>key-marker</td>
      <td>By default, entries are listed in UTF-8 binary order, and the entry list starts at marker</td>
      <td>string</td>
      <td>No</td>
   </tr>
   <tr>
      <td nowrap="nowrap">encoding-type</td>
      <td>Specifies the encoding method of the return value. Value range: url</td>
      <td>string</td>
      <td>No</td>
   </tr>
   <tr>
      <td>max-keys</td>
      <td>Maximum number of entries returned at a time; default and maximum value: 1,000</td>
      <td>string</td>
      <td>No</td>
   </tr>
   <tr>
      <td nowrap="nowrap">version-id-marker</td>
      <td>Specifies that you need to list all historical versions of an object starting from the version ID "version-id-marker". Value range: Valid version ID, Default. If no version ID is specified, the latest version of the object will be listed by default</td>
      <td>string</td>
      <td>No</td>
   </tr>
</table>

### Request Headers

This API uses only a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

### Request Body

This API has no request body.

## Response

### Response Headers

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

### Response Body

```http
<ListVersionsResult>
    <Name>exampleBucket-1250000000</Name>
    <Prefix/></Prefix>
    <KeyMarker/></KeyMarker>
    <VersionIdMarker/></VersionIdMarker>
    <MaxKeys></MaxKeys>
    <IsTruncated></IsTruncated>
    <DeleteMarker>
    	<Key>exampleObject</Key>
    	<VersionId>VersionId</VersionId>
    	<IsLatest>true</IsLatest>
    	<LastModified>Date</LastModified>
    	<Owner>
    		<UID>OwnerUin</UID>
		</Owner>
    </DeleteMarker>
    <Version>
    	<Key>exampleObject.txt</Key>
    	<VersionId>VersionId</VersionId>
    	<IsLatest>false</IsLatest>
    	<LastModified>Date</LastModified>
    	<ETag>ETag</ETag>
    	<Size>ObjectSize</Size>
    	<StorageClass>StorageClass</StorageClass>
    	<Owner>
    		<UID>OwnerUin</UID>
    	</Owner>
    </Version>
</ListVersionsResult>
```

The detailed data are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------ | ---------------------------------- | --------- |
| ListVersionsResult | None | Stores all information of the Get Bucket request results | Container |

**Content of the Container node ListVersionsResult:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------ | ------------------------------------------------------------ | --------- |
| Name | ListVersionsResult | Bucket name | string |
| Encoding-Type | ListVersionsResult | Encoding method | string |
| Prefix | ListVersionsResult | Prefix match, used to specify the prefix address of the file returned by the request response | string |
| KeyMarker | ListVersionsResult | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | string |
| MaxKeys | ListVersionsResult | Maximum number of results returned in one response | string |
| IsTruncated | Whether response entries are truncated, which is a boolean value (true or false) | boolean |
| NextMarker | ListVersionsResult | If the returned entries are truncated, then NextMarker is the starting point of the next entry | string |
| DeleteMarker | ListVersionsResult | If an object has ever been deleted, it will have a deletion flag | Container |
| Version | ListVersionsResult | If an object is not deleted and exists in the bucket, this container records the object's metadata | Container |

**Content of the Container node DeleteMarker:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------------- | ------------------------ | --------- |
| Key | ListVersionsResult.DeleteMarker | Index of the deleted objects | string |
| VersionId | ListVersionsResult.DeleteMarker | Object version ID | string |
| IsLatest | ListVersionsResult.DeleteMarker | Indicates whether the deleted object is of the latest version | string |
| LastModified | ListVersionsResult.DeleteMarker | Last modified time of the object | string |
| Owner | ListVersionsResult.DeleteMarker | Bucket owner information | Container |

**Content of the Container node Version:**

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td>Key</td>
      <td>ListVersionsResult.Version</td>
      <td>Index of the deleted objects</td>
      <td>string</td>
   </tr>
   <tr>
      <td>VersionId</td>
      <td>ListVersionsResult.Version</td>
      <td>Object version ID</td>
      <td>string</td>
   </tr>
   <tr>
      <td>IsLatest</td>
      <td>ListVersionsResult.Version</td>
      <td>Indicates whether the deleted object is of the latest version</td>
      <td>string</td>
   </tr>
   <tr>
      <td>LastModified</td>
      <td>ListVersionsResult.Version</td>
      <td>Last modified time of the object</td>
      <td>string</td>
   </tr>
   <tr>
      <td>ETag</td>
      <td>ListVersionsResult.Version</td>
      <td>An Entity Tag (ETag) is a hash value generated based on the object content rather than the metadata. Different objects have different ETags, so Etag can be used to determine whether the specified object has been modified</td>
      <td>string</td>
   </tr>
   <tr>
      <td>Size</td>
      <td>ListVersionsResult.Version</td>
      <td>Indicates the size of the object in bytes</td>
      <td>string</td>
   </tr>
   <tr>
      <td>StorageClass</td>
      <td>ListVersionsResult.Version</td>
      <td>Storage class of the object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE</td>
      <td>string</td>
   </tr>
   <tr>
      <td>Owner</td>
      <td>ListVersionsResult.Version</td>
      <td>Bucket owner information</td>
      <td>Container</td>
   </tr>
</table>

**Content of the Container node Owner:**		
		

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------------------------- | --------------------- | ------ |
| UID | ListVersionsResul t.Contents.Owner | Bucket owner's APPID | string |

## Examples

### Request

```shell
GET /?versions HTTP/1.1
Host: exampleBucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9Sm****&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=versions&q-header-list=host&q-signature=5118a936049f9d44482bbb61309235cf4abe****
```

### Response

```shell
Content-Type: application/xml
Content-Length: 35524
Connection: keep-alive
Date: Fri, 14 Apr 2019 04:14:26 GMT
Server: tencent-cos
x-cos-request-id: NWQwMzFmMjJfN2QyZjIyMDlfY2M2MV85MGE5****

<ListVersionsResult>
    <Name>exampleBucket-1250000000</Name>
    <Prefix/>
    <KeyMarker/>
    <VersionIdMarker/>
    <MaxKeys>1000</MaxKeys>
    <IsTruncated>false</IsTruncated>
    <DeleteMarker>
    	<Key>100K.txt</Key>
    	<VersionId>MTg0NDUxODM2NDIzNDY0MzIxNjQ</VersionId>
    	<IsLatest>true</IsLatest>
    	<LastModified>2019-06-13T13:09:23.000Z</LastModified>
    	<Owner>
    		<UID>1250000000</UID>
        </Owner>
    </DeleteMarker>
    <Version>
    	<Key>100K.txt</Key>
    	<VersionId>MTg0NDUxODM2NDYxNTg1MTgxODk</VersionId>
    	<IsLatest>false</IsLatest>
    	<LastModified>2019-06-13T12:05:51.000Z</LastModified>
    	<ETag>&quot;fffc7956ba9a7b58a63c01b6ce1ddc45&quot;</ETag>
    	<Size>102401</Size>
    	<StorageClass>STANDARD</StorageClass>
    	<Owner>
    		<UID>1250000000</UID>
    	</Owner>
    </Version>
    <Version>
        <Key>100K.txt</Key>
        <VersionId>null</VersionId>
        <IsLatest>false</IsLatest>
        <LastModified>2019-06-13T10:00:09.000Z</LastModified>
        <ETag>&quot;fffc7956ba9a7b58a63c01b6ce1ddc45&quot;</ETag>
        <Size>102401</Size>
        <StorageClass>STANDARD</StorageClass>
        <Owner>
        	<UID>1250000000</UID>
        </Owner>
    </Version>
        <Version>
        <Key>100M.txt</Key>
        <VersionId>MTg0NDUxODM2NDYxNTc0NDc2MTM</VersionId>
        <IsLatest>true</IsLatest>
        <LastModified>2019-06-13T12:06:15.000Z</LastModified>
        <ETag>&quot;5b98499bd9900f3dc433b63a66a35252-101&quot;</ETag>
        <Size>104857601</Size>
        <StorageClass>STANDARD</StorageClass>
        <Owner>
        	<UID>1250000000</UID>
        </Owner>
    </Version>
    <Version>
        <Key>100M.txt</Key>
        <VersionId>null</VersionId>
        <IsLatest>false</IsLatest>
        <LastModified>2019-06-13T10:00:47.000Z</LastModified>
        <ETag>&quot;620b3b3e325b1b02823046c946ecde3d-101&quot;</ETag>
        <Size>104857601</Size>
        <StorageClass>STANDARD</StorageClass>
        <Owner>
        	<UID>1250000000</UID>
        </Owner>
        </Version>
    <Version>
        <Key>1204M.txt</Key>
        <VersionId>null</VersionId>
        <IsLatest>true</IsLatest>
        <LastModified>2019-06-13T10:05:11.000Z</LastModified>
        <ETag>&quot;6e37bf6cc44744075426c14b4b2aa276-1205&quot;</ETag>
        <Size>1262485505</Size>
        <StorageClass>STANDARD</StorageClass>
        <Owner>
        	<UID>1250000000</UID>
        </Owner>
    </Version>
    <Version>
        <Key>25K.txt</Key>
        <VersionId>MTg0NDUxODM2NDYxNTg4NDU5MDE</VersionId>
        <IsLatest>true</IsLatest>
        <LastModified>2019-06-13T12:05:50.000Z</LastModified>
        <ETag>&quot;cabe069ebe3561c35c6a5ae5a362f7a5&quot;</ETag>
        <Size>25601</Size>
        <StorageClass>STANDARD</StorageClass>
        <Owner>
        	<UID>1250000000</UID>
        </Owner>
    </Version>
    <Version>
        <Key>25K.txt</Key>
        <VersionId>null</VersionId>
        <IsLatest>false</IsLatest>
        <LastModified>2019-06-13T09:59:59.000Z</LastModified>
        <ETag>&quot;cabe069ebe3561c35c6a5ae5a362f7a5&quot;</ETag>
        <Size>25601</Size>
        <StorageClass>STANDARD</StorageClass>
        <Owner>
        	<UID>1250000000</UID>
        </Owner>
    </Version>
    <Version>
        <Key>25M.txt</Key>
        <VersionId>MTg0NDUxODM2NDYxNTg2MTE5MTA</VersionId>
        <IsLatest>true</IsLatest>
        <LastModified>2019-06-13T12:05:58.000Z</LastModified>
        <ETag>&quot;b1b3fcdba0def587df7031e440d623cf-26&quot;</ETag>
        <Size>26214401</Size>
        <StorageClass>STANDARD</StorageClass>
        <Owner>
        	<UID>1250000000</UID>
        </Owner>
    </Version>
    <Version>
        <Key>25M.txt</Key>
        <VersionId>null</VersionId>
        <IsLatest>false</IsLatest>
        <LastModified>2019-06-13T10:00:08.000Z</LastModified>
        <ETag>&quot;834f90daf03a8810620175c2f2d4104a-26&quot;</ETag>
        <Size>26214401</Size>
        <StorageClass>STANDARD</StorageClass>
        <Owner>
        	<UID>1250000000</UID>
        </Owner>
    </Version>
</ListVersionsResult>
```