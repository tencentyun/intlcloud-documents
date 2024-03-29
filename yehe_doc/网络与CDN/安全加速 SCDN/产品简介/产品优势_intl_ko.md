## 다양한 기능

Tencent Cloud Secure Content Delivery Network(SCDN)는 사용자를 위해 빠르고 안전한 콘텐츠 전송 가속 서비스를 제공하고, 보안 통합 솔루션의 원클릭 활성화를 지원하며, Web 공격 방어, DDoS 방어, CC 공격 방어 등 다양한 보안 기능을 결합하여 가속 네트워크의 보안 기능을 향상시킵니다. 

### 분산형 DDoS 공격 방어

SCDN DDoS 공격 방어는 우수한 특징 인식 알고리즘을 기반으로 트래픽에 통합 클리닝을 진행하고, SYN Flood, UDP Flood, ICMP Flood 등 각종 대규모 트래픽 공격을 방어하여 원활한 서비스 운영을 보장합니다. 

SCDN 보안 노드 네트워크는 분산형 아키텍처를 기반으로 글로벌 로드 밸런서를 스마트 스케쥴링하고, 트래픽 공격이 클리닝 임계값에 도달하면 트래픽을 SCDN Advanced 클러스터로 스케쥴링하여 대규모 DDoS 트래픽 공격에 대응하여, 갑작스런 공격 발생 시에도 안정적인 서비스 액세스를 보장합니다. 

Tencent Cloud SCDN 전체 네트워크는 최대 20Tbps의 DDoS 공격을 방어할 수 있으며 단일 보안 노드는 최대 1Tbps의 DDoS 공격을 방어할 수 있습니다. 

### CC 공격 방어

SCDN CC 공격 방어는 커널 레벨 차단, 머신러닝 알고리즘을 통해 맨-머신 인식 등을 결합하여 CC 공격을 인식하고 차단합니다.

SCDN 단일 보안 노드는 최대 60만 QPS의 CC 공격을 방어하여 사용자 서비스가 이상 고빈도 액세스의 영향으로 순간적으로 크래쉬되는 것을 방지합니다. 분산형 아키텍처에서 SCDN은 노드 간 로드 밸런스를 스마트 스케쥴링하여 공격에 대응합니다. 

### Web 응용 레이어 공격 방어

SCDN Web 공격 방어는 Tencent Cloud Web Application Firewall(WAF) 기능을 기반으로 Tencent의 대규모 Web 공격 샘플 데이터베이스 및 AI+ 규칙을 통해 일반적인 Web 공격을 스마트하게 인식하고 SQL 인젝션, 불법 액세스, XSS 교차 사이트 스크립팅, CSRF 크로스 사이트 요청 위조, Webshell 트로이 목마 업로드 등 위협을 효과적으로 방어합니다. 주요 특징은 우회 방지, 낮은 알람 누락률 및 오보율입니다.

돌발적인 네트워크 보안 이벤트를 자발적으로 모니터링하고 대응하며 24시간 내에 고위험 Web 취약점 및 0day 취약점 보완 가상 패치를 전달하여 예상치 못한 Web 취약점 리스크로부터 사이트를 보호합니다.

> ! SCDN Web 공격 방어 신규 런칭, 기간 한정 무료!

### 크롤러 대응(BOT 방어)

SCDN BOT 방어는 AI+ 정책 엔진 및 규칙 라이브러리를 기반으로 공개된 유명 머신 행동 및 크롤러(웹 페이지 크롤러, 검색 엔진, 콘텐츠 취합 툴 등 1000개 이상의 공개된 크롤러 행동 포함)행동을 식별, 모니터링 및 차단하여 악성 BOT 행위로 인한 사용자 데이터 유출, 콘텐츠 무단 도용, 가격 비교, 재고 검색, 불법 SEO, 산업 정책 유출 등 리스크로부터 기업을 보호합니다. 

미공개 정책으로 식별된 BOT 공격의 경우, UA, referrer, 속도, 경로 및 특수 매개변수 매칭 설정을 지원하며 행동 모니터링, 특징 추출, 비즈니스 조정 등 방식을 통해 끊임없이 동적 대응을 진행합니다. 

> ! SCDN BOT 보호 기능은 현재 베타 테스트 중입니다.

### 사용자 정의 보호 규칙

CDN가 지원하는 기본 IP, referer, UA 블랙리스트/화이트리스트 등 기본 액세스 제어 기능 외에도 SCDN은 사용자 정의 복합 액세스 제어 규칙을 지원합니다. 클라이언트 IP, URI, Referer, User-Agent, Params 등의 필드 지정을 통한 일치, 포함, 불포함 등 규칙 지정, 비즈니스 시나리오별 요청에 대한 다중 조건 조합 필터링이 가능합니다.

## 대량의 리소스 보유

Tencent Cloud SCDN은 Tencent Cloud CDN/ECDN 노드 네트워크를 기반으로 구축되었으며, 콘텐츠 배포 및 전송 가속 기능과 함께, Web 공격, DDoS 공격, CC 공격 등 전방위적 네트워크 공격 방어 기능을 제공하여 비즈니스 보안성을 강화합니다. Tencent Cloud CDN 노드 네트워크는 중국 내 2000개 이상, 중국 외 800개 이상의 가속 노드를 보유하고 있으며 전체 네트워크의 총 보유 대역폭은 150Tbps+입니다. 모든 SCDN 노드는 사양과 보안성이 높은 데이터 센터이며, 통신사의 고품질 네트워크를 사용합니다.

## 스마트 스케쥴링

Tencent Cloud SCDN은 전체 네트워크 링크를 실시간 모니터링하고, 자체 개발한 GSLB 스케쥴링 시스템과 스마트 라우팅 기술 결합을 통해 액세스 트래픽을 최적의 SCDN 노드로 스케쥴링하여, 정상적인 서비스 요청이 빠른 응답을 받을 수 있게 보장합니다. 대규모 트래픽 공격을 받았을 때 SCDN은 노드 간 로드 밸런스를 스마트하게 스케쥴링하여 높은 서비스 가용성을 보장합니다.

## 원클릭 연결

Tencent Cloud CDN/ECDN과 SCDN을 함께 사용하면, 기존 CDN 설정 및 도메인 리졸브를 조정하지 않아도 도메인 SCDN 서비스를 바로 활성화할 수 있어, 연결 프로세스가 빠르고 편리합니다.

보안 서비스가 필요한 도메인을 Tencent Cloud CDN/ECDN에 연결한 후, SCDN 콘솔에서 도메인 보안 서비스를 실행하고 필요에 따라 각종 보안 설정을 진행하면, 약 5분 후 도메인 관련 보안 설정이 전체 네트워크 SCDN 노드로 전달됩니다. 전체 과정 중 가속 서비스는 중단되지 않으며 현재 네트워크 서비스에도 영향을 미치지 않습니다. 