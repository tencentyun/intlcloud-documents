## 기본 개념

Tencent Cloud COS는 HTTP/HTTPS 프로토콜을 사용하여 액세스하는 웹 기반 스토리지 서비스입니다. REST API 또는 [COS SDK](https://cloud.tencent.com/document/product/436/6474)를 사용하여 COS에 액세스 할 수 있습니다.

COS 접근 요청할 때 리소스를 작동하기 전에 먼저 COS 검증 및 인증을 통과해야 합니다. 따라서 신원을 식별 할 수 있는지 여부에 따라 COS 접근 요청은 익명 요청과 서명 요청의 두 가지 유형으로 나뉩니다.

- 익명 요청: 요청에 권한 부여 또는 관련 매개변수가 포함되어 있지 않거나 관련 문자를 기반으로 사용자 ID를 식별 할 수 없는 경우 해당 요청은 익명 요청으로 처리되며 인증을 진행합니다.
- 서명 요청: 서명 된 요청은 HTTP 헤더 또는 요청 패킷에 권한 부여 필드를 포함해야 합니다. 필드의 내용은 Tencent Cloud 보안 인증서 SecretID, SecretKey 및 요청의 일부 고유 값과 결합되며 암호화 알고리즘에 의해 생성됩니다.

COS SDK를 사용하여 COS에 접근하려면 요청을 시작하기 전에 보안 인증서를 구성하기만 하면 됩니다. REST API를 사용하여 COS에 접근하려면 [요청 서명](https://cloud.tencent.com/document/api/436/7778)에 따라 요청 서명을 계산하거나 [COS 서명 도구](https://cloud.tencent.com/document/product/436/30442)를 직접 생성합니다.

## 보안 인증서 취득

CAM은 COS에 대한 계정 및 인증서와 관련된 기능 및 서비스를 제공하여 고객이 Tencent Cloud 계정의 리소스에 안전하게 접근할 수 있는 권한을 관리 할 수 있도록 지원합니다. CAM을 사용하여 사용자(또는 사용자 그룹)를 생성, 관리 및 폐기하고 ID 관리 및 정책 관리를 통해 다른 사용자가 Tencent Cloud 리소스를 사용할 수 있는 권한을 관리합니다.

### 기본 계정 보안 인증서

루트 계정에 로그인한 후 CAM의 [클라우드 API 키](https://console.cloud.tencent.com/cam/capi) 페이지 접근하여 기본 계정 보안 인증서 SecretID 및 SecretKey 키를 관리하고 획득 할 수 있습니다. 다음은 키의 예시입니다.

> 36자 접근 키 ID(SecretID): AKIDHZRLB9Ibhdp7Y7gyQq6BOk1997BGmUXg
> 32자 접근 키(SecretKey): LYaWIuQmCSZ5ZMniUM6hiaLxHnW6XxRK

접근 키는 계정의 고유성을 식별하는 데 사용합니다. 키를 사용하여 서명이 생성되고 요청이 전송 된 후 Tencent Cloud는 요청 개시자의 ID를 확인한 다음 ID, 리소스, 작업 및 조건에 대한 인증을 수행하여 작업 허용 여부를 결정합니다.

>!기본 계정의 키에는 기본 계정의 모든 리소스에 대한 모든 작업 권한이 있습니다. 키를 공개하면 클라우드 자산이 손실 될 수 있으므로 하위 계정을 만들고 해당 계정에 대한 권한을 할당 한 다음 하위 계정 키를 사용하여 리소스 접근 및 관리에 대한 요청을 만드는 것이 좋습니다.

### 서브 계정 보안 자격 증명

여러 차원에서 계정 및 클라우드 리소스를 관리하려면 기본 계정 아래에 여러 개의 서브 계정을 만들어 사용자별 권한 관리를 구현할 수 있습니다. 서브 계정을 만드는 방법에 대한 자세한 내용은 CAM의 [서브 사용자](https://intl.cloud.tencent.com/document/product/598/13674)를 참조하십시오.

서브 계정을 사용하여 API 요청을 시작하기 전에 서브 계정에 대한 보안 자격 증명을 만들어야 하며 서브 계정에 고유한 키 페어가 생겨 ID 확인이 용이합니다. 서로 다른 서브 계정에 대한 사용자 정책을 만들어 리소스에 대한 접근 권한을 제어 할 수 있습니다. 또한 사용자 그룹을 생성하고 하나의 접근 정책을 사용자 그룹에 연결하여 사용자 그룹 및 자원의 중앙 관리를 용이하게 할 수 있습니다.

> !서브 계정에 해당 권한이 할당되면 리소스를 생성하거나 수정할 수 있습니다. 이제 자원은 여전히 ​​기본 계정에 속해 있으며 기본 계정은 자원에서 생성된 수수료를 지불해야 합니다.

### 임시 보안 자격 증명

루트 계정 또는 서브 계정의 보안 자격 증명을 사용하여 리소스에 접근하는 것 외에도 역할을 생성하고 역할의 임시 보안 자격 증명을 사용하여 Tencent Cloud 리소스를 관리 할 수 ​​있습니다. 역할 개념 및 역할 사용 방법에 대한 자세한 내용은 [역할 관리](https://intl.cloud.tencent.com/document/product/598/19420)를 참조하십시오.

가상 신원으로 역할에는 영구 키가 없습니다. CAM은 임시 보안 자격 증명을 생성하는 데 사용되는 STS API 세트를 제공합니다.
사용법 및 관련 예제에 대한 자세한 내용은 [역할 사용](https://intl.cloud.tencent.com/document/product/598/19419)을 참조하십시오. 임시 보안 자격 증명을 생성하는 방법에 대한 자세한 내용은 [STS API](https://intl.cloud.tencent.com/document/product/598/13895)을 참조하십시오. 임시 보안 자격 증명에는 **제한된 정책**(작업, 리소스 및 조건)과 **제한된 기간**(시작 및 종료 시간)만 포함되므로 생성된 임시 보안 자격 증명을 직접 배포하거나 사용할 수 있습니다.

API를 호출하여 임시 보안 자격 증명을 생성하고 임시 키 쌍 (tmpSecretId/tmpSecretKey) 및 보안 토큰(sessionToken)을 가져 와서 COS에 접근하는 데 사용할 수있는 보안 자격 증명을 구성 할 수 있습니다. 다음은 임시 보안 자격 증명 예제입니다 :

> 41 자 보안 토큰 (SecurityToken) : 5e776c4216ff4d31a7c74fe194a978a3ff2a42864
> 36 자 임시 접근 키 ID (SecretID) : AKIDcAZnqgar9ByWq6m7ucIn8LNEuY2MkPCl
> 32 자 임시 접근 키 (SecretKey) : VpxrX0IMCpHXWL0Wr3KQNCqJix1uhMqD

또한 이 API는 `expiration` 필드를 통해 임시 보안 자격 증명의 유효 기간을 반환합니다. 이는이 보안 자격 증명 집합이 이 기간 동안 요청을 시작하는 데만 사용될 수 있음을 의미합니다.

Tencent Cloud COS는 임시 키를 생성하는 데 사용할 수 있는 간단한 서버 SDK를 제공합니다. [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk)를 방문하여 SDK를 얻을 수 있습니다. 임시 보안 자격 증명을 얻은 후 REST API를 사용하여 요청을 시작하려면 HTTP 헤더나 POST 요청 패키지의 form-data에 `x-cos-security-token` 필드 값을 전해서 지정하여 요청에 사용 된 보안 토큰을 사용하고 임시 접근 키 페어를 사용하여 요청 서명을 생성할 수 있습니다. COS SDK를 사용하여 요청을 시작하는 방법에 대한 자세한 내용은 각 SDK 문서의 관련 섹션을 참조하십시오.

## 도메인 이름을 접근

###REST API

[지역 및 접근 도메인 이름](https://cloud.tencent.com/document/product/436/6224) 문서는 REST API를 통해 접근 요청을 시작하는 데 사용할 수있는 도메인 이름 목록을 제공합니다.

COS 버킷에 접근하려면 가상 호스팅 도메인 이름을 사용하는 것이 좋습니다. HTTP 요청을 시작하면 접근할 버킷은 `<BucketName-APPID>.cos.<Region>.myqcloud.com`과 같은 `Host` 헤더를 통해 지정됩니다. 가상 호스팅 도메인 이름을 사용하기는 가상 서버의 "루트"와 동일한 기능을 구현했습니다. 가상 호스팅 도메인 이름은 favicon.ico, robots.txt 및 crossdomain.xml과 같은 파일을 호스팅하는 데 사용할 수 있습니다. 이 파일은 호스트 된 웹 사이트를 식별할 때 기본적으로 가상 서버의 "루트"에서 많은 응용 프로그램이 검색 할 내용입니다 .

또한 경로형 요청을 사용하여 `cos.<region>.myqcloud.com/<BucketName-APPID>/`과 같은 버킷에 접근할 수 있습니다. 호스트와 서명 요청은 반드시 `cos.<region>.myqcloud.com`을 사용해야 합니다. SDK는 기본적으로 이 접근 방법을 지원하지 않습니다.

### 정적 웹 사이트의 도메인 이름

정적 웹 사이트기능을 사용하면 가상 호스팅 도메인 이름이 지정되어 관련 기능을 사용할 수 있습니다. 정적 웹 사이트의 도메인 이름은 REST API와 달리 특정 인덱스 페이지, 오류 페이지 및 리디렉션 구성 외에도 GET / HEAD / OPTIONS Object와 같은 몇 가지 작업 만 지원합니다. 업로드 또는 구성 리소스가 지원되지 않습니다.

정적 웹 사이트 도메인 이름 샘플: `<BucketName-APPID>.cos-website.<Region>.myqcloud.com`. 또한 콘솔에 로그인하여 버킷의「기본 구성 - 정적 웹 사이트 구성」으로 이동하여 도메인 이름을 가져올 수 있습니다.

## 사설망과 공용 네트워크 접근

COS의 액세스 도메인 이름은 지능형 DNS 확인을 채택합니다. 인터넷(다른 ISP 포함)을 통한 COS 접근의 경우 COS에 접근하기 위한 최적의 연결을 감지하고 선택합니다 . COS에 접근하기 위해 Tencent Cloud에 서비스를 배포한 경우 동일한 지역의 액세스가 자동으로 사설망 주소로 전달됩니다. 영역 간 액세스는 사설망에서 지원되지 않으며 COS 도메인 이름은 기본적으로 공용 네트워크 주소로 확인됩니다.

### 사설망 접근 판단 방법

동일한 지역 내의 Tencent Cloud 제품은 기본적으로 사설망를 통해 서로 접근하며 이러한 연결에 대해서는 트래픽 요금이 부과되지 않습니다. 이러한 이유로 비용 절감을 위해 다른 Tencent Cloud 제품을 구입할 때 동일한 지역을 선택하는 것이 좋습니다.

아래 사설망을 통한 접근하는지 확인하는 방법을 참고하십시오:

예를 들어, CVM 접근 COS에서 사설망이 COS에 접근하는 데 사용되는지 여부를 확인하려면 COS 도메인 이름을 확인하기 위해 CVM에서 `nslookup` 명령을 사용하십시오. 사설 IP가 반환되면 CVM과 COS 간의 접근는 사설망을 통해 이루어집니다. 그렇지 않으면 공용 네트워크를 통해 이루어집니다.

>? 일반적으로 사설 IP 주소는 `10. *. *. * ` 또는 `100. *. *. *` 형식을 취하고 VPC IP 주소는 `169.254. *. *` 형식을 취합니다.

가령 `mybucket-1250000000.cos.ap-guangzhou.myqcloud.com`은 대상 버킷의 주소이고 그 아래의 `Address : 10.148.214.13`은 접근가 사설망을 통해 이루어짐을 나타냅니다.

```shell
nslookup mybucket-1250000000.cos.ap-guangzhou.myqcloud.com

Server:         10.138.224.65
Address:        10.138.224.65  #53

Name:   mybucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.13
Name:   mybucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.14
```

### 연결 테스트

#### 기본 연결 테스트

COS는 서비스를 제공하기 위해 HTTP 프로토콜을 사용합니다. 가장 기본적인 도구 `telnet`을 사용하여 COS 접근 도메인 이름의 포트80에 대한 연결을 테스트 할 수 있습니다.

공용 네트워크를 통한 접근 예 :

```shell
telnet mybucket-1250000000.cos.ap-guangzhou.myqcloud.com 80
Trying 14.119.113.22...
Connected to gz.file.myqcloud.com.
Escape character is '^]'.
```

지역내의 Tencent Cloud CVM (기본 네트워크)을 통한 접근 예 :

```shell
telnet mybucket-1250000000.cos.ap-guangzhou.myqcloud.com 80
Trying 10.148.214.14...
Connected to 10.148.214.14.
Escape character is '^]'.
```

지역내의 Tencent Cloud CVM (VPC)을 통한 접근 예 :

```shell
telnet mybucket-1250000000.cos.ap-guangzhou.myqcloud.com 80
Trying 169.254.0.47....
Connected to 169.254.0.47.
Escape character is '^]'.
```

접근 환경에 관계없이 명령이 `Escape character is '^]'.` 필드에 반환하면 연결이 성공했음을 나타냅니다.

#### 인터넷을 통한 테스트 설명

인터넷을 통해 COS에 접근하는 것은 인터넷 서비스 고급업체의 네트워크를 통과하기 때문에 인터넷 서비스 고급업체 네트워크는 ICMP 프로토콜의 `핑(ping)` 또는 `경로 추적(traceroute)`과 같은 도구를 사용하여 연결을 테스트하지 못하게 할 수 있으므로 TCP 프로토콜 도구를 사용하여 연결성을 테스트하는 것이 좋습니다.
>!인터넷을 통한 접근는 다중 네트워크 환경의 영향을 받을 수 있습니다. 접근 권한이 부족한 경우 로컬 네트워크 링크를 확인하거나 현지 인터넷 서비스 고급업체에 문의하여 의견을 보내 주십시오.

ISP에서 ICMP 프로토콜을 사용하도록 허용하는 경우, `ping`, `traceroute` 또는 `mtr` 도구를 사용하여 링크를 확인할 수 있습니다. 그렇지 않으면 `psping`(Windows 환경, Microsoft 공식 웹 사이트에서 다운로드) 또는 'tcping'(교차 플랫폼 소프트웨어)과 같은 도구를 사용하여 대기 시간을 테스트 할 수 있습니다.

#### 사설망을 통한 테스트 설명

지역내의 Tencent Cloud VPC 네트워크를 통해 COS에 접근하는 경우 ICMP 프로토콜의 `핑(ping)` 또는 `경로 추적(traceroute)`과 같은 도구를 사용하여 연결을 테스트하지 못할 수 있습니다. 기본 연결 테스트에서 `telnet` 명령을 사용하는 것이 좋습니다.

또한 `psping` 또는 `tcping`과 같은 도구를 사용하여 접근 도메인 이름의 포트 80에 대한 대기 시간을 테스트할 수 있습니다. 테스트 전에 접근 도메인 이름이 `nsloopup` 명령을 사용하여 사설 IP로 올바르게 해석되었는지 조회하고 확인하십시오.
