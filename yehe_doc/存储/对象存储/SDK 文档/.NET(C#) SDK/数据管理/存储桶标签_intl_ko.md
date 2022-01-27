## 소개

본 문서에서는 버킷 태그에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                       |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | 버킷 태그 설정 | 기존 버킷에 대한 태그 설정         |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | 버킷 태그 조회 | 지정된 버킷의 기존 버킷 태그 조회 |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | 버킷 태그 삭제 | 지정된 버킷 태그 삭제             |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버킷 태그 설정

#### 기능 설명

PUT Bucket tagging 기존 버킷의 태그를 설정하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-bucket-tagging)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  PutBucketTaggingRequest request = new PutBucketTaggingRequest(bucket);
  string akey = "aTagKey";
  string avalue = "aTagValue";
  string bkey = "bTagKey";
  string bvalue = "bTagValue";

  request.AddTag(akey, avalue);
  request.AddTag(bkey, bvalue);
  
  //실행 요청
  PutBucketTaggingResult result = cosXml.PutBucketTagging(request);
  
  //요청 완료
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //요청 실패
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //요청 실패
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketTagging.cs)를 참고하십시오.

## 버킷 태그 조회

#### 기능 설명

GET Bucket tagging 지정된 버킷의 기존 버킷 태그를 조회하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-get-bucket-tagging)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  GetBucketTaggingRequest request = new GetBucketTaggingRequest(bucket);   
  //실행 요청
  GetBucketTaggingResult result = cosXml.GetBucketTagging(request);
  
  //요청 완료
  Tagging tagging = result.tagging;
  Console.WriteLine(tagging);
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //요청 실패
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //요청 실패
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketTagging.cs)를 참고하십시오.

## 버킷 태그 삭제

#### 기능 설명

DELETE Bucket tagging 지정된 버킷의 기존 버킷 태그를 삭제하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-delete-bucket-tagging)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  DeleteBucketTaggingRequest request = new DeleteBucketTaggingRequest(bucket);   
  //실행 요청
  DeleteBucketTaggingResult result = cosXml.DeleteBucketTagging(request);
  
  //요청 완료
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //요청 실패
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //요청 실패
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketTagging.cs)를 참고하십시오.

