## Feature Description

This API is used to create a batch operation job in a bucket. For more information, please see [Batch Operation Overview](https://cloud.tencent.com/document/product/436/38601).

When calling this API, please make sure that you have necessary permissions to perform operations on the objects in the bucket. The bucket owner has such permissions by default. If you do not have the permissions, please apply for them to the bucket owner first.

## Request

#### Sample Request

```shell
POST /jobs HTTP/1.1
x-cos-appid: <appid>
<?xml version="1.0" encoding="UTF-8"?>
<CreateJobRequest>
...
</CreateJobRequest>
```

#### Request Parameters

Calling the `CreateJob` API requires the following parameters:

| Parameter | Description | Required |
| ----------- | ------------------------ | ---- |
| x-cos-appid | User APPID with a length of 1–64 bytes. | Yes |

#### Request Headers
This API only uses common request headers. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

#### Request Body
You can set the configuration information for the inventory job in the request body with the XML language. Such information includes the objects to be analyzed by the inventory job, frequency and dimension of the analysis, and format and storage location of the analysis result.

```shell
<CreateJobRequest>
    <ClientRequestToken>string</ClientRequestToken>
    <ConfirmationRequired>boolean</ConfirmationRequired>
    <Description>string</Description>
    <Manifest>
        <Location>
            <ETag>string</ETag>
            <ObjectArn>string</ObjectArn>
            <ObjectVersionId>string</ObjectVersionId>
        </Location>
        <Spec>
            <Fields>
                <member>string</member>
                <member>string</member>
            </Fields>
            <Format>string</Format>
        </Spec>
    </Manifest>
    <Operation>
        <COSPutObjectCopy>
            <AccessControlGrants>
                <COSGrant>
                    <Grantee>
                        <Identifier>string</Identifier>
                        <TypeIdentifier>string</TypeIdentifier>
                    </Grantee>
                    <Permission>string</Permission>
                </COSGrant>
                <COSGrant>
                    <Grantee>
                        <Identifier>string</Identifier>
                        <TypeIdentifier>string</TypeIdentifier>
                    </Grantee>
                    <Permission>string</Permission>
                </COSGrant>
            </AccessControlGrants>
            <CannedAccessControlList>string</CannedAccessControlList>
            <MetadataDirective>string</MetadataDirective>
            <ModifiedSinceConstraint>timestamp</ModifiedSinceConstraint>
            <UnModifiedSinceConstraint>timestamp</UnModifiedSinceConstraint>
            <NewObjectMetadata>
                <CacheControl>string</CacheControl>
                <ContentDisposition>string</ContentDisposition>
                <ContentEncoding>string</ContentEncoding>
                <ContentType>string</ContentType>
                <HttpExpiresDate>timestamp</HttpExpiresDate>
                <SSEAlgorithm>string</SSEAlgorithm>
                <UserMetadata>
                    <member>
                        <Key>string</Key>
                        <Value>string</Value>
                    </member>
                    <member>
                        <Key>string</Key>
                        <Value>string</Value>
                    </member>
                </UserMetadata>
            </NewObjectMetadata>
            <StorageClass>string</StorageClass>
            <TargetResource>string</TargetResource>
        </COSPutObjectCopy>
    </Operation>
    <Priority>integer</Priority>
    <Report>
        <Bucket>string</Bucket>
        <Enabled>boolean</Enabled>
        <Format>string</Format>
        <Prefix>string</Prefix>
        <ReportScope>string</ReportScope>
    </Report>
    <RoleArn>string</RoleArn>
</CreateJobRequest>
```

The elements in the request body are described as below. For other elements, please see [CommonElements](https://cloud.tencent.com/document/product/436/38607).



| Node Name | Parent Node | Description | Type | Required |
| -------------------- | ---------------- | ------------------------------------------------------------ | ---------------- | -------- |
| ClientRequestToken | CreateJobRequest | Token unique to each request, which can prevent the frontend from initiating one batch operation job multiple times. The token can be 1–64 bytes long, and a UUID is recommended. | String | Yes |
| ConfirmationRequired | CreateJobRequest | Specifies whether confirmation is required before a job is carried out. Default value: `false`. | Boolean | No |
| Description | CreateJobRequest | Job description; 0–256 bytes long. This parameter will be returned if it is configured when the job is created. | String | No |
| Manifest | CreateJobRequest | Inventory of the objects to be processed. You need to record the objects you want to process in the inventory. | Manifest Object  | Yes  |
| Operation | CreateJobRequest | Operation to be performed on the objects in the inventory. Currently, COS supports the `PUT Object-Copy` operation, which allows you to copy the existing data in a bucket. | Operation Object | Yes |
| Priority | CreateJobRequest | Job priority. The higher the value, the higher the priority. Value range: 0–2,147,483,647. | Integer | Yes |
| Report | CreateJobRequest | Job report. You can configure this parameter to output a report upon job completion for the evaluation of job execution.  | Report Object | Yes |
| RoleArn | CreateJobRequest | COS resource ID used to identify the role you have created. It is required for identity verification. | String | Yes |

## Response

**Response Headers**

This API only returns common response headers. For more information, see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729).

**Response Body**

```shell
<CreateJobResult>
   <JobId>string</JobId>
</CreateJobResult>
```

The content is described in detail as below:

| Node Name | Parent Node | Description | Type |
| ------ | --------------- | ------------------------------------------------------------ | ------ |
| JobId | CreateJobResult | Job ID, which is automatically returned by COS after you create a job successfully. Length: 1–64 bytes. | String |

**Error Codes**

This request operation may return the following error messages. For other errors, please see [ErrorResponse](https://cloud.tencent.com/document/product/436/38610).

| Error Code | Description | Status Code | API |
| ------------------ | ----------------------------------------- | ------ | --------- |
| InvalidRequest | Duplicate request | 400 | CreateJob |
| InvalidRequest | Priority must be an integer between 0 and 2,147,483,647 | 400  | CreateJob |
| MalformedXML | The `XML Manifest` field in the request body does not conform to the XML syntax  | 400  | CreateJob |
| MalformedXML | The `XML Operation` field in the request body does not conform to the XML syntax  | 400  | CreateJob |
| MalformedXML | The `XML Report` field in the request body does not conform to the XML syntax  | 400  | CreateJob |
| ServiceUnavailable | The service is temporarily unavailable and unable to create a job  | 500 | CreateJob |
| TooManyJobs  | The number of jobs has reached the upper limit, making the server unavailable | 500 | CreateJob |



## Example

#### Request

```shell
POST /jobs HTTP/1.1
x-cos-appid: 1250000000
<?xml version="1.0" encoding="UTF-8"?>
<CreateJobRequest>
    <ClientRequestToken>1829b6c7-3141-42f1-9fe4-17082b841646</ClientRequestToken>
    <ConfirmationRequired>false</ConfirmationRequired>
    <Description>example job</Description>
    <Manifest>
        <Location>
            <ETag>ec75a30f3af000e9b31d62bed75cbcad</ETag>
            <ObjectArn>qcs::cos:ap-chengdu::manifest-1250000000/1250000000/source/manifest/20190715/manifest.json</ObjectArn>
        </Location>
        <Spec>
            <Format>COSInventoryReport_CSV_V1</Format>
        </Spec>
    </Manifest>
    <Operation>
        <COSPutObjectCopy>
            <MetadataDirective>Copy</MetadataDirective>
            <StorageClass>STANDARD</StorageClass>
            <TargetResource>qcs::cos:ap-chengdu::target-1250000000</TargetResource>
        </COSPutObjectCopy>
    </Operation>
    <Priority>10</Priority>
    <Report>
        <Bucket>qcs::cos:ap-beijing::result-1250000000</Bucket>
        <Enabled>true</Enabled>
        <Format>Report_CSV_V1</Format>
        <Prefix>example-job-result</Prefix>
        <ReportScope>AllTasks</ReportScope>
    </Report>
    <RoleArn>qcs::cam::uin/100000000001:roleName/examplerole</RoleArn>
</CreateJobRequest>
```

#### Response

After the request above is made, COS will return the following response, indicating that the inventory job has been successfully configured.

```shell
HTTP/1.1 200
<CreateJobResult>
   <JobId>65f2e4cf-83f5-42f1-9aa2-14720613da29</JobId>
</CreateJobResult>
```

