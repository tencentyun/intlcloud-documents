Tencent Cloud CLB는 TCP, UDP, TCP SSL, HTTP 및 HTTPS와 같은 다양한 프로토콜과 함께 제공되어 기업에 도메인 이름 및 URL 기반 포워딩 서비스를 제공합니다. 본문은 CLB 인스턴스를 빠르게 생성하고 클라이언트 요청을 두 개의 CVM 인스턴스로 포워딩하는 방법을 안내합니다.

## 전제 조건
1. 두 개의 CVM 인스턴스를 생성했습니다(본문에서는 `rs-1` 및 `rs-2`를 두 개의 예시 인스턴스로 사용). CVM 인스턴스 생성 방법에 대한 정보는 [CVM 구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오.
2. 두 CVM 인스턴스에 백엔드 서비스를 배포했습니다. 본문은 HTTP 포워딩을 예시로 들어 설명합니다. Nginx 서버는 CVM 인스턴스 `rs-1` 및 `rs-2`에 배포되었으며 두 인스턴스는 ‘Hello nginx! This is rs-1!’ 및  ‘Hello nginx! This is rs-2!’ 라는 두 개의 HTML 정적 페이지를 반환합니다. 자세한 내용은 [Deploying Nginx on CentOS](https://intl.cloud.tencent.com/document/product/214/32390)를 참고하십시오.
>!
> - 본문은 IP별 청구 계정에 대한 단계를 설명합니다. CVM별 청구 계정의 경우 먼저 CVM 인스턴스용 공중망 대역폭을 구매하십시오. 계정 유형이 확실하지 않은 경우 [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246)을 참고하십시오.
> - 이 예시에서 리얼 서버에 배포된 다른 서비스는 다른 값을 반환합니다. 모든 사용자에게 일관된 경험을 제공하기 위해 리얼 서버에 배포된 서비스는 일반적으로 동일합니다.

## 1단계: CLB 인스턴스 구매
구매 완료 후 시스템은 자동으로 VIP를 CLB 인스턴스에 할당합니다. VIP는 클라이언트에게 서비스를 제공하기 위한 IP 주소로 사용됩니다.
1. Tencent Cloud 콘솔에 로그인하여 [CLB 구매 페이지](https://buy.intl.cloud.tencent.com/lb)로 이동합니다.
2. 먼저 CVM 인스턴스와 동일한 리전을 선택합니다. 그런 다음 인스턴스 유형으로 **Cloud Load Balancer**를 선택하고 네트워크 유형으로 **공중망**을 선택합니다. 자세한 내용은 [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629)을 참고하십시오.
3. **즉시 구매**를 클릭하여 구매를 완료합니다.
4. ‘인스턴스 관리’ 페이지로 돌아가서 해당 리전을 선택하면 새 인스턴스를 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/2c2afd943a9f6a6d03f55c00e62da8b5.png)

## 2단계: CLB 리스너 구성
CLB 리스너는 지정된 프로토콜 및 포트를 통해 포워딩하는 데 사용됩니다. 본문은 클라이언트 HTTP 요청을 포워딩하도록 CLB 인스턴스를 구성하는 방법을 보여줍니다.
### HTTP 수신 프로토콜 및 포트 구성
클라이언트가 요청을 시작하면 CLB 인스턴스는 수신 프런트엔드 프로토콜 및 포트에 따라 요청을 수신하고 요청을 리얼 서버로 포워딩합니다.
1. [CLB 콘솔](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3)에 로그인합니다.
2. ‘인스턴스 관리’ 페이지에서 대상 CLB 인스턴스의 작업 열 아래에 있는 **리스너 구성**을 클릭합니다.
3. ‘리스너 관리’ 탭의 ‘HTTP/HTTPS 리스너’ 아래에서 **생성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/782c60eeb4bf9aa334e4243cf4e068d5.png)
4. ‘리스너 생성’ 창에서 다음 항목을 구성하고 **제출**을 클릭합니다.
  - 리스너 이름. 이름은 최대 60자의 영어 알파벳, 숫자, ‘-’, ‘_’ 및 ‘.’을 포함할 수 있습니다.
  - 리스너 프로토콜 포트(예시: `HTTP：80`).

### 리스너의 포워딩 규칙 구성
클라이언트가 요청을 시작하면 CLB 인스턴스는 구성된 리스너의 포워딩 규칙에 따라 요청을 포워딩합니다.
1. ‘리스너 관리’ 탭에서 새 리스너 오른쪽의 **+**를 클릭합니다.
![](https://main.qcloudimg.com/raw/f8ab76b69f8a0cfdd5b4332c8b80b1f2.png)
2. ‘포워딩 규칙 생성’ 창에서 도메인 이름, URL, 밸런싱 방식을 설정하고 **다음**을 클릭합니다.
  - 도메인 이름: 리얼 서버의 도메인 이름(예시: `www.example.com`).
  - 기본 도메인 이름: 클라이언트 요청이 리스너 도메인 이름과 일치하지 않으면 CLB 인스턴스는 요청을 기본 도메인 이름(default server)으로 포워딩합니다. 각 리스너는 하나의 기본 도메인 이름으로만 구성할 수 있습니다. 리스너에 기본 도메인 이름이 없는 경우 CLB 인스턴스는 요청을 첫 번째 도메인 이름으로 포워딩합니다. 이 예시에서는 구성 단계를 건너뜁니다.
  - URL: 리얼 서버에 대한 액세스 경로(예시: `/image/`).
  - 밸런싱 방법으로 ‘가중 라운드 로빈’을 선택하고 다음을 클릭합니다. 자세한 내용은 [Load Balancing Methods](https://intl.cloud.tencent.com/document/product/214/6153)를 참고하십시오.
![](https://main.qcloudimg.com/raw/263b2486f8a5734ea8aa643ea3b34387.png)
3. ‘상태 확인’을 활성화합니다. 도메인 및 경로 확인 필드 모두에 기본값을 사용하고 **다음**을 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/84dR058_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230710181910.png)
4. ‘세션 지속성’을 비활성화하고 **제출**을 클릭합니다.

CLB 리스너에 대한 자세한 내용은 [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151)를 참고하십시오.
>?
>- 포워딩 규칙: 각 리스너는 여러 도메인 이름으로 구성할 수 있으며 각 도메인 이름은 여러 URL로 구성할 수 있습니다. 리스너 또는 도메인 이름을 선택한 다음 **+** 아이콘을 클릭하여 새 규칙을 생성할 수 있습니다.
>- 세션 지속성: 세션 지속성이 비활성화되고 라운드 로빈 방식이 선택되면 동일한 클라이언트의 요청이 다른 리얼 서버에 순서대로 할당됩니다. 세션 지속성이 활성화되어 있거나 비활성화되어 있지만 ip_hash 밸런싱 메소드를 사용하는 경우 동일한 클라이언트의 요청은 항상 동일한 리얼 서버에 할당됩니다.
>

### 리얼 서버를 리스너에 바인딩
클라이언트가 요청을 시작하면 CLB 인스턴스는 처리를 위해 리스너에 바인딩된 CVM 인스턴스에 요청을 포워딩합니다.
1. ‘리스너 관리’ 탭에서 <b>+</b>를 클릭하여 새 리스너를 확장합니다. URL을 클릭하고 오른쪽의 ‘포워딩 규칙’ 섹션에서 **바인딩**을 클릭합니다.
![](https://main.qcloudimg.com/raw/ad3bab63556a4340792b1d5dadcc1b19.png)
2. ‘리얼 서버 바인딩’ 팝업 창에서 인스턴스 유형으로 ‘CVM’을 선택하고 두 개의 CVM 인스턴스 `rs-1` 및 `rs-2`(CLB 인스턴스와 동일한 리전에 있음)를 선택하고 포트를 ‘80’으로, 가중치를 ‘10’(기본값)으로 설정하고 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/02a6cf1b63726a7133f97f5f56c10d74.png)
3. [](id:qrjkjc)가 ‘포워딩 규칙’ 섹션으로 반환되면, 바인딩된 CVM 인스턴스와 해당 상태 확인 상태를 볼 수 있습니다. 포트 상태가 ‘Healthy’이면 CVM 인스턴스는 일반적으로 CLB 인스턴스에서 포워딩한 요청을 처리할 수 있습니다.
>!하나의 포워딩 규칙(수신 프로토콜 + 포트 + 도메인 이름 + URL)은 동일한 CVM 인스턴스의 여러 포트와 바인딩될 수 있습니다. 사용자가 `rs-1`의 포트 `80` 및 `81`에 동일한 서비스를 배포하는 경우 `rs-1`의 두 포트 `80` 및 `81` 모두 예시 포워딩 규칙으로 바인딩될 수 있으며 둘 다 CLB 인스턴스에서 포워딩된 요청을 수신합니다.

## 3단계: 보안 그룹 구성
CLB 인스턴스를 생성한 후 공중망 트래픽을 격리하도록 CLB 보안 그룹을 구성할 수 있습니다. 자세한 내용은 [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733)을 참고하십시오.

보안 그룹을 구성한 후 기본적으로 트래픽 허용 기능을 활성화 또는 비활성화할 수 있습니다.
### 방법1: 보안 그룹에서 기본적으로 트래픽 허용 활성화
자세한 내용은 [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733)을 참고하십시오.

### 방법2: CVM 보안 그룹에서 특정 클라이언트 IP 허용
자세한 내용은 [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733)을 참고하십시오.

## 4단계: CLB 서비스 확인
CLB 인스턴스를 구성한 후 동일한 CLB 인스턴스에서 서로 다른 **도메인 이름 + URL**을 통해 서로 다른 리얼 서버에 액세스하거나 **content-based routing** 기능을 통해 실효성을 확인할 수 있습니다.

### 방법1: hosts 구성 및 도메인 이름을 CLB 인스턴스에 매핑
1. Windows 장치에서 `C:\Windows\System32\drivers\etc` 디렉터리의 호스트 파일을 수정하고 도메인 이름을 CLB 인스턴스의 VIP에 매핑합니다.
![](https://main.qcloudimg.com/raw/b12ee22250cb7c24d5e12ecb803e6355.png)
2. hosts가 성공적으로 구성되었는지 확인하려면 cmd에서 `ping` 명령을 실행하여 도메인 이름이 VIP와 성공적으로 바인딩되었는지 테스트할 수 있습니다. 데이터 팩이 반환되면 성공적으로 바인딩됩니다.
![](https://main.qcloudimg.com/raw/b11b20840cba86bedbaffaa424b4e021.png)
3. 브라우저를 통해 `http://www.example.com/image/`에 액세스하여 CLB 서비스를 테스트합니다. 페이지에서 아래 이미지를 반환하면 요청이 CLB 인스턴스에 의해 CVM rs-1로 포워딩되고 CVM이 일반적으로 요청을 처리하고 서비스 페이지를 반환한 것입니다.
![](https://main.qcloudimg.com/raw/cf61264a9406d141650ed79da21c6859.png)
4. 리스너의 밸런싱 메소드는 ‘가중 라운드 로빈’이고 두 CVM 인스턴스의 가중치는 ‘10’이므로 브라우저를 새로고침하여 요청을 다시 시작할 수 있습니다. 페이지에서 아래 이미지를 반환하면 요청이 CLB 인스턴스에 의해 CVM rs-2로 포워딩된 것입니다.
![](https://main.qcloudimg.com/raw/ab7db7b5c3952739919ae6e271bb1348.png)
>!`image/`는 `/`를 생략할 수 없습니다. `/`는 image가 파일 이름 대신 기본 디렉터리임을 나타냅니다.

### 방법2: DNSPod를 통해 도메인 이름을 CLB 인스턴스에 매핑
1. 도메인 이름을 조회하고 등록합니다. `example.com`이 예시로 사용됩니다.
2. [DNSPod 콘솔](https://console.cloud.tencent.com/cns)에 로그인하고 왼쪽 사이드바에서 ‘DNS 목록’을 클릭하고 도메인 이름 오른쪽 ‘작업’에서 **리졸브**를 클릭합니다.
3. ‘레코드 관리’ 탭을 열고 **레코드 추가**를 클릭하여 다음 매개변수를 사용하여 도메인 이름에 대한 A 레코드를 추가합니다.
  - 호스트: 도메인 이름의 접두사. 다음은 모든 접두사를 리졸브하는 예시(`*.example.com`)입니다.
  - 레코드 유형: `A 레코드`.
  - 분할 영역: 기본값.
  - 값: **Tencent Cloud 리소스 연결**을 클릭한 다음 위에서 생성한 CLB 인스턴스를 선택합니다.
  - TTL: 기본값 ‘600s’로 설정합니다.
    ![]()
4. **저장**을 클릭합니다.
5. 약 10분 후 브라우저(www.example.com)에서 바인딩된 CNAME 도메인 이름을 엽니다. 해당 페이지가 정상적으로 표시될 수 있으면 CLB 인스턴스가 실행 중임을 나타냅니다.

## 리디렉션 구성(옵션)
CLB는 자동 리디렉션 및 수동 리디렉션을 지원합니다. 자세한 내용은 [Layer-7 Redirection Configuration](https://intl.cloud.tencent.com/document/product/214/8839)을 참고하십시오.
- 자동 리디렉션(강제 HTTPS): PC 또는 모바일 브라우저가 HTTP 요청으로 Web 서비스에 액세스하면 요청이 CLB 프록시를 통과한 후 브라우저에 HTTPS 응답이 반환되어 브라우저가 HTTPS를 사용하여 웹 페이지에 액세스하도록 합니다.
- 수동 리디렉션: 상품 품절, 페이지 유지 보수, 업데이트 및 업그레이드 등의 경우 Web 비즈니스를 일시적으로 비활성화하려면 원본 페이지를 새 페이지로 리디렉션해야 합니다. 그렇지 않으면 방문자의 즐겨찾기 및 검색 엔진 데이터베이스의 이전 주소가 404 또는 503 오류 메시지 페이지를 반환하여 사용자 경험을 저하시키고 트래픽 낭비를 초래하고 검색 엔진의 누적 점수를 무효화하기까지 합니다.


## 관련 작업
- [Deploying Java Web on CentOS](https://intl.cloud.tencent.com/document/product/214/32391) 
- [PHP 환경 배포](https://intl.cloud.tencent.com/document/product/213/10182)
