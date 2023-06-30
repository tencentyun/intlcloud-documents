### 리전 리스트는 어떻게 조회하나요?

아래의 방식으로 조회할 수 있습니다.
- [리전 및 가용존](https://intl.cloud.tencent.com/document/product/213/6091) 문서 조회
- API 인터페이스 조회:
 - [리전 리스트 조회](https://intl.cloud.tencent.com/document/product/213/15708)
 - [가용존 리스트 조회](https://intl.cloud.tencent.com/document/product/213/35071)

### 이미 구매한 CVM의 리전을 변경할 수 있나요?

이미 구매한 CVM의 리전은 변경할 수 없습니다. 이미 실행한 인스턴스는 가용존을 변경할 수 없으므로, 리전 또는 가용존을 변경하고 싶다면 다음의 두 가지 방법을 참조 바랍니다.

- 먼저 기존 인스턴스로 사용자 정의 이미지를 생성한 뒤, 다시 새로운 가용존에서 사용자 정의 이미지를 사용하여 인스턴스를 생성 및 실행하고 새로운 인스턴스의 구성을 갱신합니다.
  1. 현재 인스턴스의 사용자 정의 이미지 생성 상세정보는 [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942)을 참조 바랍니다.
  2. 현재 인스턴스의 네트워크 환경이 [VPC](https://intl.cloud.tencent.com/document/product/213/5227)일 때, 마이그레이션 후 현재의 개인 IP 주소를 유지하려면 현재 가용존의 서브넷을 삭제한 다음, 새로운 가용존에서 초기 서브넷과 같은 IP 주소 범위를 사용하여 서브넷을 생성합니다.
  > 삭제한 서브넷에 가용 인스턴스가 포함된 경우, 반드시 현재 서브넷의 모든 인스턴스를 새로운 인스턴스로 옮긴 후 삭제해야 합니다.
  >
  3. 방금 생성한 사용자 정의 이미지를 사용해, 새로운 가용존에서 새 인스턴스를 생성합니다.
  사용자는 원본 인스턴스와 같은 인스턴스 유형 및 구성 또는 새로운 인스턴스 유형 및 구성을 선택할 수 있습니다. 자세한 내용은 [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참조 바랍니다.
  4. 초기 인스턴스에 연결된 EIP 주소가 있을 경우, 예전 인스턴스와 연결을 해제하고 새로운 인스턴스와 연결합니다. 자세한 내용은 [EIP](https://intl.cloud.tencent.com/document/product/213/5733)를 참조 바랍니다.
  5. (선텍)기존 인스턴스가 [종량제](https://intl.cloud.tencent.com/document/product/213/2180) 유형일 경우, 초기 인스턴스를 폐기할 수 있습니다. 자세한 내용은 [인스턴스 폐기](https://intl.cloud.tencent.com/document/product/213/4930)를 참조 바랍니다.
