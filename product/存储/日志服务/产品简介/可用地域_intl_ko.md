## 개요

사용자는 CLS를 사용하는 동안 다른 지역에서 로그 집합과 로그 토픽을 생성할 수 있습니다. 지역은 물리적 IDC의 지리적 영역을 의미하며 서로 다른 지역 간의 네트워크는 완전히 격리되어 있습니다. 사용자는 자신의 비즈니스 시나리오 및 대상 사용자의 지리적 위치에 따라 가장 가까운 지리적 저장소를 선택하여 로그 데이터의 액세스 지연을 줄이고 액세스 속도를 향상시킬 수 있습니다. 


### 선전/상하이 금융 전용 지역에 대한 특별 설명

높은 보안 및 높은 격리 기능을 갖춘 금융 업계의 규정 요구 사항에 따른 맞춤형 규정 준수 영역. 현재 CLS는 선전 금융 전용 지역 및 상하이 금융 전용 지역을 지원합니다. 금융 업계의 검증된 고객은 티켓을 제출하여 전용 지역에 대한 사용을 신청할 수 있습니다. 자세한 내용은 [금융 전용 지역 소개](https://cloud.tencent.com/document/product/304/2766)를 참조하십시오.


## 가용 영역 및 약어

| 지역     | 지역 약어        | 요청 도메인 이름                         |
| -------- | --------------- | -------------------------------- |
| 베이징     | ap-beijing      | ap-beijing.cls.myqcloud.com      |
| 상하이     | ap-shanghai     | ap-shanghai.cls.myqcloud.com     |
| 광저우     | ap-guangzhou    | ap-guangzhou.cls.myqcloud.com    |
| 청두     | ap-chengdu      | ap-chengdu.cls.myqcloud.com      |
| 선전 금융 | ap-shenzhen-fsi | ap-shenzhen-fsi.cls.myqcloud.com |
| 상하이 금융 | ap-shanghai-fsi | ap-shanghai-fsi.cls.myqcloud.com |
| 토론토   | na-toronto      | na-toronto.cls.myqcloud.com      |



## 주의 사항

다른 클라우드 제품이 CLS에 연결되어 있는 경우 다른 클라우드 제품과 동일한 지역의 로그 집합을 선택하십시오. 동일한 지역의 클라우드 제품은 사설망을 통해 데이터를 읽고 쓸 수 있으므로 지연을 효과적으로 줄이고 액세스 속도를 높일 수 있습니다.

