## 소개

본문은 로그 관리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명       | 작업 설명                   |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | 로그 설정 | 소스 버킷에 대한 로그 활성화     |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | 로그 설정 쿼리 | 소스 버킷의 로그 설정 쿼리 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 로그 관리 설정

#### 기능 설명

PUT Bucket logging은 소스 버킷에 대한 로깅을 활성화하고 지정된 대상 버킷에 액세스 로그를 저장하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-bucket-logging)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  PutBucketLoggingRequest request = new PutBucketLoggingRequest(bucket);
  // 로그를 저장할 타깃 경로 설정
  request.SetTarget("targetbucket-1250000000", "logs/");
  //실행 요청
  PutBucketLoggingResult result = cosXml.PutBucketLogging(request);
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLogging.cs)를 참고하십시오.

## 로그 설정 쿼리

#### 기능 설명

GET Bucket logging은 지정된 버킷의 로그 설정 정보를 쿼리하는 데 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-get-bucket-logging)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  GetBucketLoggingRequest request = new GetBucketLoggingRequest(bucket);
  //실행 요청
  GetBucketLoggingResult getResult = cosXml.GetBucketLogging(request);
  //요청 완료
  BucketLoggingStatus status = getResult.bucketLoggingStatus;
  if (status != null && status.loggingEnabled != null) {
    string targetBucket = status.loggingEnabled.targetBucket;
    string targetPrefix = status.loggingEnabled.targetPrefix;
  }
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLogging.cs)를 참고하십시오.

