## 작업 시나리오
더 큰 종량제 인스턴스에 적용하기 위해 더 큰 [정규화 인자](#length)를 사용하여 여러 예약 인스턴스를 단일 예약 인스턴스로 병합할 수 있습니다.

## 규칙 및 제한
● 예약 인스턴스는 **활성화** 상태입니다.
● 예약 인스턴스는 동일한 가용존에 있습니다.
● 예약 인스턴스의 결제 수단은 동일합니다.
● 예약 인스턴스는 운영 체제(Windows/Linux)와 만료 시간이 동일합니다.
● 1c1g 1c2g 2c4g 예약 인스턴스의 병합은 지원되지 않습니다.
● 인스턴스 크기는 수정할 수 있지만 인스턴스 패밀리는 수정할 수 없습니다.
● 예약 인스턴스의 리전 또는 가용존 수정은 지원되지 않습니다.
● 대상 예약 인스턴스의 총 정규화 인자는 원래 예약 인스턴스의 정규화 인자와 같아야 합니다.
● 병합하기 전에 cpu:메모리 비율이 동일한지 확인하십시오.

## 작업 단계
1. CVM 콘솔에 로그인합니다.
2. 왼쪽 사이드바에서 예약 인스턴스를 클릭합니다.
3. 예약 인스턴스 페이지에서 원래 예약 인스턴스를 찾고 작업 열 아래에서 병합을 클릭합니다.
4. 팝업 창에서 병합할 예약 인스턴스를 선택하고 대상 예약 인스턴스의 새 이름을 입력합니다.

## 실행 결과
병합 후 원래 예약 인스턴스는 **만료됨** 상태가 되고 새 예약 인스턴스는 **활성화됨** 상태가 됩니다.

## <a id="length">용어 사전</a>
정규화 인자: 인스턴스의 vCPU 성능을 나타냅니다. 예약 인스턴스 분할 및 병합의 경우 =vcpu 수를 기준으로 정규화 인자를 계산합니다.
정규화 인자의 합=인스턴스 크기의 정규화 인자*인스턴스 수량. 정규화 인자의 합은 분할 전과 동일하게 유지되어야 합니다.
