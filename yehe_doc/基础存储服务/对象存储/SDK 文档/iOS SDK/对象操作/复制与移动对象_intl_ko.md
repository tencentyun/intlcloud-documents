## 소개


본 문서는 객체 이동에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명                       | 작업 설명               |
| :----------------------------------------------------------- | :--------------------------- | :--------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정(객체 속성 수정) | 파일을 타깃 경로에 복사     |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제                 | 버킷에서 지정 객체 삭제 |




## 객체 이동

객체 이동에는 타깃 위치로 원본 객체 복사 및 원본 객체 삭제의 두 가지 주요 작업이 포함되어 있습니다.

COS는 버킷 이름(Bucket)과 객체 키(ObjectKey)로 객체를 식별하므로 객체를 이동하는 경우 해당 객체의 식별자를 수정해야 합니다. 현재 COS Java SDK는 객체의 고유 식별자를 수정할 수 있는 인터페이스를 제공하지 않습니다. 하지만 **객체 복사**와 **객체 삭제**를 함께 사용하는 기본 작업으로 객체 식별자를 수정하고 객체를 이동할 수 있습니다.

예시로 mybucket-1250000000이라는 버킷의 picture.jpg 객체를 동일 버킷의 doc 경로로 이동하려면 먼저 picture.jpg 객체를 버킷의 doc 경로로 복사합니다. 즉, 객체 키를 doc/picture.jpg로 설정합니다. 복사 완료 후 picture.jpg 객체를 삭제하여 ‘이동’한 효과를 구현합니다.

마찬가지로 mybucket-1250000000 버킷의 picture.jpg 객체를 myanothorbucket-1250000000으로 이동하려면 먼저 객체를 myanothorbucket-1250000000 버킷에 복사하고 원본 객체를 삭제합니다.


#### 예시 코드

**Objective-C**

[//]: # (.cssg-snippet-move-object)
```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];
    
// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
    
// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "dir1/object1"입니다.
request.object = @"exampleobject";
    
// 파일 원본 버킷. 공개 읽기이거나 현재 계정에 권한이 있어야 합니다.
request.sourceBucket = @"sourcebucket-1250000000";
    
// 원본 파일 이름
request.sourceObject = @"sourceObject";
    
// 원본 파일의 APPID
request.sourceAPPID = @"1250000000";
    
// 출처 리전
request.sourceRegion= @"COS_REGION";
    
[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    // outputObject에서 response의 etag 또는 사용자 정의 헤더 등 정보 획득 가능
    if(! error){
        QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
            
        // 파일 원본 버킷. 공개 읽기이거나 현재 계정에 권한이 있어야 합니다.
        deleteObjectRequest.bucket = @"sourcebucket-1250000000";
            
        // 원본 파일 이름은 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 "dir1/object1"입니다.
        deleteObjectRequest.object = @"sourceObject";
            
        [deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
            // outputObject는 상응하는 모든 http 헤더를 포함합니다.
            NSDictionary* info = (NSDictionary *) outputObject;
        }];
            
        [[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
    }
}];
    
// 리전 간 이동을 할 경우 이곳에 사용한 transferManager가 있는 region은 반드시 타깃 버킷이 있는 region이어야 합니다.
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MoveObject.m)를 참조하십시오.

**Swift**

[//]: # (.cssg-snippet-transfer-copy-object)
```swift
let copyRequest = QCloudCOSXMLCopyObjectRequest.init();
        
// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
copyRequest.bucket = "examplebucket-1250000000";
                
// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "dir1/object1"입니다.
copyRequest.object = "exampleobject";
        
// 파일 원본 버킷. 공개 읽기이거나 현재 계정에 권한이 있어야 합니다.
// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
copyRequest.sourceBucket = "sourcebucket-1250000000";
        
// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "dir1/object1"입니다.
copyRequest.sourceObject = "sourceObject";
        
// 원본 파일의 APPID
copyRequest.sourceAPPID = "1250000000";
        
// 출처 리전
copyRequest.sourceRegion = "COS_REGION";
        
copyRequest.setFinish { (copyResult, error) in
    if let copyResult = copyResult {
        // 파일의 etag
        let deleteObject = QCloudDeleteObjectRequest.init();
                
        // BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
        deleteObject.bucket = "sourcebucket-1250000000";
                
        // 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "dir1/object1"입니다.
        deleteObject.object = "sourceObject";
                
        deleteObject.finishBlock = {(result, error)in
            if let result = result {
                    // result에 상응하는 header 정보 포함
            } else {
                  print(error!);
              }
        }
        QCloudCOSXMLService.defaultCOSXML().deleteObject(deleteObject);
    } else {
        print(error!);
    }
            
}
// 리전 간 이동을 할 경우 이곳에 사용한 transferManager가 있는 region은 반드시 타깃 버킷이 있는 region이어야 합니다.
QCloudCOSTransferMangerService.defaultCOSTransferManager().copyObject(copyRequest);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferCopyObject.swift)를 참고하십시오.
