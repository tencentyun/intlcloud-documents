## Overview

This document provides an overview of APIs and SDK code samples related to object content extraction.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts the content of a specified object (in CSV or JSON format) |

## Simple Operations

Requests for simple operations need to be initiated through COSClient instances. You need to create a COSClient instance before performing simple operations.

COSClient instances are concurrency safe. You are advised to create only one COSClient instance for a process and then close it when it is no longer used to initiate requests.

### Creating a COSClient instance

Before calling the COS API, you need to create a COSClient instance.

```java
// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Set the user identity information.
    // Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
    String secretId = "SECRETID";
    String secretKey = "SECRETKEY";
    COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol, `http` or `https`.
    // For 5.6.53 and earlier versions, HTTPS is recommended.
    // Starting from 5.6.54, HTTPS is used by default.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // The following settings are optional.

    // Set the read timeout period, which is 30s by default.
    clientConfig.setSocketTimeout(30*1000);
    // Set the connection timeout period, which is 30s by default.
    clientConfig.setConnectionTimeout(30*1000);

    // If necessary, set the HTTP proxy, IP, and port.
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // Generate a COS client.
    return new COSClient(cred, clientConfig);
}
```

### Creating a COSClient client with a temporary key

If you want to request COS with a temporary key, you need to create a COSClient instance with the temporary key.
This SDK does not generate temporary keys. For how to generate a temporary key, please see [Generating a Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048#cos-sts-sdk).

```java

// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Here, the temporary key information is needed.
    // For how to generate temporary keys, please visit https://intl.cloud.tencent.com/document/product/436/14048.
    String tmpSecretId = "TMPSECRETID";
    String tmpSecretKey = "TMPSECRETKEY";
    String sessionToken = "SESSIONTOKEN";

    COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol, `http` or `https`.
    // For 5.6.53 and earlier versions, HTTPS is recommended.
    // Starting from 5.6.54, HTTPS is used by default.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // The following settings are optional.

    // Set the read timeout period, which is 30s by default.
    clientConfig.setSocketTimeout(30*1000);
    // Set the connection timeout period, which is 30s by default.
    clientConfig.setConnectionTimeout(30*1000);

    // If necessary, set the HTTP proxy, IP, and port.
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // Generate a COS client.
    return new COSClient(cred, clientConfig);
}
```

## Extracting Object Content

COS Select supports extracting content from objects in the following formats:

* CSV: an object is stored in CSV format with its data records separated with a specific delimiter.
* JSON: an object is stored in JSON format, which can be either a JSON file or a JSON list.

> !
- To use COS Select, you must have the permission on `cos:GetObject`.
- CSV and JSON objects need to be encoded in UTF-8.
- COS Select can extract CSV and JSON objects compressed by gzip or bzip2.
- COS Select can extract CSV and JSON objects encrypted with SSE-COS.

### Extracting content from an object in CSV format

#### Method prototype

```java
public SelectObjectContentResult selectObjectContent(SelectObjectContentRequest selectRequest) throws CosClientException, CosServiceException {
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

String query = "select s._1 from COSObject s";

SelectObjectContentRequest request = new SelectObjectContentRequest();
request.setBucketName(bucketName);
request.setKey(key);
request.setExpression(query);
request.setExpressionType(ExpressionType.SQL);

InputSerialization inputSerialization = new InputSerialization();
CSVInput csvInput = new CSVInput();
csvInput.setFieldDelimiter(",");
csvInput.setRecordDelimiter("\n");
inputSerialization.setCsv(csvInput);
inputSerialization.setCompressionType(CompressionType.NONE);
request.setInputSerialization(inputSerialization);

OutputSerialization outputSerialization = new OutputSerialization();
outputSerialization.setCsv(new CSVOutput());
request.setOutputSerialization(outputSerialization);

final AtomicBoolean isResultComplete = new AtomicBoolean(false);
SelectObjectContentResult result = cosclient.selectObjectContent(request);
InputStream resultInputStream = result.getPayload().getRecordsInputStream(
        new SelectObjectContentEventVisitor() {
            @Override
            public void visit(SelectObjectContentEvent.StatsEvent event)
            {
                System.out.println(
                        "Received Stats, Bytes Scanned: " + event.getDetails().getBytesScanned()
                                +  " Bytes Processed: " + event.getDetails().getBytesProcessed());
            }
            @Override
            public void visit(SelectObjectContentEvent.EndEvent event)
            {
                isResultComplete.set(true);
                System.out.println("Received End Event. Result is complete.");
            }
        }
);
BufferedReader reader = new BufferedReader(new InputStreamReader(resultInputStream));
StringBuffer stringBuffer = new StringBuffer();
String line;
while((line = reader.readLine())!= null){
    stringBuffer.append(line).append("\n");
}
System.out.println(stringBuffer.toString());
// Check whether the result is completed obtained.
if (!isResultComplete.get()) {
    throw new Exception("result was incomplete");
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| --------- | -------------- |---------- |
| selectRequest | Request | SelectObjectContentRequest |

`SelectObjectContentRequest` member description:

| Parameter | Setting Method | Description | Type |
| ------------- | -------- | --------- | ------ |
| bucketName  | Set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg` | String |
| expression | Set method | Request expression | String |
| expressionType | Set method | Request expression type | String |
| inputSerialization | Set method | Format of the object to be extracted | InputSerialization |
| outputSerialization | Set method | Output format of the extraction result | OutputSerialization |

#### Response description

- Success: return `InputStream`.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Extracting content from an object in JSON format

#### Method prototype

```java
public SelectObjectContentResult selectObjectContent(SelectObjectContentRequest selectRequest) throws CosClientException, CosServiceException {
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

String query = "select * from COSObject s where mathScore > 85'";

SelectObjectContentRequest request = new SelectObjectContentRequest();
request.setBucketName(bucketName);
request.setKey(key);
request.setExpression(query);
request.setExpressionType(ExpressionType.SQL);

InputSerialization inputSerialization = new InputSerialization();
JSONInput jsonInput = new JSONInput();
jsonInput.setType(JSONType.LINES);
inputSerialization.setJson(jsonInput);
inputSerialization.setCompressionType(CompressionType.NONE);
request.setInputSerialization(inputSerialization);

OutputSerialization outputSerialization = new OutputSerialization();
outputSerialization.setJson(new JSONOutput());
request.setOutputSerialization(outputSerialization);

final AtomicBoolean isResultComplete = new AtomicBoolean(false);
SelectObjectContentResult result = cosclient.selectObjectContent(request);
InputStream resultInputStream = result.getPayload().getRecordsInputStream(
        new SelectObjectContentEventVisitor() {
            @Override
            public void visit(SelectObjectContentEvent.StatsEvent event)
            {
                System.out.println(
                        "Received Stats, Bytes Scanned: " + event.getDetails().getBytesScanned()
                                +  " Bytes Processed: " + event.getDetails().getBytesProcessed());
            }
            @Override
            public void visit(SelectObjectContentEvent.EndEvent event)
            {
                isResultComplete.set(true);
                System.out.println("Received End Event. Result is complete.");
            }
        }
);
BufferedReader reader = new BufferedReader(new InputStreamReader(resultInputStream));
StringBuffer stringBuffer = new StringBuffer();
String line;
while((line = reader.readLine())!= null){
    stringBuffer.append(line).append("\n");
}
System.out.println(stringBuffer.toString());
// Check whether the result is completed obtained.
if (!isResultComplete.get()) {
    throw new Exception("result was incomplete");
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| --------- | -------------- |---------- |
| selectRequest | Request | SelectObjectContentRequest |

`SelectObjectContentRequest` member description:

| Parameter | Setting Method | Description | Type |
| ------------- | -------- | --------- | ------ |
| bucketName  | Set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg` | String |
| expression | Set method | Request expression | String |
| expressionType | Set method | Request expression type | String |
| inputSerialization | Set method | Format of the object to be extracted | InputSerialization |
| outputSerialization | Set method | Output format of the extraction result | OutputSerialization |

#### Response description

- Success: return `InputStream`.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
