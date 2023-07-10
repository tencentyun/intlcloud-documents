## 소개

본 문서는 버전 관리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명       | 작업 설명                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 버전 관리 설정 | 버킷의 버전 관리 기능 설정 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 버전 관리 확인 | 버킷의 버전 관리 정보 조회 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버전 관리 설정

#### 기능 설명

지정된 버킷의 버전 관리 기능을 설정합니다. 버전 관리 기능을 활성화한 후에는 일시 중지만 가능하며 비활성화할 수 없습니다.

#### 예시 코드

[//]: # ".cssg-snippet-put-bucket-versioning"
```cs
// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";
PutBucketVersioningRequest request = new PutBucketVersioningRequest(bucket);
request.IsEnableVersionConfig(true); //true: 버전 관리 활성화, false: 버전 관리 일시 중지

try
{
  PutBucketVersioningResult result = cosXml.PutBucketVersioning(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketVersioning.cs)을 참고하십시오.

## 버전 관리 조회

#### 기능 설명

지정된 버킷의 버전 관리 정보를 조회합니다.

- 버킷 버전 관리 상태를 가져오려면 버킷에 대한 읽기 권한이 있어야 합니다.
- 버전 관리 상태는 버전 관리 비활성화, 버전 관리 활성화, 버전 관리 일시 중지 세 가지입니다.

#### 예시 코드

[//]: # ".cssg-snippet-get-bucket-versioning"
```cs
// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";
GetBucketVersioningRequest request = new GetBucketVersioningRequest(bucket);

try
{
  GetBucketVersioningResult result = cosXml.GetBucketVersioning(request);
  // 버킷의 라이프사이클 설정
  VersioningConfiguration conf =  result.versioningConfiguration;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketVersioning.cs)을 참고하십시오.

