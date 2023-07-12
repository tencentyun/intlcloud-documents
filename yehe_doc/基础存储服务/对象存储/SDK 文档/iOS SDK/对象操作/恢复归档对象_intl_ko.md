<!--
 * @Author: your name
 * @Date: 2020-12-07 10:53:33
 * @LastEditTime: 2021-06-08 09:25:29
 * @LastEditors: your name
 * @Description: In User Settings Edit
 * @FilePath: /qcloud-documents/product/스토리지와 CDN/객체 스토리지 4.0/SDK문서/iOS SDK/객체 작업/아카이브된 객체 복구.md
-->
## 소개

본 문서는 아카이브된 객체 복구 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 아카이브된 객체 복구 | 아카이브 유형의 객체 검색 및 액세스                      |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 아카이브된 객체 복구 

#### 기능 설명

아카이브 유형의 객체를 검색하여 액세스합니다(POST Object restore).

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-restore-object)
```objective-c
QCloudPostObjectRestoreRequest *req = [QCloudPostObjectRestoreRequest new];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
req.bucket = @"examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
req.object = @"exampleobject";

// 임시 사본의 만료 시간 설정
req.restoreRequest.days = 10;

// 복원 과정 유형 설정 정보
req.restoreRequest.CASJobParameters.tier = QCloudCASTierStandard;

[req setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject는 상응하는 모든 http 헤더 포함
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PostObjectRestore:req];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/RestoreObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-restore-object)
```swift
let restore = QCloudPostObjectRestoreRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
restore.bucket = "examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
restore.object = "exampleobject";

// 임시 사본의 만료 시간 설정
restore.restoreRequest.days = 10;

// 복원 과정 유형 설정 정보
restore.restoreRequest.casJobParameters.tier = .standard;
restore.finishBlock = {(result,error)in
    if let result = result {
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().postObjectRestore(restore);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/RestoreObject.swift)를 참고하십시오.

