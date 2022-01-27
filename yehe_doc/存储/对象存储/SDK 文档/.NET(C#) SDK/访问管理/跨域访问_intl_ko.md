## 소개

본 문서는 교차 출처 리소스 공유에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름       | 작업 설명                     |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | 교차 출처 리소스 공유 구성 설정 | 버킷 크로스 도메인 액세스 권한 설정     |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | 교차 출처 리소스 공유 구성 조회 | 버킷 교차 출처 리소스 공유 구성 정보 조회 |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | 교차 출처 리소스 공유 구성 삭제 | 교차 출처 리소스 공유 구성 정보 삭제 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 교차 출처 리소스 공유 구성 설정

#### 기능 설명

지정된 버킷의 교차 출처 리소스 공유 구성 정보(PUT Bucket cors)를 설정합니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-bucket-cors)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  PutBucketCORSRequest request = new PutBucketCORSRequest(bucket);
  //교차 출처 리소스 공유 CORS 설정
  COSXML.Model.Tag.CORSConfiguration.CORSRule corsRule = 
    new COSXML.Model.Tag.CORSConfiguration.CORSRule();
  corsRule.id = "corsconfigureId";
  corsRule.maxAgeSeconds = 6000;
  
  corsRule.allowedOrigins = new List<string>();
  corsRule.allowedOrigins.Add("http://cloud.tencent.com");

  corsRule.allowedMethods = new List<string>();
  corsRule.allowedMethods.Add("PUT");

  corsRule.allowedHeaders = new List<string>();
  corsRule.allowedHeaders.Add("Host");

  corsRule.exposeHeaders = new List<string>();
  corsRule.exposeHeaders.Add("x-cos-meta-x1");

  request.SetCORSRule(corsRule);

  //실행 요청
  PutBucketCORSResult result = cosXml.PutBucketCORS(request);
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs)를 참고하십시오.

## 교차 출처 리소스 공유 구성 조회

#### 기능 설명

지정된 버킷의 교차 출처 리소스 공유 구성 정보를 조회합니다(GET Bucket cors).

#### 예시 코드

[//]: # (.cssg-snippet-get-bucket-cors)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  GetBucketCORSRequest request = new GetBucketCORSRequest(bucket);
  //실행 요청
  GetBucketCORSResult result = cosXml.GetBucketCORS(request);
  //버킷의 CORS 구성 정보
  CORSConfiguration conf = result.corsConfiguration;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs)를 참고하십시오.

## 교차 출처 리소스 공유 구성 삭제

#### 기능 설명

지정된 버킷의 교차 출처 리소스 공유 구성을 삭제합니다(DELETE Bucket cors).

#### 예시 코드

[//]: # (.cssg-snippet-delete-bucket-cors)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  DeleteBucketCORSRequest request = new DeleteBucketCORSRequest(bucket);
  //실행 요청
  DeleteBucketCORSResult result = cosXml.DeleteBucketCORS(request);
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketCORS.cs)를 참고하십시오.


