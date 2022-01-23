VOD는 Android 클라이언트에 비디오를 업로드하기 위한 SDK를 제공합니다. 업로드 프로세스에 대한 자세한 내용은 [클라이언트 업로드 가이드](https://intl.cloud.tencent.com/document/product/266/33921)를 참고하십시오.

## 소스 코드 다운로드

1. Android 업로드 Demo 및 소스 코드를 [클릭하여 다운로드](https://ugcupload-1252463788.file.myqcloud.com/LiteAVSDK_UGC_Upload_Android.zip)하십시오.
2. 다운로드한 zip 파일의 압축을 풀면 `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload`에서 Demo 디렉터리와 업로드 소스 코드를 찾을 수 있습니다.

##  업로드 라이브러리와 소스 코드 통합

1. `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload`를 프로젝트 디렉터리에 복사하고 패키지 이름을 수동으로 수정합니다.
2. 프로젝트에 종속성을 추가하려면 `Demo/app/build.gradle`을 참고하십시오.
    ```
    implementation ('com.tencent.qcloud:cosxml:5.5.3') {
        exclude group: 'com.tencent.qcloud', module: 'mtaUtils' //mta 리포트 기능 비활성화}
    }
    ```
>?[수동 통합](https://intl.cloud.tencent.com/document/product/436/12159)을 참고하여 해당 종속 라이브러리를 통합할 수도 있습니다.
3. 비디오 업로드를 위해서는 네트워크 및 스토리지 접근 권한이 필요합니다. `AndroidManifest.xml`에 다음 권한 선언을 추가할 수 있습니다.
	```xml
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
	<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
		<intent-filter>
			<!--네트워크 변경을 감지하는 action-->
			<action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
			<category android:name="android.intent.category.DEFAULT" />
		</intent-filter>
	</receiver>
	```

##  비디오 간편 업로드
#### 업로드 객체 초기화

```java
TXUGCPublish mVideoPublish = new TXUGCPublish(this.getApplicationContext(), "independence_android")
```

#### 업로드 객체 콜백 설정

```java
mVideoPublish.setListener(new TXUGCPublishTypeDef.ITXVideoPublishListener() {
    @Override
    public void onPublishProgress(long uploadBytes, long totalBytes) {
        mProgress.setProgress((int) (100*uploadBytes/totalBytes));
    }

    @Override
    public void onPublishComplete(TXUGCPublishTypeDef.TXPublishResult result) {
        mResultMsg.setText(result.retCode + " Msg:" + (result.retCode == 0 ? result.videoURL : result.descMsg));
    }
});
```

#### 업로드 매개변수 생성

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();

param.signature = "xxx";
param.videoPath = "xxx";
```
`signature` 계산 방법에 대한 자세한 내용은 [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922)을 참고하십시오.

#### 업로드 메소드 호출

```java
int publishCode = mVideoPublish.publishVideo(param);
```

## 이미지 간편 업로드

#### 업로드 객체 초기화

```java
TXUGCPublish mVideoPublish = new TXUGCPublish(this.getApplicationContext(), "independence_android")
```

#### 업로드 객체 콜백 설정

```java
mVideoPublish.setListener(new TXUGCPublishTypeDef.ITXMediaPublishListener() {
    @Override
    public void onMediaPublishProgress(long uploadBytes, long totalBytes) {
        mProgress.setProgress((int) (100*uploadBytes/totalBytes));
    }
    @Override
    public void onMediaPublishComplete(TXUGCPublishTypeDef.TXMediaPublishResult mediaResult) {
        mResultMsg.setText(result.retCode + " Msg:" + (result.retCode == 0 ? result.videoURL : result.descMsg));
    }
});
```

#### 업로드 매개변수 생성

```java
TXUGCPublishTypeDef.TXMediaPublishParam param = new TXUGCPublishTypeDef.TXMediaPublishParam();

param.signature = "xxx";
param.mediaPath = "xxx";
```

`signature` 계산 방법에 대한 자세한 내용은 [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922)을 참고하십시오.

#### 업로드 메소드 호출

```java
int publishCode = mVideoPublish.publishMedia(param);
```

>?
>- 업로드 방법은 파일 크기에 따라 일반 업로드 또는 멀티파트 업로드를 자동으로 선택하므로 멀티파트 업로드의 각 단계를 신경 쓸 필요가 없습니다.
>- 지정된 서브 애플리케이션에 업로드하려면 [서브 애플리케이션 시스템 - 클라이언트 업로드](https://intl.cloud.tencent.com/document/product/266/33987)를 참고하십시오.
>
## 고급 기능

#### 커버 업로드

커버 이미지의 경로를 업로드 매개변수로 추가합니다.

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();
param.signature = "xxx";
param.videoPath = "xxx";
param.coverPath = "xxx";
```
`signature` 계산 방법에 대한 자세한 내용은 [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922)을 참고하십시오.

#### 업로드 취소 및 재개

업로드를 취소하려면 `TXUGCPublish의 cancelPublish()` API를 호출합니다.

```java
mVideoPublish.canclePublish();
```

업로드를 재개하려면 동일한 업로드 매개변수와 동일한 비디오 및 커버 이미지 경로를 사용하여 `TXUGCPublish`의 `publishVideo`를 다시 호출합니다.

#### 체크포인트 재시작

VOD는 업로드 중 체크포인트 재시작을 지원합니다. 업로드가 예기치 않게 종료된 경우 중단 지점에서 업로드를 재개하여 업로드 시간을 절약할 수 있습니다.

체크포인트 재시작은 1일 이내에 유효합니다. 비디오 업로드가 중단되었다가 하루 이내에 재개되면 업로드를 재개할 수 있습니다. 그렇지 않으면 전체 비디오가 다시 업로드됩니다.

업로드 매개변수 `enableResume`은 체크포인트 재시작 스위치로 기본 값은 활성화입니다.

#### 사전 업로드

업로드 오류의 대부분은 네트워크 연결 실패 또는 시간 초과로 인해 발생합니다. 이러한 문제를 해결하기 위해 HTTPDNS 리졸브, 권장 업로드 대상 리전 가져오기, 최적의 업로드 대상 리전 감지 등 최적화된 사전 업로드 로직을 추가했습니다.

App을 활성화할 때 `TXUGCPublishOptCenter.getInstance().prepareUpload(signature)`를 호출하는 것이 좋습니다. 사전 업로드 모듈은 `<도메인, IP>`의 매핑 테이블과 최적의 업로드 대상 지역을 로컬로 캐시하고 네트워크 전환이 감지되면 캐시를 자동으로 퍼지하고 새로고침합니다.

>!`AndroidManifest.xml`에 네트워크 모니터링 모듈을 등록해야 합니다.
```xml
<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
  <intent-filter>
    <!--네트워크 변경을 감지하는 action-->
    <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
    <category android:name="android.intent.category.DEFAULT" />
  </intent-filter>
</receiver>
```

`signature` 계산 방법에 대한 자세한 내용은 [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922)을 참고하십시오.


## 비디오 업로드 API 설명

업로드 객체 초기화: `TXUGCPublish`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| --------- | ---------------------- | ------- | ---- |
| context   | application 컨텍스트.        | Context | Yes    |
| customKey | 이 매개변수는 사용자를 구별하는 데 사용됩니다. 향후 문제 해결을 위해 App 계정 ID를 이 매개변수의 값으로 사용하는 것이 좋습니다. | String  | No    |

VOD appId 설정: `TXUGCPublish.setAppId`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| --------- | ---------------------- | ------- | ---- |
| appId   | VOD appId.        | int | Yes    |


비디오 업로드: `TXUGCPublish.publishVideo`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| ----- | ---- | ---------------------------------- | ---- |
| param | 업로드 매개변수. | TXUGCPublishTypeDef.TXPublishParam | Yes    |

업로드 매개변수: `TXUGCPublishTypeDef.TXPublishParam`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| ------------ | ---------------------------------- | ------- | ---- |
| signature    | [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922). | String  | Yes    |
| videoPath    | 로컬 비디오 파일 경로.                           | String  | Yes    |
| coverPath    | 로컬 커버 이미지 파일 경로. 기본 값: 커버 파일 미사용.                  | String  | No    |
| enableResume | 체크포인트 재시작 활성화 여부. 기본 값: 활성화.                      | boolean | No    |
| enableHttps  | HTTPS 활성화 여부. 기본 값: 비활성화                      | boolean | No    |
| fileName     | Tencent Cloud에 업로드된 비디오 파일의 이름입니다. 이 매개변수를 비워두면 기본적으로 로컬 파일 이름이 사용됩니다. | String  | No    |

업로드 콜백 설정: `TXUGCPublish.setListener`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| -------- | ----------- | ---------------------------------------- | ---- |
| listener | 업로드 진행률 및 결과 콜백 리스너. | TXUGCPublishTypeDef.ITXVideoPublishListener | Yes    |


진행률 콜백: `TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishProgress`

| 변수 이름        | 변수 설명     | 유형   |
| ----------- | -------- | ---- |
| uploadBytes | 업로드된 바이트 수. | long |
| totalBytes  | 총 바이트 수.     | long |

콜백 결과: `TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishComplete`

| 변수 이름   | 변수 설명 | 유형                                  |
| ------ | ---- | ----------------------------------- |
| result | 업로드 결과. | TXUGCPublishTypeDef.TXPublishResult |

업로드 결과: `TXUGCPublishTypeDef.TXPublishResult`

| 멤버 변수 이름   | 변수 설명      | 유형     |
| -------- | --------- | ------ |
| retCode  | 결과 코드.       | int    |
| descMsg  | 업로드 실패에 대한 오류 설명. | String |
| videoId  | VOD 파일 ID.  | String |
| videoURL | 비디오 스토리지 주소.    | String |
| coverURL | 커버 스토리지 주소.    | String |

사전 업로드: `TXUGCPublishOptCenter.prepareUpload`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| --------- | ---------------------- | ------- | ---- |
| signature   | [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922).        | String | Yes    |

## 이미지 업로드 API 설명

업로드 객체 초기화: `TXUGCPublish`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| --------- | --------------------------------------------------------- | ------- | ---- |
| context   | application 컨텍스트.                                        | Context | Yes   |
| customKey | 이 매개변수는 사용자를 구별하는 데 사용됩니다. 후속 문제 해결을 용이하게 하려면 App 계정 ID를 이 매개변수의 값으로 사용하는 것이 좋습니다. | String  | No   |

VOD appId 설정: `TXUGCPublish.setAppId`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| -------- | --------- | ---- | ---- |
| appId    | VOD appId. | int  | Yes   |

이미지 업로드: `TXUGCPublish.publishMedia`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| -------- | -------- | --------------------------------------- | ---- |
| param    | 업로드 매개변수. | TXUGCPublishTypeDef.TXMediaPublishParam | Yes   |

업로드 매개변수: `TXUGCPublishTypeDef.TXMediaPublishParam`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| ------------ | -------------------------------------------------- | ------- | ---- |
| signature    | [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922).       | String  | Yes   |
| mediaPath    | 로컬 이미지 파일 경로.                                   | String  | Yes   |
| enableResume | 체크포인트 재시작 활성화 여부. 기본 값: 활성화.                         | boolean | No   |
| enableHttps  | HTTPS 활성화 여부. 기본 값: 비활성화.                           | boolean | No   |
| fileName     | Tencent Cloud에 업로드된 비디오 파일의 이름. 이 매개변수를 비워두면 기본적으로 로컬 파일 이름이 사용됩니다. | String  | No   |

업로드 콜백 설정: `TXUGCPublish.setListener`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| -------- | ---------------------- | ------------------------------------------- | ---- |
| listener | 업로드 진행률 및 결과 콜백 리스너. | TXUGCPublishTypeDef.ITXMediaPublishListener | Yes   |

진행률 콜백: `TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishProgress`

| 변수 이름    | 변수 설명         | 유형 |
| ----------- | ---------------- | ---- |
| uploadBytes | 업로드된 바이트 수. | long |
| totalBytes  | 총 바이트 수.         | long |

결과 콜백: `TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishComplete`

| 변수 이름 | 변수 설명 | 유형                                |
| -------- | -------- | ----------------------------------- |
| result   | 업로드 결과. | TXUGCPublishTypeDef.TXPublishResult |

업로드 결과: `TXUGCPublishTypeDef.TXMediaPublishResult`

| 멤버 변수 이름 | 변수 설명           | 유형   |
| ------------ | ------------------ | ------ |
| retCode      | 결과 코드.             | int    |
| descMsg      | 업로드 실패에 대한 오류 설명. | String |
| mediaId      | VOD 미디어 파일 ID. | String |
| mediaURL     | 미디어 리소스 스토리지 주소.   | String |

사전 업로드: `TXUGCPublishOptCenter.prepareUpload`

| 매개변수 이름      | 매개변수 설명                  | 유형     | 필수 입력 |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922). | String | Yes   |

## 오류 코드

SDK는 API `TXUGCPublishTypeDef.ITXVideoPublishListene\ITXMediaPublishListener`를 통해 비디오 업로드 상태를 수신합니다. 따라서 `TXUGCPublishTypeDef.TXPublishResult\TXMediaPublishResult`에서 `retCode`를 사용하여 비디오 업로드 상태를 확인할 수 있습니다.

| 상태 코드  | TVCConstants         | 설명                     |
| :--: | :----------------------------- | :--------------------- |
|  0   | NO_ERROR                       | 업로드 성공.                   |
| 1001 | ERR_UGC_REQUEST_FAILED    | 업로드 요청 실패. 이는 일반적으로 클라이언트의 서명이 만료되었거나 유효하지 않기 때문입니다. App 서명을 다시 신청해야 합니다.         |
| 1002 | ERR_UGC_PARSE_FAILED           | 요청 정보 구문 분석 실패.               |
| 1003 | ERR_UPLOAD_VIDEO_FAILED        | 비디오 업로드 실패.                 |
| 1004 | ERR_UPLOAD_COVER_FAILED        | 커버 이미지 업로드 실패.                 |
| 1005 | ERR_UGC_FINISH_REQUEST_FAILED  | 업로드 요청 취소 실패.               |
| 1006 | ERR_UGC_FINISH_RESPONSE_FAILED | 업로드 종료 요청 응답 오류.               |
| 1007 | ERR_CLIENT_BUSY                | 클라이언트 사용 중(객체가 추가 요청을 처리할 수 없음).      |
| 1008 | ERR_FILE_NOEXIT                | 업로드할 파일 없음.                |
| 1009 | ERR_UGC_PUBLISHING             | 동영상 업로드 중.                |
| 1010 | ERR_UGC_INVALID_PARAM          | 업로드 매개변수 공란.                 |
| 1012 | ERR_UGC_INVALID_SIGNATURE      | 비디오 업로드 signature 공란.        |
| 1013 | ERR_UGC_INVALID_VIDOPATH       | 비디오 파일 경로 공란.              |
| 1014 | ERR_UGC_INVALID_VIDEO_FILE     | 현재 경로에 비디오 파일 없음.           |
| 1015 | ERR_UGC_FILE_NAME              | 동영상 파일 이름 40자 초과 또는 특수 기호가 포함됨. |
| 1016 | ERR_UGC_INVALID_COVER_PATH     | 잘못된 커버 이미지 경로. 파일 없음.       |
| 1017 | ERR_USER_CANCEL                | 사용자 업로드 취소.       |
| 1018 | ERR_UPLOAD_VOD                 | 5MB 미만의 파일 VOD에 직접 업로드 실패.       |


