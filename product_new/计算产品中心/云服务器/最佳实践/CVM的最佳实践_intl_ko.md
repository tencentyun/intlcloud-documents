본 문서는 사용자가 최대한 안전하고 신뢰적인 클라우드 서버를 활용할 수 있도록 도와줍니다.

## 보안 및 네트워크

- **액세스 제한**:방화벽 ([보안 그룹](https://intl.cloud.tencent.com/document/product/213/12452)) 사용을 통해 신뢰하는 주소의 액세스 인스턴스를 허용하여 액세스를 제한하고 보안 그룹에 가장 엄격한 규칙을 구성합니다. 예를 들면 포트 액세스 및 IP 주소 액세스를 제한합니다.
- **보안 레벨**:다양한 보안 그룹 규칙을 생성하여 다양한 보안 레벨의 인스턴스 그룹에 적용함으로써 중요한 서비스를 실행하는 인스턴스가 외부에 쉽게 접촉하지 않도록 합니다.
- **네트워크 논리 격리**:[사설 네트워크](https://intl.cloud.tencent.com/document/product/213/5227) 사용을 통해 논리 영역을 구분합니다.
- **계정 권한 관리**:동일한 그룹의 클라우드 리소스가 여러 개의 다양한 계정을 컨트롤할 경우 [정책 시스템 ](https://intl.cloud.tencent.com/document/product/598/10601)을 사용해 클라우드 리소스에 대한 액세스 권한을 제어합니다.
- **안전한 로그인**:[SSH 키](https://intl.cloud.tencent.com/document/product/213/6092) 방식을 사용해 사용자의 Linux류의 인스턴스에 로그인하십시오. [비밀번호 로그인](https://intl.cloud.tencent.com/document/product/213/6093)을 사용하는 인스턴스는 불규칙적으로 암호를 수정해야 합니다.

## 스토리지

- **하드웨어 스토리지**:신뢰성 요구가 매우 높은 데이터에 대해 Tencent Cloud Cloud Block Storage（CBS）를 사용해 데이터의 지속적인 스토리지 신뢰성을 확보하십시오. [로컬 디스크](https://intl.cloud.tencent.com/document/product/213/5798)는 가능한 선택하지 마십시오. 자세한 내용은 [CBS 제품 설명서](https://intl.cloud.tencent.com/document/product/362)를 참조하십시오.


## 백업 및 복구

- **동일 리전 인스턴스 백업**:**사용자 정의 미러 이미지** 및 **클라우드 드라이브 스냅샷** 방식을 사용해 사용자의 인스턴스 및 서비스 데이터를 백업할 수 있습니다. [CBS 스냅샷](https://intl.cloud.tencent.com/document/product/362/5754) 및 [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942)을 참조하십시오.
- **리전 간 인스턴스 백업:**  [미러 이미지 복사](https://intl.cloud.tencent.com/document/product/213/4943)를 사용해 리전 간 복제 및 인스턴스 백업을 실행할 수 있습니다.
- **인스턴스 장애 차단:**[EIP](https://intl.cloud.tencent.com/document/product/213/5733)를 통한 도메인 이름 매핑은 서버를 사용할 수 없는 경우 서비스 IP를 다른 클라우드 서버 인스턴스로 빠르게 재지정하여 인스턴스 장애를 차단합니다.

## 모니터링과 알람
- **모니터링과 응답 이벤트:** 정기적으로 데이터를 모니터링하고 적절한 알람을 설정합니다. 자세한 내용은 [TCOP 제품 설명서](https://intl.cloud.tencent.com/document/product/248)를 참조하십시오.
- **돌발 요청 처리:**[오토 스케일링](https://intl.cloud.tencent.com/document/product/377)을 사용해 서비스 피크에 있는 클라우드 서버 안정성을 보장하고 비정상 인스턴스를 자동으로 교체할 수 있습니다.
