## 빠른 액세스

### 액세스 준비

1. SDK는 Android 2.2 및 그 이상 버전의 휴대폰 os를 지원합니다.
2. 휴대폰은 반드시 네트워크(GPRS, 3G 또는 WIFI 등)에 연결되어야 합니다.
3. 휴대폰에 저장 공간이 없을 수는 있지만, 그럴 경우 일부 기능을 정상 작동할 수 없습니다.
4. [COS 콘솔](https://console.cloud.tencent.com/cos4/secret)에서 APPID, SecretId, SecretKey를 획득합니다.

>?문서에서 나오는 SecretId, SecretKey, Bucket 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

### SDK 통합

#### 자동 통합(**추천**)

1, 사용자의 프로젝트 루트 디렉터리의 build.gradle 파일에 maven 레지스트리를 추가합니다.

```
allprojects {

    repositories {
        ...
        // 다음 maven 레지스트리 주소 추가
        maven {
            url "https://dl.bintray.com/tencentqcloudterminal/maven"
        }
    }
}
```

2, 응용프로그램 루트 디렉터리의 build.gradle에 의존을 추가합니다.
```
dependencies {
	...
    // 이 행 추가
    compile 'com.tencent.qcloud:cosxml:5.4.19'
}
```

3, 업로드, 다운로드와 복사 기능만 사용하면, 간소판 SDK를 사용하여 상기 절치2의 의존을 다음 의존으로 변경할 수 있습니다.

```
dependencies {
	...
    // 이 행 추가
    compile 'com.tencent.qcloud:cosxml-lite:5.4.19'
}
```

4, 지속적으로 SDK 품질을 추적하고 최적화하여 사용자에게 더욱 훌륭한 사용 체험을 제공하기 위해, SDK에 Tencent 모바일 앱 분석(mta)을 통합하였습니다. 이 기능을 종료하려면, 응용프로그램 루트 디렉터리의 build.gradle에 다음 의존을 추가하십시오.

```
dependencies {
	...
    // 이 행 추가
   compile ('com.tencent.qcloud:cosxml:5.4.19'){
        exclude group:'com.tencent.qcloud', module: 'mtaUtils' //mta 보고 기능 종료
    }
}
```

간소판 SDK 코드는 다음과 같습니다.
```
dependencies {
	...
    // 이 행 추가
    compile ('com.tencent.qcloud:cosxml-lite:5.4.19'){
        exclude group:'com.tencent.qcloud', module: 'mtaUtils' //mta 보고 기능 종료
    }
}
```
#### 수동 통합

프로젝트에 다음 jar 패킷을 가져오고, libs 폴더에 저장해야 합니다.

- cos-android-sdk.jar
- qcloud-foundation.jar
- bolts-tasks.jar
- okhttp.jar(3.9 및 그 이상 버전)
- okio.jar(1.13.0 및 그 이상 버전)
- mtaUtils.jar
- mid-sdk.jar
- mta-android-sdk.jar
- logUtils.aar

[COS XML Android SDK-release](https://github.com/tencentyun/qcloud-sdk-android/releases)에서 모든 jar 패킷을 다운로드할 수 있습니다. 최신 릴리즈 채킷을 사용하길 권장합니다.

### 권한 구성

해당 SDK를 사용하려면 네트워크 연결 및 스토리지 등 관련 접근 권한이 필요합니다. AndroidManifest.xml에 다음 권한 선언(Android 5.0 이상 버전에 동적 권한 필요)을 추가할 수 있습니다.
```html
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

### 기타 리소스

**소스 코드와 예시 프로젝트**

COS Android SDK 관련 소스 코드는 [COS Android SDK Github 주소](https://github.com/tencentyun/qcloud-sdk-android)를 참조하십시오.
예시 데모는 [COS Android SDK 예시 프로젝트](https://github.com/tencentyun/qcloud-sdk-android-samples)를 참조하십시오.

**업데이트 로그**

COS Android SDK 업데이트 로그는 [COS Android SDK 업데이트 로그](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md)를 참조하십시오.

## 시작 가이드

### 초기화

COS 서비스 관련 요청 실행 전, 우선 CosXmlService 객체를 인스턴스화해야 합니다. 구체적인 절차는 다음과 같습니다.

#### 구성 초기화

**CosXmlServiceConfig**는 COS 서비스의 구성 사항입니다. 다음 코드를 사용하여 초기화할 수 있습니다.

```
String appid = "COS 서비스 APPID";
String region = "버킷 소재 지역";

//CosXmlServiceConfig 객체를 생성하고 필요에 따라 기본 구성 매개변수를 수정합니다.
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setAppidAndRegion(appid, region)
       .setDebuggable(true)
       .builder();
```

#### 권한 부여 초기화

터미널에서 영구 키를 통해 신분 인증을 진행하면 키 누설 리스크가 존재하게 됩니다. COS 터미널 SDK(Android/IOS)는 모두 임시 키를 통한 권한 부여 요청을 지원하기 때문에, 임시 키 반환 서비스 하나를 구축하면 터미널 COS 요청에 권한을 부여할 수 있습니다. 이러한 방식을 사용하길 강력하게 권장합니다. 구체적인 내용은 [모바일 응용프로그램 스트레이트 패스 실천](https://cloud.tencent.com/document/product/436/9068)을 참조하십시오.

#### 임시 키를 통해 권한 부여(추천)

- 표준 응답 본문 권한부여

임시 키 서비스를 이미 구축하고 STS SDK에서 획득한 JSON 데이터를 임시 응답 본문으로 사용하였다면(cossign은 이러한 방식을 채택하였음), 다음 코드를 사용하여 COS SDK에서 권한 부여 클래스를 생성할 수 있습니다.
```
/**
 * 권한부여 서비스의 url 주소 획드
 */
URL url = null; // 백 엔드 권한 부여 서비스의 url 주소
try {
    url = new URL("your_auth_server_url");
} catch (MalformedURLException e) {
    e.printStackTrace();
}

/**
 * {@link QCloudCredentialProvider} 객체를 초기화하여 SDK에 임시 키를 제공합니다.
 */
QCloudCredentialProvider credentialProvider = new SessionCredentialProvider(new HttpRequest.Builder<String>()
                .url(url)
                .method("GET")
                .build());
```
>!표준 응답 본문 권한부여 방식에서 서명 시작 시간은 휴대폰 현지 시간이기 때문에 휴대폰 현지 시간 편차가 너무 크면(10분 이상), 서명 오류를 초래할 수 있습니다. 이럴 때 다음 사용자 지정 응답 본문 권한 부여를 사용할 수 있습니다.

- 사용자 지정 응답 본문 권한부여

더 큰 유연성을 얻고자 할 경우 예를 들어 임시 키 서비스의 HTTP 응답 본문을 사용자가 지정하여 단말에 서버 시간을 반환하여 서명의 시작 시간으로 합니다. 사용자 핸드폰이 로컬 시간과의 과도한 편차로 인한 서명 오류를 방지하고자 하는 경우 또는 기타 프로토콜을 사용하여 단말과 서버 사이의 통신을 진행하고자 할 경우 `BasicLifecycleCredentialProvider` 클래스를 계승하여 해당 `fetchNewCredentials()`를 구현할 수 있습니다.

우선 `MyCredentialProvider` 클래스 하나를 정의합니다.

```java
public class MyCredentialProvider extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {

        // 우선 임시 키 서버에서 서명 정보를 포함한 응답을 획득합니다
        ....

        // 다음 응답 내용을 해석하고 키 정보를 획득합니다
        String tmpSecretId = ...;
        String tmpSecretKey = ...;
        String sessionToken = ...;
        long expiredTime = ...;

        // 서버 시간을 반환하여 서명의 시작 시간으로 합니다
        long beginTime = ...;

        // todo something you want

        // 마지막으로 임시 키 정보 객체를 반환합니다
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey, sessionToken, beginTime, expiredTime);
    }
}
```

그런 다음 정의한 `MyCredentialProvider` 인스턴스를 이용하여 요청을 권한 부여합니다.

```
/**
 * * {@link QCloudCredentialProvider} 객체를 초기화하여 SDK에 임시 키를 제공합니다.
 */
QCloudCredentialProvider credentialProvider = new MyCredentialProvider();
```

#### 영구 키를 통해 권한부여

임시 키 서비스를 구축하지 않았다면 영구 키를 사용하여 권한부여 클래스를 초기화할 수 있습니다. 해당 방식은 키 누설 리스크가 존재하기 때문에 **이러한 방식 사용을 추천하지 않고**, 보안 환경에서 임시 테스트 시에만 사용하길 권장합니다. 코드는 다음과 같습니다.

```
String secretId = "클라우드 API 키 SecretId";
String secretKey ="클라우드 API 키 SecretKey";

/**
 * {@link QCloudCredentialProvider} 객체를 초기화하여 SDK에 임시 키를 제공합니다.
 */
QCloudCredentialProvider credentialProvider = new ShortTimeCredentialProvider(secretId,
                secretKey, 300);
```


#### COS 서비스 클래스 초기화

**CosXmlService**는 COS 서비스 클래스로 각종 COS 서비스를 작업하는 데 사용할 수 있습니다. 이미 구성 클래스와 권한부여 클래스를 인스턴스화하면, COS 서비스 클래스를 간편하게 인스턴스화할 수 있습니다. 구체적인 코드는 다음과 같습니다.

````java
CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, qCloudCredentialProvider);
````

### 파일 업로드

**TransferManager**, **COSXMLUploadTask**는 간편 업로드, 멀티파트 업로드 API의 비동기 요청을 캡슐화하였으며, 업로드 요청 일시 정지, 복구 및 취소를 지원함과 동시에 전송 재개 기능을 지원합니다. 이러한 방식을 사용하여 파일을 업로드하길 추천합니다. 예제 코드는 다음과 같습니다.

```java

// TransferConfig 초기화
TransferConfig transferConfig = new TransferConfig.Builder().build();
/**
특별 요구 사항이 있을 경우, 다음과 같이 초기화를 사용자 지정할 수 있습니다. 예를 들어, 해당 파일이 >= 2M일 때, 멀티파트 업로드를 사용하며 파트 크기는 1M이며, 소스 파일이 5M보다 클 때 멀티파트 복사를 사용하며, 파트의 크기는 5M임을 설정할 수 있습니다.
TransferConfig transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) // 멀티파트 복사 사용 여부를 판단하기 위한 파일 최소 크기
        .setSliceSizeForCopy(5 * 1024 * 1024) //멀티파트 복사 시 파트 크기
        .setDivisionForUpload(2 * 1024 * 1024) // 멀티파트 업로드 사용 여부를 판단하기 위한 파일 최소 크기
        .setSliceSizeForCopy(1024 * 1024) //멀티파트 업로드 시 파트 크기
        .build();
*/

//TransferManager 초기화
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "버킷 이름";
String cosPath = "객체 키"; //COS로 저장되는 파일의 절대 경로로 형식은 cosPath = "test.txt"와 같습니다.
String srcPath = "로컬 파일의 절대 경로"; // 예: srcPath=Environment.getExternalStorageDirectory().getPath() + "/test.txt".
String uploadId = null; //멀티파트 업로드를 초기화한 UploadId가 존재할 경우, 해당 uploadId값을 배정하여 전송 재개하고, 그렇지 않을 경우 null을 배정합니다.
//파일 업로드
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);

/**
* 바이트 배열을 업로드할 경우, TransferManager의 upload(string, string, byte[]) 방법을 호출하여 구현할 수 있습니다.
* byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, bytes);
*/

/**
* 바이트 스트림을 업로드할 경우, TransferManager의 upload(String, String, InputStream) 방법을 호출하여 구현할 수 있습니다.；
* InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, inputStream);
*/


//업로드 진행률 콜백 설정
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
//반환 결과 콜백 설정
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//태스크 상태 콜백 설정, 태스크 과정을 조회할 수 있습니다.
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
특별 요구 사항이 있을 경우, 다음 작업을 할 수 있습니다.
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
 putObjectRequest.setRegion(region). //버킷 소재 지역 설정
 putObjectRequest.setNeedMD5(true). //Md5 검사 사용 여부
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
*/

//업로드 취소
cosxmlUploadTask.cancel();


//업로드 일시 정지
cosxmlUploadTask.pause();

//업로드 복구
cosxmlUploadTask.resume();

```
### 파일 다운로드
**TransferManager**, **COSXMLDownloadTask**는 다운로드 API의 비동기 요청을 캡슐화하였으며, 업로드 요청 일시 정지, 복구 및 취소를 지원함과 동시에 전송 재개 기능을 지원합니다. 이러한 방식을 사용하여 파일을 다운로드하길 권장합니다. 예제 코드는 다음과 같습니다.
```java
Context applicationContext = "application 콘텍스트"； // getApplicationContext()
String bucket = "버킷 이름"; //파일 소재 버킷
String cosPath = "객체 키"; //COS로 저장되는 파일의 절대 경로로 형식은 cosPath = "test.txt"와 같습니다.
String savedDirPath = "로컬로 다운로드된 파일의 폴더 경로"；
String savedFileName = "로컬로 다운로드된 파일의 파일 이름"；//입력하지 않을 경우(null), cos의 파일 이름과 같습니다.
//파일 다운로드
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(applicationContext, bucket, cosPath, savedDirPath, savedFileName);
//다운로드 진행률 콜백 설정
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
//반환 결과 콜백 설정
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//태스크 상태 콜백 설정, 태스크 과정을 조회할 수 있습니다.
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
특별 요구 사항이 있을 경우, 다음 작업을 할 수 있습니다.
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, localDir, localFileName);
getObjectRequest.setRegion(region); //버킷 소재 지역 설정
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(context, getObjectRequest);
*/

//다운로드 취소
cosxmlDownloadTask.cancel();

//다운로드 일시 정지
cosxmlDownloadTask.pause();

//다운로드 복구
cosxmlDownloadTask.resume();

```
### 파일 복사
**TransferManager**, **COSXMLCopyTask**는 간편 복사, 멀티파트 복사 API의 비동기 요청을 캡슐화하였으며, 복사 요청 일시 정지, 복구 및 취소를 지원합니다. 이러한 방식을 사용하여 파일을 복사하길 추천합니다. 예제 코드는 다음과 같습니다.
```java
String bucket = "버킷 이름"; //대상 파일의 버킷
String cosPath = "객체 키"; //COS로 저장되는 대상 파일의 절대 경로로 형식은 cosPath = "test.txt"와 같습니다.
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(
                "소스 파일 버킷 소재 appid", "소스 파일 버킷", "소스 파일 버킷 소재 지역", "소스 파일의 객체 키").// 소스 파일 소재 cos의 위치 설명
//파일 복사
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath, copySourceStruct);
//반환 결과 콜백 설정
cosxmlCopyTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//태스크 상태 콜백 설정, 태스크 과정을 조회할 수 있습니다.
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });
/**
특별 요구 사항이 있을 경우, 다음 작업을 할 수 있습니다.
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
copyObjectRequest.setRegion(region); //버킷 소재 지역 설정
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(copyObjectRequest);
*/

//복사 취소
cosxmlCopyTask.cancel();


//복사 일시 정지
cosxmlCopyTask.pause();

//복사 복구
cosxmlCopyTask.resume();
```
