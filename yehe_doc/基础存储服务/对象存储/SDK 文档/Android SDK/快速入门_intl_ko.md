## 관련 리소스

- SDK 소스 코드는 [XML Android SDK](https://github.com/tencentyun/qcloud-sdk-android)를 참고하십시오.
- 예시 Demo는 [XML Android SDK Demo](https://github.com/tencentyun/qcloud-sdk-android-samples)를 참고하십시오.
- SDK 인터페이스 및 매개변수 문서는 [SDK API 참고](https://cos-android-sdk-doc-1253960454.file.myqcloud.com)를 참고하십시오.
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/Android)를 참고하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md)를 참고하십시오.
- SDK FAQ는 [Android SDK FAQ](https://intl.cloud.tencent.com/document/product/436/38955)를 참고하십시오.

>? XML 버전 SDK 사용 중 함수 또는 메소드가 존재하지 않는 등의 오류 발생 시, XML 버전 SDK를 최신 버전으로 업그레이드한 후 재시도하십시오.
>


## 준비 작업

1. Android 애플리케이션이 필요합니다. 기존의 프로젝트 또는 새로 생성한 프로젝트 모두 가능합니다.
2. Android 애플리케이션의 타깃은 API 레벨 15(Ice Cream Sandwich) 버전 이상이어야 합니다.
3. Tencent Cloud 임시 키를 받을 수 있는 원격 주소가 필요합니다. 임시 키에 관한 설명은 [모바일 애플리케이션 다이렉트 업로드 사례](https://intl.cloud.tencent.com/document/product/436/30618)를 참고하십시오.

## 1단계: SDK 설치

### 방법1: 자동 통합(권장)

>? bintray 리포지토리는 이미 삭제되었으며, COS SDK는 mavenCentral에 마이그레이션되어 있습니다. 참고 경로가 변경되었으니 업데이트 시 새 참고 경로를 사용하십시오.
>

#### mavenCentral 라이브러리 사용

프로젝트 레벨(일반적으로 루트 디렉터리 하위)의 `build.gradle`에 다음을 추가합니다.
```
repositories {
    google()
    // 다음 행 추가
    mavenCentral() 
}
```

#### 표준 버전 SDK

애플리케이션 레벨(일반적으로 app 모듈 하위)의 `build.gradle`에 다음 종속을 추가합니다.
```
dependencies {
	...
    // 다음 행 추가
    implementation 'com.qcloud.cos:cos-android:5.7.+'
}
```

프로젝트에 kotlin 개발을 사용한 경우 Tencent Cloud의 ktx 확장 패키지를 추가할 수 있으며 호환성이 더 높은 API를 제공합니다.
```
dependencies {
	...
    // 다음 행 추가
    implementation 'com.qcloud.cos:cos-ktx:5.6.+'
}
```

#### 라이트 버전 SDK

애플리케이션 레벨(일반적으로 app 모듈 하위)의 `build.gradle`에 다음 종속을 추가합니다.
```
dependencies {
	...
    // 다음 행 추가
    implementation 'com.qcloud.cos:cos-android-lite:5.7.+'
}
```



#### beacon 리포트 기능 비활성화(5.5.8 이상 버전에 적용)

SDK의 품질을 지속적으로 모니터링 및 최적화하여 사용자에게 더 나은 경험을 제공하기 위해 SDK에 [Tencent Beacon](https://beacon.qq.com/) SDK를 도입했습니다.
>? Tencent Beacon은 COS의 요청 성능만을 모니터링하며 서비스 데이터는 리포트하지 않습니다.
>

해당 기능을 비활성화하려면 애플리케이션 레벨(일반적으로 app 모듈 하위)의 `build.gradle`에 beacon 삭제 명령어를 추가하십시오.

```
dependencies {
	...
    implementation ('com.qcloud.cos:cos-android:x.x.x'){
        // 다음 행 추가
        exclude group: 'com.tencent.qcloud', module: 'beacon-android-release'
    }
}
```


### 방법2: 수동 통합

#### 1. 보관된 파일 다운로드

정식 패키지의 최신 버전은 [고속 다운로드 주소](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-android/latest/qcloud-sdk-android.zip)에서 다운로드할 수 있으며, 이전 버전은 [SDK Releases](https://github.com/tencentyun/qcloud-sdk-android/releases)에서 찾을 수 있습니다.

다운로드 후 압축을 해제하면 `jar` 또는 `aar` 패키지가 여러 개 포함된 것을 볼 수 있습니다. 다음은 이에 대한 간단한 설명으로, 필요에 따라 패키지를 선택 및 통합하시기 바랍니다.

필수 라이브러리:
- cosxml: COS 프로토콜 구현
- qcloud-foundation: 기본 라이브러리
- [bolts-tasks](https://github.com/BoltsFramework/Bolts-Android): 3rd party Task 라이브러리
- [okhttp](https://github.com/square/okhttp): 3rd party Networking 라이브러리
- [okio](https://github.com/square/okio): 3rd party IO 라이브러리

옵션 라이브러리:
- beacon: beacon 모바일 분석. SDK 개선에 사용
- LogUtils: 로그 모듈. SDK 개선에 사용
- quic: QUIC 프로토콜. QUIC 프로토콜로 데이터 전송 시 필요

#### 2. 프로젝트에 통합

필요한 패키지를 애플리케이션 모듈의 `libs` 폴더에 넣고, 애플리케이션 레벨(일반적으로 app 모듈 하위)의 `build.gradle` 파일에 다음 종속을 추가합니다.

```
dependencies {
	...
    // 다음 행 추가
    implementation fileTree(dir: 'libs', include: ['*.jar', '*.aar'])
}
```

## 2단계: 권한 설정

### 네트워크 권한

SDK는 COS 서버와 통신을 위해 네트워크 권한이 필요합니다. 애플리케이션 모듈의 `AndroidManifest.xml`에 다음 권한 선언을 추가합니다.

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

### 스토리지 권한

응용 시나리오 중 외부 스토리지에서 파일을 읽고 써야 하는 경우, 애플리케이션 모듈의 `AndroidManifest.xml`에 다음 권한 선언을 추가합니다.

```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

>! Android 6.0(API level 23) 이상에서 실행 시 스토리지 권한 동적 신청이 필요합니다.
>

## 3단계: 사용하기

### 1. 임시 키 획득

`BasicLifecycleCredentialProvider`의 서브 클래스를 실현해 임시 키 요청 및 결과 반환 과정을 구현합니다.

```java
public static class MySessionCredentialProvider
        extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() 
            throws QCloudClientException {

        // 먼저 임시 키 서버로부터 키 정보가 포함된 응답 획득

        // 응답을 분석하여 임시 키 정보 획득
        String tmpSecretId = "SECRETID"; // 임시 키 SecretId
        String tmpSecretKey = "SECRETKEY"; // 임시 키 SecretKey
        String sessionToken = "SESSIONTOKEN"; // 임시 키 Token
        long expiredTime = 1556183496L;//임시 키 유효 기간 타임스탬프. 단위: 초

        //사용자 휴대폰 로컬 시간과의 편차가 너무 커 요청이 만료되지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다.
        // 서버 시간을 서명 시작 시간으로 반환
        long startTime = 1556182000L; //임시 키 유효 시작 시간. 단위: 초

        // 최종적으로 임시 키 정보 객체 반환
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey,
                sessionToken, startTime, expiredTime);
    }
}
```

여기서는 클래스 이름을 `MySessionCredentialProvider`로 가정합니다. 인스턴스를 초기화해 SDK에 키를 제공합니다.

```java
QCloudCredentialProvider myCredentialProvider = new MySessionCredentialProvider();
```

#### 영구 키로 로컬 디버깅 진행

Tencent Cloud의 영구 키로 개발 단계에 있는 로컬 디버깅을 진행할 수 있습니다. **해당 방법은 키가 유출될 리스크가 있으니 런칭 전 반드시 임시 키로 대체하십시오.**

```java
String secretId = "SECRETID"; //영구 키 secretId
String secretKey = "SECRETKEY"; //영구 키 secretKey

// keyDuration: 요청의 키 유효 시간, 단위: 초
QCloudCredentialProvider myCredentialProvider = 
    new ShortTimeCredentialProvider(secretId, secretKey, 300);
```

### 2. COS Service 초기화

사용자가 키를 제공하는 인스턴스 `myCredentialProvider`를 사용하려면 `CosXmlService` 인스턴스를 초기화해야 합니다.

`CosXmlService`는 COS에 액세스하는 모든 인터페이스를 제공하며, **프로그램 싱글톤**으로 사용하는 것을 권장합니다.

```java
// 버킷의 소재 리전 약칭. 예: 광저우 리전 ap-guangzhou
String region = "COS_REGION";

// CosXmlServiceConfig 객체 생성. 필요에 따라 기본 매개변수 설정 수정
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
        .setRegion(region)
        .isHttps(true) // HTTPS 요청 사용. 기본값: HTTP 요청
        .builder();

// COS Service를 초기화해 인스턴스 획득
CosXmlService cosXmlService = new CosXmlService(context, 
    serviceConfig, myCredentialProvider);
```

>? 버킷의 각 리전에 대한 약칭은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.
>

#### ktx 패키지로 COS Service 초기화

ktx를 사용하면 초기화 코드가 다음과 같이 간략합니다.

```kotlin
val cos = cosService(context = application.applicationContext) {

    configuration {
        setRegion("ap-guangzhou")
        isHttps(true)
    }

    credentialProvider {
        lifecycleCredentialProvider {
            // fetch credential from backend
            // ...
            return@lifecycleCredentialProvider SessionQCloudCredentials(
                    "temp_secret_id",
                    "temp_secret_key",
                    "session_token",
                    1556183496
            )
        }
    }
}
```

## 4단계: COS 서비스 액세스

### 객체 업로드

SDK는 로컬 파일, 바이너리 데이터, Uri, 입력 스트림을 지원합니다. 로컬 파일 업로드 예시는 다음과 같습니다.

[//]: # ".cssg-snippet-transfer-upload-file"
```java
// TransferConfig 초기화. 본 예시는 기본 설정을 사용합니다. 사용자 정의할 경우에는 SDK 인터페이스 문서를 참고하십시오.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); //로컬 파일의 절대 경로
// 멀티파트 업로드를 초기화한 UploadId가 존재하는 경우 해당하는 uploadId 값을 대입하여 계속 전달합니다. 존재하지 않는 경우 null을 대입합니다.
// 이번 업로드 작업의 uploadid는 TransferStateListener 콜백에서 가져올 수 있습니다.
String uploadId = null; 

// 파일 업로드
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        srcPath, uploadId);

//업로드 진행 콜백을 설정합니다. 여기에서 업로드 재개를 위한 uploadId를 얻을 수 있습니다.
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
        uploadId = cosxmlUploadTask.getUploadId();  
    }
});
//반환 결과 콜백 설정
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                        CosXmlClientException clientException,
                        CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
//작업 상태 콜백 설정. 작업 진행 과정을 확인할 수 있습니다.
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

#### ktx 패키지로 객체 업로드

ktx를 사용하는 경우 아래 업로드 예시 코드를 참고하십시오.

```kotlin
// 본 예시는 viewModel의 ktx 확장 사용
// viewModelScope는 viewmodel의 자체 coroutine scope
viewModelScope.launch {
    val `object` = cosObject {
        bucket = cosBucket {
            service = cosXmlService
            name = "examplebucket-1250000000"
        }
        key = "exampleObject"
    }
    // 로컬 예시 파일
    val sourceFile = File(appContext.externalCacheDir, "sourceFile")

    try {
        // upload 방법: suspend function
        val result = `object`.upload(
            localFile = sourceFile,
            progressListener = { complete, target ->
                Log.d("cosxmlktx", "upload onProgress:" +
                                " $complete / $target")
            },
            transferStateListener = { state ->
                Log.d("cosxmlktx", "upload state is : $state")
            }
        )

    } catch (e : Exception ) {
        e.printStackTrace()
    }

}
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java)를 참고하시기 바랍니다.
>- 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 [사전 서명된 링크 생성](https://intl.cloud.tencent.com/document/product/436/37680) 문서를 참고하십시오. 파일의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 시간이 있습니다.

### 객체 다운로드

[//]: #	".cssg-snippet-transfer-download-object"
```java
// 고급 다운로드 인터페이스는 중단된 지점부터 이어 올리기를 지원합니다. 따라서 다운로드 전에 HEAD를 요청하여 파일 정보를 획득하시기 바랍니다.
// 임시 키 또는 서브 계정을 사용해 액세스하는 경우 권한 리스트에 HeadObject 권한이 포함되어 있는지 확인하십시오.

// TransferConfig 초기화. 본 예시는 기본 설정을 사용합니다. 사용자 정의할 경우에는 SDK 인터페이스 문서를 참고하십시오.
TransferConfig transferConfig = new TransferConfig.Builder().build();
//TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID.
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키
//로컬 디렉터리 경로
String savePathDir = context.getExternalCacheDir().toString();
//로컬에 저장할 파일명. 입력하지 않는 경우(null) COS의 파일명과 동일
String savedFileName = "exampleobject";

Context applicationContext = context.getApplicationContext(); // application
// context
COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext,
        bucket, cosPath, savePathDir, savedFileName);

//다운로드 진행률 콜백 설정
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
//반환 결과 콜백 설정
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLDownloadTask.COSXMLDownloadTaskResult cOSXMLDownloadTaskResult =
                (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                        CosXmlClientException clientException,
                        CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
//작업 상태 콜백 설정. 작업 진행 과정을 확인할 수 있습니다.
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

#### ktx 패키지로 객체 다운로드

ktx를 사용하는 경우 아래 다운로드 예시 코드를 참고하십시오.

```kotlin
// 본 예시는 viewModel의 ktx 확장 사용
// viewModelScope는 viewmodel의 자체 coroutine scope
viewModelScope.launch {
    val `object` = cosObject {
        bucket = cosBucket {
            service = cos
            name = "examplebucket-1250000000"
        }
        key = "exampleObject"
    }

    try {
        // download 방법: suspend function
        val result = `object`.download(
            context = appContext,
            destDirectory = appContext.externalCacheDir!!,
            progressListener = { complete, target ->
                Log.d("cosxmlktx", "download onProgress: " +
                        "$complete / $target")
            },
            transferStateListener = { state ->
                Log.d("cosxmlktx", "download state is : $state")
            }
        )

    } catch (e : Exception ) {
        e.printStackTrace()
    }

}
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java)를 참고하십시오.
>- 고급 다운로드 인터페이스는 중단된 지점부터 이어 올리기를 지원합니다. 따라서 다운로드 전에 HEAD를 요청하여 파일 정보를 획득하시기 바랍니다. 임시 키 또는 서브 계정을 사용해 액세스하는 경우 권한 리스트에 HeadObject 권한이 포함되어 있는지 확인하십시오.
>
