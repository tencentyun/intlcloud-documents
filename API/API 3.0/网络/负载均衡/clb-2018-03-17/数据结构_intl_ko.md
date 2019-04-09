## Backend

수신기 백 엔드에 바인딩한 기기의 세부 정보

다음 API에 참조됨: DescribeTargets.

| 이름 | 유형 |  설명 |
|------|------|-------|
| Type | String | 포워딩 대상의 유형, 가능한 값: CVM |
| InstanceId | String | CVM의 유일한 ID, DescribeInstances API의 반환된 필드에서 unInstanceId에서 가져올 수 있음 |
| Port | Integer | 백 엔드 CVM 수신 포트 |
| Weight | Integer | 백 엔드 CVM의 포워딩 가중치, 범위: 0~100, 기본값: 10. |
| PublicIpAddresses | Array of String | CVM의 공인 IP<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| PrivateIpAddresses | Array of String | CVM의 사설 IP<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| InstanceName | String | CVM 인스턴스 이름<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| RegisteredTime | String | CVM이 수신기에 바인딩된 시간<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |

## CertificateInput

인증서 정보

다음 API에 참조됨: CreateListener, CreateRule, ModifyListener.

| 이름 | 유형 | 필수 여부 | 설명 |
|------|------|----------|------|
| SSLMode | String | 예 | 인증 유형, UNIDIRECTIONAL: 단방향 인증, MUTUAL: 상호 인증 |
| CertId | String | 아니요 | 서버 인증서의 ID. 이 항목을 입력하지 않으면 반드시 인증서(CertContent, CertKey, CertName 포함)를 업로드해야 합니다. |
| CertCaId | String | 아니요 | 클라이언트 인증서의 ID. SSLMode=mutual일 경우, 수신기가 이 항목을 입력하지 않으면 반드시 클라이언트 인증서(CertCaContent, CertCaName 포함)를 업로드해야 합니다. |
| CertName | String | 아니요 | 업로드할 서버 인증서의 이름. CertId가 없을 경우, 이 항목을 반드시 업로드해야 합니다. |
| CertKey | String | 아니요 | 업로드할 서버 인증서의 key. CertId가 없을 경우, 이 항목을 반드시 업로드해야 합니다. |
| CertContent | String | 아니요 | 업로드할 서버 인증서의 내용. CertId가 없을 경우, 이 항목을 반드시 업로드해야 합니다. |
| CertCaName | String | 아니요 | 업로드할 클라이언트 CA 인증서의 이름. SSLMode=mutual일 경우, CertCaId가 없으면 이 항목을 반드시 업로드해야 합니다. |
| CertCaContent | String | 아니요 | 업로드할 클라이언트 인증서의 내용. SSLMode=mutual일 경우, CertCaId가 없으면 이 항목을 반드시 업로드해야 합니다. |

## CertificateOutput

인증서 관련 정보

다음 API에 참조됨: DescribeListeners.

| 이름 | 유형 | 설명 |
|------|------|-------|
| SSLMode | String | 인증 유형, UNIDIRECTIONAL: 단방향 인증, MUTUAL: 상호 인증 |
| CertId | String | 서비 인증서의 ID. |
| CertCaId | String | 클라이언트 인증서의 ID.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |

## ClassicalHealth

전통형 CLB 상태 검사 정보

다음 API에 참조됨: DescribeClassicalLBHealthStatus.

| 이름 | 유형 | 설명 |
|------|------|-------|
| IP | String | CVM 사설 IP |
| Port | Integer | CVM 포트 |
| ListenerPort | Integer | CLB 수신 포트 |
| Protocol | String | 포워딩 프로토콜 |
| HealthStatus | Integer | 상태 검사 결과, 1: 정상, 0: 비정상. |

## ClassicalListener

전통형 CLB 수신기 정보

다음 API에 참조됨: DescribeClassicalLBListeners.

| 이름 | 유형 | 설명 |
|------|------|-------|
| ListenerId | String | CLB 수신기 ID |
| ListenerPort | Integer | CLB 수신기 포트 |
| InstancePort | Integer | 수신기 백 엔드 포워딩 포트 |
| ListenerName | String | 수신기 이름 |
| Protocol | String | 수신기 프로토콜 유형 |
| SessionExpire | Integer | 세션 유지 시간 |
| HealthSwitch | Integer | 검사 시작 여부: 1(시작), 0(종료) |
| TimeOut | Integer | 응답 타임아웃 시간 |
| IntervalTime | Integer | 검사 간격 |
| HealthNum | Integer | 정상 임계값 |
| UnhealthNum | Integer | 비정상 임계값 |
| HttpHash | String | 공중망(고정 IP)의 HTTP, HTTPS 프로토콜 수신기로의 라운드 로빈 방법입니다. Wrr은 가중치에 따른 라운드 로빈이고, ip_hash는 접근의 오리진 IP에 따른 일치성 해시 방법에 따라 배포를 의미합니다. |
| HttpCode | Integer | 공중망(고정 IP)의 HTTP, HTTPS 프로토콜 수신기의 상태 검사 반환 코드입니다. 구체적인 내용은 수신기 생성 중 해당 필드에 대한 해석을 참조하십시오. |
| HttpCheckPath | String | 공중망(고정 IP)의 HTTP, HTTPS 프로토콜 수신기의 상태 검사 경로입니다. |
| SSLMode | String | 공중망(고정 IP)의 HTTPS 프로토콜 수신기의 인증 방식입니다. |
| CertId | String | 공중망(고정 IP)의 HTTPS 프로토콜 수신기 서버 인증서 ID입니다. |
| CertCaId | String | 공중망(고정 IP)의 HTTPS 프로토콜 수신기 클라이언트 인증서 ID입니다. |
| Status | Integer | 수신기의 상태. 0은 생성 중, 1은 운행 중. |

## ClassicalLoadBalancerInfo

CLB 정보

다음 API에 참조됨: DescribeClassicalLBByInstanceId.

| 이름 | 유형 | 설명 |
|------|------|-------|
| InstanceId | String | 백 엔드 인스턴스 ID |
| LoadBalancerIds | Array of String | 로드밸런서 인스턴스 ID 리스트<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |

## ClassicalTarget

전통형 CLB 백 엔드 정보

다음 API에 참조됨: DescribeClassicalLBTargets.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Type | String | 포워딩 대상의 유형, 가능한 값: CVM |
| InstanceId | String | CVM의 유일한 ID, DescribeInstances API의 반환된 필드에서 unInstanceId에서 가져올 수 있음 |
| Weight | Integer | 백 엔드 CVM의 포워딩 가중치, 범위: 0~100, 기본값: 10. |
| PublicIpAddresses | Array of String | CVM의 공인 IP<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| PrivateIpAddresses | Array of String | CVM의 사설 IP<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| InstanceName | String | CVM 인스턴스 이름<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| RunFlag | Integer | CVM 상태<br/>1: 고장, 2: 운행 중, 3: 생성 중, 4: 종료됨, 5: 리턴됨, 6: 리턴 중, 7: 다시 시작 중, 8: 시작 중, 9: 종료 중, 10: 비밀번호 재설정 중, 11: 포맷 중, 12: 이미지 제작 중, 13: 대역폭 설정 중, 14: 시스템 다시 설치 중, 19: 업그레이드 중, 21: 핫 마이그레이션 중<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |

## ClassicalTargetInfo

전통형 백 엔드 정보

다음 API에 참조됨: RegisterTargetsWithClassicalLB.

| 이름 | 유형 | 필수 여부 | 설명 |
|------|------|----------|------|
| InstanceId | String | 예| 백 엔드 인스턴스 ID |
| Weight | Integer | 아니요 | 가중치 범위: 0 - 100 |

## HealthCheck

상태 검사 정보

다음 API에 참조됨: CreateListener, CreateRule, DescribeListeners, ModifyListener, ModifyRule.

| 이름 | 유형 | 필수 여부 | 설명 |
|------|------|----------|------|
| HealthSwitch | Integer | 아니요 | 상태 검사 시작 여부: 1(시작), 0(종료) |
| TimeOut | Integer | 아니요 | 상태 검사 응답 타임아웃 시간, 범위: 2 ~60, 기본값: 2, 단위: 초. 응답 타임아웃 시간은 검사 간격 시간보다 작아야 합니다.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| IntervalTime | Integer | 아니요 | 상태 검사 프로브 간격 시간, 기본값: 5, 범위: 5~300, 단위: 초.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| HealthNum | Integer | 아니요 | 상태 임계값, 기본값: 3. 이는 3 회 연속으로 정상적인 것으로 확인되면 포워딩이 정상으로 간주됨을 의미합니다. 범위: 2-10; 단위: 회.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| UnHealthNum | Integer | 아니요 | 상태 임계값, 기본값: 3. 이는 3 회 연속으로 비정상적인 것으로 확인되면 포워딩이 이상으로 간주됨을 의미합니다. 범위: 2-10; 단위: 회.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| HttpCode | Integer | 아니요 | 상태 검사 상태 코드(HTTP/HTTPS 포워딩 규칙에만 적용). 범위: 1 ~ 31 기본값: 31.<br/>1을 선택하고 프로빙한 후 반환값 1xx이(가)인 경우 정상을 의미합니다. 2를 선택하고 프로빙한 후 반환값 2xx이(가)인 경우 정상을 의미합니다. 4를 선택하고 프로빙한 후 반환값 3xx이(가)인 경우 정상을 의미합니다. 8을 선택하고 프로빙한 후 반환값 4xx이(가)인 경우 정상을 의미합니다, 16을 선택하고 프로빙한 후 반환값 5xx이(가)인 경우 정상을 의미합니다. 여러 코드가 모두 정상임을 표시하려면 해당하는 값을 추가하면 됩니다.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 취하지 못했음을 의미합니다. |
| HttpCheckPath | String | 아니요 | 상태 검사 경로(HTTP/HTTPS 포워딩 규칙에만 적용)<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| HttpCheckDomain | String | 아니요 | 상태 검사 도메인 이름(HTTP/HTTPS 포워딩 규칙에만 적용).<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| HttpCheckMethod | String | 아니요 | 상태 검사 방법(HTTP/HTTPS 포워딩 규칙에만 적용)으로 값은 HEAD 또는 GET입니다.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |

## Listener

수신기 정보

다음 API에 참조됨: DescribeListeners.

| 이름 | 유형 | 설명 |
|------|------|-------|
| ListenerId | String | 응용형 CLB 수신기 ID |
| Protocol | String | 수신기 프로토콜 |
| Port | Integer | 수신기 포트 |
| Certificate | [CertificateOutput](#CertificateOutput) | 수신기가 바인딩한 인증서 정보.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| HealthCheck | [HealthCheck](#HealthCheck) | 수신기의 상태 검사 정보.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Scheduler | String | 요청 스케줄링 방식.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| SessionExpireTime | Integer | 세션 유지 시간.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| SniSwitch | Integer | SNI 특성 시작 여부(HTTPS 수신기에만 적용)<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Rules | Array of [RuleOutput](#RuleOutput) | 수신기의 전체 포워딩 규칙(HTTP/HTTPS 수신기에만 적용).<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| ListenerName | String | 수신기의 이름<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |

## ListenerBackend

수신기에 등록한 RS 정보

다음 API에 참조됨: DescribeTargets.

| 이름 | 유형 | 설명 |
|------|------|-------|
| ListenerId | String | 수신기 ID |
| Protocol | String | 수신기 프로토콜|
| Port | Integer | 수신기 포트 |
| Rules | Array of [RuleTargets](#RuleTargets) | 수신기의 규칙 정보(HTTP/HTTPS 수신기에만 적용).<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Targets | Array of [Backend](#Backend) | 수신기에 등록한 서버 리스트(TCP/UDP/TCP_SSL 수신기에만 적용).<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |

## LoadBalancer

로드밸런서 인스턴스 정보

다음 API에 참조됨: DescribeLoadBalancers.

| 이름 | 유형 | 필수 여부 | 설명 |
|------|------|----------|------|
| LoadBalancerId | String | 아니요 | 로드밸런서 인스턴스 ID. |
| LoadBalancerName | String | 아니요 | 로드밸런서 인스턴스의 이름. |
| LoadBalancerType | String | 아니요 | 로드밸런서 인스턴스의 네트워크 유형<br/>OPEN: 공중망 속성, INTERNAL: 사설망 속성. |
| Forward | Integer | 아니요 | 응용형 CLB 식별, 1: 응용형 CLB, 0: 전통형 CLB. |
| Domain | String | 아니요 | 로드밸런서 인스턴스의 도메인 이름 사설망 기반 로드밸런싱 및 응용형 로드밸런서 인스턴스는 해당 필드를 제공하지 않습니다.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| LoadBalancerVips | Array of String | 아니요 | 로드밸런서 인스턴스의 VIP 리스트.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Status | Integer | 아니요 | 로드밸런서 인스턴스의 상태,<br/>0: 생성 중, 1: 정상 운행 중.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| CreateTime | String | 아니요 | 로드밸런서 인스턴스의 생성 시간.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| StatusTime | String | 아니요 | 로드밸런서 인스턴스의 마지막 상태 전환 시간.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| ProjectId | Integer | 아니요 | 로드밸런서 인스턴스 소속 프로젝트 ID로 0은 기본 프로젝트를 의미합니다. |
| VpcId | String | 아니요 | VPC의 ID.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| OpenBgp | Integer | 아니요 | Anti-DDoS LB의 식별, 1: Anti-DDoS CLB, 0: Anti-DDoS CLB가 아님.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Snat | Boolean | 아니요 | 2016년 12월 이전의 전통형 사설망 기반 로드밸런서는 모두 snat을 시작한 것입니다.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Isolation | Integer | 아니요 | 0: 격리되지 않음, 1: 격리됨.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Log | String | 아니요 | 사용자 로그 활성화 여부 정보. HTTP 및 HTTPS 수신기가 생성된 공중망 기반 로드밸런서에만 로그가 있습니다.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| SubnetId | String | 아니요 | 로드밸런서 인스턴스가 속한 서브넷(사설 VPC형 LB에만 적용).<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |

## RuleInput

HTTP/HTTPS 포워딩 규칙(입력)

다음 API에 참조됨: CreateRule.

| 이름 | 유형 | 필수 여부 | 설명 |
|------|------|----------|------|
| Domain | String | 예 | 포워딩 규칙의 도메인 이름. |
| Url | String | 예 | 포워딩 규칙의 경로. |
| SessionExpireTime | Integer | 아니요 | 세션 유지 시간 |
| HealthCheck | [HealthCheck](#HealthCheck) | 아니요 | 상태 검사 정보 |
| Certificate | [CertificateInput](#CertificateInput) | 아니요 | 인증서 정보 |
| Scheduler | String | 아니요 | 규칙의 요청 포워딩 방식 |

## RuleOutput

HTTP/HTTPS 포워딩 규칙(출력)

다음 API에 참조됨: DescribeListeners.

| 이름 | 유형 | 설명 |
|------|------|-------|
| LocationId | String | 포워딩 규칙의 ID. 입력 시 이 필드가 필요하지 않습니다. |
| Domain | String | 포워딩 규칙의 도메인 이름.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Url | String | 포워딩 규칙의 경로.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| SessionExpireTime | Integer | 세션 유지 시간 |
| HealthCheck | [HealthCheck](#HealthCheck) | 상태 검사 정보.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Certificate | [CertificateOutput](#CertificateOutput) | 인증서 정보.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Scheduler | String | 규칙의 요청 포워딩 방식 |

## RuleTargets

HTTP/HTTPS 수신기의 포워딩 규칙의 서버 바인딩 정보

다음 API에 참조됨: DescribeTargets.

| 이름 | 유형 | 설명 |
|------|------|-------|
| LocationId | String | 포워딩 규칙의 ID |
| Domain | String | 포워딩 규칙의 도메인 이름 |
| Url | String | 포워딩 규칙의 경로. |
| Targets | Array of [Backend](#Backend) | RS의 정보.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |

## Target

포워딩 대상으로 로드밸런서에 바인딩한 RS.

다음 API에 참조됨: DeregisterTargets, ModifyTargetPort, ModifyTargetWeight, RegisterTargets.

| 이름 | 유형 | 필수 여부 | 설명 |
|------|------|----------|------|
| InstanceId | String | 예 | CVM의 유일한 ID, DescribeInstances API의 반환된 필드에서 unInstanceId에서 가져올 수 있습니다.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Port | Integer | 예 | 백 엔드 CVM 수신 포트입니다<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Type | String | 아니요 | 포워딩 대상의 유형으로 현재 가능 값은 CVM 뿐입니다.<br/>주의: 이 필드는 null을 반환할 수 있으며 유효값을 얻지 못했음을 의미합니다. |
| Weight | Integer | 아니요 | 백 엔드 CVM의 포워딩 가중치. 값 범위: 0 ~ 100, 기본값: 10. |


