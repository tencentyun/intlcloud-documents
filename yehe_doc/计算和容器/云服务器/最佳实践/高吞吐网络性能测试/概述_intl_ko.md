Tencent Cloud는 SA3, S6, C6 등 차세대 클라우드 서버 인스턴스에 최고 수준의 네트워크 성능을 제공합니다. 자세한 사항은 [인스턴스 사양](https://intl.cloud.tencent.com/document/product/213/11518)을 참고하십시오. 본문에서 제공하는 netperf 및 DPDK 두 종류의 네트워크 성능 테스트 방법을 통해 높은 처리량에 대한 클라우드 서버 네트워크 성능을 테스트할 수 있습니다.

netperf 방식으로 테스트하는 것을 추천합니다. netperf는 일반적으로 사용되는 테스트 방식으로 대부분의 테스트 시나리오 니즈를 충족합니다. 그러나 디바이스 사양이 높을 때(pps 1000만 초과, 대역폭 50Gbps 이상) netperf는 가상 컴퓨터 커널 프로토콜 스택의 전체 프로세싱 경로가 포함되어 있어 네트워크 성능 손실이 큽니다. DPDK는 가상 머신 커널 프로토콜 스택의 차이를 차단하여 가상 머신 ENI의 네트워크 성능을 가져옵니다. 이 때 DPDK 테스트 방식을 선택할 수 있습니다. 
 - [netperf 테스트 방식](https://intl.cloud.tencent.com/document/product/213/42166)
 - [DPDK 테스트 방식](https://intl.cloud.tencent.com/document/product/213/42167)

 
