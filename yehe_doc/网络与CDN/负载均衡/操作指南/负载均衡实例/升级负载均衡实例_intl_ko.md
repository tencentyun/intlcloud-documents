CLB 인스턴스는 공유 CLB 인스턴스와 LCU 지원 인스턴스의 두 가지 유형으로 제공됩니다. 공유 CLB 인스턴스를 LCU 지원 CLB 인스턴스로 업그레이드할 수 있습니다.


## LCU 지원 CLB의 장점
- 공유 CLB 인스턴스는 최대 5만개의 동시 접속, 초당 5000개의 신규 접속 및 5000개의 QPS(초당 쿼리 수)를 유지할 수 있습니다. 보장된 성능 범위 내에서 전용 포워딩 성능을 누리고 과도한 성능을 위해 공유 클러스터 리소스를 사용하므로 성능 선점이 발생할 수 있습니다.
- 각 LCU 지원 CLB 인스턴스는 최대 100만 동시 접속, 10만개의 새 연결 및 5만 QPS를 지원합니다. 능력을 높이려면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1)하십시오.


## 업그레이드 영향
- **속도 제한**
	- 업그레이드 중 사설망 LCU 지원 인스턴스의 기본 대역폭은 10Gbps이며 조정할 수 있는 반면, 공중망 LCU 지원 인스턴스의 인스턴스는 동일하게 유지되며 조정할 수 없습니다(업그레이드 후 콘솔에서 조정할 수 있음).
	- 최대 용량은 100만 동시 접속, 10만 개의 새로운 연결/초, 50만 개의 QPS입니다. 상한을 초과하면 속도 제한 및 패킷 손실이 발생합니다. LCU 지원 인스턴스의 속도 제한 지표는 아래를 참고하십시오. 자세한 내용은 [모니터링 지표](https://intl.cloud.tencent.com/document/product/214/32389)를 참고하십시오.
		- ClientConcurConn(클라이언트-CLB 동시 접속)
		- ClientNewConn(클라이언트-CLB 신규 연결)
		- TotalReq(초당 쿼리 수)
		- ClientOuttraffic(클라이언트-CLB 아웃바운드 대역폭)
		- ClientIntraffic(클라이언트-CLB 인바운드 대역폭)
	- 업그레이드된 인스턴스의 최대 용량을 초과하지 않으면 기존 연결은 영향을 받지 않습니다.


- **과금**
	 - 과금 방식은 변경되지 않습니다.
	 - LCU 요금은 시간당 사용된 LCU 수를 기준으로 청구됩니다. 자세한 내용은 [LCU Pricing](https://www.tencentcloud.com/document/product/214/41563)을 참고하십시오.

- **네트워크 연결**
	 업그레이드는 네트워크 연결을 방해하지 않으며 1분 이내에 완료될 수 있습니다.

- **롤백**
	 한 번 업그레이드된 인스턴스는 공유 인스턴스로 다운그레이드할 수 없습니다.

## 제한 사항
- 현재 LCU 지원 인스턴스 유형은 베타 버전입니다. 업그레이드하거나 구매하려면 [Submit Ticket](https://console.tencentcloud.com/workorder/category)하여 신청하십시오.
- 여러 종량제 공유 CLB 인스턴스 업그레이드가 지원됩니다.
- 기존 CLB 인스턴스 업그레이드는 허용되지 않습니다.
- 기본 네트워크 CLB 인스턴스 업그레이드는 허용되지 않습니다.




## 업그레이드 방법
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 **인스턴스 관리**를 클릭합니다.
2. CLB 인스턴스 목록에서 대상 공유 인스턴스를 선택하고 인스턴스 목록 위에서 **업그레이드**를 클릭합니다.
![]()
3. ‘인스턴스 업그레이드’ 팝업 창에서 **확인**을 클릭합니다.
![]()


## 관련 문서
[LCU Pricing](https://www.tencentcloud.com/document/product/214/41563)
