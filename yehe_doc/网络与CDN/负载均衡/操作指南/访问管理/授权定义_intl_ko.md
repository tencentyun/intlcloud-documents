## CAM에서 권한 부여 가능한 CLB 리소스 유형
| 리소스 유형 | 권한 부여 정책 중 리소스 메소드 설명 |
| :-------- | -------------- |
| CLB 인스턴스 |  ` qcs::clb:$region::clb/$loadbalancerid`  |
| CLB 리얼 서버 |   `qcs::cvm:$region:$account:instance/$cvminstanceid` |

이 중,
- `$region`은 항상 region의 ID여야 하며 비워 둘 수 있습니다.
- `$account`는 항상 리소스 소유자의 AccountId 또는 ‘\*’여야 합니다.
- `$loadbalancerid`는 항상 loadbalancer 인스턴스의 ID 또는 ‘\*’여야 합니다.

등등.

## CAM의 CLB에 대해 권한 부여가 가능한 API
CAM에서 CLB 리소스에 대해 다음 Action을 권한 부여할 수 있습니다.
### 인스턴스

| API 작업 | 리소스 설명 | API 설명 |
| :-------- | :--------| :------ |
| DescribeLoadBalancers|  CLB 인스턴스 목록 쿼리 | `*` API만 인증함을 나타냄 |
| CreateLoadBalancer|  CLB 인스턴스 구매 | `qcs:$projectid:clb:$region:$account:clb/*` |
| DeleteLoadBalancers|  CLB 인스턴스 삭제 | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyLoadBalancerAttributes|  CLB 인스턴스 속성 수정 | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyForwardLBName|  CLB 인스턴스 이름 수정 | `qcs::clb:$region:$account:clb/$loadbalancerid` |

### 리스너

| API 작업 | 리소스 설명 | API 설명 |
| :-------- | :---------| :------ |
|DeleteLoadBalancerListeners|CLB 리스너 삭제| `qcs::clb:$region:$account:clb/$loadbalancerid`  |
|DescribeLoadBalancerListeners|CLB 리스너 목록 가져오기|`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|ModifyLoadBalancerListener|CLB 리스너의 속성 수정|`qcs::clb:$region:$account:clb/$loadbalancerid` |
|CreateLoadBalancerListeners|CLB 리스너 생성|`qcs::clb:$region:$account:clb/$loadbalancerid` |
|DeleteForwardLBListener|CLB 리스너(레이어 4 및 레이어 7) 삭제|`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|ModifyForwardLBSeventhListener|CLB 레이어 7 리스너 속성 수정|`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|ModifyForwardLBFourthListener|CLB 레이어 4 리스너 속성 수정|`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|DescribeForwardLBListeners|CLB 리스너 목록 쿼리|`qcs::clb:$region:$account:clb/$loadbalancerid` |
|CreateForwardLBSeventhLayerListeners|레이어 7 CLB 리스너 생성|`qcs::clb:$region:$account:clb/$loadbalancerid` |
|CreateForwardLBFourthLayerListeners|레이어 4 CLB 리스너 생성|`qcs::clb:$region:$account:clb/$loadbalancerid` |

### CLB 도메인 이름 + URL

| API 작업 | 리소스 설명 | API 설명 |
| :-------- | --------| :------ |
|ModifyForwardLBRulesDomain|CLB 리스너의 포워딩 규칙의 도메인 이름 수정  |`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|CreateForwardLBListenerRules|CLB 리스너 포워딩 규칙 생성|`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|DeleteForwardLBListenerRules|레이어 7 CLB 리스너 규칙 삭제|`qcs::clb:$region:$account:clb/$loadbalancerid` |
|DeleteRewrite|CLB 인스턴스의 포워딩 규칙의 리디렉션 관계 삭제|`qcs::clb:$region:$account:clb/$loadbalancerid` |
|ManualRewrite|CLB 인스턴스의 포워딩 규칙의 리디렉션 관계 수동 추가| `qcs::clb:$region:$account:clb/$loadbalancerid`  |
|AutoRewrite|CLB 인스턴스의 포워딩 규칙의 리디렉션 관계 자동 생성|`qcs::clb:$region:$account:clb/$loadbalancerid`  |

### 리얼 서버

| API 작업 | 리소스 설명 | API 설명 |
| :-------- | :--------| :------ |
|ModifyLoadBalancerBackends| CLB 인스턴스의 리얼 서버 가중치 수정|`qcs::clb:$region:$account:clb/$loadbalancerid` |
|DescribeLoadBalancerBackends| CLB 인스턴스에 바인딩된 리얼 서버 목록 가져오기|`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|DeregisterInstancesFromLoadBalancer |리얼 서버 바인딩 해제|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|RegisterInstancesWithLoadBalancer| 리얼 서버를 CLB 인스턴스에 바인딩|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|DescribeLBHealthStatus| CLB 상태 쿼리|`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|ModifyForwardFourthBackendsPort| 레이어 4 리스너의 포워딩 규칙에서 CVM 인스턴스 포트 수정|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|ModifyForwardFourthBackendsWeight|레이어 4 리스너의 포워딩 규칙에서 CVM 인스턴스 가중치 수정|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|RegisterInstancesWithForwardLBSeventhListener| CLB 레이어 7 리스너의 포워딩 규칙에 CVM 인스턴스 바인딩|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|RegisterInstancesWithForwardLBFourthListener| CLB 레이어 4 리스너의 포워딩 규칙에 CVM 인스턴스 바인딩|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|DeregisterInstancesFromForwardLBFourthListener|CLB 레이어 4 리스너의 포워딩 규칙에서 CVM 인스턴스 바인딩 해제|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|DeregisterInstancesFromForwardLB| CLB 레이어 7 리스너의 포워딩 규칙에서 CVM 인스턴스 바인딩 해제|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|ModifyForwardSeventhBackends| 레이어 7 리스너의 포워딩 규칙에서 CVM 인스턴스 가중치 수정|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|ModifyForwardSeventhBackendsPort| 레이어 7 리스너의 포워딩 규칙에서 CVM 인스턴스 포트 수정|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|DescribeForwardLBBackends |CLB 인스턴스의 CVM 인스턴스 목록 쿼리|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/*`|
|DescribeForwardLBHealthStatus|CLB 상태 확인 상태 쿼리|`qcs::clb:$region:$account:clb/*`  |
|ModifyLoadBalancerRulesProbe| CLB 리스너의 포워딩 규칙 상태 확인 및 포워딩 경로 수정|`qcs::clb:$region:$account:clb/$loadbalancerid` |


