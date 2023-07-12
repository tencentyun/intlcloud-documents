## 소개

본문은 정적 웹 사이트에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름           | 작업 설명                 |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | 정적 웹 사이트 설정     | 버킷의 정적 웹 사이트 구성 설정 |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | 정적 웹 사이트 설정 조회 | 버킷 정적 웹 사이트 설정 조회 |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | 정적 웹 사이트 설정 삭제 | 버킷 정적 웹 사이트 설정 삭제 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 정적 웹 사이트 설정

#### 기능 설명

PUT Bucket website는 버킷 정적 웹 사이트를 설정하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-bucket-website)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  PutBucketWebsiteRequest putRequest = new PutBucketWebsiteRequest(bucket);
  putRequest.SetIndexDocument("index.html");
  putRequest.SetErrorDocument("eroror.html");
  putRequest.SetRedirectAllRequestTo("index.html");
  PutBucketWebsiteResult putResult = cosXml.PutBucketWebsite(putRequest);
  
  //요청 완료
  Console.WriteLine(putResult.GetResultInfo());
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketWebsite.cs)를 참고하십시오.

## 정적 웹 사이트 설정 조회

#### 기능 설명

GET Bucket website는 버킷과 연결된 정적 웹 사이트 설정 정보를 조회하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-get-bucket-website)
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketWebsite.cs)를 참고하십시오.

## 정적 웹 사이트 설정 삭제

#### 기능 설명

DELETE Bucket website는 버킷의 정적 웹 사이트 설정을 삭제하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-delete-bucket-website)
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketWebsite.cs)를 참고하십시오.

