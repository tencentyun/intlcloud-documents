## Feature Description

This API is used to create a one-time inventory job for a bucket, which is different from `PUT Bucket inventory`. Once created, the inventory job will be executed, and each job will be executed only once instead of repeated execution. You can use this API to get the object inventory of a bucket and manage objects in a refined way.

> !
> - You must add a bucket policy to the destination bucket for COS to write the output file of the inventory job to the destination bucket.
> - To call this API, make sure that you have the necessary permission for bucket inventory jobs; the bucket owner has this permission by default. If you do not have it, you should request it from the bucket owner first.  
> - If you specify a prefix for the destination path of the inventory report, COS will automatically append a slash (/) to the specified prefix. For example, if you set the prefix to `Prefix`, COS will deliver the inventory report to `Prefix/inventory_report`.
> - If you submit another inventory job with the same ID or use the same ID as the periodic inventory job before the first one is completed, the server will return a duplication error.
>

## Request

#### Sample request

```plaintext
POST /?inventory&id=inventory-configuration-ID HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Content-MD5: MD5
```

>?Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>

#### Request parameters

To call `POST Bucket inventory`, specify the following parameter:

| Parameter | Description | Type |Required |
| ---- | ------------------------------------------------------------ | ------ | -------- |
| id   | Inventory job name. Default value: None<br>Valid character: `a-z, A-Z, 0-9, -, _, .`<br>Note: We recommend that you should not use the same ID as the periodic inventory job or submit duplicate IDs within one day. Otherwise, errors will be returned. | String | Yes       |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

You can use the XML language in request body to configure the inventory job by following the rules below:

>!
>- The one-time inventory job cannot include `IsEnabled` or `Schedule` parameter.
>- All other parameters are the same as [PUT Bucket Inventory](https://intl.cloud.tencent.com/document/product/436/30625).  
>

  

```plaintext
<InventoryConfiguration>
    <Id>list1</Id>
    <Destination>
        <COSBucketDestination>
            <Format>CSV</Format>
            <AccountId>100000000001</AccountId>
            <Bucket>qcs::cos:ap-guangzhou::examplebucket-1250000000</Bucket>
            <Prefix>list1</Prefix>
            <Encryption>
                <SSE-COS></SSE-COS>
            </Encryption>
        </COSBucketDestination>
    </Destination>
    <Filter>
    	<And>
        	<Prefix>myPrefix</Prefix>
            <Tag>
                <Key>string</Key>
                <Value>string</Value>
            </Tag>
        </And>
    </Filter>
    <IncludedObjectVersions>All</IncludedObjectVersions>
    <OptionalFields>
        <Field>Size</Field>
        <Field>LastModifiedDate</Field>
        <Field>ETag</Field>
        <Field>StorageClass</Field>
        <Field>IsMultipartUploaded</Field>
        <Field>ReplicationStatus</Field>
	</OptionalFields>
</InventoryConfiguration>
```



## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example: Filter by the specified prefix to generate a one-time inventory

#### Request

This example describes initiating an inventory job in `examplebucket-1250000000`.

- The object (including its all versions) prefixed with `myPrefix` and tagged with {age:18} in the bucket will be analyzed.
- Analysis dimensions: `Size`; `LastModifiedDate`; `StorageClass`; `ETag`; `Tag`.
- The result will be saved in the format of CSV in the bucket `examplebucket-1250000000`.

```plaintext
POST /?inventory&id=disposable HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503888878;1503889238&q-key-time=1503888878;1503889238&q-header-list=host&q-url-param-list=inventory&q-signature=254bf9cd3d6615e89a36ab652437f9d45c5f****
Content-MD5: AAq9nzrpsz5LJ4UEe1f6Q==
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1024

<?xml version = "1.0" encoding = "UTF-8">
<InventoryConfiguration xmlns = "http://....">
    <Id>disposable</Id>
    <Destination>
        <COSBucketDestination>
            <Format>CSV</Format>
            <AccountId>100000000001</AccountId>
            <Bucket>qcs::cos:ap-guangzhou::inventorybucket-1250000000</Bucket>
        </COSBucketDestination>
    </Destination>
    <Filter>
    	<And>
        	<Prefix>myPrefix</Prefix>
            <Tag>
                <Key>age</Key>
                <Value>18</Value>
            </Tag>
        </And>
    </Filter>
    <IncludedObjectVersions>All</IncludedObjectVersions>
    <OptionalFields>
        <Field>Size</Field>
        <Field>LastModifiedDate</Field>
        <Field>StorageClass</Field>
        <Field>ETag</Field>
        <Field>Tag</Field>
	</OptionalFields>
</InventoryConfiguration>
```

#### Response

After the above request is made, COS will return the following response, indicating that the inventory job has been successfully submitted.

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Mon, 28 Aug 2018 02:53:38 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF8****
```
