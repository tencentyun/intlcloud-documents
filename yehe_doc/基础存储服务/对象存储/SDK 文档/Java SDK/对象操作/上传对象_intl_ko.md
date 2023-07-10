## 소개

본 문서는 객체 업로드와 관련된 API 및 SDK 코드 샘플에 대한 개요를 제공합니다.

**간단한 작업**

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 객체 업로드       | 버킷에 객체를 업로드    |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | 폼을 사용한 객체 업로드   | 폼을 사용하여 객체 업로드를 요청합니다.                     |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | 객체 추가 업로드 | 멀티파트에 추가하는 방식으로 객체 업로드 |

**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 쿼리   | 진행 중인 멀티파트 업로드를 쿼리합니다.         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 업로드 작업 초기화     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 멀티파트 업로드       | 객체 멀티파트 업로드                        |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 기타 객체를 멀티파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 파트 삭제 |


## 고급 인터페이스(권장)

고급 API는 TransferManager 클래스를 통해 간단한 API를 캡슐화하여 보다 쉬운 작업을 위한 API를 제공합니다. 내부적으로 스레드 풀은 사용자의 요청을 동시에 수락하고 처리하는 데 사용되므로 여러 작업을 제출한 후 작업 비동기 실행을 선택할 수 있습니다.

TransferManager 인스턴스 동시성은 안전합니다. 프로세스에 대해 하나의 TransferManager 인스턴스만 생성한 다음 고급 API를 호출하는 데 더 이상 사용되지 않을 때 종료하는 것이 좋습니다.


### 기능 설명

고급 API는 단순 업로드 및 멀티파트 업로드 API를 캡슐화하고 파일 크기에 따라 업로드 방법을 지능적으로 선택할 수 있습니다. 또한 체크포인트 재시작 및 업로드 진행률 표시와 같은 기능을 지원합니다.

>?
> - 파트 임계값은 전체 또는 파트 업로드 여부를 결정하는 데 사용됩니다. 임계값은 구성 가능하며 기본적으로 5MB입니다.
> - 멀티파트 크기는 사용자가 설정할 수 있으며 기본값은 1MB입니다.
> - 스트림 업로드의 경우 스트림 크기가 파트 임계값 미만이거나 Content-Length 헤더가 지정되지 않은 경우 스트림 전체가 업로드됩니다.
> - 스트림 업로드의 경우 스트림 크기가 파트 임계값을 초과하고 Content-Length 헤더가 지정된 경우 고급 API는 멀티파트 업로드를 선택합니다.
> - 파일 업로드의 경우 파일 크기가 파트 임계값 미만인 경우 파일 전체가 업로드되고, 파일 크기가 파트 임계값을 초과하는 경우 부분적으로 업로드됩니다.
> - 파트 파일 업로드의 경우 멀티 파트가 멀티 스레드와 동시에 업로드됩니다.
> - 멀티 파트 업로드의 경우 고급 업로드 API는 업로드 진행률을 가져오는 기능을 제공합니다. 자세한 내용은 아래 예시를 참고하십시오.
> 

### TransferManager 인스턴스 생성

고급 API를 사용하기 전에 먼저 TransferManager 인스턴스를 생성해야 합니다.

```java
// 추후 고급 API를 호출하는 데 사용되는 TransferManager 인스턴스를 생성합니다.
TransferManager createTransferManager() {
    // COS 서비스에 액세스하기 위한 기본 인스턴스인 COSClient 클라이언트를 생성합니다.
    // 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
    COSClient cosClient = createCOSClient();

    // 스레드 풀 크기를 설정합니다. 클라이언트 및 COS 네트워크가 충분한 경우(예: 동일한 리전의 CVM 인스턴스에서 COS 버킷으로 파일 업로드) 네트워크 리소스 활용도를 최대화하려면 스레드 풀의 크기를 16 또는 32로 설정하는 것이 좋습니다.
    // 공용 네트워크를 이용한 전송 및 네트워크 대역폭의 품질이 좋지 않은 경우 해당 값을 줄이길 권장합니다. 네트워크 속도가 느려져 요청 시간이 초과할 수 있습니다.
    ExecutorService threadPool = Executors.newFixedThreadPool(32);

    // threadpool을 전송합니다. 스레드 풀을 전송하지 않을 경우 기본적으로 TransferManager에 싱글 스레드의 스레드 풀이 생성됩니다.
    TransferManager transferManager = new TransferManager(cosClient, threadPool);

    // 고급 API의 구성 항목을 설정합니다.
    // 멀티파트 업로드의 임계값과 파트 크기를 각각 5MB와 1MB로 설정합니다.
    TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
    transferManagerConfiguration.setMultipartUploadThreshold(5*1024*1024);
    transferManagerConfiguration.setMinimumUploadPartSize(1*1024*1024);
    transferManager.setConfiguration(transferManagerConfiguration);

    return transferManager;
}
```

### 매개변수 설명

TransferManagerConfiguration 유형은 고급 인터페이스의 설정 정보를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

|  멤버 이름 | 설정 방법            | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize   | set 메소드 | 멀티파트 업로드의 파트 크기입니다. 단위는 바이트(Byte)이며, 기본값은 5MB입니다. | long         |
| multipartUploadThreshold   | set 메소드 | 해당 값보다 크거나 같고 동시 접속하는 멀티파트 업로드 파일입니다. 단위는 바이트(Byte)이며, 기본값은 5MB입니다. | long         |
| multipartCopyThreshold         | set 메소드 | 해당 값보다 크거나 같고 동시 접속하는 멀티파트 복사 파일입니다. 단위는 바이트(Byte)이며, 기본값은 5GB입니다. | long           |
| multipartCopyPartSize        | set 메소드 | 멀티파트 복사 시 파트의 크기입니다. 단위는 바이트(Byte)이며, 기본값은 100MB입니다.           | long    |

### TransferManager 인스턴스 종료

프로세스가 더 이상 TransferManager 인스턴스를 사용하여 고급 API를 호출하지 않는 것을 확인한 후 리소스 유출을 방지하기 위해 종료해야 합니다.

```java
void shutdownTransferManager(TransferManager transferManager) {
    // 매개변수가 true로 설정되면 TransferManager 인스턴스의 COSClient 인스턴스도 동시에 종료됩니다.
    // 매개변수가 false로 설정되면 TransferManager 인스턴스의 COSClient 인스턴스가 종료되지 않습니다.
    transferManager.shutdownNow(true);
}
```

### 로컬 파일 업로드

업로드 소스는 로컬 파일입니다.

#### 메소드 프로토타입

```java
// 객체 업로드
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### 요청 예시

```java
// 고급 인터페이스를 사용하려면 먼저 이 프로세스에 TransferManager 인스턴스가 있는지 확인하고 없다면 생성합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> TransferManager 인스턴스 생성
TransferManager transferManager = createTransferManager();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// 로컬 파일 경로
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

//객체의 사용자 정의 Headers를 설정해야 하는 경우 다음 코드를 참고할 수 있으며, 필요하지 않은 경우 다음 행을 생략할 수 있습니다. 객체의 사용자 정의 Headers에 대한 자세한 내용은 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/13361
ObjectMetadata objectMetadata = new ObjectMetadata();

//Content-Type, Cache-Control, Content-Disposition, Content-Encoding, Expires 5개 단어를 설정하여 Headers를 사용자 정의할 경우, objectMetadata.setHeader()를 사용하는 것이 좋습니다.
objectMetadata.setHeader(key, value);
// ‘x-cos-meta-[사용자 정의 접미사]’와 같은 사용자 정의 Header를 설정하려면 다음을 사용하는 것이 좋습니다.
Map<String, String> userMeta = new HashMap<String, String>();
userMeta.put("x-cos-meta-[사용자 정의 접미사]", "value");
objectMetadata.setUserMetadata(userMeta);

putObjectRequest.withMetadata(objectMetadata);

try {
    // 고급 인터페이스는 비동기화 결과 Upload를 반환합니다.
    // waitForUploadResult 메소드를 동기화 호출하여 업로드 완료를 대기할 수 있습니다. 성공 시 UploadResult를 반환하고 실패 시 이상 경고가 발생합니다.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 transferManager 인스턴스를 사용하지 않음을 확인한 후 종료합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> TransferManager 비활성화
shutdownTransferManager(transferManager);
```

#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 메소드              | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 구조 함수 또는 set 메소드 | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         |
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         |
| file         | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    |
| metadata     | 구조 함수 또는 set 메소드 | 파일의 메타데이터                                                 | ObjectMetadata |
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|No|

#### 반환값

- 성공: Upload를 반환합니다. 업로드의 종료 여부를 확인할 수 있으며, 업로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

Upload의 waitForUploadResult() 방법을 호출하여 획득한 객체 업로드 정보는 UploadResult 유형에 기록됩니다. UploadResult 유형의 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName       | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String           |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br/>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| requestId  | 요청 Id                                                       | String |
| dateStr    | 현재 서버 시간                                               | String |
| versionId  | 버킷의 버전 관리 기능이 활성화되면 객체의 버전 넘버 Id 반환                      | String |
| crc64Ecma  | 서버에서 객체 콘텐츠에 따라 계산한 CRC64                           | String |

### 스트림 업로드 유형

업로드 소스는 InputStream 유형(및 서브 유형)의 스트림 인스턴스입니다.

#### 메소드 프로토타입

```java
// 객체 업로드
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### 요청 예시

```java
// 고급 인터페이스를 사용하려면 먼저 이 프로세스에 TransferManager 인스턴스가 있는지 확인하고 없다면 생성합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> TransferManager 인스턴스 생성
TransferManager transferManager = createTransferManager();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";

// 여기서는 ByteArrayInputStream 스트림을 예시로 생성했습니다. 실제로는 업로드를 위해 InputStream 유형의 스트림을 생성해야 합니다.
long inputStreamLength = 1024 * 1024;
byte data[] = new byte[inputStreamLength];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
// 업로드된 스트림의 정확한 길이를 알 수 있다면 content-length를 입력하는 것이 좋습니다.
// 그렇지 않으면 다음 행을 생략할 수 있지만 고급 API는 멀티파트 업로드를 사용할 수 없습니다.
objectMetadata.setContentLength(inputStreamLength);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

try {
    // 고급 인터페이스는 비동기화 결과 Upload를 반환합니다.
    // waitForUploadResult 메소드를 동기화 호출하여 업로드 완료를 대기할 수 있습니다. 성공 시 UploadResult를 반환하고 실패 시 이상 경고가 발생합니다.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 transferManager 인스턴스를 사용하지 않음을 확인한 후 종료합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> TransferManager 비활성화
shutdownTransferManager(transferManager);
```

#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 메소드              | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 구조 함수 또는 set 메소드 | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         |
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         |
| file         | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    |
| metadata     | 구조 함수 또는 set 메소드 | 파일의 메타데이터                                                 | ObjectMetadata |
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|No|

#### 반환값

- 성공: Upload를 반환합니다. 업로드의 종료 여부를 확인할 수 있으며, 업로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

Upload의 waitForUploadResult() 방법을 호출하여 획득한 객체 업로드 정보는 UploadResult 유형에 기록됩니다. UploadResult 유형의 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName       | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String           |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br/>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| requestId  | 요청 Id                                                       | String |
| dateStr    | 현재 서버 시간                                               | String |
| versionId  | 버킷의 버전 관리 기능이 활성화되면 객체의 버전 넘버 Id 반환                      | String |
| crc64Ecma  | 서버에서 객체 콘텐츠에 따라 계산한 CRC64                           | String |

### 업로드 진행률 표시

>? 업로드 진행률은 멀티파트 업로드를 사용하는 API에 대해서만 표시될 수 있습니다.
>

업로드 진행률을 표시하려면 진행 상황을 출력하는 함수가 필요합니다. 여기서 API가 호출되어 성공적으로 업로드된 객체의 크기를 가져온 다음 현재 업로드 진행률을 계산합니다.

#### 메소드 프로토타입

```java
// 객체 업로드
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### 요청 예시

```java
// 필요에 따라 다음 샘플 코드를 조정하여 고유한 코드를 구성할 수 있습니다.
void showTransferProgress(Transfer transfer) {
    // 여기서 Transfer는 비동기 업로드 결과 Upload의 상위 클래스입니다.
    System.out.println(transfer.getDescription());

    // transfer.isDone()을 사용하여 업로드가 완료되었는지 확인합니다.
    while (transfer.isDone() == false) {
        try {
            // 2초마다 진행 상황을 가져옵니다.
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }

        TransferProgress progress = transfer.getProgress();
        long sofar = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("upload progress: [%d / %d] = %.02f%%\n", sofar, total, pct);
    }

    // 업로드가 완료되면 Completed가 반환됩니다. 그렇지 않으면 Failed가 반환됩니다.
    System.out.println(transfer.getState());
}
```

파일 업로드 작업과 결합된 샘플 코드는 다음과 같습니다.

```java
// 고급 인터페이스를 사용하려면 먼저 이 프로세스에 TransferManager 인스턴스가 있는지 확인하고 없다면 생성합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> TransferManager 인스턴스 생성
TransferManager transferManager = createTransferManager();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// 로컬 파일 경로
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    // 고급 인터페이스는 비동기화 결과 Upload를 반환합니다.
    Upload upload = transferManager.upload(putObjectRequest);
    // 업로드가 완료될 때까지 업로드 진행 상황을 출력합니다.
    showTransferProgress(upload);
    // 발생 가능한 예외를 캡처합니다.
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 transferManager 인스턴스를 사용하지 않음을 확인한 후 종료합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> TransferManager 비활성화
shutdownTransferManager(transferManager);
```

#### 진행률 가져오기 설명

이 클래스의 getProgress를 업로드하여 TransferProgress 클래스를 얻을 수 있습니다. 이 클래스의 아래 세 가지 방법으로 업로드 진행률을 얻을 수 있습니다.

| 메소드 이름                 | 설명                | 유형    |
| ----------------------- | ------------------ | -----   |
| getBytesTransferred     | 업로드된 바이트 수 획득   | long   |
| getTotalBytesToTransfer | 총 파일의 바이트 수 획득   | long   |
| getPercentTransferred   | 업로드된 바이트 백분율 획득  | double |

#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 메소드              | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 구조 함수 또는 set 메소드 | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         |
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         |
| file         | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    |
| metadata     | 구조 함수 또는 set 메소드 | 파일의 메타데이터                                                 | ObjectMetadata |
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|No|

#### 반환값

- 성공: Upload를 반환합니다. 업로드의 종료 여부를 확인할 수 있으며, 업로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

Upload의 waitForUploadResult() 방법을 호출하여 획득한 객체 업로드 정보는 UploadResult 유형에 기록됩니다. UploadResult 유형의 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName       | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String           |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br/>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| requestId  | 요청 ID                                                       | String |
| dateStr    | 현재 서버 시간                                               | String |
| versionId  | 버킷의 버전 관리 기능이 활성화되면 객체의 버전 넘버 ID 반환                      | String |
| crc64Ecma  | 서버에서 객체 콘텐츠에 따라 계산한 CRC64                           | String |

### 업로드 일시 중지, 재개 또는 취소

이 API는 업로드 작업을 일시 중지, 재개 또는 취소하는 데 사용할 수 있습니다.

> ?
> - 스트림 업로드는 일시 중지, 재개 또는 취소할 수 없습니다.
> - 간편 업로드는 일시 중지, 재개 또는 취소할 수 없습니다.
> - 암호화된 업로드는 일시 중지, 재개 또는 취소할 수 없습니다.

#### 메소드 프로토타입

```java
// 객체 업로드
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### 요청 예시

```java
// 고급 인터페이스를 사용하려면 먼저 이 프로세스에 TransferManager 인스턴스가 있는지 확인하고 없다면 생성합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> 예시 코드: TransferManager 생성
TransferManager transferManager = createTransferManager();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// 로컬 파일 경로
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    // 고급 인터페이스는 비동기화 결과 Upload를 반환합니다.
    Upload upload = transferManager.upload(putObjectRequest);
    // 파일의 일부가 업로드될 때까지 3초 동안 기다립니다.
    Thread.sleep(3000);
    // 업로드를 일시 중지하고 나중에 업로드를 재개하기 위해 PersistableUpload 인스턴스를 가져옵니다.
    PersistableUpload persistableUpload = upload.pause();
    // 복잡한 일시 중지 및 재개:
    // PersistableUpload 인스턴스는 파일 내용을 serialize하고 저장한 다음 deserialize하여 업로드 재개에 사용할 수 있습니다.
    // persistableUpload.serialize(out);
    // 업로드 재개
    upload = transferManager.resumeUpload(persistableUpload);
    // 발생 가능한 예외를 캡처합니다.
    UploadResult uploadResult = upload.waitForUploadResult();

    // 또는 업로드를 직접 취소합니다.
    // upload.abort();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 transferManager 인스턴스를 사용하지 않음을 확인한 후 종료합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> 예시 코드: TransferManager 인스턴스 종료
shutdownTransferManager(transferManager);
```

#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 메소드              | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 구조 함수 또는 set 메소드 | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         |
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         |
| file         | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    |
| metadata     | 구조 함수 또는 set 메소드 | 파일의 메타데이터                                                 | ObjectMetadata |
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|No|

#### 반환값

- 성공: Upload를 반환합니다. 업로드의 종료 여부를 확인할 수 있으며, 업로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

Upload의 waitForUploadResult() 방법을 호출하여 획득한 객체 업로드 정보는 UploadResult 유형에 기록됩니다. UploadResult 유형의 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName       | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String           |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br/>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| requestId  | 요청 ID                                                       | String |
| dateStr    | 현재 서버 시간                                               | String |
| versionId  | 버킷의 버전 관리 기능이 활성화되면 객체의 버전 넘버 ID 반환                      | String |
| crc64Ecma  | 서버에서 객체 콘텐츠에 따라 계산한 CRC64                           | String |

### 로컬 디렉터리 업로드

TransferManager 인스턴스는 로컬 디렉터리에서 파일을 읽고 COS에 업로드하는 기능을 캡슐화합니다. 이 기능은 디렉터리 구조를 파괴하지 않고 파일을 업로드할 수 있습니다. 한 디렉터리에서 다른 디렉터리로 파일을 업로드할 수도 있습니다.

>? 재귀적 디렉터리 업로드가 지원됩니다. 업로드한 디렉터리가 너무 크면 업로드가 느려지거나 오랜 시간 차단될 수 있습니다. 디렉터리를 재귀적으로 업로드할 때 용량이 작은 디렉터리(예: 1024개 이하 파일)를 업로드하는 것이 좋습니다. 대용량 디렉터리를 업로드하는 경우 일괄 호출을 위해 여러 개의 작은 디렉터리로 분할하는 것이 좋습니다.
>

#### 메소드 프로토타입

```java
public MultipleFileUpload uploadDirectory(String bucketName, String virtualDirectoryKeyPrefix,
            File directory, boolean includeSubdirectories);
```

#### 요청 예시

```java
// 고급 인터페이스를 사용하려면 먼저 이 프로세스에 TransferManager 인스턴스가 있는지 확인하고 없다면 생성합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> 예시 코드: TransferManager 생성
TransferManager transferManager = createTransferManager();
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

// 파일이 bucket에 업로드된 후 접두사 디렉터리를 설정합니다. “”로 설정하는 경우 bucket의 루트 디렉터리로 업로드된 것을 의미합니다.
String cos_path = "/prefix";
// 업로드할 폴더의 절대 경로
String dir_path = "/path/to/localdir";
// 디렉터리의 서브 디렉터리 재귀 업로드 여부입니다. true이면 서브 디렉터리의 파일도 업로드하고 cos에 디렉터리 구조가 유지됩니다.
Boolean recursive = false;

try {
    // 비동기 결과 Upload를 반환합니다. 동시에 waitForUploadResult를 호출하여 upload 결과를 기다릴 수 있습니
다. 성공하면 UploadResult를 반환하고, 실패하면 이상 경고 메시지를 표시합니다.
    MultipleFileUpload upload = transferManager.uploadDirectory(bucketName, cos_path, new File(dir_path), recursive);

    // 업로드 진행 상황 확인을 선택할 수 있습니다. 함수에 대한 자세한 내용은 고급 API -> 파일 업로드 -> 업로드 진행률 표시를 참고하십시오.
    showTransferProgress(upload);

    // 또는 정체된 대기를 완료합니다.
    upload.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 transferManager 인스턴스를 사용하지 않음을 확인한 후 종료합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> 예시 코드: TransferManager 인스턴스 종료
shutdownTransferManager(transferManager);
```

#### 매개변수 설명

| 매개변수 이름                   | 설명                  | 유형             |
| ------------------------- | -------------------- | ---------------- |
| bucketName                | cos의 bucket       | GetObjectRequest |
| virtualDirectoryKeyPrefix | cos의 object 접두사   | String           |
| directory                 | 업로드할 폴더의 절대 경로  | File             |
| includeSubDirectory       | 서브 디렉터리 재귀 업로드 여부       | Boolean          |

#### 반환값

- 성공: MultipleFileUpload를 반환합니다. 업로드의 종료 여부를 확인할 수 있으며, 업로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

## 간단한 작업

단순 작업에 대한 요청은 COSClient 인스턴스를 통해 시작해야 합니다. 간단한 작업을 수행하기 전에 COSClient 인스턴스를 생성해야 합니다.

COSClient 인스턴스 동시성은 안전합니다. 프로세스에 대해 COSClient 인스턴스를 하나만 생성한 다음 요청 시작에 더 이상 사용되지 않을 때 종료하는 것이 좋습니다.

### COSClient 인스턴스 생성

COS API를 호출하기 전에 먼저 COSClient 인스턴스를 생성해야 합니다.

```java
// 추후 요청 초기화에 사용되는 COSClient 인스턴스를 생성합니다.
COSClient createCOSClient() {
    // 사용자 ID 정보를 설정합니다.
    // SECRETID 및 SECRETKEY는 CAM 콘솔 https://console.cloud.tencent.com/cam/capi에 로그인하여 조회 및 관리하십시오.
    String secretId = "SECRETID";
    String secretKey = "SECRETKEY";
    COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

    // ClientConfig에는 후속 COS 요청에 대한 COS 클라이언트 구성이 포함됩니다.
    ClientConfig clientConfig = new ClientConfig();

    // bucket 리전을 설정합니다.
    // COS_REGION에 대한 자세한 내용은 https://cloud.tencent.com/document/product/436/6224을(를) 참고하십시오.
    clientConfig.setRegion(new Region("COS_REGION"));

    // 요청 프로토콜을 http 또는 https로 설정합니다.
    // 5.6.53 이하 버전의 경우 https를 권장합니다.
    // 5.6.54부터 https가 기본으로 사용됩니다.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // 다음 설정은 선택 사항입니다.

    // socket 읽기 제한 시간을 설정합니다. 기본 값: 30s
    clientConfig.setSocketTimeout(30*1000);
    // 연결 제한 시간을 설정합니다. 기본 값: 30s
    clientConfig.setConnectionTimeout(30*1000);

    // 필요 시 http 프록시, ip 및 port를 설정합니다.
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // cos 클라이언트 생성.
    return new COSClient(cred, clientConfig);
}
```

### 임시 키로 COSClient 인스턴스 생성

임시 키로 COS를 요청하려면 임시 키로 COSClient 인스턴스를 생성해야 합니다.
이 SDK는 임시 키를 생성하지 않습니다. 임시 키 생성 방법은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.

```java

// 추후 요청 초기화에 사용되는 COSClient 인스턴스를 생성합니다.
COSClient createCOSClient() {
    // 여기에는 임시 키 정보가 필요합니다.
    // 임시 키 생성 방법은 https://intl.cloud.tencent.com/document/product/436/14048을(를) 참고하십시오.
    String tmpSecretId = "TMPSECRETID";
    String tmpSecretKey = "TMPSECRETKEY";
    String sessionToken = "SESSIONTOKEN";

    COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);

    // ClientConfig에는 후속 COS 요청에 대한 COS 클라이언트 구성이 포함됩니다.
    ClientConfig clientConfig = new ClientConfig();

    // bucket 리전을 설정합니다.
    // COS_REGION에 대한 자세한 내용은 https://cloud.tencent.com/document/product/436/6224을(를) 참고하십시오.
    clientConfig.setRegion(new Region("COS_REGION"));

    // 요청 프로토콜을 http 또는 https로 설정합니다.
    // 5.6.53 이하 버전의 경우 https를 권장합니다.
    // 5.6.54 이상 버전의 경우 https가 기본으로 사용됩니다.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // 다음 설정은 선택 사항입니다.

    // socket 읽기 제한 시간을 설정합니다. 기본 값: 30s
    clientConfig.setSocketTimeout(30*1000);
    // 연결 제한 시간을 설정합니다. 기본 값: 30s
    clientConfig.setConnectionTimeout(30*1000);

    // 필요 시 http 프록시, ip 및 port를 설정합니다.
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // cos 클라이언트 생성.
    return new COSClient(cred, clientConfig);
}
```

### 로컬 파일 업로드

업로드 소스는 로컬 파일입니다.

#### 메소드 프로토타입

```java
// 방법1  로컬 파일을 COS에 업로드
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// 방법2  입력 스트림을 COS에 업로드
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// 방법3  위의 두 가지 방법 패키지에 더 세분화된 매개변수 제어를 지원(예: content-type, content-disposition 등)
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// 로컬 파일 경로
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    System.out.println(putObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 cosClient 인스턴스를 사용하지 않음을 확인한 후 종료합니다.
cosClient.shutdown();
```

#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 메소드 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   | 설명                                                         | 유형   | 필수 입력 |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         | Yes|
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         | Yes|
| file         | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |No|
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    | No|
| metadata     | 구조 함수 또는 set 메소드 | 객체의 메타데이터                                                 | ObjectMetadata | No|
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|No|

ObjectMetadata 유형은 객체의 메타 정보를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | 캐시의 타임아웃 시간은 HTTP 응답 헤더의 Expires 필드 값 | Date                |
| ongoingRestore  | 현재 CAS 유형에서 해당 객체를 복구하는 중                        | Boolean             |
| userMetadata    | 접두사가 x-cos-meta-인 사용자 정의 메타 정보               | Map&lt;String, String&gt; |
| metadata        | 사용자 정의 메타 정보를 제외한 기타 헤더                    | Map&lt;String, String&gt; |
| restoreExpirationTime  | 보관된 객체 복구 사본의 만료 시간  | Date |

#### 반환 결과 설명

- 성공: 파일의 eTag 등 정보를 포함한 PutObjectResult입니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

PutObjectResult 유형은 결과 정보 반환에 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | 요청 ID | String                |
| dateStr  | 현재 서버 시간                        | String             |
| versionId    | 버전 관리 버킷을 활성화한 후 객체의 버전 넘버 ID를 반환              | String |
| eTag        | 단순 업로드 API에서 반환된 객체의 MD5 값, 예시: 09cba091df696af91549de27b8e7d0f6, **참고: ETag 응답 헤더 값에 큰따옴표가 있지만 여기에서 구문 분석된 eTag 문자열 값에는 큰따옴표가 없습니다.** | String |
|crc64Ecma| 서버에서 객체 콘텐츠에 따라 계산한 CRC64| String |

### 스트림 업로드 유형

업로드 소스는 InputStream 유형(및 해당 서브 유형)의 스트림 인스턴스입니다.

#### 메소드 프로토타입

```java
// 방법1  로컬 파일을 COS에 업로드
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// 방법2  입력 스트림을 COS에 업로드
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// 방법3  위의 두 가지 방법 패키지에 더 세분화된 매개변수 제어를 지원(예: content-type, content-disposition 등)
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";

// 여기서는 ByteArrayInputStream 스트림을 예시로 생성했습니다. 실제로는 업로드를 위해 InputStream 유형의 스트림을 생성해야 합니다.
long inputStreamLength = 1024 * 1024;
byte data[] = new byte[inputStreamLength];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
// 업로드된 스트림의 정확한 길이를 알 수 있다면 content-length를 입력하는 것이 좋습니다.
// 그렇지 않으면 다음 행을 생략할 수 있지만 고급 API는 멀티파트 업로드를 사용할 수 없습니다.
objectMetadata.setContentLength(inputStreamLength);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    System.out.println(putObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 cosClient 인스턴스를 사용하지 않음을 확인한 후 종료합니다.
cosClient.shutdown();
```

#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 메소드 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   | 설명                                                         | 유형   | 필수 입력 |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         | Yes|
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         | Yes|
| file         | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |No|
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    | No|
| metadata     | 구조 함수 또는 set 메소드 | 객체의 메타데이터                                                 | ObjectMetadata | No|
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|No|

ObjectMetadata 유형은 객체의 메타 정보를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | 캐시의 타임아웃 시간은 HTTP 응답 헤더의 Expires 필드 값 | Date                |
| ongoingRestore  | 현재 CAS 유형에서 해당 객체를 복구하는 중                        | Boolean             |
| userMetadata    | 접두사가 x-cos-meta-인 사용자 정의 메타 정보               | Map&lt;String, String&gt; |
| metadata        | 사용자 정의 메타 정보를 제외한 기타 헤더                    | Map&lt;String, String&gt; |
| restoreExpirationTime  | 보관된 객체 복구 사본의 만료 시간  | Date |

#### 반환 결과 설명

- 성공: 파일의 eTag 등 정보를 포함한 PutObjectResult입니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

PutObjectResult 유형은 결과 정보 반환에 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | 요청 ID | String                |
| dateStr  | 현재 서버 시간                        | String             |
| versionId    | 버전 관리 버킷을 활성화한 후 객체의 버전 넘버 ID를 반환              | String |
| eTag        | 단순 업로드 API에서 반환된 객체의 MD5 값, 예시: 09cba091df696af91549de27b8e7d0f6, **참고: ETag 응답 헤더 값에 큰따옴표가 있지만 여기에서 구문 분석된 eTag 문자열 값에는 큰따옴표가 없습니다.** | String |
|crc64Ecma| 서버에서 객체 콘텐츠에 따라 계산한 CRC64| String |

### 디렉터리 생성

COS는 디렉터리 자체의 개념이 없지만 슬래시 ‘/’로 구분된 객체 경로를 버츄얼 디렉터리로 간주할 수 있습니다.

>?
> - 디렉터리가 필요한 경우 원하는 디렉터리에 파일을 업로드하면 디렉터리가 자동으로 생성됩니다. 예를 들어 /dir/example.txt와 같은 파일을 업로드하면 /dir 디렉터리가 자동으로 생성됩니다. 자세한 내용은 이 페이지의 로컬 파일 업로드를 참고하십시오.
> 

파일이 없는 디렉터리가 필요한 경우 슬래시 ‘/’로 끝나는 경로에 빈 스트림을 업로드하면 버츄얼 디렉터리가 생성됩니다.

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 생성할 디렉터리의 경로를 지정합니다.
String key = "/example/dir/";

// 여기에서는 예시로 빈 ByteArrayInputStream을 생성합니다.
byte data[] = new byte[0];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setContentLength(0);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    System.out.println(putObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 cosClient 인스턴스를 사용하지 않음을 확인한 후 종료합니다.
cosClient.shutdown();
```

### 부분 추가 업로드

이 API는 부분을 추가하여 객체를 업로드하는 데 사용됩니다.

#### 메소드 프로토타입

```java
public AppendObjectResult appendObject(AppendObjectRequest appendObjectRequest)
        throws CosServiceException, CosClientException
```

#### 요청 예시

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";

// 업로드를 위해 이 두 파일의 콘텐츠를 추가해야 한다고 가정합니다.
File part1File = new File("/path/to/part1File");
File part2File = new File("/path/to/part2File");

try {
    AppendObjectRequest appendObjectRequest = new AppendObjectRequest(bucketName, key, part1File);
    appendObjectRequest.setPosition(0L);
    AppendObjectResult appendObjectResult = cosClient.appendObject(appendObjectRequest);
    long nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);

    appendObjectRequest = new AppendObjectRequest(bucketName, key, part2File);
    appendObjectRequest.setPosition(nextAppendPosition);
    appendObjectResult = cosClient.appendObject(appendObjectRequest);
    nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// 클라이언트 종료
cosClient.shutdown();
```

#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| -------------------- | ------------ | ---------------- |
| appendObjectRequest | 파일 추가 업로드 요청 | AppendObjectRequest |

AppendObjectRequest 참석자 설명: 

| Request 멤버 | 설정 방법   | 설명                                                         | 유형   | 필수 입력 여부 |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         | Yes|
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         | Yes|
| localfile    | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |No|
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    | No|
| metadata     | 구조 함수 또는 set 메소드 | 객체의 메타데이터                                                 | ObjectMetadata | No|
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|No|
| position | set 메소드| 작업 시작 위치 추가, 단위: byte | Long | Yes |

#### 반환 결과 설명

- 성공: AppendObjectResult.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

AppendObjectResult 유형은 결과 정보 반환에 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| metadata | 헤더 반환 | ObjectMetadata               |
| nextAppendPosition| 다음에 추가될 위치 | Long |

### HTML 양식을 사용한 객체 업로드

폼을 사용해 객체 업로드를 요청합니다.

#### 업로드용 form body 구성

이 API는 양식 매개변수에 따라 맨 처음에 form body 부분을 구성하는 데 사용됩니다.

```java
String buildPostObjectBody(String boundary, Map<String, String> formFields, String filename, String contentType) {
    StringBuffer stringBuffer = new StringBuffer();
    for(Map.Entry entry: formFields.entrySet()) {
        // --로 시작하는 boundary 행을 추가합니다.
        stringBuffer.append("--").append(boundary).append("\r\n");
        // 필드 이름
        stringBuffer.append("Content-Disposition: form-data; name=\""
                + entry.getKey() + "\"\r\n\r\n");
        // 필드 값
        stringBuffer.append(entry.getValue() + "\r\n");
    }
    // --로 시작하는 boundary 행을 추가합니다.
    stringBuffer.append("--").append(boundary).append("\r\n");
    // 파일 이름
    stringBuffer.append("Content-Disposition: form-data; name=\"file\"; "
            + "filename=\"" + filename + "\"\r\n");
    // 파일 유형
    stringBuffer.append("Content-Type: " + contentType + "\r\n\r\n");
    return stringBuffer.toString();
}
```

#### 로컬 파일 업로드

```java
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// COS_REGION에 대한 자세한 내용은 https://cloud.tencent.com/document/product/436/6224을(를) 참고하십시오.
String endpoint = "cos.{COS_REGION}.myqcloud.com";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// SECRETID 및 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리합니다.
String secretId = "AKIDXXXXXXXX";
String seretKey = "1A2Z3YYYYYYYYYY";

String localFilePath = "/path/to/localFile";
String contentType = "image/jpeg";

long startTimestamp = System.currentTimeMillis() / 1000;
long endTimestamp = startTimestamp +  30 * 60;
String endTimestampStr = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'").format(endTimestamp * 1000);

String keyTime = startTimestamp + ";" + endTimestamp;
String boundary = "----WebKitFormBoundaryZBPbaoYE2gqeB21N";

// 양식의 body 필드를 설정합니다.
Map<String, String> formFields = new HashMap<>();
formFields.put("q-sign-algorithm", "sha1");
formFields.put("key", key);
formFields.put("q-ak", secretId);
formFields.put("q-key-time", keyTime);

// 정책을 구성합니다. 자세한 내용은 https://intl.cloud.tencent.com/document/product/436/14690을(를) 참고하십시오.
String policy = "{\n" +
        "    \"expiration\": \"" + endTimestampStr + "\",\n" +
        "    \"conditions\": [\n" +
        "        { \"bucket\": \"" + bucketName + "\" },\n" +
        "        { \"q-sign-algorithm\": \"sha1\" },\n" +
        "        { \"q-ak\": \"" + secretId + "\" },\n" +
        "        { \"q-sign-time\":\"" + keyTime + "\" }\n" +
        "    ]\n" +
        "}";

// policy는 양식에 배치되기 전에 base64로 인코딩되어야 합니다.
String encodedPolicy = new String(Base64.encodeBase64(policy.getBytes()));
// policy를 설정합니다.
formFields.put("policy", encodedPolicy);
// 인코딩된 policy와 secretKey에 따라 서명을 계산합니다.
COSSigner cosSigner = new COSSigner();
String signature = cosSigner.buildPostObjectSignature(seretKey,
        keyTime, policy);
// 서명을 설정합니다.
formFields.put("q-signature", signature);

// 상기 양식 매개변수에 따라 맨 처음에 body 부분을 구성합니다.
String formBody = buildPostObjectBody(boundary, formFields,
        localFilePath, contentType);

HttpURLConnection conn = null;
try {
    String urlStr = "http://" + bucketName + "." + endpoint;
    URL url = new URL(urlStr);
    conn = (HttpURLConnection) url.openConnection();
    conn.setRequestMethod("POST");
    conn.setRequestProperty("User-Agent", VersionInfoUtils.getUserAgent());
    conn.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
    conn.setDoOutput(true);
    conn.setDoInput(true);

    OutputStream out = new DataOutputStream(conn.getOutputStream());
    // 양식의 맨 처음에 씁니다.
    out.write(formBody.getBytes());

    // 파일 콘텐츠를 출력 스트림에 씁니다.
    File file = new File(localFilePath);
    DataInputStream in = new DataInputStream(new FileInputStream(file));
    int readBytes;
    byte[] bytes = new byte[4096];
    while ((readBytes = in.read(bytes)) != -1) {
        out.write(bytes, 0, readBytes);
    }
    in.close();

    // --로 시작하고 끝나는 마지막 구분자를 추가합니다.
    byte[] endData = ("\r\n--" + boundary + "--\r\n").getBytes();
    out.write(endData);
    out.flush();
    out.close();

    // 응답 헤더를 읽습니다.
    for (Map.Entry<String, List<String>> entries : conn.getHeaderFields().entrySet()) {
        String values = "";
        for (String value : entries.getValue()) {
            values += value + ",";
        }
        if(entries.getKey() == null) {
            System.out.println("reponse line:" +  values );
        } else {
            System.out.println(entries.getKey() + ":" +  values );
        }
    }
} catch (Exception e) {
    e.printStackTrace();
    throw e;
} finally {
    if (conn != null) {
        conn.disconnect();
    }
}
```

## 멀티파트 작업

대용량 파일이 업로드되면 대용량 파일의 긴 업로드 시간으로 인해 발생할 수 있는 중단을 해결하기 위해 파일이 일련의 파트로 업로드됩니다.

>? 업로드된 파일이나 스트림을 전체적으로 얻으려면 고급 API를 사용하는 것이 좋습니다.
>

### 작업 단계

#### 멀티파트 업로드 프로세스

1. 멀티파트 업로드를 초기화(Initiate Multipart Upload)하고 UploadId 획득
2. UploadId를 사용해 파트를 업로드합니다(Upload Part).
3. 멀티파트 업로드 완료(Complete Multipart Upload)

#### 멀티파트 업로드 재개 프로세스

1. 멀티파트 업로드의 UploadId를 기록하지 않은 경우 먼저 멀티파트 업로드 목록(List Multipart Uploads)을 쿼리하여 파일의 UploadId를 가져올 수 있습니다.
2. UploadId를 사용해 업로드된 멀티파트 나열(List Parts)
3. UploadId를 사용해 나머지 파트를 업로드합니다(Upload Part).
4. 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 멀티파트 업로드 프로세스 종료

1. 멀티파트 업로드의 UploadId를 기록하지 않은 경우 멀티파트 업로드 목록(List Multipart Uploads)을 사용하여 멀티파트 업로드 작업을 쿼리하여 파일의 UploadId를 가져올 수 있습니다.
2. 멀티파트 업로드를 중지하고 업로드된 멀티파트 삭제(Abort Multipart Upload)

### 멀티파트 업로드 초기화

이 API는 멀티파트 업로드를 초기화하여 후속 작업에 대한 uploadId를 가져오는 데 사용됩니다.

#### 메소드 프로토타입

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### 요청 예시

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";

InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, key);

// 멀티파트 업로드 시 멀티파트 업로드를 초기화해야만 업로드된 파일의 metadata를 지정할 수 있습니다.
// 원하는 헤더를 지정합니다.
ObjectMetadata objectMetadata = new ObjectMetadata();
request.setObjectMetadata(objectMetadata);

try {
    InitiateMultipartUploadResult initResult = cosClient.initiateMultipartUpload(request);
    // uploadid 가져오기
    String uploadId = initResult.getUploadId();
    System.out.println(uploadId);
} catch (CosServiceException e) {
    throw e;
} catch (CosClientException e) {
    throw e;
}
```

#### 매개변수 설명

| 매개변수 이름                       | 설명 | 유형                           |
| ------------------------------ | ---- | ------------------------------ |
| initiateMultipartUploadRequest | 요청 | InitiateMultipartUploadRequest |

Request 멤버 설명:

| 매개변수 이름   | 설정 방법            | 설명                                                         | 유형   |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String            |
| key        | 구조 함수 또는 set 메소드 | 멀티파트 업로드할 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 지정합니다. 예를 들어 객체 키는 folder/picture.jpg입니다.  | String |

#### 반환 결과 설명

- 성공: 이번 멀티파트 업로드의 uploadId를 포함한 InitiateMultipartUploadResult를 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

### 멀티파트 업로드 쿼리

이 API(List Multipart Uploads)는 원하는 멀티파트 업로드 작업의 uploadId를 찾기 위해 진행 중인 모든 멀티파트 업로드 작업을 가져오는 데 사용됩니다.

#### 메소드 프로토타입

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### 요청 예시

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

// 쿼리할 멀티파트 업로드 작업의 key
String targetKey = "targetKey";

ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
// 요청당 나열할 수 있는 멀티파트 업로드 작업의 최대 수
listMultipartUploadsRequest.setMaxUploads(100);
// 쿼리할 멀티파트 업로드 작업의 대상 접두사(key)를 설정합니다.
listMultipartUploadsRequest.setPrefix("targetKey");

MultipartUploadListing multipartUploadListing = null;

boolean found = false;

do {
    multipartUploadListing = cosClient.listMultipartUploads(listMultipartUploadsRequest);
    List<MultipartUpload> multipartUploads = multipartUploadListing.getMultipartUploads();

    for (MultipartUpload mUpload : multipartUploads) {
        if (mUpload.getKey().equals(targetKey)) {
            System.out.println(mUpload.getUploadId());
            found = true;
            break;
        }
    }

    if (found) {
        break;
    }

} while (multipartUploadListing.isTruncated());

if (!found) {
    System.out.printf("do not found upload task with key: %s\n", targetKey);
}
```

#### 매개변수 설명

| 매개변수 이름                    | 설명                                        | 유형     |
| --------------------------- | ---- | --------------------------- |
| listMultipartUploadsRequest | 요청 | ListMultipartUploadsRequest |

Request 멤버 설명:

| 매개변수 이름       | 설명                                                         | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName     | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| keyMarker      | 해당 key값부터 시작하여 항목 열거                                      | String |
| delimiter      | 구분 문자는 하나의 부호입니다. Prefix가 있으면 Prefix에서 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의한 후 모든 Common Prefix를 나열합니다. Prefix가 없으면 경로의 시작점부터 시작합니다. | String |
| prefix         | 접두사가 Prefix인 Object key를 반환하도록 한정. Prefix를 사용하여 조회할 경우 반환되는 key에는 Prefix가 포함되므로 주의해야 합니다. | String |
| uploadIdMarker | 해당 UploadId 값부터 시작하여 항목 열거                                 | String |
| maxUploads     | 반환되는 최대 multipart 수량 설정. 유효한 값 범위: 1-1000.                 | String |
| encodingType   | 반환값의 인코딩 방식을 규정. 옵션값: url                            | String |

#### 반환 결과 설명

- 성공: 현재 진행 중인 멀티파트 업로드 정보를 포함한 MultipartUploadListing을 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

### 멀티파트 업로드

객체를 멀티파트 업로드합니다(Upload Part).

#### 메소드 프로토타입

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### 요청 예시

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// uploadId는 멀티파트 업로드 작업의 고유 식별자로, 멀티파트 업로드를 초기화하거나 멀티파트 업로드 작업을 쿼리하여 얻을 수 있습니다.
String uploadId = "exampleuploadid";

// 각 파트가 업로드되면 etag가 반환됩니다. 저장하고 나중에 파트를 결합하는 데 사용할 수 있습니다.
List<PartETag> partETags = new LinkedList<>();

// 데이터를 업로드합니다. 여기에 10개의 파트(각 1M)가 업로드됩니다.
for (int i = 1; i <= 10; i++) {
    byte data[] = new byte[1024 * 1024];
    // 여기서는 ByteArrayInputStream 스트림을 예시로 생성했습니다. 실제로는 업로드를 위해 InputStream 유형의 스트림을 생성해야 합니다.
    long inputStreamLength = 1024 * 1024;
    byte data[] = new byte[inputStreamLength];
    InputStream inputStream = new ByteArrayInputStream(data);

    UploadPartRequest uploadPartRequest = new UploadPartRequest();
    uploadPartRequest.setBucketName(bucketName);
    uploadPartRequest.setKey(key);
    uploadPartRequest.setUploadId(uploadId);
    uploadPartRequest.setInputStream(inputStream(data));
    // 파트 길이 설정
    uploadPartRequest.setPartSize(data.length);
    // 1부터 시작하는 파트 번호를 설정합니다.
    uploadPartRequest.setPartNumber(i);

    try {
        UploadPartResult uploadPartResult = cosClient.uploadPart(uploadPartRequest);
        PartETag partETag = uploadPartResult.getPartETag();
        partETags.add(partETag);
    } catch (CosServiceException e) {
        throw e;
    } catch (CosClientException e) {
        throw e;
    }
}

System.out.println(partETags);
```

#### 매개변수 설명

| 매개변수 이름         | 설명                                                         | 유형   |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | 요청 | UploadPartRequest |

Request 멤버 설명:

| 매개변수 이름    | 설정 방법 | 설명                                                         | 유형        |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | set 메소드  | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String      |
| key         | set 메소드 | 멀티파트 업로드할 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 지정합니다. 예를 들어 객체 키는 folder/picture.jpg입니다. | String      |
| uploadId    | set 메소드  | 지정한 멀티파트 업로드의 uploadId를 식별                                  | String      |
| partNumber  | set 메소드  | 지정한 멀티파트의 번호를 식별. 번호는 반드시 1보다 크거나 같아야 합니다.                                | int         |
| inputStream | set 메소드  | 멀티파트를 업로드할 입력 스트림을 기다립니다.                                           | InputStream |
|trafficLimit| set 메소드| 멀티파트 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어는 비활성화되어 있습니다.  | Int|

#### 반환 결과 설명

- 성공: 멀티파트 업로드의 eTag 정보를 포함한 UploadPartResult를 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

UploadPartResult 유형은 결과 정보 반환에 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | 지정한 멀티파트의 번호를 식별 | String                |
| eTag        | 멀티파트 업로드의 MD5 값을 반환                   | String |
|crc64Ecma| 서버에서 멀티파트 콘텐츠에 따라 계산한 CRC64| String |

### 업로드된 멀티파트 조회

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다(List Parts).

#### 메소드 프로토타입

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// uploadId는 멀티파트 업로드 작업의 고유 식별자로, 멀티파트 업로드를 초기화하거나 멀티파트 업로드 작업을 쿼리하여 얻을 수 있습니다.
String uploadId = "exampleuploadid";

// 업로드된 모든 파트의 정보를 저장하기 위해 사용합니다.
List<PartETag> partETags = new LinkedList<>();

PartListing partListing = null;
ListPartsRequest listPartsRequest = new ListPartsRequest(bucketName, key, uploadId);
do {
    try {
        partListing = cosClient.listParts(listPartsRequest);
    } catch (CosServiceException e) {
        throw e;
    } catch (CosClientException e) {
        throw e;
    }

    for (PartSummary partSummary : partListing.getParts()) {
        partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
    }

    listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());
```

#### 매개변수 설명

| 매개변수 이름         | 설정 방법            | 설명                                                         | 유형   |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName       | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key              | 구조 함수 또는 set 메소드 | 객체의 이름                                                   | String |
| uploadId         | 구조 함수 또는 set 메소드 | 이번에 조회할 멀티파트 업로드의 uploadId                               | String |
| maxParts         | set 메소드            | 한 번에 반환 가능한 최대 항목 수. 기본값: 1000                             | String |
| partNumberMarker | set 메소드            | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 marker부터 시작  | String |
| encodingType     | set 메소드            | 반환값의 인코딩 방식을 규정                                         | String |

#### 반환 결과 설명

- 성공: 모든 파트의 ETag와 번호 및 다음 list의 시작 marker를 포함한 PartListing을 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

### 멀티파트 업로드 완료

전체 파일의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

>? 멀티파트 업로드가 완료되면 멀티파트 업로드 작업이 삭제되고 uploadId는 더 이상 유효하지 않습니다.
>

#### 메소드 프로토타입

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### 요청 예시

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// uploadId는 멀티파트 업로드 작업의 고유 식별자로, 멀티파트 업로드를 초기화하거나 멀티파트 업로드 작업을 쿼리하여 얻을 수 있습니다.
String uploadId = "exampleuploadid";

// 멀티파트 업로드 API에서 가져올 수 있는 업로드된 파트의 정보를 저장하는 데 사용됩니다.
List<PartETag> partETags = new LinkedList<>();

// 멀티파트 업로드가 완료된 후 complete를 호출하여 업로드를 완료합니다.
CompleteMultipartUploadRequest completeMultipartUploadRequest =
        new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
try {
    CompleteMultipartUploadResult completeResult =
            cosClient.completeMultipartUpload(completeMultipartUploadRequest);
    System.out.println(completeResult.getRequestId());
} catch (CosServiceException e) {
    throw e;
} catch (CosClientException e) {
    throw e;
}

// cosClient 인스턴스가 더 이상 사용되지 않음을 확인한 후 종료합니다.
cosClient.shutdown();
```

#### 매개변수 설명

| 매개변수 이름   | 설정 방법&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            | 설명                                                         | 유형              |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String            |
| key        | 구조 함수 또는 set 메소드 | 멀티파트 업로드할 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 지정합니다. 예를 들어 객체 키는 folder/picture.jpg입니다. | String            |
| uploadId   | 구조 함수 또는 set 메소드 | 지정한 멀티파트 업로드의 uploadId를 식별                                  | String            |
| partETags  | 구조 함수 또는 set 메소드 | 멀티파트의 번호와 업로드에서 반환하는 eTag를 식별                            | List&lt;PartETag&gt; |

#### 반환 결과 설명

- 성공: 완료된 객체의 eTag 정보를 포함한 CompleteMultipartUploadResult를 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

### 멀티파트 업로드 중지

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다(Abort Multipart Upload).

>? 멀티파트 업로드가 중단되면 멀티파트 업로드 작업과 업로드된 파트가 모두 삭제되고 uploadId는 더 이상 유효하지 않습니다.
>

#### 메소드 프로토타입

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### 요청 예시

```java
// COS API를 사용하기 전에 프로세스에 COSClient 인스턴스가 포함되어 있는지 확인해야 합니다. 그렇지 않은 경우 생성하십시오.
// 상세 코드 참고 페이지: 간단한 작업 -> COSClient 인스턴스 생성
COSClient cosClient = createCOSClient();
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 이 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// uploadId는 멀티파트 업로드 작업의 고유 식별자로, 멀티파트 업로드를 초기화하거나 멀티파트 업로드 작업을 쿼리하여 얻을 수 있습니다.
String uploadId = "exampleuploadid";

AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
try {
    cosClient.abortMultipartUpload(abortMultipartUploadRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// cosClient 인스턴스가 더 이상 사용되지 않음을 확인한 후 종료합니다.
cosClient.shutdown();
```

#### 매개변수 설명

| 매개변수 이름   | 설정 방법            | 설명                                                         | 유형   |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key        | 구조 함수 또는 set 메소드 | 멀티파트 업로드할 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)입니다. 예를 들어 객체 키는 folder/picture.jpg입니다. | String |
| uploadId   | 구조 함수 또는 set 메소드 | 지정한 멀티파트 업로드의 uploadId를 식별                                  | String            |

#### 반환 결과 설명

- 성공: 반환값 없음.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.
