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
```cs
try
{
    // Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
    string bucket = "examplebucket-1250000000";
    string key = "exampleobject"; // Object key

    SelectObjectRequest request = new SelectObjectRequest(bucket, key);

    ObjectSelectionFormat.JSONFormat jSONFormat = new ObjectSelectionFormat.JSONFormat();
    jSONFormat.Type = "DOCUMENT";
    jSONFormat.RecordDelimiter = "\n";
    
    string outputFile = "select_local_file.json";

    request.SetExpression("Select * from COSObject")
            .SetInputFormat(new ObjectSelectionFormat(null, jSONFormat))
            .SetOutputFormat(new ObjectSelectionFormat(null, jSONFormat))
            .SetCosProgressCallback(delegate (long progress, long total) {
                Console.WriteLine("OnProgress : " + progress + "," + total);
            })
            .OutputToFile(outputFile)
            ;

    SelectObjectResult selectObjectResult =  cosXml.SelectObject(request);
    Console.WriteLine(selectObjectResult.stat);
}
catch (COSXML.CosException.CosClientException clientEx)
{
    Console.WriteLine("CosClientException: " + clientEx.StackTrace);
    Console.WriteLine("CosClientException: " + clientEx.Message);
}
catch (COSXML.CosException.CosServerException serverEx)
{
    Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/SelectObject.cs).

