## 소개

본 문서는 버킷, 객체의 액세스 제어에 대한 리스트(ACL) 관련 API 개요 및 SDK 샘플 코드를 제공합니다.

**버킷 ACL**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 버킷 ACL 설정 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 설정 |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) |버킷 ACL 조회 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 조회 |

**객체 ACL**

| API                                                          | 작업명       | 작업 설명                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정 | 버킷의 특정 객체의 액세스 제어 리스트 설정 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | 객체 액세스 제어 리스트 조회             |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.


## 버킷 ACL

### 버킷 ACL 설정

#### 기능 설명

지정 버킷의 액세스 권한 리스트(ACL)를 설정합니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-bucket-acl)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  PutBucketACLRequest request = new PutBucketACLRequest(bucket);
  //개인 읽기/쓰기 권한 설정
  request.SetCosACL(CosACL.Private);
  //1131975903 계정에 읽기 권한 부여
  COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
  readAccount.AddGrantAccount("1131975903", "1131975903");
  request.SetXCosGrantRead(readAccount);
  //실행 요청
  PutBucketACLResult result = cosXml.PutBucketACL(request);
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketACL.cs)를 참고하십시오.

### 버킷 ACL 조회

#### 기능 설명

지정 버킷의 액세스 권한 리스트(ACL)를 조회합니다.

#### 예시 코드

[//]: # (.cssg-snippet-get-bucket-acl)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  GetBucketACLRequest request = new GetBucketACLRequest(bucket);
  //실행 요청
  GetBucketACLResult result = cosXml.GetBucketACL(request);
  //버킷의 ACL 정보
  AccessControlPolicy acl = result.accessControlPolicy;
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketACL.cs)를 참고하십시오.

## 객체 ACL

### 객체 ACL 설정

#### 기능 설명

버킷의 한 객체의 액세스 제어 리스트(ACL)를 설정합니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-object-acl)
```cs
// 버킷 ACL은 최대 1000개이므로, ACL이 최댓값에 도달하는 것을 방지하기 위해,
// 필요하지 않은 경우 객체에 대해 별도로 ACL을 설정하지 않는 것을 권장합니다(객체는 기본적으로 bucket 권한을 상속함).
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
  //개인 읽기/쓰기 권한 설정 
  request.SetCosACL(CosACL.Private);
  //1131975903 계정에 읽기 권한 부여 
  COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
  readAccount.AddGrantAccount("1131975903", "1131975903");
  request.SetXCosGrantRead(readAccount);
  //실행 요청
  PutObjectACLResult result = cosXml.PutObjectACL(request);
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectACL.cs)를 참고하십시오.

### 객체 ACL 조회

#### 기능 설명

객체의 액세스 제어 리스트를 조회합니다.

#### 예시 코드

[//]: # (.cssg-snippet-get-object-acl)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
  //실행 요청
  GetObjectACLResult result = cosXml.GetObjectACL(request);
  //객체의 ACL 정보
  AccessControlPolicy acl = result.accessControlPolicy;
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
>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectACL.cs)를 참고하십시오.



