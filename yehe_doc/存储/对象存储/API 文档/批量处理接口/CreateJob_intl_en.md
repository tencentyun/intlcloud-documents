## Feature

This API is used to create a batch operation job in a bucket. For more information, please see [Batch Operation Overview](https://cloud.tencent.com/document/product/436/38601).

When calling this API, make sure you have the permission to operate on objects in the bucket. The bucket owner has such permission by default, please apply with the bucket owner for the permission first if you do not have it.

## Request

#### Sample Request

```shell
POST /jobs HTTP/1.1
Host: <UIN>.cos-control.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Authorization: Auth String
x-cos-appid: <appid>

<?xml version="1.0" encoding="UTF-8" ?>
<CreateJobRequest>
...
</CreateJobRequest>
```

>Authorization: Auth String (see [Request Signature](https://cloud.tencent.com/document/product/436/7778) for more information).

#### Request Parameters

Calling the `CreateJob` API requires the following parameters:

| Parameter | Description | Required |
| ----------- | ------------------------ | ---- |
| x-cos-appid | User APPID with a length of 1–64 bytes. | Yes |

#### Request Headers
This API only uses common request headers. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

#### Request Body
You can set the configuration information for the inventory job in the request body with the XML language. This information includes objects to be analyzed by the inventory job, frequency and dimension of the analysis, and format and storage location of the analysis result.

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

For other elements, see [Common Elements](https://cloud.tencent.com/document/product/436/38607).



| Node Name | Parent Node | Description | Type | Required |
| -------------------- | ---------------- | ------------------------------------------------------------ | ---------------- | -------- |
| ClientRequestToken | CreateJobRequest | Token unique to each request, which prevents the frontend from initiating the same batch operation job multiple times. The token can be 1–64 bytes long, and a UUID is recommended | String | Yes |
| ConfirmationRequired | CreateJobRequest | Specifies whether confirmation is required before a job is executed on. Default value: `false`. | Boolean | No |
| Description | CreateJobRequest | Job description; 0–256 bytes long. This parameter will be returned if it is configured when the job is created | String | No |
| Manifest | CreateJobRequest | Inventory of objects to be processed. You need to record in the corresponding inventory objects to be processed | Manifest Object  | Yes |
| ConfirmationRequired | CreateJobRequest | Specifies whether confirmation is required before a job is executed on. Default value: `false`. | Boolean | No |
| Priority | CreateJobRequest | Job priority. The higher the value, the higher the priority. Value range: 0–2,147,483,647 | Integer | Yes |
| Report | CreateJobRequest | Job report. You can configure this parameter to output a report upon job completion to evaluate the job execution  | Report Object | Yes |
| RoleArn | CreateJobRequest | COS resource ID used to identify the role you have created, required for identity verification | String | Yes |

## Response

**Response header**

This API only returns common response headers. For more information, see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729).

**Response Body**

```shell
<CreateJobResult>
   <JobId>string</JobId>
</CreateJobResult>
```

The content is described in details below:

| Node Name | Parent Node | Description | Type |
| ------ | --------------- | ------------------------------------------------------------ | ------ |
| JobId | CreateJobResult | Job ID, which is automatically returned by COS after a job is created successfully. Length: 1–64 bytes | String |

**Error Codes**

This request operation may return the following error messages. For other errors, please see [Error Response](https://cloud.tencent.com/document/product/436/38610).

| Error Code | Description | Status Code | API |
| ------------------ | ----------------------------------------- | ------ | --------- |
| InvalidRequest | Duplicate request | 400 | CreateJob |
| InvalidRequest | Priority must be an integer between 0 and 2,147,483,647 | 400 | CreateJob |
| MalformedXML | The `XML Manifest` field in the request body does not conform to the XML syntax  | 400 | CreateJob |
| MalformedXML | The `XML Operation` field in the request body does not conform to the XML syntax | 400 | CreateJob |
| MalformedXML | The `XML Report` field in the request body does not conform to the XML syntax | 400 | CreateJob |
| ServiceUnavailable | The service is temporarily unavailable and unable to create a job | 500 | CreateJob |
| TooManyJobs  | The number of jobs has reached the upper limit, making the server unavailable | 500 | CreateJob |



## Use Cases

#### Request

```shell
POST /jobs HTTP/1.1
Host: 100000000001.cos-control.ap-chengdu.myqcloud.com
Date: Thu, 08 Aug 2019 09:15:29 GMT
x-cos-appid: 1250000000
Content-Type: application/xml
Content-Length: 1056
Content-MD5: hHcgq5mu8s0YP4WTGiQ+uA==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560760213;1560767413&q-key-time=1560760213;1560767413&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=acl&q-signature=70f96b91823f3715905df125d96fe447554e****
Connection: close

<CreateJobRequest>
	<ClientRequestToken>1829b6c7-3141-42f1-9fe4-17082b841646</ClientRequestToken>
	<ConfirmationRequired>false</ConfirmationRequired>
	<Description>example job</Description>
	<Manifest>
		<Location>
			<ETag>"15150651828fa9cdcb8356b6d1c7638b"</ETag>
			<ObjectArn>qcs::cos:ap-chengdu::manifest-1250000000/1250000000/source/manifest/20190715/manifest.json</ObjectArn>
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
			<TargetResource>qcs::cos:ap-chengdu::target-1250000000</TargetResource>
		</COSPutObjectCopy>
	</Operation>
	<Priority>10</Priority>
	<Report>
		<Bucket>qcs::cos:ap-chengdu::sourcebucket-1250000000</Bucket>
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
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 89
Connection: close
Date: Thu, 08 Aug 2019 09:15:29 GMT
Server: tencent-cos
x-cos-request-id: NWRmYmJhYmRfMjViMjU4NjRfNmIzYV8xMDE2****

<CreateJobResult>
	<JobId>53dc6228-c50b-46f7-8ad7-65e7159f1aae</JobId>
</CreateJobResult>
```

