## 소개

이 문서는 업로드 및 다운로드 인터페이스 호출 시 링크 속도 제한에 대한 정보를 제공합니다.

## 사용 설명

속도 제한값 설정 범위: **819200 - 838860800**, 기본 단위: bit/s, 즉 100KB/s - 100MB/s입니다. 이 범위를 초과하면 400 오류가 반환됩니다.

#### 예시 코드1: 업로드 시 단일 링크 속도 제한

[//]: # (.cssg-snippet-upload-object-traffic-limit)
```cs
TransferConfig transferConfig = new TransferConfig();

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";
string cosPath = "dir/exampleObject"; // 객체 키
string srcPath = @"temp-source-file";//로컬 파일 절대 경로

PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
putObjectRequest.LimitTraffic(8 * 1024 * 1024); // 1MB/s로 제한

COSXMLUploadTask uploadTask = new COSXMLUploadTask(putObjectRequest);

uploadTask.SetSrcPath(srcPath);

await transferManager.UploadAsync(uploadTask);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs)를 참고하십시오.

#### 예시 코드2: 다운로드 시 단일 링크 속도 제한

[//]: # (.cssg-snippet-download-object-traffic-limit)
```cs
TransferConfig transferConfig = new TransferConfig();

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

// 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
string bucket = "examplebucket-1250000000";
string cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
string localDir = System.IO.Path.GetTempPath();//로컬 폴더
string localFileName = "my-local-temp-file"; //로컬 저장 파일 이름 지정

GetObjectRequest request = new GetObjectRequest(bucket, 
        cosPath, localDir, localFileName);
request.LimitTraffic(8 * 1024 * 1024); // 1MB/s로 제한

COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
await transferManager.DownloadAsync(downloadTask);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs)를 참고하십시오.

