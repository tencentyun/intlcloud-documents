VOD는 iOS 클라이언트에 비디오를 업로드하기 위한 SDK를 제공합니다. 업로드 프로세스에 대한 자세한 내용은 [클라이언트 업로드 가이드](https://intl.cloud.tencent.com/document/product/266/33921)를 참고하십시오.

## 소스 코드 다운로드
1. iOS 업로드 Demo 및 소스 코드를 다운로드하려면 [여기를 클릭](https://ugcupload-1252463788.file.myqcloud.com/TXUGCUploadDemo_iOS.zip)하십시오.
2. 다운로드한 zip 패키지의 압축을 풀면 TXUGCUploadDemo 디렉터리를 볼 수 있습니다. 업로드 소스 코드는 `TXUGCUploadDemo/upload` 디렉터리에 있습니다.

## 업로드 라이브러리와 소스 코드 통합

1. 업로드 소스 코드 디렉터리 `TXUGCUploadDemo/upload`를 프로젝트에 복사하십시오.
2. 동적 라이브러리 `QCloudCore.framework`, `QCloudCOSXML.framework` 및 정적 라이브러리 `libmtasdk.a`(`TXUGCUploadDemo/upload/COSSDK/` 디렉터리에 있음)를 프로젝트로 가져오고 다음 종속성 라이브러리를 추가하십시오.
    ```
    1. CoreTelephony.framework
    2. Foundation.framework
    3. SystemConfiguration.framework
    4. libc++.tbd
    ``` 
3. Build Settings에서 Other Linker Flags를 설정하고 `-ObjC` 매개변수를 추가합니다.

##  비디오 간편 업로드

#### 업로드 객체 초기화

```objc
TXUGCPublish *_videoPublish = [[TXUGCPublish alloc] initWithUserID:@"upload_video_userid"];
```

#### 업로드 객체 콜백 설정

```objc
_videoPublish.delegate = self;
```

```objc
#pragma mark - TXVideoPublishListener

- (void)onPublishProgress:(NSInteger)uploadBytes totalBytes:(NSInteger)totalBytes {
    self.progressView.progress = (float)uploadBytes/totalBytes;
    NSLog(@"onPublishProgress [%ld/%ld]", uploadBytes, totalBytes);
}

- (void)onPublishComplete:(TXPublishResult*)result {
    NSString *string = [NSString stringWithFormat:@"업로드 완료, 오류 코드[%d], 메시지[%@]", result.retCode, result.retCode == 0? result.videoURL: result.descMsg];
    [self showErrorMessage:string];
    NSLog(@"onPublishComplete [%d/%@]", result.retCode, result.retCode == 0? result.videoURL: result.descMsg);
}
```

#### 업로드 매개변수 생성

```objc
TXPublishParam *publishParam = [[TXPublishParam alloc] init];

publishParam.signature  = @"귀하의 비즈니스 백엔드에서 생성된 서명";
publishParam.videoPath  = @"비디오 파일의 경로";
```
`signature`계산 방법에 대한 자세한 내용은 [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922)을 참고하십시오.

#### 업로드 메소드 호출

```objc
[_videoPublish publishVideo:publishParam];
```
>?
>- 업로드 방법은 파일 크기에 따라 단순 업로드 또는 멀티파트 업로드를 자동으로 선택하므로 멀티파트 업로드의 각 단계를 신경 쓸 필요가 없습니다.
>- 지정된 서브 애플리케이션에 업로드하려면 [서브 애플리케이션 시스템 - 클라이언트에서 업로드](https://intl.cloud.tencent.com/document/product/266/33987)를 참고하십시오.

## 고급 기능
#### 커버 업로드

업로드 매개변수에 커버 이미지를 포함합니다.

```objc
TXPublishParam *publishParam = [[TXPublishParam alloc] init];
publishParam.signature  = @"귀하의 비즈니스 백엔드에서 생성된 서명";
publishParam.coverPath = @"커버 이미지 파일의 경로";
publishParam.videoPath  = @"비디오 파일의 경로";
```

#### 업로드 취소 및 재개

업로드를 취소하려면 `canclePublish`를 호출합니다.

```objc
[_videoPublish canclePublish];
```

업로드를 재개하려면 동일한 업로드 매개변수와 동일한 비디오 및 커버 이미지 경로를 사용하여 `TXUGCPublish`의 `publishVideo`를 다시 호출합니다.

#### 체크포인트 재시작

VOD는 업로드 중 체크포인트 재시작을 지원합니다. 업로드가 예기치 않게 종료된 경우 중단 지점에서 업로드를 재개하여 업로드 시간을 절약할 수 있습니다.

체크포인트 재시작은 1일 이내에 유효합니다. 비디오 업로드가 중단되었다가 하루 이내에 재개되면 업로드를 재개할 수 있습니다. 그렇지 않으면 전체 비디오가 다시 업로드됩니다.

업로드 매개변수 `enableResume`은 체크포인트 재시작 스위치로, 기본 값은 활성화입니다.


## 이미지 및 미디어 업로드

```objc
// 객체 생성
TXUGCPublish *_imagePublish = [[TXUGCPublish alloc] initWithUserID:@"upload_image_userid"];

// 콜백 설정
_imagePublish.mediaDelegate = self;

// 업로드 매개변수 생성
TXMediaPublishParam *publishParam = [[TXMediaPublishParam alloc] init];
publishParam.signature  = @"귀하의 비즈니스 백엔드에서 생성된 서명";
publishParam.mediaPath = @"이미지 파일의 경로";

// 이미지 또는 미디어 파일 업로드
[_imagePublish publishMedia:publishParam];

```


## 비디오 업로드 API 설명

업로드 객체 초기화: `TXUGCPublish::initWithUserID`

| 매개변수 이름   | 매개변수 설명               | 유형        | 필수 입력   |
| ------ | ------------------ | --------- | ---- |
| userID | 사용자를 고유하게 식별하는 사용자 ID. | NSString | No    |

업로드 시작: `TXUGCPublish.publishVideo`

| 매개변수 이름  | 매개변수 설명 | 유형            | 필수 입력   |
| ----- | ---- | --------------- | ---- |
| param | 게시 매개변수. | TXPublishParam | Yes    |

업로드 매개변수: `TXPublishParam`

| 매개변수 이름         | 매개변수 설명                             | 유형     | 필수 입력   |
| ------------ | ---------------------------------- | --------- | ---- |
| signature    | [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922). | NSString* | Yes    |
| videoPath    | 로컬 비디오 파일 경로.                           | NSString* | Yes    |
| coverPath    | 로컬 커버 이미지의 경로. 옵션.                 | NSString*  | No    |
| fileName     | Tencent Cloud에 업로드된 비디오 파일 이름. 이 매개변수를 비워두면 기본적으로 로컬 파일 이름이 사용됩니다.  | NSString*  | No    |
| enableResume | 체크포인트 재시작 활성화 여부. 기본 값: 활성화.                  | BOOL      | No    |
| enableHttps  | HTTPS 활성화 여부. 기본 값: 비활성화.                     | BOOL      | No    |


업로드 콜백 설정: `TXUGCPublish.delegate`

| 멤버 변수 이름   | 변수 설명        | 유형                     | 필수 입력   |
| -------- | ----------- | ---------------------- | ---- |
| delegate | 업로드 진행 상황 및 결과 콜백에 대한 리스너. | TXVideoPublishListener | Yes    |


업로드 진행률 콜백: `onPublishProgress`

| 변수 이름        | 변수 설명     | 유형        |
| ----------- | -------- | --------- |
| uploadBytes | 업로드된 바이트 수. | NSInteger |
| totalBytes  | 총 바이트 수.     | NSInteger |

업로드 결과 콜백: `onPublishComplete`

| 변수 이름   | 변수 설명 | 유형               |
| ------ | ---- | ---------------- |
| result | 업로드 결과. | TXPublishResult |

업로드 이벤트 콜백: `onPublishEvent`

| 변수 이름   | 변수 설명 | 유형               |
| ------ | ---- | ---------------- |
| evt | 디버깅 정보 출력용 이벤트. | NSDictionary |

업로드 결과: `TXPublishResult`

| 멤버 변수 이름   | 변수 설명      | 유형        |
| -------- | --------- | --------- |
| retCode  | 오류 코드.       | int       |
| descMsg  | 실패한 업로드에 대한 오류 설명. | NSString |
| videoId  | VOD 파일 ID.  | NSString |
| videoURL | 비디오 스토리지 주소.    | NSString |
| coverURL | 커버 스토리지 주소.    | NSString |

사전 업로드: `TXUGCPublishOptCenter.prepareUpload`
    
| 매개변수 이름  | 매개변수 설명                        | 유형   | 필수 입력 |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922). | NSString | Yes   |


#### 오류 코드

SDK는 `TXVideoPublishListener` API를 통해 비디오 업로드 상태를 수신합니다. 따라서 `TXPublishResult`의 `retCode`로 비디오 게시 상태를 확인할 수 있습니다.

| 오류 코드  | TVCCommon의 상수           | 의미              |
| :--: | :---------------------------- | :-------------- |
|  0   | TVC_OK                        | 업로드 성공.            |
| 1001 | TVC_ERR_UGC_REQUEST_FAILED    | 업로드 요청 실패. 이는 일반적으로 클라이언트의 서명이 만료되었거나 유효하지 않기 때문입니다. App 서명을 다시 신청해야 합니다.         |
| 1002 | TVC_ERR_UGC_PARSE_FAILED      | 요청 정보 구문 분석 실패.        |
| 1003 | TVC_ERR_VIDEO_UPLOAD_FAILED   | 비디오 업로드 실패.          |
| 1004 | TVC_ERR_COVER_UPLOAD_FAILED   | 커버 업로드 실패.          |
| 1005 | TVC_ERR_UGC_FINISH_REQ_FAILED | 업로드 종료 요청 실패.        |
| 1006 | TVC_ERR_UGC_FINISH_RSP_FAILED | 업로드 종료 요청 응답 오류.        |



## 이미지 및 미디어 업로드 API 설명

업로드 객체 초기화: `TXUGCPublish::initWithUserID`

| 매개변수 이름   | 매개변수 설명               | 유형        | 필수 입력   |
| ------ | ------------------ | --------- | ---- |
| userID | 사용자를 고유하게 식별하는 사용자 ID입니다. | NSString | No    |

업로드 시작: `TXUGCPublish.publishMedia`

| 매개변수 이름  | 매개변수 설명 | 유형            | 필수 입력   |
| ----- | ---- | --------------- | ---- |
| param | 게시 매개변수. | TXMediaPublishParam | Yes    |

매개변수 업로드: `TXMediaPublishParam`

| 매개변수 이름       | 매개변수 설명                              | 유형       | 필수 입력 |
| ------------ | ---------------------------------- | --------- | ---- |
| signature    | [클라이언트 업로드용 서명](https://cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/266/33922). | NSString* | Yes    |
| mediaPath    | 로컬 이미지/미디어 파일 경로.                           | NSString* | Yes    |
| fileName     | Tencent Cloud에 업로드된 이미지/미디어 파일 이름. 이 매개변수를 비워두면 기본적으로 로컬 파일 이름이 사용됩니다.  | NSString*  | No    |
| enableResume | 체크포인트 재시작 활성화 여부. 기본 값: 활성화.                  | BOOL      | No    |
| enableHttps  | HTTPS 활성화 여부. 기본 값: 비활성화.                     | BOOL      | No    |


업로드 콜백 설정: `TXUGCPublish.TXMediaPublishListener`

| 멤버 변수 이름   | 변수 설명        | 유형                     | 필수 입력   |
| -------- | ----------- | ---------------------- | ---- |
| mediaDelegate | 업로드 진행률 및 결과 콜백에 대한 리스너. | TXMediaPublishListener | Yes    |


업로드 진행 콜백: `onMediaPublishProgress`

| 변수 이름        | 변수 설명     | 유형        |
| ----------- | -------- | --------- |
| uploadBytes | 업로드된 바이트 수. | NSInteger |
| totalBytes  | 총 바이트 수.     | NSInteger |

업로드 결과 콜백: `onMediaPublishComplete`

| 변수 이름   | 변수 설명 | 유형               |
| ------ | ---- | ---------------- |
| result | 업로드 결과. | TXMediaPublishResult |

업로드 이벤트 콜백: `onMediaPublishEvent`

| 변수 이름   | 변수 설명 | 유형               |
| ------ | ---- | ---------------- |
| evt | 디버깅 정보 출력용 이벤트. | NSDictionary |

업로드 결과: `TXMediaPublishResult`

| 맴버 변수 이름   | 변수 설명      | 유형        |
| -------- | --------- | --------- |
| retCode  | 오류 코드.       | int       |
| descMsg  | 업로드 실패 오류 설명. | NSString |
| mediaId  | 이미지/미디어 파일 ID.  | NSString |
| mediaURL | 이미지/미디어 스토리지 주소.    | NSString |

사전 업로드: `TXUGCPublishOptCenter.prepareUpload`
    
| 매개변수 이름  | 매개변수 설명                        | 유형   | 필수 입력 |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922). | NSString | Yes   |


#### 오류 코드

SDK는 `TXMediaPublishListener` API를 통해 이미지/미디어 업로드 상태를 수신합니다. 따라서 `TXMediaPublishResult`의 `retCode`로 이미지/미디어 게시 상태를 확인할 수 있습니다.

| 오류 코드  | TVCCommon의 상수           | 의미              |
| :--: | :---------------------------- | :-------------- |
|  0   | MEDIA_PUBLISH_RESULT_OK                        | 업로드 성공.            |
| 1001 | MEDIA_PUBLISH_RESULT_UPLOAD_REQUEST_FAILED    | 업로드 요청 실패. 이는 일반적으로 클라이언트의 서명이 만료되었거나 유효하지 않기 때문입니다. App 서명을 다시 신청해야 합니다.         |
| 1002 | MEDIA_PUBLISH_RESULT_UPLOAD_RESPONSE_ERROR      | 요청 정보 구문 분석 실패.        |
| 1003 | MEDIA_PUBLISH_RESULT_UPLOAD_VIDEO_FAILED   | 이미지/미디어 업로드 실패.          |
| 1005 | MEDIA_PUBLISH_RESULT_PUBLISH_REQUEST_FAILED | 업로드 종료 요청 실패.        |
| 1006 | MEDIA_PUBLISH_RESULT_PUBLISH_RESPONSE_ERROR | 업로드 종료 요청 응답 오류.        |





