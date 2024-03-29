

Tencent Cloud Content Delivery Network(CDN)는 경로(파일 유형, 폴더, 전체 경로 파일(예: /test/1.jpg) 또는 Origin-pull에 대한 홈페이지 지정) 및 클라이언트 IP 지역을 기반으로 Origin-pull 요청을 전달하기 위해 세분화된 Origin-pull 구성을 제공합니다.

>!
>- Client IP 지역을 기반으로 하는 Origin-pull은 베타 버전이므로 공식 출시를 기다려 주시기 바랍니다.
>- 현재까지는 메인 회선만 지원하며, 마스터 원본 서버를 기반으로 보다 세분화된 Origin-pull 설정이 수행됩니다(원본 서버 유형과 호스트 헤더는 기본적으로 기본 마스터 원본 서버를 상속하며 다른 규칙에 따른 변경을 지원하지 않습니다).

## 설정 가이드

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 후, 왼쪽 메뉴바에서 [도메인 관리]를 선택한 뒤 도메인 작업 열의 [관리]를 클릭하여 도메인 설정 페이지로 이동합니다. [기본 설정] 탭의 [원본 서버 정보] 최하단에 [고급 Origin-pull 설정]이 있으며, 클릭하여 펼쳐볼 수 있습니다.
![](https://main.qcloudimg.com/raw/17e0385a7cea2cbdd0ae012cae8b2555.png)

### 규칙 추가

규칙 추가를 클릭하여 필요에 따라 규칙을 추가할 수 있습니다. 마스터 원본 서버 [편집]을 클릭한 후 [고급 Origin-pull 설정]을 클릭하여 편집할 수 있습니다.
![](https://main.qcloudimg.com/raw/ef2ae0e51a0cb032d493f89b8029b316.png)

**설정 제한**

- 도메인당 최대 50개까지 규칙을 추가할 수 있습니다.
- 단일 규칙의 origin-pull 주소는 IP, 도메인 이름 및 포트일 수 있습니다(범위: 0 - 65535, 포트는 생략 가능). Origin-pull 프로토콜로 HTTPS 또는 Follow Protocol을 선택한 경우, 포트는 443이거나 비어 있어야 합니다.
- 더 많은 작업: 여러 규칙에 대한 우선순위 조정 및 규칙의 일괄 편집과 삭제를 지원합니다.

>?
>- 하위 우선순위가 상위 우선순위보다 높음 - 이와 같은 상대적 위치의 우선순위 조정은 여러 경로별 원본 요청 규칙(지정 파일 유형/폴더/모든 경로 파일/메인 화면 원본 요청 규칙) 또는 Client IP 소재 리전에 따른 원본 요청 규칙과 같은 동일한 유형의 원본 요청 규칙에만 적용됩니다.
>- 동일한 요청이 서로 다른 유형의 원본 요청 규칙에 부합하는 경우, 유형별 우선순위에 따라 실행되며 그 순서는 경로별 > Client IP입니다.
예시: `Client IP의 소재지가 지앙쑤이고 1.1.1.1로 Origin-pull`하며 `/test는 2.2.2.2로 Origin-pull`하는 경우, 지앙쑤에 소재한 Client IP가 /test에 액세스할 때 2.2.2.2로 Origin-pull합니다.
