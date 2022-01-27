## 소개
본 문서는 라이프사이클에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름       | 작업 설명                     |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | 라이프사이클 설정 | 버킷의 라이프사이클 관리 구성 설정 |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | 라이프사이클 쿼리 | 버킷 라이프사이클 관리 설정 쿼리   |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | 라이프사이클 삭제 | 버킷 라이프사이클 관리 구성 삭제   |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 라이프사이클 설정

#### 기능 설명

지정된 버킷의 라이프사이클 설정 정보를 설정합니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
  //lifecycle 설정
  LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
  rule.id = "lfiecycleConfigureId";
  rule.status = "Enabled"; //Enabled，Disabled

  rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
  rule.filter.prefix = "2/";

  //만료된 파트 삭제 작업 지정
  rule.abortIncompleteMultiUpload = new LifecycleConfiguration.AbortIncompleteMultiUpload();
  rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

  request.SetRule(rule);

  //실행 요청
  PutBucketLifecycleResult result = cosXml.PutBucketLifecycle(request);
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLifecycle.cs)을 참고하십시오.


## 라이프사이클 쿼리

#### 기능 설명

버킷 라이프사이클 관리 설정을 쿼리합니다.

#### 예시 코드

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
  //실행 요청
  GetBucketLifecycleResult result = cosXml.GetBucketLifecycle(request);
  //버킷 라이프사이클 설정
  LifecycleConfiguration conf = result.lifecycleConfiguration;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLifecycle.cs)을 참고하십시오.

## 라이프사이클 삭제

#### 기능 설명

버킷 라이프사이클 관리 설정을 삭제합니다.

#### 예시 코드

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
  //실행 요청
  DeleteBucketLifecycleResult result = cosXml.DeleteBucketLifecycle(request);
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLifecycle.cs)을 참고하십시오.

