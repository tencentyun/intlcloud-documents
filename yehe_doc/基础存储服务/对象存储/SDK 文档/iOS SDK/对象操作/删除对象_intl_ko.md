## 소개

본 문서는 객체의 삭제 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제   | 버킷에서 지정 객체 삭제 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)	 | 다수의 객체 삭제	| 버킷에서 객체 일괄 삭제  |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 객체 삭제

#### 기능 설명

지정 객체를 삭제합니다(DELETE Object).

#### 예시 코드1: 단일 객체 삭제
**Objective-C**

[//]: # (.cssg-snippet-delete-object)
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
deleteObjectRequest.bucket = @"examplebucket-1250000000";


// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject는 상응하는 모든 http 헤더를 포함합니다.
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-delete-object)
```swift
let deleteObject = QCloudDeleteObjectRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
deleteObject.bucket = "examplebucket-1250000000";


// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
deleteObject.object = "exampleobject";

deleteObject.finishBlock = {(result, error)in
    if let result = result {
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteObject(deleteObject);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift)를 참고하십시오.


#### 예시 코드2: 디렉터리 삭제
**Objective-C**

[//]: # (.cssg-snippet-delete-dir)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// 한 번에 반환 가능한 최대 항목 수, 기본값: 1000
request.maxKeys = 100;

//삭제할 디렉터리 이름: '/' 수반
request.prefix = @"prefix";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    if(! error){
        NSMutableArray *deleteInfosArr = [NSMutableArray array];
        for (QCloudBucketContents *content in result.contents) {
            QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
            delteRequest.bucket = request.bucket;

            QCloudDeleteObjectInfo *object = [QCloudDeleteObjectInfo new];
            object.key = content.key;
            [deleteInfosArr addObject:object];
        }
            
        QCloudDeleteInfo *deleteInfos = [QCloudDeleteInfo new];
        deleteInfos.objects = [deleteInfosArr copy];
          
        QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
        delteRequest.bucket = @"examplebucket-1250000000";
        delteRequest.deleteObjects = deleteInfos;
        [delteRequest setFinishBlock:^(QCloudDeleteResult *outputObject, NSError *error) {
            NSLog(@"outputObject = %@",outputObject);
        }];

        [[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
            
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-delete-dir)
```swift
let getBucketReq = QCloudGetBucketRequest.init();
        
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";
        
// 한 번에 반환 가능한 최대 항목 수, 기본값: 1000
getBucketReq.maxKeys = 100;
        
//삭제할 디렉터리 이름: '/' 수반
getBucketReq.prefix = "dir/";
        
getBucketReq.setFinish { (result, error) in
    if let result = result {
        let contents = result.contents;
        let infos = NSMutableArray.init();
        for content in contents {
            let info = QCloudDeleteObjectInfo.init();
            info.key = content.key;
            infos.add(info);
        }
        let mutipleDel = QCloudDeleteMultipleObjectRequest.init();
        // 삭제할 파일 집합
        let deleteInfos = QCloudDeleteInfo.init();
        // BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
        mutipleDel.bucket = "examplebucket-1250000000";
                
        deleteInfos.objects = infos as! [QCloudDeleteObjectInfo];
                
        // Boolean 값, 이 값으로 Quiet 모드의 실행 여부 결정
        // true: Quiet 모드 실행
        // false: Verbose 모드 실행
        // 기본값: False
        deleteInfos.quiet = false;
                
        // 일괄 삭제할 다수의 객체 정보 먹싱
        mutipleDel.deleteObjects = deleteInfos;
                
        mutipleDel.setFinish { (result, error) in
            if let result = result {
                let deleted = result.deletedObjects
                let failed = result.deletedFailedObjects
            } else {
                print(error!);
            }
        }
        QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift)를 참고하십시오.

## 다수의 객체 삭제

#### 기능 설명

다수의 객체를 일괄 삭제합니다(DELETE Multiple Objects).

#### 예시 코드1: 객체 일괄 삭제

**Objective-C**

[//]: # (.cssg-snippet-delete-multi-object)
```objective-c
QCloudDeleteMultipleObjectRequest* delteRequest = [QCloudDeleteMultipleObjectRequest new];
delteRequest.bucket = @"examplebucket-1250000000";

// 삭제할 단일 파일
QCloudDeleteObjectInfo* deletedObject0 = [QCloudDeleteObjectInfo new];

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
deletedObject0.key = @"exampleobject";

// 삭제할 파일 집합
QCloudDeleteInfo* deleteInfo = [QCloudDeleteInfo new];

// Boolean 값, 이 값으로 Quiet 모드의 실행 여부 결정
// true: Quiet 모드 실행
// false: Verbose 모드 실행
// 기본값: False
deleteInfo.quiet = NO;

// 삭제할 객체 정보를 보관할 배열
deleteInfo.objects = @[deletedObject0];

// 일괄 삭제할 다수의 객체 정보 먹싱
delteRequest.deleteObjects = deleteInfo;

[delteRequest setFinishBlock:^(QCloudDeleteResult* outputObject,
                               NSError *error) {
    // outputObject에서 response의 etag 또는 사용자 정의 헤더 등 정보 획득 가능
    
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-delete-multi-object)
```swift
let mutipleDel = QCloudDeleteMultipleObjectRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
mutipleDel.bucket = "examplebucket-1250000000";

// 삭제할 단일 파일
let info1 = QCloudDeleteObjectInfo.init();

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
info1.key = "exampleobject";

let info2 = QCloudDeleteObjectInfo.init();

// 삭제할 파일 집합
let deleteInfos = QCloudDeleteInfo.init();

// 삭제할 객체 정보를 보관할 배열
deleteInfos.objects = [info1,info2];

// Boolean 값, 이 값으로 Quiet 모드의 실행 여부 결정
// true: Quiet 모드 실행
// false: Verbose 모드 실행
// 기본값: False
deleteInfos.quiet = false;

// 일괄 삭제할 다수의 객체 정보 먹싱
mutipleDel.deleteObjects = deleteInfos;

mutipleDel.setFinish { (result, error) in
    if let result = result {
        let deleted = result.deletedObjects
        let failed = result.deletedFailedObjects
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift)를 참고하십시오.

#### 예시 코드2: 지정 접두사를 가진 객체 삭제
**Objective-C**

[//]: # (.cssg-snippet-delete-dir)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// 한 번에 반환 가능한 최대 항목 수, 기본값: 1000
request.maxKeys = 100;

//접두사가 prefix인 파일을 지정 삭제
request.prefix = @"prefix";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    if(! error){
        NSMutableArray *deleteInfosArr = [NSMutableArray array];
        for (QCloudBucketContents *content in result.contents) {
            QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
            delteRequest.bucket = request.bucket;

            QCloudDeleteObjectInfo *object = [QCloudDeleteObjectInfo new];
            object.key = content.key;
            [deleteInfosArr addObject:object];
        }
            
        QCloudDeleteInfo *deleteInfos = [QCloudDeleteInfo new];
        deleteInfos.objects = [deleteInfosArr copy];
          
        QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
        delteRequest.bucket = @"examplebucket-1250000000";
        delteRequest.deleteObjects = deleteInfos;
        [delteRequest setFinishBlock:^(QCloudDeleteResult *outputObject, NSError *error) {
            NSLog(@"outputObject = %@",outputObject);
        }];

        [[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
            
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-delete-dir)
```swift
let getBucketReq = QCloudGetBucketRequest.init();
        
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";
        
// 한 번에 반환 가능한 최대 항목 수, 기본값: 1000
getBucketReq.maxKeys = 100;
        
//접두사가 prefix인 파일을 지정 삭제
getBucketReq.prefix = "dir/";

        
getBucketReq.setFinish { (result, error) in
    if let result = result {
        let contents = result.contents;
        let infos = NSMutableArray.init();
        for content in contents {
            let info = QCloudDeleteObjectInfo.init();
            info.key = content.key;
            infos.add(info);
        }
        let mutipleDel = QCloudDeleteMultipleObjectRequest.init();
        // 삭제할 파일 집합
        let deleteInfos = QCloudDeleteInfo.init();
        // BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
        mutipleDel.bucket = "examplebucket-1250000000";
                
        deleteInfos.objects = infos as! [QCloudDeleteObjectInfo];
                
        // Boolean 값, 이 값으로 Quiet 모드의 실행 여부 결정
        // true: Quiet 모드 실행
        // false: Verbose 모드 실행
        // 기본값: False
        deleteInfos.quiet = false;
                
        // 일괄 삭제할 다수의 객체 정보 먹싱
        mutipleDel.deleteObjects = deleteInfos;
                
        mutipleDel.setFinish { (result, error) in
            if let result = result {
                let deleted = result.deletedObjects
                let failed = result.deletedFailedObjects
            } else {
                print(error!);
            }
        }
        QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift)를 참고하십시오.

