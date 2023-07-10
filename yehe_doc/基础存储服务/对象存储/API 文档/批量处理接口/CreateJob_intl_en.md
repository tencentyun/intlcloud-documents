## API Description

This API is used to create a batch operation job in a bucket. For more information, please see [Batch Processing Overview](https://intl.cloud.tencent.com/document/product/436/32958).

When calling this API, make sure you have permission to perform operations on the objects in the bucket. The bucket owner has permission by default and can grant such permission to other users. Please apply for permission from the bucket owner if you do not have it.

## Request

#### Sample request 

```shell
POST /jobs HTTP/1.1
Host: <UIN>.cos-control.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Authorization: Auth String
x-cos-appid: <appid>

<?xml version="1.0" encoding="UTF-8"?>
<CreateJobRequest>
...
</CreateJobRequest>
```

>?Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request fields

Calling the `CreateJob` API requires the following parameters:

| Parameter | Description | Required |
| ----------- | -------------------------------- | -------- |
| x-cos-appid | User APPID with a length of 1–64 bytes. | Yes |

#### Request headers
This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body
You can set the configuration for the inventory job in the request body by using the XML markup language. This information includes objects to be analyzed by the inventory job, the frequency and dimension of the analysis, and the format and storage location of the analysis result.

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
        <COSInitiateRestoreObject>   
            <ExpirationInDays> integer </ExpirationInDays>
            <JobTier> string </JobTier>
        </COSInitiateRestoreObject>
        <COSPutObjectCopy> 
            <AccessControlDirective>string</AccessControlDirective>
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
            <PrefixReplace>boolean</PrefixReplace>
            <ResourcesPrefix>string</ResourcesPrefix>
            <TargetKeyPrefix>string</TargetKeyPrefix>
            <CannedAccessControlList>string</CannedAccessControlList>
            <MetadataDirective>string</MetadataDirective>
            <ModifiedSinceConstraint>timestamp</ModifiedSinceConstraint>
            <UnModifiedSinceConstraint>timestamp</UnModifiedSinceConstraint>
            <MetadataDirective>string</MetadataDirective>
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
            <TaggingDirective>string</TaggingDirective>
            <NewObjectTagging>
                <COSTag>
                    <Key>string</Key> 
                    <Value>string</Value>
                </COSTag>
            </NewObjectTagging>
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

For other elements, see [Common Elements](https://intl.cloud.tencent.com/document/product/436/33786).



| Node Name | Parent Node | Description | Type | Required |
| -------------------- | ---------------- | ------------------------------------------------------------ | ---------------- | -------- |
| ClientRequestToken | CreateJobRequest | Token unique to each request; it prevents the frontend from initiating the same batch operation job multiple times. The token can be 1–64 bytes long, and a UUID is recommended | String | Yes |
| ConfirmationRequired | CreateJobRequest | Specifies whether confirmation is required before a job is executed. Default value: `false`. | Boolean | No |
| Description | CreateJobRequest | Job description with a length of 0–256 bytes. This parameter will be returned if it is configured when the job is created | String | No |
| Manifest             | CreateJobRequest | Inventory of the objects to be processed. These objects must be recorded in the object inventory. You can use [Enabling Inventory](https://intl.cloud.tencent.com/document/product/436/30624) to generate a file inventory.   | Manifest Object  | Yes       |
| Operation            | CreateJobRequest | Specifies the operation to perform on the objects in the file inventory. COS currently supports operations such as [copying objects in batches](https://intl.cloud.tencent.com/document/product/436/32960) and [restoring archived objects in batches](https://intl.cloud.tencent.com/document/product/436/34075), and you can process the inventory data in the bucket accordingly. | Operation Object | Yes       |
| Priority | CreateJobRequest | Job priority. The higher the value, the higher the priority. Value range: 0–2147483647 | Integer | Yes |
| Report | CreateJobRequest | Job report. You can configure this parameter to output a report upon job completion to evaluate the job execution  | Report Object | Yes |
| RoleArn | CreateJobRequest | COS resource ID used to identify the role you have created, required for identity verification | String | Yes |

## Response

**Response header**

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Response body**

```shell
<CreateJobResult>
   <JobId>string</JobId>
</CreateJobResult>
```

The nodes are described as follows:

| Node Name | Parent Node | Description | Type |
| ------ | --------------- | ------------------------------------------------------------ | ------ |
| JobId | CreateJobResult | Job ID. This value is automatically returned by COS after a job is created successfully. Length: 1–64 bytes | String |

**Error codes**

This request operation may return the following error messages. For other error information, please see [Error Response](https://intl.cloud.tencent.com/document/product/436/33787).

| Error Code | Description | Status Code | API |
| ------------------ | ------------------------------------------ | ------ | --------- |
| InvalidRequest | Duplicate request | 400 | CreateJob |
| InvalidRequest | Priority must be an integer between 0 and 2147483647 | 400 | CreateJob |
| MalformedXML | The `XML Manifest` field in the request body does not conform to XML syntax  | 400 | CreateJob |
| MalformedXML | The `XML Operation` field in the request body does not conform to XML syntax | 400 | CreateJob |
| MalformedXML | The `XML Report` field in the request body does not conform to XML syntax | 400 | CreateJob |
| ServiceUnavailable | Unable to create a job as the service is temporarily unavailable | 500 | CreateJob |
| TooManyJobs  | The number of jobs has reached the upper limit, making the server unavailable | 500 | CreateJob |



## Use Cases

#### Request

```shell
POST /jobs HTTP/1.1
Host: 100000000001.cos-control.ap-chengdu.myqcloud.com
Date: Thu, 19 Dec 2019 18:00:29 GMT
x-cos-appid: 1250000000
Content-Type: application/xml
Content-Length: 1056
Content-MD5: hHcgq5mu8s0YP4WTGiQ+uA==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1576778429;1576785629&q-key-time=1576778429;1576785629&q-header-list=content-length;content-md5;content-type;date;host;x-cos-appid&q-url-param-list=&q-signature=8e0db6883376b5df713819f878da5020c5b6****
Connection: close

<CreateJobRequest>
	<ClientRequestToken>184ce261-18af-5e3d-3e30-253723cfd937</ClientRequestToken>
	<ConfirmationRequired>false</ConfirmationRequired>
	<Description>example-job</Description>
	<Manifest>
		<Location>
			<ETag>"15150651828fa9cdcb8356b6d1c7638b"</ETag>
			<ObjectArn>qcs::cos:ap-chengdu::sourcebucket-1250000000/manifests/batch-copy-manifest.csv</ObjectArn>
		</Location>
		<Spec>
			<Fields>
				<member>Bucket</member>
				<member>Key</member>
			</Fields>
			<Format>COSBatchOperations_CSV_V1</Format>
		</Spec>
	</Manifest>
	<Operation>
		<COSPutObjectCopy>
			<TargetResource>qcs::cos:ap-chengdu:uid/1250000000:destinationbucket-1250000000</TargetResource>
		</COSPutObjectCopy>
	</Operation>
	<Priority>10</Priority>
	<Report>
		<Bucket>qcs::cos:ap-chengdu::sourcebucket-1250000000</Bucket>
		<Enabled>true</Enabled>
		<Format>Report_CSV_V1</Format>
		<Prefix>job-result</Prefix>
		<ReportScope>AllTasks</ReportScope>
	</Report>
	<RoleArn>qcs::cam::uin/100000000001:roleName/COS_Batch_QcsRole</RoleArn>
</CreateJobRequest>
```

#### Response

After the above request is made, COS will return the following response, indicating that the inventory job has been successfully configured.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 89
Connection: close
Date: Thu, 19 Dec 2019 18:00:30 GMT
Server: tencent-cos
x-cos-request-id: NWRmYmJhYmRfMjViMjU4NjRfNmIzYV8xMDE2****

<CreateJobResult>
	<JobId>53dc6228-c50b-46f7-8ad7-65e7159f1aae</JobId>
</CreateJobResult>
```
