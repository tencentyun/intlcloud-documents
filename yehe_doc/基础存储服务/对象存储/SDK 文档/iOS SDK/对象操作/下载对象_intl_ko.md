## 소개

본 문서는 객체의 다운로드 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬에 객체 다운로드        |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 고급 인터페이스(권장)

### 객체 다운로드

고급 인터페이스는 다운로드 요청 일시 중지, 복구, 취소를 지원하며, 중단된 지점부터 다운로드 기능을 제공합니다.


#### 예시 코드1: 단일 객체 다운로드

**Objective-C**

[//]: # (.cssg-snippet-transfer-download-object)
```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = @"exampleobject";

// 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

// 로컬에 다운로드한 파일 크기. 처음부터 다운로드하는 경우 설정하지 않습니다.
request.localCacheDownloadOffset = 100;

// 다운로드 결과 수신
[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject는 상응하는 모든 http 헤더를 포함합니다.
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-transfer-download-object)
```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = "exampleobject";

// 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
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
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참고하십시오.

#### 예시 코드2: 다운로드 일시 중지, 재개 및 취소
**Objective-C**

다운로드 작업은 다음 방식으로 일시 중지할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-pause)
```objective-c
[request cancel];
```

일시 정지 후 다음 방법으로 업로드를 재개할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-resume)
```objective-c
// 로컬에 다운로드한 파일 크기
int64_t localCacheDownloadOffset = 0;
request.localCacheDownloadOffset = localCacheDownloadOffset;
```

다음 방법을 통해 다운로드를 취소할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```objective-c
[request cancel];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참고하십시오.

**Swift**

다운로드 작업은 다음 방식으로 일시 중지할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-pause)
```swift
request.cancel();
```

일시 정지 후 다음 방법으로 업로드를 재개할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-resume)
```swift
// 로컬에 다운로드한 파일 크기

let localCacheDownloadOffset = 100;
request.localCacheDownloadOffset = Int64(localCacheDownloadOffset);
```

다음 방법을 통해 다운로드를 취소할 수 있습니다.

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```swift
request.cancel();
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참고하십시오.

#### 예시 코드3: 체크포인트부터 다운로드
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-download-resumable)
```objective-c
   QCloudCOSXMLDownloadObjectRequest *getObjectRequest = [[QCloudCOSXMLDownloadObjectRequest alloc] init];
    //중단된 지점부터 다운로드를 지원하며, 기본값은 비활성화입니다.
    getObjectRequest.resumableDownload = true;
    // BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
    getObjectRequest.bucket = transferTestBucket.name;
    // 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
    getObjectRequest.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
    // 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
    getObjectRequest.object = put.object;
    // 다운로드 결과 수신
    [getObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
        // outputObject는 상응하는 모든 http 헤더를 포함합니다.
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-transfer-batch-download-resumable)
```swift
        let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
        
        // BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
        request.bucket = "examplebucket-1250000000";
        
        // 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
        request.object = "exampleobject";
        
        request.resumableDownload = true;
        // 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
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
                // result에 상응하는 header 정보 포함
            } else {
                print(error!);
            }
        }
        
    QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참고하십시오.

#### 예시 코드4: 일괄 다운로드
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```objective-c
for (int i = 0; i<20; i++) {
    QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
    
    // BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
    request.bucket = @"examplebucket-1250000000";
    
   // 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
    request.object = @"exampleobject";
    
    // 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
    request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];
    
    // 로컬에 다운로드한 파일 크기. 처음부터 다운로드하는 경우 설정하지 않습니다.
    request.localCacheDownloadOffset = 100;
    
    // 다운로드 결과 수신
    [request setFinishBlock:^(id outputObject, NSError *error) {
        // outputObject는 상응하는 모든 http 헤더를 포함합니다.
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```swift
for i in 1...10 {
    let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
    
    // BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
    request.bucket = "examplebucket-1250000000";
    
    // 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
    request.object = "exampleobject";
    
    // 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
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
            // result에 상응하는 header 정보 포함
        } else {
            print(error!);
        }
    }
    
    QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
}
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참고하십시오.

#### 샘플 코드4: 폴더 및 해당 파일 다운로드
**Objective-C**

[//]: # (.cssg-snippet-transfer-download-folder)
```objective-c
    QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

    // BucketName-APPID 형식의 버킷 이름
    request.bucket = @"examplebucket-1250000000";
    // 한 번에 반환 가능한 최대 항목 수, 기본값: 1000
    request.maxKeys = 100;

    //다운로드할 폴더의 cos상의 전체 경로

    request.prefix = @"cos_path";


    [request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
        if(! error){
            for (QCloudBucketContents *content in result.contents) {
                QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
                
                // BucketName-APPID 형식의 버킷 이름
                request.bucket = @"examplebucket-1250000000";
                
                // 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "dir1/object1"입니다.
                request.object = content.key;
                
                // 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
                request.downloadingURL = [NSURL fileURLWithPath:[@"Local File Path" stringByAppendingFormat:@"/%@",content.key]];
                
                // 다운로드 결과 수신
                [request setFinishBlock:^(id outputObject, NSError *error) {
                    // outputObject는 상응하는 모든 http 헤더를 포함합니다.
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
           
            
        }
    }];

    [[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-transfer-download-folder)
```swift
        let getBucketReq = QCloudGetBucketRequest.init();
        
        // BucketName-APPID 형식의 버킷 이름
        getBucketReq.bucket = "examplebucket-1250000000";
        
        // 한 번에 반환 가능한 최대 항목 수, 기본값: 1000
        getBucketReq.maxKeys = 100;
        
        //다운로드할 폴더의 cos상의 전체 경로
        getBucketReq.prefix = "cos_path";
        
        getBucketReq.setFinish { (result, error) in
            if let result = result {
                let contents = result.contents;
                for content in contents {
                    let info = QCloudDeleteObjectInfo.init();
                    let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
                    
                    // BucketName-APPID 형식의 버킷 이름
                    request.bucket = "examplebucket-1250000000";
                    
                    // 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "dir1/object1"입니다.
                    request.object = content.key;
                    
                    // 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
                    
                    request.downloadingURL = NSURL.fileURL(withPath: "Local File Path" ) as URL?;
                    
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
                            // result에 상응하는 header 정보 포함
                        } else {
                            print(error!);
                        }
                    }
                    
                    QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
                }
            } else {
                print(error!);
            }
        }
        QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참고하십시오.


#### 예시 코드5: 다운로드 속도 제한

>! COS iOS SDK v5.9.5 이상 버전이 필요합니다.


**Objective-C**

[//]: # (.cssg-snippet-transfer-download-object)
```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = @"exampleobject";

// 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

// 로컬에 다운로드한 파일 크기. 처음부터 다운로드하는 경우 설정하지 않습니다.
request.localCacheDownloadOffset = 100;

// trafficLimit 매개변수 설정을 사용하여 다운로드 속도를 제한합니다. 단위: bit/s, 속도 제한 설정 범위: 819200-838860800, 즉 100KB/s-100MB/s.
request.trafficLimit = 819200;

// 다운로드 결과 수신
[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject는 상응하는 모든 http 헤더를 포함합니다.
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

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-transfer-download-object)
```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = "exampleobject";

// 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

// 로컬에 다운로드한 파일 크기. 처음부터 다운로드하는 경우 설정하지 않습니다.
request.localCacheDownloadOffset = 100;

// trafficLimit 매개변수 설정을 사용하여 다운로드 속도를 제한합니다. 단위: bit/s, 속도 제한 설정 범위: 819200-838860800, 즉 100KB/s-100MB/s.
request.trafficLimit = 819200;

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
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참고하십시오.

## 간단한 작업

### 객체 다운로드

#### 기능 설명

Object(파일/객체)를 로컬에 다운로드합니다(GET Object).

#### 예시 코드1: 객체 다운로드
**Objective-C**

[//]: # (.cssg-snippet-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];

// 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = @"exampleobject";

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject에서 response의 etag 또는 사용자 정의 헤더 등 정보 획득 가능
    NSDictionary* info = (NSDictionary *) outputObject;
    // 서버 파일의 Crc64
    result[@"x-cos-hash-crc64ecma"] 
    // 로컬 파일로 다운로드한 crc64에서 반환된 crc64가 로컬 계산과 일치하면, 다운로드한 파일이 원격 파일과 완전히 일치한다는 의미입니다.
    uint64_t localCrc64 = [로컬 파일 data qcloud_crc64];
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

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
getObject.bucket = "examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
getObject.object = "exampleobject";
// 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!
    .appendingPathComponent(getObject.object);
getObject.finishBlock = {(result,error) in
    if let result = result {
        // 서버 파일의 Crc64
        result["x-cos-hash-crc64ecma"] 
        // 로컬 파일로 다운로드한 crc64에서 반환된 crc64가 로컬 계산과 일치하면, 다운로드한 파일이 원격 파일과 완전히 일치한다는 의미입니다.
        uint64_t localCrc64 = 로컬 파일 data.qcloud_crc64();
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

#### 예시 코드2: 다운로드 속도 제한
>! COS iOS SDK v5.9.5 이상 버전이 필요합니다.
>
**Objective-C**

[//]: # (.cssg-snippet-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];

// 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = @"exampleobject";

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// trafficLimit 매개변수 설정을 사용하여 다운로드 속도를 제한합니다. 단위: bit/s, 속도 제한 설정 범위: 819200-838860800, 즉 100KB/s-100MB/s.
request.trafficLimit = 819200;

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject에서 response의 etag 또는 사용자 정의 헤더 등 정보 획득 가능
    NSDictionary* info = (NSDictionary *) outputObject;
    // 파일 crc64 가져오기
    NSString * crc64 = [[outputObject __originHTTPURLResponse__].allHeaderFields valueForKey:@"x-cos-hash-crc64ecma"];
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

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
getObject.bucket = "examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
getObject.object = "exampleobject";
// 다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!
    .appendingPathComponent(getObject.object);
    
// trafficLimit 매개변수 설정을 사용하여 다운로드 속도를 제한합니다. 단위: bit/s, 속도 제한 설정 범위: 819200-838860800, 즉 100KB/s-100MB/s.
getObject.trafficLimit = 819200;

getObject.finishBlock = {(result,error) in
    if let result = result {
        // result에 상응하는 header 정보 포함
        // 파일 crc64 가져오기
        let crc64 = result?.__originHTTPURLResponse__.allHeaderFields["x-cos-hash-crc64ecma"];
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
