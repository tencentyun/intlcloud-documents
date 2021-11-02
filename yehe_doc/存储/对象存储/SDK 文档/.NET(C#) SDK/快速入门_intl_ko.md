## 관련 리소스

- SDK 소스 코드 다운로드는 [XML .NET SDK](https://github.com/tencentyun/qcloud-sdk-dotnet)를 참고하십시오.
- SDK 고속 다운로드 주소: [XML .NET SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-dotnet/latest/qcloud-sdk-dotnet.zip).
- SDK 인터페이스와 매개변수 문서는 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com)를 참고하십시오.
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/dotnet)를 참고하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md)를 참고하십시오.
- SDK FAQ는 [.NET（C#）SDK FAQ](https://intl.cloud.tencent.com/document/product/436/40773)를 참고하십시오.


>? SDK 사용 시 함수 또는 메소드 없음 등 오류가 발생하였을 경우, 먼저 SDK를 최신 버전으로 업데이트한 후 재시도하십시오.
>


## 1단계: SDK 통합

#### 환경 종속

.NET SDK 개발은 .NET Standard 2.0 에 기초합니다.

- Windows: .NET Core 2.0 이상의 버전 또는 .NET Framework 2.0 이상의 버전 설치. 
- Linux/Mac: .NET Core 2.0 이상의 버전 설치.

#### SDK 추가

`Nuget` 통합 방법을 제공합니다. 프로젝트의 `csproj` 파일에 추가할 수 있습니다.

```xml
<PackageReference Include="Tencent.QCloud.Cos.Sdk" Version="5.4.*" />
```

.NET CLI를 사용할 경우, 다음 명령어를 사용하여 설치하십시오.

```sh
dotnet add package Tencent.QCloud.Cos.Sdk
```

타깃 프레임워크 .Net Framework 4.0 및 이전 버전 개발에 사용할 경우 [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases)를 다운로드하고 COSXML-Compatible.dll 파일을 사용하십시오.

Visual Studio 프로젝트에서 **프로젝트**> **참조 추가**> **브라우징**> **COSXML-Compatible.dll**을 선택하여 .NET(C#) SDK를 추가합니다.

>? .NET SDK의 하위 호환 특징은 [하위 호환 가이드](https://cloud.tencent.com/document/product/436/61569)를 참고하십시오.
>


## 2단계: COS 서비스 초기화

COS .NET SDK를 사용한 초기화 클라이언트, 버킷 생성, 버킷 리스트 조회, 객체 업로드, 객체 리스트 조회, 객체 다운로드, 객체 삭제 등의 기본 작업 방법은 아래와 같습니다.


>? 본 문서에 나오는 SecretId, SecretKey, Bucket 등의 이름의 의미 및 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.
>

SDK에서 자주 사용하는 네임스페이스는 아래와 같습니다.

```C#
using COSXML;
using COSXML.Auth;
using COSXML.Model.Object;
using COSXML.Model.Bucket;
using COSXML.CosException;
```

COS 서비스와 관련된 모든 요청을 실행하기 전에 `CosXmlConfig`, `QCloudCredentialProvider`, `CosXmlServer` 3개 객체를 인스턴스화 해야 합니다. 그 중,

- `CosXmlConfig`는 SDK 인터페이스를 제공합니다.
- `QCloudCredentialProvider`는 키 정보 설정 인터페이스를 제공합니다.
- `CosXmlServer`는 각종 COS API 서비스 인터페이스를 제공합니다.

>? 하기 초기화 예시에서 사용한 임시 키의 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.
>

### 1. 초기화 서비스 설정

```cs
//CosXmlConfig 초기화 
string appid = "1250000000";//Tencent Cloud 계정의 계정 식별 APPID 설정
string region = "COS_REGION"; //기본 버킷 리전 설정
CosXmlConfig config = new CosXmlConfig.Builder()
  .IsHttps(true)  //기본 HTTPS 요청 설정
  .SetRegion(region)  //기본 버킷 리전 설정
  .SetDebugLog(true)  //로그 표시
  .Build();  //CosXmlConfig 객체 생성
```

### 2. 액세스 자격 증명

SDK에서 영구 키, 지속적으로 갱신되는 임시 키, 불변의 임시 키 3가지 방법을 제공합니다.

**방법 1：영구 키**

```cs
string secretId = "SECRET_ID"; //"Tencent Cloud API 키 SecretId";
string secretKey = "SECRET_KEY"; //"Tencent Cloud API 키 SecretKey";
long durationSecond = 600;  //매번 서명의 유효 기간을 요청하며, 단위는 초 입니다.
QCloudCredentialProvider cosCredentialProvider = new DefaultQCloudCredentialProvider(
  secretId, secretKey, durationSecond);
```

**방법 2: 지속적으로 갱신되는 임시 키**

임시 키는 일정 시간 후 만료되기 때문에, 만료 후 자동으로 새로운 임시 키를 확보할 수 있는 방법은 다음과 같습니다.

```cs
public class CustomQCloudCredentialProvider : DefaultSessionQCloudCredentialProvider
{

  // 시작부터 키가 없다고 가정하며, 초기 임시 키를 사용하여 초기화할 수 있습니다.
  public CustomQCloudCredentialProvider(): base(null, null, 0L, null) {
    ;
  }

  public override void Refresh()
  {
    //... 먼저 Tencent Cloud를 통해 임시 키를 요청합니다.
    string tmpSecretId = "SECRET_ID"; //"임시 키 SecretId";
    string tmpSecretKey = "SECRET_KEY"; //"임시 키 SecretKey";
    string tmpToken = "COS_TOKEN"; //"임시 키 token";
    long tmpStartTime = 1546860702;//임시 키는 유효한 시작 시간이 있으며, 초 단위까지 정확합니다.
    long tmpExpiredTime = 1546862502;//임시 키는 유효한 종료 시간이 있으며, 초 단위까지 정확합니다.
    // 인터페이스 호출을 통한 키 갱신
    SetQCloudCredential(tmpSecretId, tmpSecretKey, 
      String.Format("{0};{1}", tmpStartTime, tmpExpiredTime), tmpToken);
  }
}

QCloudCredentialProvider cosCredentialProvider = new CustomQCloudCredentialProvider();
```

**방법 3: 불변의 임시 키(권장하지 않음)**

>! 임시 키는 일정 시간 경과 후 만료됩니다. 본 방법은 만료 후에는 요청이 불가하여 사용을 권장하지 않습니다.
>

```cs
string tmpSecretId = "SECRET_ID"; //"임시 키 SecretId";
string tmpSecretKey = "SECRET_KEY"; //"임시 키 SecretKey";
string tmpToken = "COS_TOKEN"; //"임시 키 token";
long tmpExpireTime = 1546862502;//임시 키는 유효 기간이 있으며, 초 단위까지 정확합니다.
QCloudCredentialProvider cosCredentialProvider = new DefaultSessionQCloudCredentialProvider(
  tmpSecretId, tmpSecretKey, tmpExpireTime, tmpToken);
```

### 3. CosXmlService 초기화

`CosXmlConfig`, `QCloudCredentialProvider`를 사용하여 `CosXmlServer` 서비스 클래스를 초기화합니다. 서비스 클래스는 프로그램에서 **싱글톤**으로 사용할 것을 권장합니다.

```cs
CosXml cosXml = new CosXmlServer(config, cosCredentialProvider);
```

## 3단계: COS 서비스 액세스

### 버킷 생성
```cs
try
{
  string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
  PutBucketRequest request = new PutBucketRequest(bucket);
  //실행 요청
  PutBucketResult result = cosXml.PutBucket(request);
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

### 버킷 리스트 조회
```cs
try
{
  GetServiceRequest request = new GetServiceRequest();
  //실행 요청
  GetServiceResult result = cosXml.GetService(request);
  //모든 buckets 획득
  List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
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

### 객체 업로드
```cs
// TransferConfig 초기화
TransferConfig transferConfig = new TransferConfig();

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자, 즉 객체 키
String srcPath = @"temp-source-file";//로컬 파일 절대 경로

// 객체 업로드
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, cosPath);
uploadTask.SetSrcPath(srcPath);

uploadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};

try {
  COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = await 
    transferManager.UploadAsync(uploadTask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

### 객체 리스트 조회

```cs
try
{
  string bucket = "examplebucket-1250000000"; //형식: BucketName-APPID
  GetBucketRequest request = new GetBucketRequest(bucket);
  //실행 요청
  GetBucketResult result = cosXml.GetBucket(request);
  //bucket 관련 정보
  ListBucket info = result.listBucket;
  if (info.isTruncated) {
    // 데이터 잘림, 기록 표시
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

### 객체 다운로드

```cs
// TransferConfig 초기화
TransferConfig transferConfig = new TransferConfig();

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자, 즉 객체 키
string localDir = System.IO.Path.GetTempPath();//로컬 폴더
string localFileName = "my-local-temp-file"; //로컬 저장 파일 이름 지정

// 객체 다운로드
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
  localDir, localFileName);

downloadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};

try {
  COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = await 
    transferManager.DownloadAsync(downloadTask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

### 객체 삭제

```cs
try
{
  String bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
  string key = "exampleobject"; //객체 키
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  //실행 요청
  DeleteObjectResult result = cosXml.DeleteObject(request);
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
