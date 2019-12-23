JSON Java SDK과 XML Java SDK의 문서를 자세히 비교해보면, 간단한 증분 업데이트가 아니라는 것을 알 수 있습니다. XML Java SDK는 아키텍처, 가용성 및 안전성 면에서 크게 향상되었으며, 사용 편의성, 견고성 그리고 성능에서도 크게 개선하였습니다. XML Java SDK로 업그레이드하려면 아래 가이드를 참조하여 Java SDK의 업그레이드 작업을 완료하십시오.

## 기능 비교

| 기능       | XML Java SDK         | JSON Java SDK                         |
| -------- | :------------: | :------------------:    |
| 파일 업로드 | 로컬 파일, 바이트 스트림, 입력 스트림 업로드 <br>덮어쓰기 업로드<br>스마트한 업로드 모드 판단: 간편 업로드 최대 5GB 지원<br>멀티파트 업로드 최대 48.82TB(50,000GB) 지원| 로컬 파일 업로드만 지원<br>덮어쓰기 여부 선택 가능<br>간편 업로드 또는 멀티파트 업로드 수동 선택<br>간편 업로드 최대 20MB 지원<br>멀티파트 업로드 최대 64GB 지원 |
| 파일 삭제 | 배치 삭제 지원 | 단일 파일 삭제만 지원 |
| 버킷 기본 조작 | 버킷 생성<br>버킷 획득<br>버킷 삭제   | 지원하지 않음 |
| 버킷 ACL 조작 | 버킷 ACL 설정<br>버킷 ACL 설정 획득<br>버킷 ACL 설정 삭제   | 지원되지 않음 |
| 버킷 수명 주기 | 버킷 수명 주기 생성<br>버킷 수명 주기 획득<br>버킷 수명 주기 삭제 | 지원하지 않음 |
| 디렉터리 조작 | API가 별도로 제공되지 않음   | 디렉터리 생성<br>디렉터리 조회<br>디렉터리 삭제 |

## 업그레이드 절차
다음 절차에 따라 Java SDK를 업그레이드하십시오.

**1. Java SDK 업데이트**

XML Java SDK는 [maven](https://mvnrepository.com/artifact/com.qcloud/cos_api) 중앙 리포지터리에 배포되며, maven을 사용하여 종속성 방식 가져오기를 자동 관리할 것을 권장합니다.

maven 프로젝트의 pom.xml 파일에 다음 종속성을 추가합니다.

```xml
<!-- https://mvnrepository.com/artifact/com.qcloud/cos_api -->
<dependency>
    <groupId>com.qcloud</groupId>
    <artifactId>cos_api</artifactId>
    <version>5.x.x</version>
</dependency>

```

물론 [maven](https://mvnrepository.com/artifact/com.qcloud/cos_api) 중앙 리포지터리에서 대응하는 jar 패키지 버전을 직접 다운로드하여 수동으로 프로젝트에 추가할 수도 있습니다.


#### 2. 버킷 이름과 가용 영역 약칭 변경

XML Java SDK 의 버킷 이름과 가용 영역의 약칭은 JSON Java SDK와 다르므로 해당 변경을 진행해야 합니다.

**버킷 Bucket**

XML SDK 버킷 이름은 사용자 지정 문자열과 APPID 두 부분으로 구성되며 양자 사이는 대시 "-"로 연결됩니다.
예를 들어 `examplebucket-1250000000`, 여기서 `examplebucket`은 사용자 지정 문자열이고, `1250000000`은 APPID입니다.

>?APPID 는 Tencent Cloud 계정의 계정 식별자 중 하나로, 관련 클라우드 리소스를 연결하는 데 사용됩니다. 사용자가 Tencent Cloud 계정 신청에 성공한 후, 시스템은 자동으로 사용자에게 하나의 APPID를 할당합니다. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)의 [계정 정보]에서 APPID를 조회할 수 있습니다.

Bucket 설정은 다음 예제 코드를 참조하십시오.

```java
COSCredentials cred = new BasicCOSCredentials("COS_SECRETID", "COS_SECRETKEY");
// 새 region 이름을 사용했을 경우, 사용 가능한 region의 목록을 공식 웹사이트 문서에서 획득하거나, 다음 XML SDK 및 JSON SDK의 지역 비교표를 참조할 수 있습니다.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
COSClient cosclient = new COSClient(cred, clientConfig);
// bucket의 이름은 필요시 appid를 포함해야 합니다
String bucketName = "examplebucket-1250000000";

// 다음은 이 버킷에 파일을 업로드하는 예시입니다
String key = "docs/exampleobject.doc";
File localFile = new File("src/test/resources/len10M.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// 스토리지 클래스를 설정합니다. 기본적으로 표준(Standard), 저빈도(standard_ia)입니다.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
try {
	PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
	// putobjectResult는 파일의 etag를 반환합니다.
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
	e.printStackTrace();
} catch (CosClientException e) {
	e.printStackTrace();
}

// 클라이언트를 종료합니다.
cosclient.shutdown();

```

**버킷 가용 영역 약칭 Region**
XML SDK의 버킷 가용 지역 약칭에 변화가 생겼을 경우, 다른 지역의 JSON SDK 및 XML SDK의 대응 관계는 다음 표를 참조하십시오.

| 지역       | XML SDK 지역 약칭         | JSON SDK 지역 약칭                         |
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

`COSClient`초기화 시, 버킷 소재 지역 이름의 약칭을 `ClientConfig`에 설정하십시오.

```java
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
COSClient cosclient = new COSClient(cred, clientConfig);

```

**3. API 변경**
XML SDK로 업그레이드 한 후 일부 작업의 API가 변경되었으므로 실제 수요에 따라 해당 변경을 진행하십시오. 동시에 패키징을 통해 SDK를 보다 쉽게 이용할 수 있도록 하였습니다. 자세한 내용은 예시와 [API 문서](https://cloud.tencent.com/document/product/436/12263)를 참조하십시오.

API의 주요 변경 사항은 다음과 같습니다.

**1)독립적인 디렉터리 API 없음**

XML SDK에서는 개별적인 디렉토리 API를 더 이상 제공하지 않습니다. COS 자체는 폴더와 디렉터리라는 개념이 없으며 COS는 업로드 객체 `project/a.txt`로 인해 project 폴더를 생성하지 않습니다. 사용자의 사용습관을 충족시키기 위해 COS는 콘솔, COS 브라우저 등 그래픽 도구에 「폴더」 또는 「디렉터리」의 표시 방식을 시뮬레이션합니다. 구체적으로 키 값이 `project/`이고 내용이 비어있는 객체의 생성을 통해 구현되고, 표시 방식은 전통 폴더를 시뮬레이션하였습니다.

예를 들어 업로드 객체 `project/doc/a.txt`의 구분자 `/`는 「폴더」의 표시 방식을 시뮬레이션하기 때문에 콘솔에 「폴더」 project와 doc가 나타나고, 여기서 doc는 project 하위 「폴더」이고 a.txt 파일을 포함합니다.

따라서 단지 파일 업로드 시나리오의 경우, 바로 업로드하면 되며, 먼저 폴더를 생성할 필요가 없습니다. 적용 시나리오에 폴더의 개념이 있으면 폴더를 생성하는 기능을 제공해야 합니다. 경로가 `/`로 끝나는 0KB 파일 하나를 업로드하면 됩니다. 그러면 GetBucket API를 사용했을 때 해당 파일을 폴더로 할 수 있습니다.

**2)TransferManager**

XML Java SDK 에서 업로드, 다운로드 및 복사 작업을 캡슐화하여 `TransferManager`라고 명명하였으며. API 디자인 및 전송 성능을 최적화하였으므로 직접 사용하실 것을 권장합니다.

`TransferManager`의 주요 특징:

- 업로드 다운로드 과정의 일시 중지 및 복구를 지원합니다
- 파일 크기에 따라 간편 업로드 또는 멀티파트 업로드에 대해 스마트한 선택을 지원합니다. 판단 임계값을 설정할 수 있습니다.
- 테스크 상태의 수신을 지원합니다.

`TransferManager`을 사용하여 업로드하는 샘플 코드는 다음과 같습니다:

```java
TransferManager transferManager = new TransferManager(cosclient, threadPool);

String key = "docs/exampleobject.doc";
File localFile = new File("src/test/resources/len30M.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
try {
    // 비동기화 결과 Upload를 반환하며, waitForUploadResult를 동기화 호출하여 upload 종료를 대기할 수 있으며, 성공하는 경우 UploadResult를 반환하고 실패 시 이상을 throw합니다.
    Upload upload = transferManager.upload(putObjectRequest);
    Thread.sleep(10000);
    // 작업 일시 중지
    PersistableUpload persistableUpload = upload.pause();
    // 업로드 복구
    upload = transferManager.resumeUpload(persistableUpload);
    // 업로드 진행률 표시 가능
    showTransferProgress(upload);
    // 업로드 작업 완료 대기
    UploadResult uploadResult = upload.waitForUploadResult();
    System.out.println(uploadResult.getETag());

    // 추가로 업로드 작업 취소 또한 지원
    transferManager.cancel();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

ransferManager.shutdownNow();
cosclient.shutdown();

```

**3)서명 알고리즘이 다름**

일반적으로 수동으로 서명을 계산할 필요가 없지만, SDK의 서명을 프런트 엔드에 반환하는 경우 서명 알고리즘에 변화가 생겼다는 점에 유의하십시오. 서명은 더 이상 단일 서명과 다중 서명을 구분하지 않으며 서명의 유효 기간을 설정하여 보안성을 보장합니다. 구체적인 알고리즘은 [XML 서명 요청](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.

**4) API 새로 추가**

XML Java SDK에서 새로 추가된 API는 수요에 따라 호출할 수 있습니다. 다음을 포함합니다.

* 버킷의 조작, 즉 createBucket, GetBucket(List Objects), ListBuckets 등입니다.
* 버킷 ACL의 조작, 즉 getBucketAcl, setBucketAcl 등입니다.
* 버킷의 수명 주기 조작, 즉 setBucketLifecycleConfiguration, getBucketLifecycleConfiguration, deleteBucketLifecycleConfiguration 등입니다.

더 자세한 정보는 [Java SDK API 문서](https://cloud.tencent.com/document/product/436/12263)를 참조하십시오.
