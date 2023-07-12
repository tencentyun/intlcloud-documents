## 기본 개념

Tencent Cloud COS는 HTTP/HTTPS 프로토콜을 사용해 액세스하는 Web 스토리지 서비스입니다. [REST API](https://intl.cloud.tencent.com/document/product/436/7751) 또는 [COS SDK](https://intl.cloud.tencent.com/document/product/436/6474)를 사용해 COS에 액세스할 수 있습니다.

COS 액세스 요청 실행 시, COS 인증을 거쳐야만 리소스 작업이 가능합니다. 따라서 신분 식별 가능 여부에 근거하여, COS 액세스 요청은 익명 요청과 서명 요청의 2가지 유형으로 나뉩니다.

- 익명 요청: Authorization 또는 관련 매개변수를 가지고 있지 않거나, 관련 문자가 사용자의 신분 특징을 식별할 수 없는 경우, 익명 요청으로 간주되어 인증을 진행합니다.
- 서명 요청: 서명된 요청은 HTTP 헤더 또는 요청 패킷에 Authorization 필드가 포함돼야 합니다. 해당 필드의 콘텐츠는 Tencent Cloud의 보안 자격 증명 SecretID, SecretKey 및 요청된 일부 특징 값을 결합한 것이며, 암호화 알고리즘으로 생성됩니다.

COS SDK 호출을 사용할 경우 보안 자격 증명만 설정하면 요청을 발송할 수 있습니다. REST API 호출을 사용할 경우 [서명 요청](https://www.tencentcloud.com/document/product/436/7778) 문서를 참고하여 직접 요청 서명을 계산해야 합니다.

## 보안 자격 증명 얻기

CAM은 COS에 계정 및 보안 자격 증명 관련 기능과 서비스를 제공합니다. 주로 Tencent Cloud 계정에 있는 리소스의 액세스 권한을 안전하게 관리할 수 있도록 지원합니다. 사용자는 CAM을 통해 사용자(그룹)를 생성, 관리, 폐기할 수 있고 신분 관리 및 정책 관리를 사용해 기타 사용자의 Tencent Cloud 리소스 사용 권한을 제어할 수 있습니다.

### 루트 계정의 보안 자격 증명

루트 계정 로그인 후, CAM의 [Tencent Cloud API 키](https://console.cloud.tencent.com/cam/capi) 페이지를 통해 루트 계정 보안 자격 증명 SecretID와 SecretKey를 관리하고 얻을 수 있습니다. 다음은 한 그룹 키의 예시입니다.

- 36개 문자로 된 액세스 키 ID(SecretID): AKIDHZRLB9Ibhdp7Y7gyQq6BOk1997xxxxxx
- 32개 문자로 된 액세스 키(SecretKey): LYaWIuQmCSZ5ZMniUM6hiaLxHnxxxxxx

액세스 키는 고유한 계정을 표시하는 데 사용할 수 있습니다. 키 서명을 사용하여 요청을 보내면 Tencent Cloud는 요청 실행자의 신분을 식별하고 인증한 후, 신분, 리소스, 작업, 조건 등 인증을 거쳐 이 작업 실행을 허가할지 여부를 판단합니다.

>!루트 계정 키는 그에 속한 모든 리소스의 모든 조작 권한을 가지고 있습니다. 키가 유출되면 클라우드 리소스 손실 가능성이 있으므로, 서브 계정을 생성하고 적절히 권한을 할당할 것을 강력히 권장합니다. 서브 계정의 키 생성을 요청하여 리소스에 액세스 및 관리하십시오.

### 서브 계정의 보안 자격 증명

사용자 및 클라우드 리소스를 다각도로 관리해야 하는 경우, 루트 계정에 속한 여러 개의 서브 계정을 생성한 후 리소스 권한을 여러 계정이 나누어 관리하도록 할 수 있습니다. 서브 계정 생성에 대한 자세한 내용은 CAM의 [사용자 관리](https://intl.cloud.tencent.com/document/product/598/13674) 관련 문서를 참고하십시오.

서브 계정을 사용한 API 요청 발송 전, 서브 계정을 위한 보안 자격 증명을 생성해야 하며, 서브 계정도 신분 식별을 위해 고유한 키 쌍을 가지고 있어야 합니다. 각 서브 계정의 사용자 정책을 작성하면 리소스에 대한 각 계정의 액세스 권한을 제어할 수 있습니다. 또한 사용자 그룹을 생성하고 사용자 그룹에 통일된 액세스 정책을 추가하면 인원 그룹별 및 리소스에 대한 통합 관리가 가능합니다.

> !서브 계정은 해당 권한을 할당 받은 후, 리소스를 생성 또는 수정할 수 있습니다. 이 경우 리소스는 여전히 루트 계정에 속하며, 해당 리소스에서 발생하는 비용 역시 루트 계정이 지불합니다.

### 임시 보안 자격 증명

루트 계정 또는 서브 계정의 보안 자격 증명을 통한 리소스 액세스 외에도 Tencent Cloud는 역할 생성을 지원하고, 임시 보안 자격 증명을 사용하여 Tencent Cloud 리소스를 관리합니다. 역할 관련 기본 개념 및 사용 방법은 CAM의 [역할 관리](https://intl.cloud.tencent.com/document/product/598/19420) 문서를 참고하십시오.

역할은 가상 신분이기 때문에 영구적인 키를 가지고 있지 않으므로 Tencent Cloud의 CAM은 임시 보안 자격 증명을 생성하기 위한 STS API를 제공합니다.
사용 방법과 세부 예시는 [Using Role](https://intl.cloud.tencent.com/document/product/598/19419) 문서나 [CreateRole](https://intl.cloud.tencent.com/document/product/598/33561) 문서에서 임시 보안 자격 증명 생성 방식을 참고하십시오. 임시 보안 자격 증명에는 보통 **정책 제한**(작업, 리소스, 조건) 및 **시간 제한**(시작 및 종료 유효 시간)만 포함되므로, 생성된 임시 보안 자격 증명은 자체 배포하거나 직접 사용할 수 있습니다.

임시 보안 자격 증명을 생성하는 인터페이스를 호출하면 한 쌍의 임시 키(tmpSecretId/tmpSecretKey)와 보안 토큰(sessionToken)을 획득하게 되며, 이는 COS에 액세스하는 데 사용하는 보안 자격 증명을 구성합니다. 예시는 다음과 같습니다.

- 41개 문자로 된 보안 토큰(SecurityToken): 5e776c4216ff4d31a7c74fe194a978a3ff2xxxxxx
- 36개 문자로 된 임시 액세스 키 ID(SecretID): AKIDcAZnqgar9ByWq6m7ucIn8LNEuYxxxxxx
- 32개 문자로 된 임시 액세스 키(SecretKey): VpxrX0IMCpHXWL0Wr3KQNCqJixxxxxxx

해당 인터페이스는 또한 `expiration` 필드를 통해 임시 보안 자격 증명의 유효 시간을 반환하는데, 이는 이 시간 내에 해당 보안 자격 증명을 사용해야만 요청을 실행할 수 있음을 의미합니다.

Tencent Cloud COS는 임시 키 생성에 사용되는 간단한 서버 SDK를 제공하며, [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk)에 액세스하여 획득할 수 있습니다. 임시 보안 자격 증명을 받은 후 REST API를 사용하여 요청을 발송하려면 HTTP 헤더 또는 POST 요청 패킷의 form-data에 `x-cos-security-token` 필드를 전송하여 해당 요청에 사용한 보안 토큰을 표시한 한 후, 임시 액세스 키 쌍을 사용하여 요청 서명을 계산해야 합니다. COS SDK를 사용한 액세스 실행은 각 SDK 문서의 관련 부분을 참고하십시오.

## 도메인 이름 액세스

### REST API

[리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 문서에 REST API 호출 실행에 사용하는 리전 리스트가 나열되어 있습니다.

COS는 가상 호스팅형 도메인을 사용하여 버킷에 액세스하는 것을 권장합니다. HTTP 요청 실행 시 `<BucketName-APPID>.cos.<Region>.myqcloud.com`과 같이 직접 `Host` 헤더를 통해 액세스해야 하는 버킷을 가져옵니다. 가상 호스팅형 도메인을 사용해 가상 서버의 [루트 디렉터리]와 유사한 기능을 구현하며, favicon.ico, robots.txt, crossdomain.xml과 같은 파일을 호스팅하는 데 사용할 수 있습니다. 이 파일들은 여러 응용 프로그램이 호스팅 웹 사이트를 식별할 때 기본적으로 가상 서버의 [루트 디렉터리]에서 콘텐츠를 인덱스합니다.

경로형 요청을 통해 버킷에 액세스할 수도 있습니다. 예를 들어, `cos.<region>.myqcloud.com/<BucketName-APPID>/`의 경로를 사용하여 버킷에 액세스할 수 있습니다. 이와 마찬가지로, Host와 서명 요청은 `cos.<region>.myqcloud.com`을 사용해야 하며, SDK는 기본적으로 해당 액세스 방식을 지원하지 않습니다.

### 정적 웹 사이트 도메인

버킷의 정적 웹 사이트 기능 활성화 시, 관련 기능을 사용할 수 있도록 가상 호스팅형 도메인을 할당합니다. 정적 웹 사이트 도메인의 성능은 REST API와 다릅니다. 정적 웹 사이트 도메인은 특정 인덱스 페이지, 오류 페이지 및 리디렉션 설정을 제외하고 GET/HEAD/OPTIONS Object 등 몇 가지 작업만 지원하며, 업로드 또는 리소스 설정 작업은 지원하지 않습니다.

정적 웹 사이트 도메인 예시로는 `<BucketName-APPID>.cos-website.<Region>.myqcloud.com`가 있고, 콘솔의 버킷 [기본 설정 - 정적 웹 사이트 설정] 모듈을 통해 이 도메인을 얻을 수 있습니다.

<span id="network"></span>

## 사설망 액세스

Tencent Cloud COS의 액세스 도메인은 스마트 DNS 레졸루션을 사용하여 각 통신사 환경의 인터넷에서 COS 액세스를 검증하고 최적의 링크를 제공합니다.

Tencent Cloud에서 배포한 CVM 서비스가 사설망에서 COS에 액세스하려면, 먼저 CVM과 COS 버킷이 동일한 리전에 속하는지 확인한 후 CVM에서 `nslookup` 명령을 사용하여 COS 도메인 이름을 해석해야 합니다. 내부 IP가 반환되면 CVM과 COS 간에 사설망 액세스를 나타내고, 그렇지 않으면 공중망 액세스를 나타냅니다.

Tencent Cloud에서 배포한 CVM 서비스의 리전이 COS 버킷이 속한 리전과 다르지만, COS 사용 가능 리전 범위 내에 있는 경우, COS 사설망 전역 가속 도메인 이름을 통해 파일에 액세스하여 CVM과 COS의 리전 간 액세스를 구현할 수 있습니다.

### 사설망 액세스 판단 방법

동일한 리전 내의 Tencent Cloud 제품은 사설망을 통해 서로 액세스할 수 있으므로 트래픽 비용이 발생하지 않습니다. 따라서 비용을 절약하기 위해 다른 Tencent Cloud 제품을 구매할 때 동일한 리전을 선택하는 것이 좋습니다.

>! 퍼블릭 클라우드 리전의 사설망은 금융 클라우드 리전의 사설망과 상호 연결되지 않습니다.

다음은 사설망을 통한 액세스를 확인하는 방법입니다.

Tencent CVM을 통한 COS 액세스의 경우, 내부 인터넷을 이용하여 COS에 액세스했는지 판단하려면, CVM에서 `nslookup` 명령어를 사용하여 COS 도메인을 해석할 수 있습니다. 내부 IP를 반환한다면 CVM과 COS 간 사설망으로 액세스한 것이고, 아니라면 공중망으로 액세스한 것입니다.

>?내부 IP 주소는 일반적으로 `10.*.*.*`, `100.*.*.*` 형식이며, VPC 네트워크는 일반적으로 `169.254.*.*` 등의 형식입니다. 해당 두 가지 형식의 IP는 사설망에 속합니다.

`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`이 타깃 버킷 주소라고 가정하면, `nslookup` 명령어 실행 후 다음과 같은 정보를 확인할 수 있습니다.

![](https://main.qcloudimg.com/raw/49a7d7429ec2a96d271f6a63926286ea.png)

여기서 `10.148.214.13`와 `10.148.214.14`의 두 IP는 사설망을 통해 COS에 액세스했음을 의미합니다.


### 연결성 테스트

#### 기본 연결 테스트

COS는 HTTP 프로토콜을 사용하여 외부로 서비스를 제공합니다. 가장 기본적인 `telnet` 툴로 COS 액세스 도메인의 80 포트에 대해 액세스 테스트를 실행할 수 있습니다.

공중망을 통한 액세스 예시는 다음과 같습니다.

```shell
telnet examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com 80
Trying 14.119.113.22...
Connected to gz.file.myqcloud.com.
Escape character is '^]'.
```

같은 리전 내 Tencent Cloud CVM(기본 네트워크) 액세스 예시는 다음과 같습니다.

```shell
telnet examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com 80
Trying 10.148.214.14...
Connected to 10.148.214.14.
Escape character is '^]'.
```

같은 리전 내 Tencent Cloud CVM(VPC 네트워크) 액세스 예시는 다음과 같습니다.

```shell
telnet examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com 80
Trying 169.254.0.47....
Connected to 169.254.0.47.
Escape character is '^]'.
```

액세스 환경에 관계 없이, 명령어가 `Escape character is '^]'.` 필드를 반환한다면 연결에 성공했음을 의미합니다.

#### 인터넷 테스트를 통한 설명

인터넷을 통해 COS에 액세스하면 ISP 네트워크를 거치게 됩니다. ISP 네트워크는 ICMP 프로토콜의 `ping` 또는 `traceroute` 등 툴을 사용한 연결성 테스트를 허용하지 않습니다. 따라서 TCP 프로토콜의 툴을 사용한 연결성 테스트를 권장합니다.
>!인터넷을 통해 액세스하면 다양한 인터넷 환경의 영향을 받을 수 있습니다. 만약 액세스가 원활하지 못하다면, 로컬 네트워크 링크를 진단하거나 로컬 통신사에 연락하여 피드백을 받으십시오.

ISP가 ICMP 프로토콜을 허용하는 경우 `ping`, `traceroute` 또는 `mtr` 툴을 사용해 링크 상황을 검사할 수 있습니다. ISP가 ICMP 프로토콜을 허용하지 않을 경우 `psping`(Windows 환경, Microsoft 공식 홈페이지에서 다운로드) 또는 `tcping`(크로스 플랫폼 소프트웨어) 등의 툴을 사용해 딜레이 시간을 테스트할 수 있습니다.

#### 사설망 테스트 설명

같은 리전 내 Tencent Cloud VPC 네트워크를 통해 객체 스토리지 COS에 액세스하면, ICMP 프로토콜의 `ping` 또는 `traceroute` 등 툴을 사용하여 연결성을 테스트할 수 없습니다. 기본 연결 테스트 중 `telnet` 명령어를 사용하여 테스트를 진행할 것을 권장합니다.

`psping` 또는 `tcping` 등의 툴을 사용하여 직접 액세스 도메인의 80 포트에 대한 딜레이 시간 테스트를 시도해 볼 수도 있습니다. 테스트 전, `nslookup` 명령어를 통해 액세스 도메인이 사설망 주소에 정확하게 해석되었는지 조회 및 확인하십시오.


