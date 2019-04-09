[//]: # (chinagitpath:XXXXX)

본 문서는 웹사이트 유형이 아닌 비즈니스 사용자가 비즈니스를 Anti-DDoS Advanced 인스턴스에 액세스하고 방어 구성을 인증하는 방법을 소개합니다.

## 전제 조건

- 포워딩 규칙 추가 전, **Anti-DDoS Advanced 인스턴스 구매**를 성공적으로 완성해야 합니다.
- 비즈니스 도메인 이름 DNS 정보 수정 전, **도메인 이름 해석 제품** 구매를 성공적으로 완성해야 합니다.

## 프로세스

![](https://main.qcloudimg.com/raw/35bbfec94b24a02010941bbb3e86867d.png)

## 작업 절차
<span id="step1"></span> 
### 포워딩 규칙 구성

   1. [Anti-DDoS Advanced 콘솔](https://console.cloud.tencent.com/dayu/bgpip)에 로그인하여 대상 인스턴스를 찾아 인스턴스 ID를 클릭한 뒤 구성 페이지에 진입합니다.
   2. **포워딩 규칙** 구성란에서 **생성**을 클릭하여 생성합니다.

   ![](https://main.qcloudimg.com/raw/80dda47083ae23cd814bf45788aa8617.png)
    
  3. 실제 수요에 따라 아래 매개변수를 구성하고 **확인**을 클릭합니다.

 - 포워딩 프로토콜: 현재 TCP와 UDP를 지원합니다.
 - 포워딩 포트: 접근용 Anti-DDoS Advanced IP 포트로 오리진 서버와 동일한 포트 사용을 권장합니다. Anti-DDoS Advanced는 843, 1433, 1434, 3306, 3389, 36000 및 56000 포트를 포워딩 포트로 사용하도록 지원하지 않습니다.
 - 오리진 서버 포트: 사용자 비즈니스 웹사이트의 실제 포트입니다.
 - 오리진 서버 IP: 오리진 서버의 IP 주소를 입력합니다. 여러 개의 오리진 서버 IP와 대응할 경우, 모두 입력할 수 있으며 Enter 키로 여러 개의 IP를 구분합니다. 최대 20개 IP를 지원합니다. Anti-DDoS Advanced는 라운드 로빈의 로드밸런싱 알고리즘을 사용해 비즈니스 트래픽 오리진 요청을 수행합니다.
 
 ![](https://main.qcloudimg.com/raw/7aee6b44bcbb34e262f17ff7bedda5cf.png)

<span id="step2"></span> 
### 오리진 요청 IP 허용

오리진 서버가 Anti-DDoS Advanced의 오리진 요청 IP를 가로막아 비즈니스에 영향을 끼치는 걸 방지하기 위해 오리진 서버의 방화벽, Web 응용프로그램 방화벽, IPS 침입 방지 시스템, 트래픽 관리 등 하드웨어 장치에서 화이트리스트 전략을 설정하기를 권장합니다. 오리진 서버의 호스트 방화벽과 Safedog 등 기타 보안 소프트웨어의 방어 기능을 비활성화하거나 화이트리스트 전략을 설정하여 Anti-DDoS Advanced의 오리진 요청 IP가 오리진 서버 보안 전략의 영향을 받지 않도록 합니다.
상세한 Anti-DDoS Advanced 오리진 요청 IP 범위를 조회하려면 Tencent Cloud A/S에 연락하십시오.

<span id="step3"></span> 
### 로컬 검증 구성

포워딩 규칙을 구성한 후, Anti-DDoS Advanced 서비스팩의 Anti-DDoS Advanced IP는 포워딩 규칙에 따라 관련 포트의 메시지를 오리진 서버의 대응 포트에 포워딩합니다.
비즈니스 안정을 최대한 보장하기 위해, 비즈니스를 전체 전환하기 전에 우선 로컬 테스트를 진행하길 권장합니다. 구체적인 검증 방법은 다음과 같습니다.

- **IP로 접근하는 비즈니스**
  IP를 통해 직접 인터랙션하는 비즈니스(예: 게임 비즈니스)는 `telnet` 명령을 통해 Anti-DDoS Advanced IP 포트에 접근하여 연결 가능 여부를 조회할 수 있습니다. 로컬 클라이언트에서 서버 IP를 직접 입력할 수 있을 경우, Anti-DDoS Advanced IP를 직접 입력해 테스트를 진행하여 로컬 클라이언트가 제대로 연결되었는지 확인할 수 있습니다.
  예를 들어, Anti-DDoS Advanced IP는 10.1.1.1이고 포워딩 포트는 1234, 오리진 서버 IP는 10.2.2.2, 오리진 서버 포트는 1234입니다. 로컬 클라이언트에서 `telnet` 명령을 통해 10.1.1.1:1234에 접근할 때, `telnet` 명령이 연결될 수 있으면 포워딩 성공을 의미합니다.
- **도메인 이름으로 접근하는 비즈니스**
  도메인 이름을 통해 접근하는 비즈니스는 아래 방법을 통해 구성 효력 발생 여부를 검증할 수 있습니다.
 1. 로컬 hosts 파일을 수정하여 로컬이 방어받은 웹사이트에 대한 요청은 Anti-DDoS Advanced IP로 지향하도록 합니다.
   Windows 운영체제 예시:
   1. 로컬 컴퓨터 C:\Windows\System32\drivers\etc 경로의 hosts 파일을 열어 파일 끝에 다음 내용을 추가합니다.
   `<Anti-DDoS Advanced IP 주소> <방어받은 웹사이트의 도메인 이름>`
   예를 들어, Anti-DDoS Advanced IP는 10.1.1.1이고 도메인 이름은 [www.qq.com](www.qq.com)이면 다음이 추가됩니다.
   `10.1.1.1       www.qq.com`
   2. hosts 파일을 저장합니다.
 2. 로컬 컴퓨터에서 방어받은 도메인 이름에 `ping` 명령을 실행합니다.
   해석한 IP 주소가 hosts 파일에 바인딩한 Anti-DDoS Advanced IP 주소일 경우, 포워딩 성공을 의미합니다.
 > ?해석한 IP 주소가 여전히 오리진 서버 주소일 경우, Windows 명령 프롬프트에서 `ipconfig/flushdns` 명령을 실행하여 로컬 DNS 캐시를 갱신하도록 명령합니다.

  3. hosts 바인딩이 효력 발생했는지 확인한 후, 도메인 이름을 사용하여 검증합니다.
   정상 접근할 수 있으면 구성 효력이 이미 발생하였음을 의미합니다.

> ?정확한 방법을 사용하여도 여전히 검증에 실패할 경우, [Anti-DDoS Advanced 콘솔](https://console.cloud.tencent.com/dayu/bgpip)에 로그인하여 구성이 올바른지를 검사하십시오. 구성 오류와 부정확한 검증 방법을 배제한 후에도 여전히 문제가 존재할 경우, Tencent Cloud A/S에 연락하십시오.

<span id="step4"></span>
### 비즈니스 도메인 이름 DNS 해석 수정

  Anti-DDoS Advanced에 포워딩 규칙 그룹을 바인딩한 후에, 사용자는 Anti-DDoS Advanced의 포워딩 포트부터 오리진 서버의 오리진 서버 포트까지의 연결을 검증할 수 있습니다. 비즈니스 IP를 Anti-DDoS    Advanced로 지향하도록 구성하면 액세스 구성을 완료합니다.
  
  비즈니스에 DNS 해석 서비스를 사용하는 경우, DNS 서비스 제공업체에서 도메인 이름 해석을 변경할 수 있으며, 기존의 비즈니스 IP 주소를 바인딩한 Anti-DDoS Advanced IP 주소로 변경합니다.
  
  DNS 해석을 수정하면 모든 사용자의 접근 트래픽이 Anti-DDoS Advanced IP를 통과해 오리진 서버(모든 트래픽을 방어 IP로 라우팅하는 것과 같음)로 반환됩니다.

