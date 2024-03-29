## 简介

本文档提供关于检索对象内容操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | 检索对象内容 | 从指定对象（CSV 格式或者 JSON 格式）中检索内容                      |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 检索对象内容

#### 功能说明

COS Select 支持检索以下格式的对象数据：

* CSV 格式：对象以 CSV 格式存储，并以固定的分隔符划分。
* JSON 格式：对象以 JSON 格式存储，可以是 JSON 文件或者 JSON 列表。

> !
>- 使用 COS Select，您必须具有 `cos:GetObject` 的授权。
>- CSV、JSON 对象需要以 UTF-8 格式编码。
>- COS Select 支持检索 GZIP 或者 BZIP2 压缩的 CSV、JSON 对象。
>- COS Select 支持检索 SSE-COS 加密的 CSV、JSON 对象。

#### 示例代码

[//]: # (.cssg-snippet-select-object)
```cs
try
{
    // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
    string bucket = "examplebucket-1250000000";
    string key = "exampleobject"; //对象键

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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/SelectObject.cs) 查看。

