### 클라이언트 네트워크는 정상인데 HTTP로 COS 액세스가 굉장히 느리거나 Connection reset 오류가 발생합니다. 어떻게 처리해야 하나요?
일부 지역 ISP에서 COS 도메인을 하이재킹했을 수 있습니다. 최대한 HTTPS를 사용해 COS에 액세스하시기 바랍니다.

### SDK 실행 후 java.lang.NoSuchMethodError 오류가 발생합니다. 어떻게 처리해야 하나요?

원인: 일반적으로 JAR 패키지 충돌이 발생했기 때문입니다. 예를 들어 사용자가 작업하는 httpclient 라이브러리의 JAR 패키지 버전은 A 방법이 없는데 SDK에 종속된 JAR 패키지가 A 방법을 사용하는 경우입니다. 이로 인해 실행 시 로딩 순서에 문제가 생기고, 사용자 프로그램의 httpclient 라이브러리가 로딩되어 NoSuchMethodError 오류가 발생하게 됩니다.
해결 방법:
방법1: 프로그램 중 NoSuchMethodError 오류를 일으키는 패키지 버전을 SDK pom.xml 내의 해당 라이브러리의 버전과 일치하도록 변경하십시오.
방법2: cos-java-sdk를 cos_api-bundle로 변경합니다. 이 방법은 cos-java-sdk의 모든 종속을 독립적으로 설치하여 더 많은 용량을 차지합니다.
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### Java SDK의 기본 타임아웃 시간은 얼마나 되나요?

Java SDK의 기본 연결 타임아웃 시간은 45000ms이며, 기본 읽기/쓰기 타임아웃 시간은 45000ms입니다. SDK의 SetConnectionTimeoutMs 방법과 SetReadWriteTimeoutMs 방법을 사용해 변경할 수 있습니다.

### Java SDK 업로드 속도가 느리고 로그에서 IOException이 빈번하게 출력됩니다. 어떻게 처리해야 하나요?

원인과 해결 방법은 다음과 같습니다.

1. 먼저 공용 네트워크로 COS에 액세스하지 않았는지 확인합니다. 현재 동일 리전 내 CVM은 내부 네트워크로 COS에 액세스합니다. 내부 네트워크가 리졸브되는 IP 대역은 10, 100, 169입니다. COS 도메인과 관련된 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. 공용 네트워크로 내보내는 대역폭이 좁지 않은지 또는 다른 프로그램이 대역폭 리소스를 점유하고 있지 않은지 확인하십시오.
2. 생성 환경의 로그 레벨이 DEBUG가 아닌지 확인하십시오. INFO 로그 사용을 권장합니다.
3. 현재 간편 업로드의 속도는 10MB에 달하며, 고급 API로 32개를 동시 업로드를 하는 경우 60MB에 달합니다. 만약 속도가 이 두 값보다 훨씬 낮다면 위의 두 사항을 참고하십시오.
4. WARN 로그에서 IOException이 출력되면 SDK가 재시작되므로 무시해도 됩니다. IOException의 원인이 너무 느린 네트워크 속도 때문이라면 해결 방법 1과 2를 참고하십시오.

### 파일 업로드 요청 경로에 '+'가 있으면 Code: 403  SignatureDoesNotMatch 오류가 발생합니다. 어떻게 처리해야 하나요?
예상 원인: 사용자 Java 환경의 httpclient 버전으로 인한 urlencode 인코딩 오류일 수 있습니다.
해결 방법: 다음 방법을 통해 해결하는 것을 권장합니다.
방법1: httpclient 4.5.3 버전 사용
```
<groupId>org.apache.httpcomponents</groupId>
       <artifactId>httpclient</artifactId>
 <version>4.5.3</version> 
```

방법2: cos-java-sdk를 cos_api-bundle로 변경합니다. 이 방법은 cos-java-sdk의 모든 종속을 독립적으로 설치하여 더 많은 용량을 차지합니다.
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### Java SDK 사용 시 특정 종속 버전이 너무 낮다고 안내되며 오류가 발생합니다. 어떻게 처리해야 하나요?
원인: 사용자의 Java 환경 종속 버전과 Java SDK에서 필요한 종속 버전에 충돌이 발생한 경우일 수 있습니다.
해결 방법:
방법1: 안내에 따라 해당 종속을 필요한 버전으로 업데이트하십시오.
방법2: cos-java-sdk를 cos_api-bundle로 변경합니다. 이 방법은 cos-java-sdk의 모든 종속을 독립적으로 설치하여 더 많은 용량을 차지합니다.
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### SDK는 어떻게 디렉터리를 생성하나요?

COS에서 파일과 디렉터리는 모두 객체이며 디렉터리는 `/`로 끝나는 객체입니다. 파일 생성 시 디렉터리를 생성할 필요가 없습니다. 예를 들어 객체 키가 `xxx/yyy/zzz.txt`인 파일을 생성할 때는 key를 `xxx/yyy/zzz.txt`로 설정하면 되고 `xxx/yyy/` 객체를 생성할 필요가 없습니다. 콘솔에서 표시할 때 `/`로 분리되어 디렉터리 계층적 효과를 나타내지만, 해당 디렉터리 객체는 존재하지 않습니다. 디렉터리 객체를 생성하려면 아래 예시 코드를 사용할 수 있습니다.

```java
String bucketName = "examplebucket-1250000000";
String key = "folder/images/";
// 디렉터리 객체는 /로 끝나는 빈 파일이며, 길이가 0인 byte 스트림을 업로드함
InputStream input = new ByteArrayInputStream(new byte[0]);
ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setContentLength(0);

PutObjectRequest putObjectRequest =
new PutObjectRequest(bucketName, key, input, objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### SDK는 HTTPS를 어떻게 사용하나요?

SDK 관련 설정은 ClientConfig 클래스에 통합되어 있으며 예시 코드는 아래와 같습니다.

```java
// 사용자의 개인 정보(secretId, secretKey) 초기화
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// bucket의 리전 설정. COS 리전의 약칭은 https://intl.cloud.tencent.com/document/product/436/6224 참고
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// https 사용 설정
clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
```

### SDK는 프록시를 어떻게 사용하나요?

프록시로 COS 액세스가 필요한 클라이언트의 경우 ClientConfig 클래스에서 사용할 프록시 IP(혹은 도메인) 및 포트를 설정하십시오. 예시 코드는 아래와 같습니다.

```java
// 사용자의 개인 정보(secretId, secretKey) 초기화
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// bucket의 리전 설정. COS 리전의 약칭은 https://intl.cloud.tencent.com/document/product/436/6224 참고
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 사용할 프록시 설정(IP와 포트를 함께 설정해야 함)
// 프록시 IP 설정(도메인 입력 가능)
clientConfig.setHttpProxyIp("192.168.2.3");
// 프록시 포트 설정
clientConfig.setHttpProxyPort(8080);
// cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
```

### 사용자 정의 EndpointBuilder는 어떻게 설정하나요?
시나리오에서 API가 요청한 Endpoint를 지정해야 할 수 있습니다. 이때 EndpointBuilder 인터페이스 내 buildGeneralApiEndpoint와 buildGetServiceApiEndpoint에서 두 가지 함수를 구현해야 하며, 각각 일반 API 요청과 GETService 요청에 대한 원격 Endpoint를 지정해야 합니다. 사용 예시는 아래와 같습니다.
```
// 1단계: EndpointBuilder 인터페이스의 두 가지 함수 구현
class SelfDefinedEndpointBuilder implements EndpointBuilder {
    @Override
    public String buildGeneralApiEndpoint(String bucketName) {
        return String.format("%s.%s", bucketName, "mytest.com");
    }

    @Override
    public String buildGetServiceApiEndpoint() {
        return "service.mytest.com";
    }
}

// 2단계: 클라이언트 초기화
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
SelfDefinedEndpointBuilder selfDefinedEndpointBuilder = new SelfDefinedEndpointBuilder();
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
clientConfig .setEndpointBuilder(selfDefinedEndpointBuilder);
COSClient cosClient = new COSClient(cred, clientConfig);
```

### SDK 업로드, 다운로드, 일괄 삭제 등의 작업 시 사용하는 key 값에 접두사 `/`를 추가해야 하나요?
COS의 key 값은 `/` 접두사가 필요 없습니다. 예를 들어 객체 key 값을 exampleobject로 업로드 객체로 설정하면 URL: `http://cos.ap-guangzhou.myqcloud.com/exampleobject`로 액세스할 수 있습니다.
>!일괄 삭제 요청 시 접두사 `/`로 시작하는 key를 넣지 마십시오. 객체 삭제에 실패할 수 있습니다.


### COS에서 Java SDK로 업로드 시 please make sure bucket name must contain legal appid when appid is missing. example: bucektname-1250000000 오류가 발생합니다. 어떻게 처리해야 하나요?

COS Java SDK 구 버전은 예를 들어 125로 시작하는 APPID만 지원합니다. 만약 130으로 시작하는 APPID를 사용하는 경우 SDK를 최신 버전으로 업데이트하는 것을 권장합니다. Java SDK의 다운로드 및 설치는 [Java SDK 문서](https://intl.cloud.tencent.com/document/product/436/10199)를 참고하십시오.

### COS Java SDK로 대용량 파일을 업로드하면 오류가 발생합니다. 어떻게 처리해야 하나요?

Java SDK로 5G를 초과하는 파일을 업로드하는 경우 [고급 업로드 인터페이스](https://intl.cloud.tencent.com/document/product/436/31534) 사용을 권장합니다. 고급 업로드 인터페이스는 사용자 파일의 크기와 데이터 유형에 따라 간편 업로드 또는 멀티파트 업로드 방식을 자동으로 선택합니다.

### Java SDK에서 파일 업로드 진행률은 어떻게 확인하나요?

업로드 진행률을 확인하려면 [고급 업로드](https://intl.cloud.tencent.com/document/product/436/31534) 인터페이스 사용을 권장합니다. Upload의 getProgress() 방법을 호출하여 업로드 진행률인 TransferProgress 유형을 가져옵니다.

### Java SDK는 로컬 파일의 CRC64 계산을 지원하나요?

COS Java SDK 자체는 로컬 파일의 crc64 계산을 지원하지 않으며, 사용자의 서비스에서 직접 구현해야 합니다. [Java issues](https://github.com/tencentyun/cos-java-sdk-v5/issues/63)를 참고하여 방법을 확인하십시오.

### Java SDK가 COS에서 반환된 CRC64가 21비트인지 확인하고, 로컬에서 계산된 CRC64와 비교하는 방법은 무엇입니까?

Java의 Long은 20자리 숫자만 지원합니다. 다음 비교 방식을 참고하십시오.

```java
CRC64 localCRC = new CRC64();
// 로컬 crc64 계산
localCRC.update();
//...

// COS 가 반환한 CRC 를 Long으로 변환
cosCRC = crc64ToLong(strCOSCRC);

// 비교
if (cosCRC == localCRC.getValue()) {
   xxx
}

// COS에서 반환된 CRC64를 1개 Java 내 Long으로 변환하는 데 사용
long crc64ToLong(String crc64) {
   if (crc64.charAt(0) == '-') {
       return negativeCrc64ToLong(crc64);
   } else {
       return positiveCrc64ToLong(crc64);
   }
}

long positiveCrc64ToLong(String strCrc64) {
   BigInteger crc64 = new BigInteger(strCrc64);
   BigInteger maxLong = new BigInteger(Long.toString(Long.MAX_VALUE));

   int maxCnt = 0;

   while (crc64.compareTo(maxLong) > 0) {
       crc64 = crc64.subtract(maxLong);
       maxCnt++;
   }

   return crc64.longValue() + Long.MAX_VALUE * maxCnt;
}

long negativeCrc64ToLong(String strCrc64) {
   BigInteger crc64 = new BigInteger(strCrc64);
   BigInteger minLong = new BigInteger(Long.toString(Long.MIN_VALUE));

   int minCnt = 0;

   while (crc64.compareTo(minLong) < 0) {
       crc64 = crc64.subtract(minLong);
       minCnt++;
   }

   return crc64.longValue() + Long.MIN_VALUE * minCnt;
}
```

### Java SDK에서 장기간 연결을 사용할 수 있나요?

Java SDK는 기본적으로 장기간 연결을 사용합니다.

### Java SDK로 지정 디렉터리의 모든 경로를 어떻게 획득하나요? 경로가 파일인지 폴더인지 어떻게 판단하나요?

Java SDK의 [객체 리스트 조회](https://intl.cloud.tencent.com/document/product/436/10199#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8) 기능으로 버킷에 있는 객체를 나열할 수 있으며, **prefix 매개변수로 디렉터리 접두사를 지정할 수 있습니다.**



