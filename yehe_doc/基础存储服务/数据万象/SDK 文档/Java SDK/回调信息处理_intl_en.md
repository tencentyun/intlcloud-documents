## Overview

This document provides SDK code samples for standard callback information parsing in CI.

## XML Callback Content Parsing

### Description

The common XML callback information in CI is parsed into Java objects.

### Examples

This example shows you how to parse the XML callback data by getting Unmarshallers.
>? You can get the required XML parser by viewing the APIs of COSClient. You can also find out which Unmarshaller is being used by viewing the query API corresponding to the feature.
>

For example, the query API corresponding to the file preview callback information is `describeDocProcessJob`.
- The code snippet in [COSClient](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/COSClient.java) used to check which Unmarshaller is used by the `invoke` method.
```java
@Override
public DocJobResponse describeDocProcessJob(DocJobRequest request) {
    this.checkCIRequestCommon(request);
    CosHttpRequest<DocJobRequest> httpRequest = this.createRequest(request.getBucketName(), "/doc_jobs/" + request.getJobId(), request, HttpMethodName.GET);
    return this.invoke(httpRequest, new Unmarshallers.DescribeDocJobUnmarshaller());
}
```
- Use Unmarshaller to parse the response content.
```java
public static void processCINotifyResponse(String response) throws Exception {
    Unmarshallers.DescribeDocJobUnmarshaller describeDocJobUnmarshaller = new Unmarshallers.DescribeDocJobUnmarshaller();
    InputStream is = new ByteArrayInputStream(response.getBytes());
    DocJobResponse docJobResponse = describeDocJobUnmarshaller.unmarshall(is);
}
```

## JSON Callback Content Parsing

### Description

The common JSON callback information in CI is parsed into Java objects.

### Examples

>? 
> - Essentially, processing JSON callbacks is to convert JSON to XML before processing.
> - The demo uses org.json to convert JSON to XML. This dependency is not provided in the POM of the SDK and needs to be imported by yourself.
> 

For example, the query API corresponding to image moderation callback information is `describeAuditingImageJob`.
- The code snippet in [COSClient](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/COSClient.java) used to check which Unmarshaller is used by the `invoke` method.
```java
@Override
public ImageAuditingResponse describeAuditingImageJob(DescribeImageAuditingRequest imageAuditingRequest) {
    rejectNull(imageAuditingRequest.getBucketName(),
            "The bucketName parameter must be specified setting the object tags");
    rejectNull(imageAuditingRequest.getJobId(),
            "The jobId parameter must be specified setting the object tags");
    CosHttpRequest<DescribeImageAuditingRequest> request = createRequest(imageAuditingRequest.getBucketName(), "/image/auditing/" + imageAuditingRequest.getJobId(), imageAuditingRequest, HttpMethodName.GET);
    return invoke(request, new Unmarshallers.ImageAuditingDescribeJobUnmarshaller());
}
```
- Use Unmarshaller to parse the response content after converting the JSON response to XML.
```java
// Callback demo
public static void processJsonCINotifyResponse(String jsonResponse) throws Exception {
    JSONObject response = new JSONObject(jsonResponse);
    JSONObject json = new JSONObject();
    json.put("Response",response);
    String xml = XML.toString(json);
    Unmarshallers.ImageAuditingDescribeJobUnmarshaller imageJobUnmarshaller = new Unmarshallers.ImageAuditingDescribeJobUnmarshaller();
    InputStream is = new ByteArrayInputStream(xml.getBytes());
    ImageAuditingResponse imageAuditingResponse = imageJobUnmarshaller.unmarshall(is);
}
```

org.json.json is used in the above example, which is not provided in the SDK. If you need to use it, add the following dependencies:
```xml
<dependency>
    <groupId>org.json</groupId>
    <artifactId>json</artifactId>
    <version>20180130</version>
</dependency>
```
