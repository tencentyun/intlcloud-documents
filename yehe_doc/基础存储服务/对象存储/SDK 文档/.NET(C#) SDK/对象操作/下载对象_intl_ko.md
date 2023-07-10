## 소개

본 문서는 객체의 다운로드 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름   | 작업 설명           |
| ------------------------------------------------------------ | -------- | ------------------ |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드 | 로컬에 객체 다운로드 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 고급 인터페이스(권장)

### 객체 다운로드(체크포인트 재시작)

고급 인터페이스는 다운로드 요청 일시 중지, 복구, 취소를 지원하며, 다운로드 체크포인트 재시작 기능을 제공합니다.

>? .NET Framework 4.0 및 이전 버전 사용자의 경우 고급 인터페이스를 일시적으로 사용할 수 없습니다. 자세한 내용은 [하위 호환 가이드](https://intl.cloud.tencent.com/document/product/436/42378)를 참고하십시오.
> 

#### 예시 코드1: 객체 다운로드

[//]: #	".cssg-snippet-transfer-download-object"

```cs
using COSXML.Model.Object;
using COSXML.Auth;
using COSXML.Transfer;
using System;
using COSXML;

namespace COSSnippet
{
    public class TransferDownloadObjectModel {

      private CosXml cosXml;

      TransferDownloadObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // 기본 리전을 설정합니다. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참고하십시오.
          .Build();
        
        string secretId = "SECRET_ID";   // Tencent Cloud API 키 SecretId, API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        string secretKey = "SECRET_KEY"; // Tencent Cloud API 키 SecretKey, API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        long durationSecond = 600;          //매회 서명 요청의 유효 기간. 단위: 초.
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// 고급 인터페이스 객체 다운로드
      public async void TransferDownloadObject()
      {
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
      }


      static void Main(string[] args)
      {
        TransferDownloadObjectModel m = new TransferDownloadObjectModel();

        /// 고급 인터페이스 객체 다운로드
        m.TransferDownloadObject();
      }
    }
}
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs)를 참고하십시오.
>

#### 예시 코드2: 다운로드 체크포인트 재시작 설정

[//]: #	".cssg-snippet-transfer-download-resumable"

```cs
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
 //다운로드 체크포인트 재시작 활성화, 로컬로 다운로드되지 않은 파일이 있을 경우 끝까지 추가 다운로드
 //로컬 파일에 다운로드에 부적합한 콘텐츠가 존재하여 다운로드에 실패할 수 있습니다. 파일을 삭제하고 다시 시도해 보십시오.
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

// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";
string localDir = System.IO.Path.GetTempPath();//로컬 폴더

for (int i = 0; i < 5; i++) {
  // 객체 다운로드
  string cosPath = "exampleobject" + i; //버킷 내 객체 위치 식별자. 즉, 객체 키
  string localFileName = "my-local-temp-file"; //로컬 저장 파일 이름 지정
  COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
    localDir, localFileName);
  await transferManager.DownloadAsync(downloadTask);
}
```
>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs)를 참고하십시오.
>

#### 예시 코드4: 단일 링크 속도 제한 다운로드
[//]: #	".cssg-snippet-transfer-download-objects-with-speed-limit"
```cs
TransferConfig transferConfig = new TransferConfig();

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
string localDir = System.IO.Path.GetTempPath();//로컬 폴더
string localFileName = "my-local-temp-file"; //로컬 저장 파일 이름 지정
        
GetObjectRequest request = new GetObjectRequest(bucket, 
        cosPath, localDir, localFileName);
request.LimitTraffic(8 * 1000 * 1024); // 제한은 1MB/s입니다.

COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
await transferManager.DownloadAsync(downloadTask);
```


>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs)를 참고하십시오.
>

## 간단한 작업

### 객체 다운로드

#### 기능 설명

Object(파일/객체)를 로컬에 다운로드합니다(GET Object).

#### 예시 코드1: 단일 객체 간편 다운로드

[//]: #	".cssg-snippet-get-object"

```cs
using COSXML.Model.Object;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class GetObjectModel {

      private CosXml cosXml;

      GetObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // 기본 리전을 설정합니다. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참고하십시오. 
          .Build();
        
        string secretId = "SECRET_ID";   // Tencent Cloud API 키 SecretId. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        string secretKey = "SECRET_KEY"; // Tencent Cloud API 키 SecretKey. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        long durationSecond = 600;          //매회 서명 요청의 유효 기간. 단위: 초.
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// 객체 다운로드
      public void GetObject()
      {
        //.cssg-snippet-body-start:[get-object]
        try
        {
          // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; //객체 키
          string localDir = System.IO.Path.GetTempPath();//로컬 폴더
          string localFileName = "my-local-temp-file"; //로컬 저장 파일 이름 지정
          GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
          //진행률 콜백 설정
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
      }

      static void Main(string[] args)
      {
        GetObjectModel m = new GetObjectModel();
        /// 객체 다운로드
        m.GetObject();
      }
    }
}

```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs)를 참고하십시오.
>

#### 예시 코드2: 객체를 메모리에 다운로드

[//]: #	".cssg-snippet-get-object"

```cs
using COSXML.Model.Object;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class GetObjectModel {

      private CosXml cosXml;

      GetObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // 기본 리전을 설정합니다. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참고하십시오. 
          .Build();
        
        string secretId = "SECRET_ID";   // Tencent Cloud API 키 SecretId. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        string secretKey = "SECRET_KEY"; // Tencent Cloud API 키 SecretKey. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        long durationSecond = 600;          //매회 서명 요청의 유효 기간. 단위: 초.
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// 반환된 bytes 데이터 다운로드
      public void downloadToMem() {
        try
        {
          // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; //객체 키
        
          GetObjectBytesRequest request = new GetObjectBytesRequest(bucket, key);
          //진행률 콜백 설정
          request.SetCosProgressCallback(delegate (long completed, long total)
          {
            Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
          });
          //실행 요청
          GetObjectBytesResult result = cosXml.GetObject(request);
          //콘텐츠를 byte 배열로 가져오기
          byte[] content = result.content;
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
      }

      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        GetObjectModel m = new GetObjectModel();

        /// 객체를 메모리에 다운로드
        m.downloadToMem();
        // .cssg-methods-pragma
      }
    }
}

```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs)를 참고하십시오.
>
