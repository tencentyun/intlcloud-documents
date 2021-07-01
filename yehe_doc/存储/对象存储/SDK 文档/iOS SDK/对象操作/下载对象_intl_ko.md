## 소개

본 문서는 객체의 다운로드 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬에 객체 다운로드        |

## SDK API 참조

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참조하십시오.

## 고급 인터페이스(권장)

### 객체 다운로드

고급 인터페이스는 다운로드 요청 일시 중지, 복구, 취소를 지원하며, 중단된 지점부터 다운로드 기능을 제공합니다.

#### 예시 코드1: 객체 다운로드
**Objective-C**

[//]: # (.cssg-snippet-transfer-download-object)
```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];

// BucketName-APPID 포맷의 버킷 이름
request.bucket = @"examplebucket-1250000000";

// 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
request.object = @"exampleobject";

//다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

// 로컬에 다운로드한 파일 크기. 처음부터 다운로드하는 경우 설정하지 않습니다.
request.localCacheDownloadOffset = 100;

// 다운로드 결과 수신
[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject에 모든 http 응답 헤더 포함
    NSDictionary* info = (NSDictionary *) outputObject;
}];

// 다운로드 진행률 수신
[request setDownProcessBlock:^(int64_t bytesDownload,
                               int64_t totalBytesDownload,
                               int64_t totalBytesExpectedToDownload) {
    
    // bytesDownload                   증가 바이트 수
    // totalBytesDownload              이번에 다운로드한 총 바이트 수
    // totalBytesExpectedToDownload    이번에 다운로드한 타깃 바이트 수
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참조하십시오.

**Swift**

[//]: # (.cssg-snippet-transfer-download-object)
```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();

// BucketName-APPID 포맷의 버킷 이름
request.bucket = "examplebucket-1250000000";

// 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
request.object = "exampleobject";

//다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

// 로컬에 다운로드한 파일 크기. 처음부터 다운로드하는 경우 설정하지 않습니다.
request.localCacheDownloadOffset = 100;

// 다운로드 진행률 수신
request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    
    // bytesDownload                   증가 바이트 수
    // totalBytesDownload              이번에 다운로드한 총 바이트 수
    // totalBytesExpectedToDownload    이번에 다운로드한 타깃 바이트 수
}

// 다운로드 결과 수신
request.finishBlock = { (result, error) in
    if let result = result {
        // result에 응답 header 정보 포함
    } else {
        print(error!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참조하십시오.

#### 예시 코드2: 다운로드 일시 중지, 계속, 취소
**Objective-C**

다운로드 작업은 다음 방식으로 일시 중지할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-pause)
```objective-c
[request cancel];
```

일시 중지 후 다음 방식으로 재개할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-resume)
```objective-c
// 로컬에 다운로드한 파일 크기
int64_t localCacheDownloadOffset = 0;
request.localCacheDownloadOffset = localCacheDownloadOffset;
```

다음 방법을 통해 다운로드를 취소할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```objective-c
undefined
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참조하십시오.

**Swift**

다운로드 작업은 다음 방식으로 일시 중지할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-pause)
```swift
request.cancel();
```

일시 중지 후 다음 방식으로 재개할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-resume)
```swift
// 로컬에 다운로드한 파일 크기

let localCacheDownloadOffset = 100;
request.localCacheDownloadOffset = Int64(localCacheDownloadOffset);
```

다음 방법을 통해 다운로드를 취소할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```swift
undefined
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참조하십시오.

#### 예시 코드3: 중단된 지점부터 다운로드
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-download-resumable)
```objective-c
   QCloudCOSXMLDownloadObjectRequest *getObjectRequest = [[QCloudCOSXMLDownloadObjectRequest alloc] init];
    //중단된 지점부터 다운로드를 지원하며, 기본값은 비활성화입니다.
    getObjectRequest.resumableDownload = true;
    // BucketName-APPID 포맷의 버킷 이름
    getObjectRequest.bucket = transferTestBucket.name;
    //다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
    getObjectRequest.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
    // 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
    getObjectRequest.object = put.object;
    // 다운로드 결과 수신
    [getObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
        // outputObject에 모든 http 응답 헤더 포함
        NSDictionary* info = (NSDictionary *) outputObject;
    }];
    
    // 다운로드 진행률 수신
    [getObjectRequest setDownProcessBlock:^(int64_t bytesDownload,
                                   int64_t totalBytesDownload,
                                   int64_t totalBytesExpectedToDownload) {
        
        // bytesDownload                   증가 바이트 수
        // totalBytesDownload              이번에 다운로드한 총 바이트 수
        // totalBytesExpectedToDownload    이번에 다운로드한 타깃 바이트 수
    }];
    
    [[QCloudCOSTransferMangerService costransfermangerServiceForKey:kHTTPServiceKey] DownloadObject:getObjectRequest];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참조하십시오.

**Swift**

[//]: # (.cssg-snippet-transfer-batch-download-resumable)
```swift
        let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
        
        // BucketName-APPID 포맷의 버킷 이름
        request.bucket = "examplebucket-1250000000";
        
        // 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
        request.object = "exampleobject";
        
        request.resumableDownload = true;
        //다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
        request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;
        
        // 로컬에 다운로드한 파일 크기. 처음부터 다운로드하는 경우 설정하지 않습니다.
        request.localCacheDownloadOffset = 100;

        // 다운로드 진행률 수신
        request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
            totalBytesExpectedToDownload) in
            
            // bytesDownload                   증가 바이트 수
            // totalBytesDownload              이번에 다운로드한 총 바이트 수
            // totalBytesExpectedToDownload    이번에 다운로드한 타깃 바이트 수
        }

        // 다운로드 결과 수신
        request.finishBlock = { (result, error) in
            if let result = result {
                // result에 응답 header 정보 포함
            } else {
                print(error!);
            }
        }
        
    QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참조하십시오.

#### 예시 코드3: 일괄 다운로드
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```objective-c
for (int i = 0; i<20; i++) {
    QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
    
    // BucketName-APPID 포맷의 버킷 이름
    request.bucket = @"examplebucket-1250000000";
    
   // 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
    request.object = @"exampleobject";
    
    //다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
    request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];
    
    // 로컬에 다운로드한 파일 크기. 처음부터 다운로드하는 경우 설정하지 않습니다.
    request.localCacheDownloadOffset = 100;
    
    // 다운로드 결과 수신
    [request setFinishBlock:^(id outputObject, NSError *error) {
        // outputObject에 모든 http 응답 헤더 포함
        NSDictionary* info = (NSDictionary *) outputObject;
    }];
    
    // 다운로드 진행률 수신
    [request setDownProcessBlock:^(int64_t bytesDownload,
                                   int64_t totalBytesDownload,
                                   int64_t totalBytesExpectedToDownload) {
        
        // bytesDownload                   증가 바이트 수
        // totalBytesDownload              이번에 다운로드한 총 바이트 수
        // totalBytesExpectedToDownload    이번에 다운로드한 타깃 바이트 수
    }];
    
    [[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참조하십시오.

**Swift**

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```swift
for i in 1...10 {
    let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
    
    // BucketName-APPID 포맷의 버킷 이름
    request.bucket = "examplebucket-1250000000";
    
    // 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
    request.object = "exampleobject";
    
    //다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
    request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;
    
    // 로컬에 다운로드한 파일 크기. 처음부터 다운로드하는 경우 설정하지 않습니다.
    request.localCacheDownloadOffset = 100;

    // 다운로드 진행률 수신
    request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
        totalBytesExpectedToDownload) in
        
        // bytesDownload                   증가 바이트 수
        // totalBytesDownload              이번에 다운로드한 총 바이트 수
        // totalBytesExpectedToDownload    이번에 다운로드한 타깃 바이트 수
    }

    // 다운로드 결과 수신
    request.finishBlock = { (result, error) in
        if let result = result {
            // result에 응답 header 정보 포함
        } else {
            print(error!);
        }
    }
    
    QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참조하십시오.

## 간단한 작업

### 객체 다운로드

#### 기능 설명

Object(파일/객체)를 로컬에 다운로드합니다(GET Object).

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];

//다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];

// 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
request.object = @"exampleobject";

// BucketName-APPID 포맷의 버킷 이름
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject에서 response의 etag 또는 사용자 정의 헤더 등 정보를 획득할 수 있습니다.
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    
    // 다운로드 과정에서의 진행률
    // bytesDownload       다운로드 바이트 수
    // totalBytesDownload  수신한 총 바이트 수
    // totalBytesExpectedToDownload 파일의 총 바이트

}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/GetObject.m)를 참조하십시오.

**Swift**

[//]: # (.cssg-snippet-get-object)
```swift
let getObject = QCloudGetObjectRequest.init();

// BucketName-APPID 포맷의 버킷 이름
getObject.bucket = "examplebucket-1250000000";

// 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
getObject.object = "exampleobject";
//다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!
    .appendingPathComponent(getObject.object);
getObject.finishBlock = {(result,error) in
    if let result = result {
        // result에 응답 header 정보 포함
    } else {
        print(error!);
    }
};
getObject.downProcessBlock = {(bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    // bytesDownload       다운로드 바이트 수
    // totalBytesDownload  수신한 총 바이트 수
    // totalBytesExpectedToDownload 파일의 총 바이트
}
QCloudCOSXMLService.defaultCOSXML().getObject(getObject);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/GetObject.swift)를 참조하십시오.
