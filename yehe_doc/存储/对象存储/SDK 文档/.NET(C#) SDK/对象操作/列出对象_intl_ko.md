## 소개

본 문서는 객체 나열 관련 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명                   | 작업 설명                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회             | 버킷의 일부 또는 모든 객체 조회                 |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | 객체 및 이전 버전 리스트 조회 | 버킷의 일부 또는 모든 객체와 이전 버전 정보 조회 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 예시 코드 1: 첫 페이지 데이터 가져오기

[//]: #	".cssg-snippet-get-bucket"

```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  GetBucketRequest request = new GetBucketRequest(bucket);
  //실행 요청
  GetBucketResult result = cosXml.GetBucket(request);
  //bucket 관련 정보
  ListBucket info = result.listBucket;
  if (info.isTruncated) {
    // 데이터 잘림. 데이터의 nextMarker 기록.
    this.nextMarker = info.nextMarker;
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

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs)을 참고하십시오.

#### 예시 코드 2: 다음 페이지 데이터 요청

[//]: #	".cssg-snippet-get-bucket-next-page"

```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  GetBucketRequest request = new GetBucketRequest(bucket);
  // 이전 요청의 "nextMarker" 사용
  request.SetMarker(this.nextMarker);
  //실행 요청
  GetBucketResult result = cosXml.GetBucket(request);
  //bucket 관련 정보
  ListBucket info = result.listBucket;
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

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs)을 참고하십시오.

#### 예시 코드 3: 객체 및 하위 디렉터리 목록 가져오기

[//]: #	".cssg-snippet-get-bucket-with-delimiter"

```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  GetBucketRequest request = new GetBucketRequest(bucket);
  //a/ 아래에 있는 객체와 하위 디렉터리 가져오기
  request.SetPrefix("a/");
  request.SetDelimiter("/");
  //실행 요청
  GetBucketResult result = cosXml.GetBucket(request);
  //bucket 관련 정보
  ListBucket info = result.listBucket;
  // 객체 리스트
  List<ListBucket.Contents> objects = info.contentsList;
  // 하위 디렉터리 리스트
  List<ListBucket.CommonPrefixes> subDirs = info.commonPrefixesList;
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

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs)을 참고하십시오.

## 객체 버전 목록 쿼리

#### 기능 설명

버전 관리가 활성화된 버킷의 일부 또는 모든 객체를 조회합니다.

#### 예시 코드 1: 객체 버전 목록의 첫 번째 페이지 데이터 가져오기

[//]: #	".cssg-snippet-list-objects-versioning"

```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  ListBucketVersionsRequest request = new ListBucketVersionsRequest(bucket);
  //실행 요청
  ListBucketVersionsResult result = cosXml.ListBucketVersions(request);
  //bucket 관련 정보
  ListBucketVersions info = result.listBucketVersions;

  List<ListBucketVersions.Version> objects = info.objectVersionList;
  List<ListBucketVersions.CommonPrefixes> prefixes = info.commonPrefixesList;

  if (info.isTruncated) {
    // 데이터 잘림. 데이터의 nextMarker 기록.
    this.keyMarker = info.nextKeyMarker;
    this.versionIdMarker = info.nextVersionIdMarker;
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

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjectsVersioning.cs)을 참고하십시오.

#### 예시 코드 2: 개체 버전 목록의 다음 페이지 데이터 가져오기

[//]: #	".cssg-snippet-list-objects-versioning-next-page"

```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  ListBucketVersionsRequest request = new ListBucketVersionsRequest(bucket);

  // 이전 요청의 "nextMarker" 사용
  request.SetKeyMarker(this.keyMarker);
  request.SetVersionIdMarker(this.versionIdMarker);

  //실행 요청
  ListBucketVersionsResult result = cosXml.ListBucketVersions(request);
  ListBucketVersions info = result.listBucketVersions;

  if (info.isTruncated) {
    // 데이터 잘림. 데이터의 nextMarker 기록.
    this.keyMarker = info.nextKeyMarker;
    this.versionIdMarker = info.nextVersionIdMarker;
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

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjectsVersioning.cs)을 참고하십시오.
