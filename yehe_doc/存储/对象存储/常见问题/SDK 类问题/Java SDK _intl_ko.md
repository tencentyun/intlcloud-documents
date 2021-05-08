
### 클라이언트 네트워크는 정상인데 HTTP로 COS 액세스가 굉장히 느리거나 Connection reset 오류가 발생합니다. 어떻게 처리해야 하나요?
일부 지역 ISP에서는 COS 도메인을 하이재킹하기도 합니다. 최대한 HTTPS를 사용해 COS에 액세스하시기 바랍니다.

### SDK 실행 후 java.lang.NoSuchMethodError 오류가 발생합니다. 어떻게 처리해야 하나요?

일반적으로 JAR 패킷 충돌이 발생했기 때문입니다. 예를 들어 사용자가 작업하는 httpclient 라이브러리의 JAR 패킷 버전은 A 방법이 없는데 SDK에 종속된 JAR 패킷이 A 방법을 사용하는 경우입니다. 이 때문에 실행 시 로딩 순서에 문제가 생기고 사용자가 작업하는 httpclient 라이브러리가 로딩되어 NoSuchMethodError 오류가 발생하게 됩니다.
해결 방법: 작업 중 NoSuchMethodError 오류를 유발하는 패킷 버전을 SDK의 pom.xml 안에 있는 해당 라이브러리 버전과 동일한 버전으로 변경하십시오.

### SDK 업로드 속도가 느리고 로그에서 IOException 오류가 빈번하게 출력됩니다. 어떻게 처리해야 하나요?

원인과 해결 방법:

 a. 먼저 공용 네트워크로 COS에 액세스하지 않았는지 확인합니다. 현재 동일 리전 내 CVM은 내부 네트워크로 COS에 액세스합니다. 내부 네트워크가 리졸브되는 IP 대역은 10, 100, 169입니다. COS 도메인에 대한 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. 공용 네트워크인 경우, 출력 대역폭이 좁지 않은지, 또는 다른 프로그램이 대역폭 리소스를 점유하고 있지 않은지 확인하십시오.
 b. 생성 환경에서의 로그 레벨이 DEBUG가 아닌지 확인하십시오. INFO 로그 사용을 권장합니다.
 c. 현재 간편 업로드 속도가 10MB에 달하며, 고급 API를 이용해 32개 동시 업로드를 하는 경우는 60MB에 달합니다. 속도가 해당 두 값보다 많이 낮다면 a와 b를 참고하십시오.
 d. WARN 로그의 IOException 출력은 무시해도 되며, SDK가 재시작됩니다. 네트워크 속도가 느려 IOException 오류가 발생한다면 a와 b를 참고하십시오.

### SDK는 어떻게 디렉터리를 생성하나요?

COS에서 파일과 디렉터리는 모두 객체이며, 디렉터리는 `/`로 끝나는 객체입니다. 파일 생성 시 디렉터리를 생성할 필요가 없습니다. 예를 들어 객체 키가 `xxx/yyy/zzz.txt`인 파일을 생성할 때는 key를 `xxx/yyy/zzz.txt`로 설정하면 되고 `xxx/yyy/` 객체를 생성할 필요가 없습니다. 콘솔에서 표시될 때 `/`로 분리되어 디렉터리의 계층적 효과를 나타내지만, 해당 디렉터리 객체는 존재하지 않습니다. 디렉터리 객체를 생성하려면 아래 예시 코드를 사용하십시오.

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
// bucket의 리전 설정, COS 리전의 약칭은 https://intl.cloud.tencent.com/document/product/436/6224 참조
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// https 사용 설정
clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
```

### SDK는 프록시를 어떻게 사용하나요?

프록시로 COS 액세스가 필요한 클라이언트의 경우, ClientConfig 클래스에서 사용하는 프록시 IP(혹은 도메인) 및 포트를 설정하십시오. 예시 코드는 아래와 같습니다.

```java
// 사용자의 개인 정보(secretId, secretKey) 초기화
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// bucket의 리전 설정, COS 리전의 약칭은 https://intl.cloud.tencent.com/document/product/436/6224 참조
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 사용할 프록시 설정(IP와 포트를 모두 설정해야 함)
// 프록시 IP 설정(도메인 입력 가능)
clientConfig.setHttpProxyIp("192.168.2.3");
// 프록시 포트 설정
clientConfig.setHttpProxyPort(8080);
// cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
```

### 사용자 정의 EndpointBuilder는 어떻게 설정하나요?
시나리오에서 API 요청의 Endpoint를 지정해야 할 수 있습니다. 이때 EndpointBuilder 인터페이스의 buildGeneralApiEndpoint와 buildGetServiceApiEndpoint 두 함수를 구현해야 하며, 이는 각각 일반 API 요청과 GETService 요청에 원격 Endpoint를 지정합니다. 사용 예시는 아래와 같습니다.
```
// 1단계: EndpointBuilder 인터페이스의 두 함수 구현
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
COS의 key 값에는 `/` 접두사가 필요 없습니다. 예를 들어 객체 key 값을 exampleobject로 업로드한 객체로 설정하면 URL: `http://cos.ap-guangzhou.myqcloud.com/exampleobject`를 통해 액세스할 수 있습니다.
>!일괄 삭제 요청 시, 접두사 `/`로 시작하는 key를 넣지 마십시오. 객체 삭제 실패 오류가 발생할 수 있습니다.
