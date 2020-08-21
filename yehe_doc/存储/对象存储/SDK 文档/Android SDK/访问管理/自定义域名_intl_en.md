## Overview

This document provides an overview of APIs and SDK code samples related to custom domain name.

| API | Operation Name | Operation Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting custom domain name | Sets custom domain name information for a bucket |
| GET Bucket domain | Querying custom domain name | Queries the custom domain name information of a bucket |

## Setting Custom Domain Name

#### Feature description

This API (PUT Bucket domain) is used to configure a custom domain name for a bucket.

#### Method prototype

```
PutBucketDomainResult putBucketDomain(PutBucketDomainRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketDomainAsync(PutBucketDomainRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketDomainRequest putBucketDomainRequest = new PutBucketDomainRequest(bucket);
DomainConfiguration.DomainRule domainRule = new DomainConfiguration.DomainRule(
        DomainConfiguration.STATUS_ENABLED,
        "www.example.com",
        DomainConfiguration.TYPE_REST
);
domainRule.forcedReplacement = DomainConfiguration.REPLACE_CNAME;
putBucketDomainRequest.addDomainRule(domainRule);

// Use the sync method
try {
    PutBucketDomainResult putBucketDomainResult = cosXmlService.putBucketDomain(putBucketDomainRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.putBucketDomainAsync(putBucketDomainRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketDomainResult putBucketDomainResult = (PutBucketDomainResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| bucket            | Bucket for which to set a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| name                  | Custom domain name                                                   | String |
| status            | Domain name status. Valid values: ENABLED, DISABLED                     | String |
| type              | Type of bound origin server. Valid values: REST, WEBSITE                       | String |
| forcedReplacement | Forcibly overwrites existing configuration. Valid values: CNAME, TXT                    | String |

#### Response description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

#### Error codes

Some frequent special errors that may occur with this request are listed below:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | The domain name record already exists, and no forced overwriting is set in the request. Or, the domain name record does not exist, but forced overwriting is set in the request. |
| HTTP 451 Unavailable For Legal Reasons | The domain name is served in Mainland China but has no ICP filing.                          |

## Querying Custom Domain Name

#### Feature description

This API (GET Bucket domain) is used to query the custom domain name information of a bucket.

#### Method prototype

```
GetBucketDomainResult getBucketDomain(GetBucketDomainRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketDomainAsync(GetBucketDomainRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketDomainRequest getBucketDomainRequest = new GetBucketDomainRequest(bucket);
// Set signature verification host. All headers are to be verified by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
// Use the sync method
try {
    GetBucketDomainResult getBucketTaggingResult = cosXmlService.getBucketDomain(getBucketDomainRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getBucketDomainAsync(getBucketDomainRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketDomainResult getBucketTaggingResult = (GetBucketDomainResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket            | Bucket for which to query a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |

#### Response description

| Member Variable | Description | Type |
| ------------------- | -------------------------------------------------------- | ------------------- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
| domainConfiguration | Returns bucket object's `DomainConfiguration` information                | DomainConfiguration |

#### Response parameters

<table>
<thead>
<tr>
<th>Parameter Name</th>
<th>Description</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">x-cos-domain-txt-verification</td>
<td>Domain name verification information. This field is an MD5 check value, whose original string is in the following format: <code>cos[Region][BucketName-APPID][BucketCreateTime]</code>, where `Region` is the bucket region and `BucketCreateTime` is the bucket creation time in GMT</td>
<td>String</td>
</tr>
</tbody></table>
