## 응용형 CLB 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [DescribeTaskStatus](https://cloud.tencent.com/document/api/214/30683) | 비동기 태스크 상태 조회 |
| [CreateLoadBalancer](https://cloud.tencent.com/document/api/214/30692) | 로드밸런서 인스턴스 구매 |
| [DescribeLoadBalancers](https://cloud.tencent.com/document/api/214/30685) | 로드밸런서 인스턴스 리스트 조회 |
| [ModifyLoadBalancerAttributes](https://cloud.tencent.com/document/api/214/30680) | 로드밸런서 인스턴스의 속성 수정 |
| [DeleteLoadBalancer](https://cloud.tencent.com/document/api/214/30689) | 로드밸런서 인스턴스 삭제 |
| [CreateListener](https://cloud.tencent.com/document/api/214/30693) | 로드밸런서 수신기 생성 |
| [DescribeListeners](https://cloud.tencent.com/document/api/214/30686) | 응용형 CLB 수신기 리스트 조회 |
| [ModifyListener](https://cloud.tencent.com/document/api/214/30681) | 로드밸런서 수신기 속성 수정 |
| [DeleteListener](https://cloud.tencent.com/document/api/214/30690) | 로드밸런서 수신기 삭제 |
| [CreateRule](https://cloud.tencent.com/document/api/214/30691) | 로드밸런서 7계층 수신기 포워딩 규칙 생성 |
| [ModifyDomain](https://cloud.tencent.com/document/api/214/30682) | 7계층 포워딩 규칙의 도메인 이름 수정 |
| [ModifyRule](https://cloud.tencent.com/document/api/214/30679) | 응용형 CLB 수신기 포워딩 규칙 수정 |
| [DeleteRule](https://cloud.tencent.com/document/api/214/30688) | 응용형 7계층 로드밸런서 수신기 규칙 삭제 |
| [RegisterTargets](https://cloud.tencent.com/document/api/214/30676) | RS를 수신기에 바인딩 |
| [DescribeTargets](https://cloud.tencent.com/document/api/214/30684) | 응용형 CLB CVM 리스트 조회 |
| [ModifyTargetPort](https://cloud.tencent.com/document/api/214/30678) | 수신기가 바인딩한 RS의 포트 수정 |
| [ModifyTargetWeight](https://cloud.tencent.com/document/api/214/30677) | 수신기가 바인딩한 RS의 포워딩 가중치 수정 |
| [DeregisterTargets](https://cloud.tencent.com/document/api/214/30687) | 응용형 CLB 수신기에 등록한 RS 언바인딩 |

## 전통형 CLB 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [DescribeClassicalLBListeners](https://cloud.tencent.com/document/api/214/31791) | 전통형 CLB 수신기 리스트 획득 |
| [RegisterTargetsWithClassicalLB](https://cloud.tencent.com/document/api/214/31789) | RS를 전통형 CLB에 바인딩 |
| [DescribeClassicalLBTargets](https://cloud.tencent.com/document/api/214/31790) | 전통형 CLB가 바인딩한 RS 리스트 획득 |
| [DescribeClassicalLBHealthStatus](https://cloud.tencent.com/document/api/214/31792) | 전통형 CLB RS의 상태 검사 획득 |
| [DeregisterTargetsFromClassicalLB](https://cloud.tencent.com/document/api/214/31794) | 전통형 CLB의 RS 언바인딩 |
| [DescribeClassicalLBByInstanceId](https://cloud.tencent.com/document/api/214/31793) | 백 엔드 CVM을 통해 바인딩한 전통형 CLB 찾기 |


