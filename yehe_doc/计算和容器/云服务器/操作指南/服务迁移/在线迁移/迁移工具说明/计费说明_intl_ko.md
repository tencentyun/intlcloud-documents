서비스 마이그레이션 자체는 무료로 서비스를 제공하나, 마이그레이션 툴을 사용하는 과정에서 **릴레이 인스턴스**, **네트워크** 등의 요금이 발생할 수 있습니다. 이 문서에서는 서비스 마이그레이션 프로세스 중에 발생할 수 있는 요금 및 과금 방식에 대해 설명합니다.

## 릴레이 인스턴스
- 마이그레이션 대상이 CVM 이미지인 경우 마이그레이션 시작 후 계정에 “do_not_delete_csm_instance”라는 릴레이 인스턴스가 생성되며 인스턴스 요금, 클라우드 디스크 요금 등 일정 요금이 발생합니다.
- 과금 방식: [종량제](https://intl.cloud.tencent.com/document/product/213/2180)
- 마이그레이션이 완료될 때까지 시스템 재설치, 종료, 폐기, 비밀번호 재설정 등의 작업을 수행하지 마십시오. 마이그레이션이 완료되면 생성된 릴레이 인스턴스가 자동으로 폐기됩니다.


## 공중망 트래픽
온라인 마이그레이션 과정에서 일정량의 트래픽이 발생하며 요금은 다음과 같습니다.
- 공중망 마이그레이션을 사용하는 경우 원본 인스턴스의 대역폭이 고정된 경우 추가 요금이 발생하지 않으며, 대상이 인바운드 트래픽인 경우에도 요금이 발생하지 않습니다.
- 공중망 마이그레이션을 사용하는 경우 원본 인스턴스가 사용된 트래픽에 따라 과금되면 원본 인스턴스에서 네트워크 요금이 발생하며, 대상이 인바운드 트래픽이면 요금이 발생하지 않습니다.
- [VPC Peering Connection](https://www.tencentcloud.com/document/product/553), [VPN Connections](https://www.tencentcloud.com/document/product/1037), [Cloud Connect Network](https://www.tencentcloud.com/document/product/1003) 또는 [Direct Connect](https://www.tencentcloud.com/document/product/216) 등을 통해 연결 채널을 구축합니다. 구체적인 요금은 네트워크 요금을 참고하십시오.
