## 소개

본 문서는 객체의 다운로드 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름   | 작업 설명           |
| ------------------------------------------------------------ | -------- | ------------------ |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬에 객체 다운로드        |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 고급 인터페이스(권장)

### 객체 다운로드(중단된 지점부터 이어서 전송)

고급 인터페이스는 다운로드 요청 일시 중지, 복구, 취소를 지원하며, 중단된 지점부터 다운로드 기능을 제공합니다.

>?.NET Framework 4.0 및 이전 버전 사용자의 경우 고급 인터페이스를 일시적으로 사용할 수 없습니다. 자세한 내용은 [하위 호환 가이드](https://intl.cloud.tencent.com/document/product/436/42378)를 참고하십시오.
> 

#### 예시 코드1: 객체 다운로드

[//]: #	".cssg-snippet-transfer-download-object"

```cs
// TransferConfig 초기화
TransferConfig transferConfig = new TransferConfig();

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs)를 참고하십시오.
>

#### 예시 코드 2: 다운로드 재개 설정

[//]: #	".cssg-snippet-transfer-download-resumable"

```cs
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
 //중단점부터 다운로드 재개 활성화, 로컬로 다운로드되지 않은 파일이 있을 경우 끝까지 추가 다운로드
 // 로컬 파일에 다운로드에 부적합한 콘텐츠가 존재하여 다운로드에 실패할 수 있습니다. 파일을 삭제하고 다시 시도해 보십시오.
 downloadTask.SetResumableDownload(true);
 try {
   COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = await 
   transferManager.DownloadAsync(downloadTask);
   Console.WriteLine(result.GetResultInfo());
   string eTag = result.eTag;
 } catch (Exception e) {
   Console.WriteLine("CosException: " + e);
 }
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs)를 참고하십시오.
>

#### 예시 코드3: 일괄 다운로드

[//]: #	".cssg-snippet-transfer-batch-download-objects"

```cs
TransferConfig transferConfig = new TransferConfig();

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
string localDir = System.IO.Path.GetTempPath();//로컬 폴더

for (int i = 0; i < 5; i++) {
  // 객체 다운로드
  string cosPath = "exampleobject" + i; //버킷 내 객체 위치 식별자. 즉, 객체 키.
  string localFileName = "my-local-temp-file"; //로컬 저장 파일 이름 지정
  COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
    localDir, localFileName);
  await transferManager.DownloadAsync(downloadTask);
}
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs)를 참고하십시오.
>

## 간단한 작업

### 객체 다운로드

#### 기능 설명

Object(파일/객체)를 로컬에 다운로드합니다(GET Object).

#### 예시 코드

[//]: #	".cssg-snippet-get-object"

```cs
try
{
  String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
  string key = "exampleobject"; //객체 키
  string localDir = System.IO.Path.GetTempPath();//로컬 폴더
  string localFileName = "my-local-temp-file"; //로컬 저장 파일 이름 지정
  GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
  //진행율 콜백 설정
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  //실행 요청
  GetObjectResult result = cosXml.GetObject(request);
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs)를 참고하십시오.
>
