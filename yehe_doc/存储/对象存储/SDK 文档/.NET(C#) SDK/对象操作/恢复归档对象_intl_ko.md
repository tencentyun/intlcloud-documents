## 소개

본 문서는 아카이브된 객체 복구 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 아카이브된 객체 복구 | 아카이브 유형의 객체 검색 및 액세스                      |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 아카이브된 객체 복구 

#### 기능 설명

아카이브 유형의 객체를 검색하여 액세스합니다(POST Object restore).

#### 예시 코드

[//]: # (.cssg-snippet-restore-object)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  RestoreObjectRequest request = new RestoreObjectRequest(bucket, key);
  //복구 시간
  request.SetExpireDays(3);
  request.SetTier(COSXML.Model.Tag.RestoreConfigure.Tier.Bulk);

  //실행 요청
  RestoreObjectResult result = cosXml.RestoreObject(request);
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/RestoreObject.cs)을 참고하십시오.

