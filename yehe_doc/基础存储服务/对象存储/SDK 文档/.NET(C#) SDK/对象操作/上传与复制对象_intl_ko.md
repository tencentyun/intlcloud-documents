## 소개

본 문서는 객체의 업로드, 복사 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


**간단한 작업**

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 객체 간편 업로드       | 하나의 객체를 버킷에 업로드     |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | 폼을 사용한 객체 업로드   | 폼을 사용한 객체 업로드 요청                     |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정(객체 속성 수정)   | 파일을 타깃 경로에 복사                       |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | 객체 추가 업로드 | 멀티파트에 추가하는 방식으로 객체 업로드 |

**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 업로드 작업 초기화     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 멀티파트 업로드       | 객체 멀티파트 업로드                        |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지 | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 파트 삭제 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 고급 인터페이스(권장)

### 객체 업로드

#### 기능 설명


고급 인터페이스는 간편 업로드, 멀티파트 업로드 인터페이스를 캡슐화합니다. 파일 크기에 따라 스마트하게 업로드 방식을 선택하며, 업로드 재개 기능을 지원합니다.

>?
> - 파일 크기가 멀티파트 임계값보다 작으면 간편 업로드를 사용하고, 파일 크기가 임계값보다 크면 멀티파트 업로드를 사용합니다. 임계값은 사용자가 설정할 수 있으며 기본값은 5MB입니다.
> - 멀티파트 크기는 사용자가 설정할 수 있으며 기본값은 1MB입니다.
> - .NET Framework 4.0 및 이전 버전 사용자의 경우 고급 인터페이스를 일시적으로 사용할 수 없습니다. 자세한 내용은 [하위 호환 가이드](https://intl.cloud.tencent.com/document/product/436/42378)를 참고하십시오.
> 

#### 예시 코드1: 고급 인터페이스 로컬 파일 업로드

[//]: # (.cssg-snippet-transfer-upload-file)
```cs
using COSXML.Model.Object;
using COSXML.Auth;
using COSXML.Transfer;
using System;
using COSXML;

namespace COSSnippet
{
    public class TransferUploadObjectModel {

      private CosXml cosXml;

      TransferUploadObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // 기본 리전을 설정합니다. COS 리전 약칭은 https://cloud.tencent.com/document/product/436/6224를 참고하십시오.
          .Build();
        
        string secretId = "SECRET_ID";   // Tencent Cloud API 키 SecretId. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        string secretKey = "SECRET_KEY"; // Tencent Cloud API 키 SecretKey. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        long durationSecond = 600;          //매회 서명 요청의 유효 기간. 단위: 초.
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// 고급 인터페이스 파일 업로드
      public async void TransferUploadFile()
      {
        // TransferConfig 초기화
        TransferConfig transferConfig = new TransferConfig();
        
        // TransferManager 초기화
        TransferManager transferManager = new TransferManager(cosXml, transferConfig);
        // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
        String bucket = "examplebucket-1250000000"; 
        String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
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

      }

      static void Main(string[] args)
      {
        TransferUploadObjectModel m = new TransferUploadObjectModel();
        /// 고급 인터페이스 객체 업로드
        m.TransferUploadFile();
        // .cssg-methods-pragma
      }
    }
}
```

>?
> - 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs)를 참고하십시오.
> - 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 [사전 서명된 링크 생성](https://intl.cloud.tencent.com/document/product/436/38068)을 참고하십시오. 파일의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 시간이 있습니다.
>

#### 예시 코드2: 바이너리 데이터 업로드

[//]: # (.cssg-snippet-transfer-upload-bytes)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string cosPath = "exampleObject"; // 객체 키
  byte[] data = new byte[1024]; // 바이너리 데이터
  PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
  // 요청 발송
  cosXml.PutObject(putObjectRequest);
  // 객체의 eTag
  string eTag = result.eTag;
  // 객체의 crc64ecma 검사 값
  string crc64ecma = result.crc64ecma;
  // 요청 결과 출력
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

>?
> - 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs)를 참고하십시오.
> - 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 [사전 서명된 링크 생성](https://intl.cloud.tencent.com/document/product/436/38068)을 참고하십시오. 파일의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 시간이 있습니다.
>

#### 예시 코드3: 파일 스트림에서 업로드

[//]: # (.cssg-snippet-transfer-upload-bytes)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  string srcPath = @"temp-source-file";//로컬 파일 절대 경로
  // 읽기 전용 파일 스트림 객체를 엽니다.
  FileStream fileStream = new FileStream(srcPath, FileMode.Open, FileAccess.Read);
  // 업로드 요청을 어셈블합니다. 여기서 offset sendLength는 옵션 매개변수입니다.
  long offset = 0L;
  long sendLength = fileStream.Length;
  PutObjectRequest request = new PutObjectRequest(bucket, key, fileStream, offset, sendLength);
  //진행률 콜백 설정
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //실행 요청
  PutObjectResult result = cosXml.PutObject(request);
  //파일 스트림 비활성화
  fileStream.Close();
  //객체의 eTag
  string eTag = result.eTag;
  //객체의 crc64ecma 검사 값
  string crc64ecma = result.crc64ecma;
  //요청 결과 출력
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
>?
> - 파일 스트림 업로드 기능은 버전 5.4.24부터 지원됩니다. 새 버전의 SDK를 다운로드하려면 [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases)로 이동하거나 [시작하기](https://intl.cloud.tencent.com/document/product/436/30594)를 참고하십시오.
> - Changelog 버전을 보려면 [GitHub](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md)으로 이동하십시오.
> - 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/blob/master/dotnet/dist/PutObject.cs)를 참고하십시오.
> - 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 [사전 서명된 링크 생성](https://intl.cloud.tencent.com/document/product/436/38068)을 참고하십시오. 파일의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 시간이 있습니다.
>

#### 예시 코드4: 업로드 일시 중지, 재개 및 취소

업로드 작업은 다음 방법으로 일시 정지할 수 있습니다.

[//]: # (.cssg-snippet-transfer-upload-pause)
```cs
uploadTask.Pause();
```

일시 정지 후 다음 방법으로 업로드를 재개할 수 있습니다.

[//]: # (.cssg-snippet-transfer-upload-resume)
```cs
uploadTask.Resume();
```

다음 방법으로 업로드를 취소할 수 있습니다.

[//]: # (.cssg-snippet-transfer-upload-cancel)
```cs
uploadTask.Cancel();
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs)를 참고하십시오.
>

#### 예시 코드5: 일괄 업로드

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```cs
TransferConfig transferConfig = new TransferConfig();

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);
// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";

for (int i = 0; i < 5; i++) {
  // 객체 업로드
  string cosPath = "exampleobject" + i; //버킷 내 객체 위치 식별자. 즉, 객체 키
  string srcPath = @"temp-source-file";//로컬 파일 절대 경로
  COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, cosPath); 
  uploadTask.SetSrcPath(srcPath);
  await transferManager.UploadAsync(uploadTask);
}
```

#### 예시 코드6: 디렉터리 생성

[//]: # (.cssg-snippet-create-directory)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string cosPath = "dir/"; // 객체 키
  PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, new byte[0]);
  
  cosXml.PutObject(putObjectRequest);
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

>?
> - 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs)를 참고하십시오.
> - 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 [사전 서명된 링크 생성](https://intl.cloud.tencent.com/document/product/436/38068)을 참고하십시오. 파일의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 시간이 있습니다.
> 

### 객체 복사

#### 기능 설명

고급 인터페이스는 간편 복사 및 멀티파트 복사 인터페이스의 비동기화 요청을 캡슐화합니다. 복사 요청 일시 정지, 복구 및 취소를 지원합니다.

>?
> - 객체 크기가 멀티파트 임계값보다 작으면 간편 복사를 사용하고, 객체 크기가 임계값보다 크면 멀티파트 복사를 사용합니다. 임계값은 사용자가 설정할 수 있으며 기본값은 5MB입니다.
> - 멀티파트 크기는 사용자가 설정할 수 있으며 기본값은 2MB입니다.
> 

#### 예시 코드

[//]: # (.cssg-snippet-transfer-copy-object)
```cs
// TransferConfig 초기화
TransferConfig transferConfig = new TransferConfig();

//멀티파트 복사 임계값은 수동으로 설정하며 기본값은 5MB입니다. 임계값보다 작은 객체는 간편 복사를 사용하고 임계값보다 큰 객체는 멀티파트 복사를 사용합니다.
transferConfig.DivisionForCopy = 5242880;
//고급 인터페이스의 자동 멀티파트 크기는 수동으로 설정하며 기본값은 2MB입니다.
transferConfig.SliceSizeForCopy = 2097152;

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

string sourceAppid = "1250000000"; //계정 appid
string sourceBucket = "sourcebucket-1250000000"; //"원본 객체 소재 버킷
string sourceRegion = "COS_REGION"; //원본 객체의 버킷 소재 리전
string sourceKey = "sourceObject"; //원본 객체 키
//원본 객체 속성 구성
CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

string bucket = "examplebucket-1250000000"; //타깃 버킷. 포맷: BucketName-APPID
string key = "exampleobject"; //타깃 객체의 객체 키

COSXMLCopyTask copytask = new COSXMLCopyTask(bucket, key, copySource);

try {
  COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = await 
    transferManager.CopyAsync(copytask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferCopyObject.cs)를 참고하십시오.
>

## 간단한 작업

### 객체 간편 업로드

#### 기능 설명

PUT Object 인터페이스는 객체를 지정된 버킷에 업로드할 수 있습니다. 이 작업은 요청자가 버킷에 대한 WRITE 권한을 가지고 있어야 합니다. 최대 5GB 이하인 객체의 업로드를 지원합니다. 5GB 이상의 객체는 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) 혹은 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) 업로드를 사용하십시오.

>!
> - Key(파일명)는 `/`로 끝날 수 없습니다. 그렇지 않을 경우 폴더로 인식될 수 있습니다.
> - 루트 계정(동일한 APPID)당 버킷의 ACL 규칙 수량은 최대 1000개이며, 객체 ACL 규칙 수량은 제한이 없습니다. 객체 ACL 제어가 필요하지 않을 경우 업로드 시 설정하지 마십시오. 기본적으로 버킷 권한이 상속됩니다.
> 

#### 예시 코드

[//]: # (.cssg-snippet-put-object)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  string srcPath = @"temp-source-file";//로컬 파일 절대 경로

  PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
  //진행률 콜백 설정
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //실행 요청
  PutObjectResult result = cosXml.PutObject(request);
  //객체의 eTag
  string eTag = result.eTag;
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

>?
> - 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PutObject.cs)를 참고하십시오.
> - 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 [사전 서명된 링크 생성](https://intl.cloud.tencent.com/document/product/436/38068)을 참고하십시오. 파일의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 시간이 있습니다.
> 

### 입력 폼 객체 업로드

#### 기능 설명

폼을 사용해 객체 업로드를 요청합니다.

#### 예시 코드

[//]: # (.cssg-snippet-post-object)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키.
  string srcPath = @"temp-source-file";//로컬 파일 절대 경로
  PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
  //진행률 콜백 설정
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //실행 요청
  PostObjectResult result = cosXml.PostObject(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PostObject.cs)를 참고하십시오.
>

### 객체 복사(속성 수정)

#### 기능 설명

타깃 경로에 파일을 복사합니다(PUT Object-Copy).
객체 인터페이스 복사. 복사 요청에서 객체 속성 및 메타데이터 수정을 설정할 수 있으며 원위치 복사가 지원됩니다. 즉 객체 메타데이터의 원위치 수정 기능을 지원할 수 있습니다.


#### 예시 코드1: 객체 복사 시 객체 속성 유지

[//]: # (.cssg-snippet-copy-object)
```cs
try
{
  string sourceAppid = "1250000000"; //계정 appid
  string sourceBucket = "sourcebucket-1250000000"; //"원본 객체 소재 버킷
  string sourceRegion = "COS_REGION"; //원본 객체의 버킷 소재 리전
  string sourceKey = "sourceObject"; //원본 객체 키
  //원본 객체 속성 구성
  CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  //복사 소스 설정
  request.SetCopySource(copySource);
  //복사 또는 업데이트 여부를 설정하며 여기에서 복사가 사용됩니다.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Copy);
  //실행 요청
  CopyObjectResult result = cosXml.CopyObject(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/CopyObject.cs)를 참고하십시오.
>

#### 예시 코드2: 객체 스토리지 유형 수정

>?
> - 표준 스토리지는 표준IA 스토리지, 인텔리전트 티어링, 아카이브 및 딥 아카이브 등으로 수정할 수 있습니다.
> - 아카이브 또는 딥 아카이브 객체를 다른 스토리지 유형으로 수정하려면 먼저 [PostRestore](https://intl.cloud.tencent.com/document/product/436/38066)를 사용하여 아카이브 또는 딥 아카이브 객체를 워밍업해야만 이 인터페이스를 사용하여 스토리지 유형 수정을 요청할 수 있습니다.
> - 스토리지 유형에 대한 더 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오.
> 

[//]: # (.cssg-snippet-modify-object-storage-class)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  string appId = "1250000000"; //계정 appid
  string region = "COS_REGION"; //원본 객체 버킷 소재 리전
  //객체 속성 생성
  CopySourceStruct copySource = new CopySourceStruct(appId, bucket, 
    region, key);

  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  //복사 소스 설정
  request.SetCopySource(copySource);
  //복사 또는 업데이트 여부를 설정하며 여기에서 복사가 사용됩니다.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // 아카이브로 수정
  request.SetCosStorageClass("ARCHIVE");
  //실행 요청
  CopyObjectResult result = cosXml.CopyObject(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ModifyObjectProperty.cs)를 참고하십시오.

#### 예시 코드3: 객체 복사 시 객체 속성 변경

[//]: # (.cssg-snippet-copy-object-replaced)
```cs
try
{
  string sourceAppid = "1250000000"; //계정 appid
  string sourceBucket = "sourcebucket-1250000000"; //"원본 객체 소재 버킷
  string sourceRegion = "COS_REGION"; //원본 객체의 버킷 소재 리전
  string sourceKey = "sourceObject"; //원본 객체 키
  //원본 객체 속성 구성
  CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  //복사 소스 설정
  request.SetCopySource(copySource);
  //복사 또는 업데이트 여부를 설정하며 여기에서 복사가 사용됩니다.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // 메타데이터 교체
  request.SetRequestHeader("Content-Disposition", "attachment; filename=example.jpg");
  //실행 요청
  CopyObjectResult result = cosXml.CopyObject(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/CopyObject.cs)를 참고하십시오.
>

#### 예시 코드4: 객체 메타데이터 수정

[//]: # (.cssg-snippet-modify-object-metadata)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  string appId = "1250000000"; //계정 appid
  string region = "COS_REGION"; //원본 객체 버킷 소재 리전
  //객체 속성 생성
  CopySourceStruct copySource = new CopySourceStruct(appId, bucket, 
    region, key);

  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  //복사 소스 설정
  request.SetCopySource(copySource);
  //복사 또는 업데이트 여부를 설정하며 여기에서 복사가 사용됩니다.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // 메타데이터 교체
  request.SetRequestHeader("Content-Disposition", "attachment; filename=example.jpg");
  request.SetRequestHeader("Content-Type", "image/png");
  //실행 요청
  CopyObjectResult result = cosXml.CopyObject(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ModifyObjectProperty.cs)를 참고하십시오.
>


### 객체 추가 업로드

#### 기능 설명

멀티파트 추가 방식으로 객체를 업로드합니다.

>? 이 기능은 버전 5.4.22부터 지원되며 Changelog 버전을 보려면 [GitHub](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md)를 참고하십시오.
>

#### 예시 코드

[//]: # (.cssg-snippet-append-object)
```cs
try
{
    // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
    string bucket = "examplebucket-1250000000";
    string key = "exampleobject"; //객체 키
    string srcPath = @"temp-source-file";//로컬 파일 절대 경로

    //최초 append 업로드는, 추가 위치를 0으로 하고, appendable 객체를 생성합니다.
    long next_append_position = 0;
    AppendObjectRequest request = new AppendObjectRequest(bucket, key, srcPath, next_append_position);
    //진행률 콜백 설정
    request.SetCosProgressCallback(delegate (long completed, long total)
    {
        Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
    });
    AppendObjectResult result = cosXml.AppendObject(request);
    //다음 추가 위치 가져오기
    next_append_position = result.nextAppendPosition;
    Console.WriteLine(result.GetResultInfo());

    //추가 작업 실행. 이전에 획득한 객체의 끝에 전달
    request = new AppendObjectRequest(bucket, key, srcPath, next_append_position);
    request.SetCosProgressCallback(delegate (long completed, long total)
    {
        Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
    });
    result = cosXml.AppendObject(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/AppendObject.cs)를 참고하십시오.

## 멀티파트 작업

여기서는 멀티파트 업로드 프로세스를 설명합니다.

#### 멀티파트 업로드와 복사 프로세스

1. 멀티파트 업로드를 초기화(Initiate Multipart Upload)하고 UploadId를 획득합니다.
2. UploadId를 사용해 멀티파트를 업로드(Upload Part)하거나 멀티파트를 복사(Upload Part Copy)합니다.
3. 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 멀티파트 업로드 재개와 복사 프로세스

1. UploadId를 기록하지 않은 경우 멀티파트 업로드 작업을 조회(List Multipart Uploads)하여 해당 파일의 UploadId를 획득합니다.
2. UploadId를 사용해 업로드된 멀티파트를 나열합니다(List Parts).
3. UploadId를 사용해 남은 멀티파트를 업로드(Upload Part)하거나 남은 멀티파트를 복사(Upload Part Copy)합니다.
4. 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 멀티파트 업로드 및 복사 중지 프로세스

1. UploadId를 기록하지 않은 경우 멀티파트 업로드 작업을 조회(List Multipart Uploads)하여 해당 파일의 UploadId를 획득합니다.
2. 멀티파트 업로드를 중지하고 업로드된 멀티파트를 삭제합니다(Abort Multipart Upload).

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드를 조회합니다(List Multipart Uploads).

#### 예시 코드

[//]: # (.cssg-snippet-list-multi-upload)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
  //실행 요청
  ListMultiUploadsResult result = cosXml.ListMultiUploads(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs)를 참고하십시오.
>

### 멀티파트 업로드 초기화

#### 기능 설명

Multipart Upload 업로드 작업을 초기화하고 해당하는 uploadId를 가져옵니다(Initiate Multipart Upload).

#### 예시 코드

[//]: # (.cssg-snippet-init-multi-upload)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
  //실행 요청
  InitMultipartUploadResult result = cosXml.InitMultipartUpload(request);
  //요청 완료
  this.uploadId = result.initMultipartUpload.uploadId; //후속 멀티파트 업로드에 사용할 uploadId
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs)를 참고하십시오.
>

### 멀티파트 업로드

#### 기능 설명

객체를 멀티파트 업로드합니다(Upload Part).

#### 예시 코드

[//]: # (.cssg-snippet-upload-part)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  string uploadId = "exampleUploadId"; //멀티파트 업로드가 초기화될 때 반환된 uploadId
  int partNumber = 1; //1부터 증가하는 멀티파트 번호
  string srcPath = @"temp-source-file";//로컬 파일 절대 경로
  UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, 
    uploadId, srcPath, 0, -1);
  //진행률 콜백 설정
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //실행 요청
  UploadPartResult result = cosXml.UploadPart(request);
  //요청 완료
  //반환된 멀티파트의 eTag 가져오기. 후속 CompleteMultiUploads에 사용
  this.eTag = result.eTag;
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs)를 참고하십시오.
>

### 멀티파트 복사

#### 기능 설명

다른 객체를 한 파트로 복사합니다(Upload Part-Copy).

#### 예시 코드

[//]: # (.cssg-snippet-upload-part-copy)
```cs
try
{
  string sourceAppid = "1250000000"; //계정 appid
  string sourceBucket = "sourcebucket-1250000000"; //"원본 객체 소재 버킷
  string sourceRegion = "COS_REGION"; //원본 객체의 버킷 소재 리전
  string sourceKey = "sourceObject"; //원본 객체 키
  //원본 객체 속성 구성
  COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, 
    sourceBucket, sourceRegion, sourceKey);

  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  string uploadId = this.uploadId; //멀티파트 업로드가 초기화될 때 반환된 uploadId
  int partNumber = 1; //1부터 증가하는 멀티파트 번호
  UploadPartCopyRequest request = new UploadPartCopyRequest(bucket, key 
    partNumber, uploadId);
  //복사 소스 설정
  request.SetCopySource(copySource);
  //복사할 멀티파트 범위 설정(예: 0 ~ 1 M)
  request.SetCopyRange(0, 1024 * 1024);
  //실행 요청
  UploadPartCopyResult result = cosXml.PartCopy(request);
  //요청 완료
  //반환된 멀티파트의 eTag 가져오기. 후속 CompleteMultiUploads에 사용
  this.eTag = result.copyPart.eTag;
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsCopyObject.cs)를 참고하십시오.
>

### 업로드된 멀티파트 조회

#### 기능 설명

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다(List Parts).

#### 예시 코드

[//]: # (.cssg-snippet-list-parts)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키.
  string uploadId = "exampleUploadId"; //멀티파트 업로드가 초기화될 때 반환된 uploadId
  ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
  //실행 요청
  ListPartsResult result = cosXml.ListParts(request);
  //요청 완료
  //업로드된 멀티파트를 나열합니다.
  List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs)를 참고하십시오.
>

### 멀티파트 업로드 완료

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 예시 코드
[//]: # (.cssg-snippet-complete-multi-upload)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  string uploadId = "exampleUploadId"; //멀티파트 업로드가 초기화될 때 반환된 uploadId
  CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, 
    key, uploadId);
  //업로드된 parts를 partNumber에 따라 오름차순으로 설정
  request.SetPartNumberAndETag(1, this.eTag);
  //실행 요청
  CompleteMultipartUploadResult result = cosXml.CompleteMultiUpload(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs)를 참고하십시오.
>

### 멀티파트 업로드 중지

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다(Abort Multipart Upload).

#### 예시 코드

[//]: # (.cssg-snippet-abort-multi-upload)
```cs
try
{
  // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //객체 키
  string uploadId = "exampleUploadId"; //멀티파트 업로드가 초기화될 때 반환된 uploadId
  AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
  //실행 요청
  AbortMultipartUploadResult result = cosXml.AbortMultiUpload(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/AbortMultiPartsUpload.cs)를 참고하십시오.
>


