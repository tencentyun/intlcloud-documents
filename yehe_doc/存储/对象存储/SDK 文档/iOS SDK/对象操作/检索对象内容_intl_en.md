## Overview

This document provides an overview of APIs and SDK code samples related to object content extraction.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts the content of a specified object (in CSV or JSON format) |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Extracting Object Content

#### Description

COS Select supports extracting content from objects in the following formats:

* CSV: an object is stored in CSV format with its data records separated with a specific delimiter.
* JSON: an object is stored in JSON format, which can be either a JSON file or a JSON list.

> !
>- To use COS Select, you must have the permission on `cos:GetObject`.
>- CSV and JSON objects need to be encoded in UTF-8.
>- COS Select can extract CSV and JSON objects compressed by gzip or bzip2.
>- COS Select can extract CSV and JSON objects encrypted with SSE-COS.

#### Sample code

[//]: # (.cssg-snippet-select-object)
```objective-c
QCloudSelectObjectContentRequest *request = [QCloudSelectObjectContentRequest new];
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = @"exampleobject";
request.selectType = @"2";
// Select file configuration
QCloudSelectObjectContentConfig *config= [QCloudSelectObjectContentConfig new];
/**SQL expression, representing the extract operation you need to initiate. For example, you can use the `SELECT s._1 FROM COSObject s` expression
 to extract the first column of data from a CSV-formatted object. For more information on SQL expressions,
 please see [SELECT Command](https://cloud.tencent.com/document/product/436/37636).
*/
config.express = @"select * from COSObject";
/**
Expression type, which is an extension. Currently, only SQL expressions and parameters are supported.
*/
config.expressionType = QCloudExpressionTypeSQL;
/**
 Specify the format of the object to extract.
 */
QCloudInputSerialization *inputS = [QCloudInputSerialization new];
inputS.compressionType = QCloudCOSXMLCompressionTypeNONE;
/**
Specify the required file parameters for the JSON object format.
*/
QCloudSerializationJSON *inputJson = [QCloudSerializationJSON new];
/**
    JSON file type:
    `DOCUMENT` indicates that the JSON file contains only one independent JSON object and the object can be cut into multiple lines.
    `LINES` indicates that each line in the JSON object contains an independent JSON object.
    Valid values: DOCUMENT, LINES
    */
inputJson.type = QCloudInputJSONFileTypeDocument;
inputS.serializationJSON = inputJson;
config.inputSerialization = inputS;
/**
 Specify the output format of extraction results.
 */
QCloudOutputSerialization *outputS = [QCloudOutputSerialization new];

QCloudSerializationJSON *outputJson = [QCloudSerializationJSON new];
/**
    A character that separates each data record in the output result into different lines, which is `\n` by default. You can specify any octal character
 such as a comma, semicolon, and tab. This parameter supports up to 2 bytes, i.e., you can enter a delimiter in the format of `\r\n`. Default value: `\n`.
    */
outputJson.outputRecordDelimiter = @"\n";
/**
     Specify the required file parameters for the JSON object format.
     */
outputS.serializationJSON = outputJson;

config.outputSerialization = outputS;
/**
 Specify whether to return the query progress information (`QueryProgress`). If this parameter is used, COS Select will periodically return the query progress.
 */
QCloudRequestProgress *requestProgress = [QCloudRequestProgress new];
requestProgress.enabled = @"FALSE";
config.requestProgress =requestProgress;
request.selectObjectContentConfig  = config;
/**
 Local save path of the file
 */
request.downloadingURL = [NSURL fileURLWithPath:QCloudFileInSubPath(@"test", @"2.json")];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
    NSLog(@"⏬⏬⏬⏬DOWN [Total]%lld  [Downloaded]%lld [Download]%lld", totalBytesExpectedToDownload, totalBytesDownload, bytesDownload);
}];

[request setFinishBlock:^(id  _Nonnull result, NSError * _Nonnull error) {
    NSLog(@"result = %@",result);
}];
[[QCloudCOSXMLService defaultCOSXML] SelectObjectContent:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # (.cssg-snippet-select-object)
```swift
let request = QCloudSelectObjectContentRequest.init();
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = "exampleobject";
// Version information of the API
request.selectType = "2";
// Select file configuration
let config = QCloudSelectObjectContentConfig();
/**SQL expression, representing the extract operation you need to initiate. For example, you can use the `SELECT s._1 FROM COSObject s` expression
 to extract the first column of data from a CSV-formatted object. For more information on SQL expressions,
 please see [SELECT Command](https://cloud.tencent.com/document/product/436/37636).
*/

config.express = "Select * from COSObject";
/**
Expression type, which is an extension. Currently, only SQL expressions and parameters are supported.
*/
config.expressionType = .SQL;

/**
 Specify the format of the object to extract.
 */
let inputS = QCloudInputSerialization();
inputS.compressionType = .NONE;
/**
    Specify the required file parameters for the JSON object format.
    */
let inputJson = QCloudSerializationJSON.init();
/**
    JSON file type:
    `DOCUMENT` indicates that the JSON file contains only one independent JSON object and the object can be cut into multiple lines.
    `LINES` indicates that each line in the JSON object contains an independent JSON object.
    Valid values: DOCUMENT, LINES
    */
inputJson.type = .document;

inputS.serializationJSON = inputJson;

config.inputSerialization = inputS;

/**
 Specify the output format of extraction results.
 */
let outputS = QCloudOutputSerialization.init();

let outputJson = QCloudSerializationJSON.init();
/**
    A character that separates each data record in the output result into different lines, which is `\n` by default. You can specify any octal character
 such as a comma, semicolon, and tab. This parameter supports up to 2 bytes, i.e., you can enter a delimiter in the format of `\r\n`. Default value: `\n`.
    */
outputJson.outputRecordDelimiter = "\n";
outputS.serializationJSON = outputJson;

config.outputSerialization = outputS;
/**
 Specify whether to return the query progress information (`QueryProgress`). If this parameter is used, COS Select will periodically return the query progress.
 */
let requestProgress = QCloudRequestProgress.init();
requestProgress.enabled = "FALSE";
config.requestProgress = requestProgress;
request.selectObjectContentConfig = config;
// Local save path of the file
request.downloadingURL = NSURL.fileURL(withPath: QCloudFileInSubPath("test", "2.json"));
request.finishBlock = {(result,error) in
    if error != nil{
        print(error!)
    }else{
        print(result!);
    }
 }

QCloudCOSXMLService.defaultCOSXML().selectObjectContent(request);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/SelectObject.swift).
