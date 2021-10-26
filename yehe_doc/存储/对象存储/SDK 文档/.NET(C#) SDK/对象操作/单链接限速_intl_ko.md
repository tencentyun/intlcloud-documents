## 소개

본문은 업로드 또는 다운로드 인터페이스 호출 시 링크 속도 제한에 대해 설명합니다.

## 사용 설명

속도 제한 설정 범위는 **819200 - 838860800**이며 기본 단위는 bit/s입니다. 즉 100KB/s - 100MB/s 범위에서 설정할 수 있으며, 이 범위를 넘으면 400 오류가 반환됩니다.

#### 예시 코드1: 업로드 시 단일 링크에 대한 속도 제한

[//]: # (.cssg-snippet-upload-object-traffic-limit)
```cs
TransferConfig transferConfig = new TransferConfig();

// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
string cosPath = "dir/exampleObject"; // 객체 키
string srcPath = @"temp-source-file";//로컬 파일 절대 경로

PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
putObjectRequest.LimitTraffic(8 * 1024 * 1024); // 1MB/s로 제한합니다.

COSXMLUploadTask uploadTask = new COSXMLUploadTask(putObjectRequest);

uploadTask.SetSrcPath(srcPath);

await transferManager.UploadAsync(uploadTask);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs)를 참고하십시오.

#### 예시 코드2: 다운로드 시 단일 링크에 대한 속도 제한

[//]: # (.cssg-snippet-download-object-traffic-limit)
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
request.LimitTraffic(8 * 1024 * 1024); // 1MB/s로 제한합니다.

COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
await transferManager.DownloadAsync(downloadTask);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs)를 참고하십시오.

