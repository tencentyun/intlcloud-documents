## 개요
건강한 모니터링 환경은 Tencent Cloud Tencent Kubernetes Engine(TKE)의 높은 안정성, 고가용성 및 고성능을 보장합니다. 다양한 리소스에 대한 다양한 차원의 모니터링 데이터를 수집할 수 있으므로 모든 리소스의 사용 정보를 쉽게 이해하고 오류를 빠르게 찾을 수 있습니다.
Tencent Cloud TKE는 클러스터, 노드, 워크로드, Pod 및 Container의 5가지 수준에서 모니터링 데이터를 수집하고 표시합니다.
모니터링 데이터 수집을 통해 클러스터 성능에 대한 일반적인 표준을 설정할 수 있습니다. 다른 시간과 다른 부하 조건에서 컨테이너 클러스터의 성능을 테스트하면 컨테이너 클러스터 또는 서비스의 정상적인 성능을 더 잘 이해할 수 있습니다. 이를 통해 현재 모니터링 데이터를 기반으로 실행 상태가 예외적인지 빠르게 판단하고 신속하게 솔루션을 찾을 수 있습니다. 예를 들어 서비스의 CPU 사용률, 메모리 사용률 또는 디스크 I/O를 모니터링할 수 있습니다.

## 모니터링
TKE 모니터링에 대한 자세한 내용은 [모니터링 데이터 조회](https://intl.cloud.tencent.com/document/product/457/30689)를 참고하십시오.
현재 지원되는 모니터링 지표에 대한 자세한 내용은 [모니터링 및 알람 지표 목록](https://intl.cloud.tencent.com/document/product/457/30691)을 참고하십시오.

## 알람
TKE 예외를 신속하게 감지하고 비즈니스의 안정성과 신뢰성을 보장하기 위해 모든 프로덕션 클러스터에 필요한 알람을 설정하는 것이 좋습니다. 알람 설정 관련 자세한 내용은 [Setting Alarm](https://intl.cloud.tencent.com/document/product/457/30690)을 참고하십시오.
현재 지원되는 알람 지표에 대한 자세한 내용은 [모니터링 및 알람 지표 목록](https://intl.cloud.tencent.com/document/product/457/30691)을 참고하십시오.

>TKE 모니터링 및 알람 기능은 주로 Kubernetes 객체의 핵심 지표 및 이벤트를 다룹니다. 보다 세분화된 측정 항목 범위를 보장하려면 [Cloud Monitoring](https://console.cloud.tencent.com/monitor/overview)에서 제공하는 기본 리소스 모니터링(예: CVM, Cloud Block Storage, CLB 등)과 함께 이러한 기능을 사용하십시오.
