JSON Android SDK와 XML Android SDK의 문서를 세심하게 비교해 보면 간단한 증분이 아님을 발견할 수 있습니다. XML Android SDK는 구조와 가용성, 안전성에서 대폭 향상할 뿐만 아니라 사용 간편성과 전송 성능에서 대폭 개선되었습니다. XML Android SDK로 업그레이드하려면 다음 가이드를 참조하여 SDK 업그레이드 작업을 완료하십시오.

## 기능 비교

아래 표는 JSON Android SDK와 XML Android SDK의 주요 기능을 비교한 것입니다.

| 기능       | XML Android SDK         | JSON Android SDK                         |
| -------- | :------------: | :------------------:    |
| 파일 업로드 | 로컬 파일, 바이트 스트림, 입력 스트림 업로드 지원<br>기본으로 업로드 덮어쓰기함<br>업로드 모드 스마트 지정<br>간편 업로드 최대 5G 지원<br>멀티파트 업로드 최대 48.82TB(50,000GB) 지원 | 로컬 파일 업로드만 지원<br>덮어쓰기 여부 선택 가능<br>간편 업로드 또는 멀티파트 업로드의 선택 수동 구성 필요<br>간편 업로드 최대 20MB 지원<br>멀티파트 업로드 최대 64GB 지원|
| 파일 삭제 | 배치 삭제 지원 | 단일 파일 삭제만 지원 |
| 버킷 기본 조작 | 버킷 생성<br>버킷 획득<br>버킷 삭제   | 지원하지 않음 |
| 버킷 ACL 조작 | 버킷 ACL 설정<br>버킷 ACL 획득<br>버킷 ACL 삭제   | 지원하지 않음 |
| 버킷 수명 주기 | 버킷 수명 주기 생성<br>버킷 수명 주기 획득<br>버킷 수명 주기 삭제 | 지원하지 않음 |
| 디렉터리 조작 | API가 별도로 제공되지 않음   | 디렉터리 생성<br>디렉터리 조회<br>디렉터리 삭제 |

## 업그레이드 절차
다음 절차에 따라 Android SDK를 업그레이드하십시오.

**1. Android SDK 업데이트**

COS XML Android SDK를 [Bintray](https://bintray.com)의 maven 패킷 관리 플랫폼에 배포합니다. 자동 통합 방식을 사용하여 업데이트를 진행하길 권장합니다.

프로젝트 루트 디렉터리의 build.gradle 파일에 maven 레지스트리를 추가합니다. 코드는 다음과 같습니다.

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

응용프로그램 루트 디렉터리의 build.gradle에 의존을 추가합니다. 코드는 다음과 같습니다.

```
dependencies {
	...
    // 이 행 추가
    compile 'com.tencent.qcloud:cosxml:5.4.+'
}
```

수동 jar 패킷 의존도 선택할 수 있으며, [COS XML Android SDK-release](https://github.com/tencentyun/qcloud-sdk-android/releases)에서 모든 jar 패킷을 다운로드할 수 있습니다.

**2. SDK 인증 방식 변경**

JSON Android SDK의 경우, 백 엔드에서 서명을 계산한 뒤, 다시 클라이언트에 반환하여 사용해야 합니다. 그러나 XML Android SDK의 경우, 새로운 인증 알고리즘이 사용되었기 때문에 백 엔드에서 임시 키(STS) 방안을 액세스하길 강력하게 권장합니다. 해당 방안은 서명 계산 과정을 이해할 필요 없이 서버에서 CAM을 액세스하고 획득한 임시 키를 클라이언트에 반환해 SDK에 설정하기만 하면 되며, SDK는 키 관리와 서명 계산을 수행합니다. 임시 키는 일정 시간 후 자동 실효되는 반면 영구 키는 노출되지 않습니다.
서로 다른 세분성에 따라 액세스 권한을 제어할 수도 있습니다. 구체적인 절차는 [모바일 응용프로그램 직접 전송 사례](https://cloud.tencent.com/document/product/436/9068) 및 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오.

여전히 백 엔드에서 수동으로 서명을 계산하고 다시 프론트 엔드에 반환하는 방식을 사용하는 경우, 서명 알고리즘에 변화가 생겼다는 점에 유의하십시오. 서명은 더 이상 1회 및 여러 차례 서명을 구분하지 않고 서명의 유효기간 설정을 통해 보안성을 보장합니다. [XML 서명 요청](https://intl.cloud.tencent.com/document/product/436/7778) 파일을 참고하여 서명을 업데이트하십시오.

**3. SDK 초기화 변경**

XML Android SDK 중, 초기화 API에는 일정 변경 사항이 있습니다.

* 구분하기 위해 `CosXmlServiceConfig`으로 `COSClientConfig`을, `CosXmlService`로 `COSClient`를 대체하였지만 효과는 동일합니다.
* 1개의 유효 키를 제공하기 위해 초기화 시 1개의 키 제공자 `QCloudCredentialProvider`를 인스턴스화해야 합니다. 임시 키 사용을 권장합니다.

**JSON SDK의 초기화 방식은 다음과 같습니다:**

```
//COSClientConfig 객체를 생성하고, 필요에 따라 기본 설정의 구성 매개변수를 수정합니다.
COSClientConfig config = new COSClientConfig();
//지역 설정
config.setEndPoint(COSEndPoint.COS_GZ);

Context context = getApplicationContext()；
String appid =  "Tencent Cloud에 등록한 appid";
String peristenceId = "지속화 ID";

//COSlient 객체를 생성하여 COS 작업을 구현합니다.
COSClient cos = new COSClient(context,appid,config,peristenceId);
```

**XML SDK의 초기화 방식은 다음과 같습니다:**

```
String appid = "1250000000";
String region = "ap-guangzhou"; 

//CosXmlServiceConfig 객체를 생성하고 필요에 따라 기본 구성 매개변수를 수정합니다.
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setAppidAndRegion(appid, region)
       .builder();
       
/**
 * 권한부여 서비스의 url 주소 획드
 */
URL url = null; 
try {
    url = new URL("your_auth_server_url"); // 백 엔드 권한 부여 서비스의 url 주소
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
                
                
CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, credentialProvider);
```


**4. 버킷 이름 및 가용 영역 약칭 변경**

XML SDK의 버킷 이름과 가용 지역의 약칭은 JSON SDK와 다르므로 상응하는 변경을 진행해야 합니다.

**버킷 Bucket**

XML Android SDK 버킷 이름은 사용자 지정 문자열과 APPID 두 부분으로 구성되며 이들 사이에 대시 '-'로 서로 연결합니다. 예: `examplebucket-1250000000`. 그 중 `examplebucket`은 사용자 지정 문자열이고, `1250000000`은 APPID입니다.

>?APPID는 Tencent Cloud 계정의 계정 식별자 중 하나로 클라우드 리소스를 연결하는 데 사용됩니다. 사용자가 Tencent Cloud 계정 신청에 성공하면, 시스템은 사용자를 위해 APPID 1개를 분배합니다. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)을 통해 [계정 정보]에서 APPID를 조회할 수 있습니다.

버킷 구성 시, 다음 예제 코드를 참조하십시오.

```
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject.doc";
String srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject.doc";
//파일 업로드
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);
```

**버킷 가용 영역 약칭 Region**

XML Android SDK의 버킷 가용 지역 약칭이 변경되었으며, 아래 테이블은 JSON Android SDK와 XML Android SDK에서 각기 다른 지역의 대응 관계를 열거하였습니다.

| 지역       | XML Android SDK 지역 약칭         | JSON Android SDK 지역 약칭                         |
| -------- | ------------ | ---------------------------------------- |
| 베이징 1지역(화북) | ap-beijing-1 | tj |
| 베이징       | ap-beijing   | bj |
| 상하이(화동)   | ap-shanghai  | sh |
| 광저우(화남)   | ap-guangzhou | gz |
| 청두(서남)   | ap-chengdu   | cd |
| 충칭       | ap-chongqing | 없음 |
| 싱가포르      | ap-singapore | sgp |
| 홍콩       | ap-hongkong  | hk |
| 토론토      | na-toronto   | ca |
| 프랑크푸르트     | eu-frankfurt | ger |
| 뭄바이       | ap-mumbai    | 없음 |
| 서울       | ap-seoul     | 없음 |
| 실리콘 밸리       | na-siliconvalley     | 없음 |
| 버지니아       | na-ashburn     | 없음 |
| 방콕       | ap-bangkok     | 없음 |
| 모스크바       | eu-moscow     | 없음 |

초기화 시, 버킷 소재 지역 약칭을 `CosXmlServiceConfig`으로 설정하십시오.

```
String appid = "1250000000";
String region = "ap-guangzhou"; 

CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setAppidAndRegion(appid, region)
       .builder();
```

**5. API 변경**

XML SDK로 업그레이드한 뒤, 일부 작업의 API가 변경되었습니다. 실제 수요에 따라 그에 맞게 변경하십시오. 동시에 API를 캡슐화하여 SDK 사용 간편성을 높였습니다. 구체적인 내용은 예시와 [API 문서](https://cloud.tencent.com/document/product/436/11238)를 참조하십시오.

API 변경 내용은 다음의 세 가지입니다.

**1)독립적인 디렉터리 API 없음**

XML SDK에서는 별도의 디렉토리 API를 더 이상 제공하지 않습니다. COS 자체가 파일 폴더와 디렉터리 개념이 없으며 COS는 업로드 객체 project/a.txt를 업로드하여 project 폴더를 만들지 않습니다.
사용자의 사용 습관을 고려하여 COS는 콘솔, COS browser 등 그래픽 도구에서 「폴더」또는「디렉터리」 디스플레이 방식을 시뮬레이션하였습니다. 이는 키 값이 project/, 내용이 비어 있는 객체 1개를 생성하고 전통 폴더의 디스플레이 방식을 시뮬레이션함으로써 구현하였습니다.

예: 객체 project/doc/a.txt를 업로드합니다. 구분 문자 /는 「폴더」의 디스플레이 방식을 시뮬레이션하게 되기 때문에 콘솔에 「폴더」project와 doc이 나타나게 됩니다. 그 중 doc는 project의 하위 「폴더」이며 a.txt를 포함합니다.

따라서 단지 파일 업로드 시나리오의 경우, 바로 업로드하면 되며, 먼저 폴더를 생성할 필요가 없습니다.

적용 시나리오에 폴더의 개념이 있으면 폴더를 생성하는 기능을 제공해야 합니다. 경로가 '/'로 끝나는 0KB 파일 하나를 업로드하면 됩니다. 그러면 `GetBucket` API를 사용했을 때 해당 파일을 폴더로 할 수 있습니다.


**2)TransferManager**

XML SDK에 업로드, 다운로드와 복사 작업을 캡슐화하였으며 `TransferManager`라는 이름을 지정하였을 뿐만 아니라 API의 설계와 전송 성능을 최적화하였으니 바로 사용하길 권장합니다. `TransferManager`의 주요 특징은 다음과 같습니다.

* 업로드 다운로드 과정의 일시 정지와 복원을 지원합니다.
* 파일 크기에 따라 간편 업로드 또는 멀티파트 업로드를 스마트하게 선택할 수 있습니다. 판단 기준/임계값을 설정할 수 있습니다.
* 태스크 상태 수신을 지원합니다.

`TransferManager`를 사용하여 업로드한 예제 코드는 다음과 같습니다.

```
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
String cosPath = "객체 키"; // COS로 저장되는 파일의 절대 경로로 형식은 cosPath = "exampleobject.doc"와 같습니다.
String srcPath = "로컬 파일의 절대 경로"; // 예: srcPath=Environment.getExternalStorageDirectory().getPath() + "/exampleobject.doc".
String uploadId = "멀티파트 업로드의 UploadId";//업로드 재개에 사용되며, 없으면 null이 됩니다.
//파일 업로드
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);
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
 putObjectRequest.setRegion(region); //버킷 소재 지역 설정
 putObjectRequest.setSign(600); //서명 유효 기간 설정
 putObjectRequest.setNeedMD5(true); //Md5 검사 사용 여부
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
*/

//업로드 취소
cosxmlUploadTask.cancel();


//업로드 일시 정지
cosxmlUploadTask.pause();

//업로드 복구
cosxmlUploadTask.resume();
```

**3) API 새로 추가**

XML Android SDK는 새로 추가된 API로 요구에 따라 호출할 수 있습니다. 다음을 포함합니다.

* 버킷 작업, 예 PutBucketRequest, GetBucketRequest, ListBucketRequest 등.
* 버킷 ACL의 작업, PutBucketACLRequest, GetBucketACLRequest 등.
* 버킷의 수명 주기 작업, PutBucketLifecycleRequest, GetBucketLifecycleRequest 등.

구체적인 내용은 [Android SDK API 문서](https://cloud.tencent.com/document/product/436/11238)를 참조하십시오.

