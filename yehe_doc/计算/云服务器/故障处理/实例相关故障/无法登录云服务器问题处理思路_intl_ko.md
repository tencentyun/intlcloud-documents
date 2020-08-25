본 문서에서는 CVM(Cloud Virtual Machine) 인스턴스를 구매한 후 인스턴스 로그인 오류를 해결하는 방법을 설명합니다.

## 장애 주요 원인

아래 이미지는 CVM 인스턴스에 연결할 수 없는 주요 원인 및 발생 확률을 보여줍니다. 인스턴스에 연결할 수 없으면, 스마트 진단 툴과 결합해 아래 원인에 따라 문제를 해결하시기 바랍니다.
<img src="https://main.qcloudimg.com/raw/d8e0151489003a251514eebe74dc201a.png" height="310" width="520" />

## 장애 처리 순서

### 인스턴스 유형 확인

먼저 구매한 인스턴스 유형이 Windows 시스템 인스턴스인지 Linux 시스템 인스턴스인지 파악합니다. 파악한 다음 각 인스턴스 유형마다 CVM에 로그인할 수 없는 원인이 다르므로 구매한 인스턴스 유형에 맞게 다음 문서를 참조하여 문제를 진단하고 해결합니다.
- [Windows 인스턴스에 로그인할 수 없는 경우](http://intl.cloud.tencent.com/document/product/213/10339)
- [Linux 인스턴스에 로그인할 수 없는 경우](https://intl.cloud.tencent.com/document/product/213/32500)

### 점검 툴로 원인 진단
Tencent Cloud는 [자가 진단](https://console.cloud.tencent.com/workorder/check)과 [보안 그룹(포트)검증 툴](https://console.cloud.tencent.com/vpc/helper)을 제공하여 로그인할 수 없는 원인을 판단합니다. 약 70%의 로그인 문제는 툴을 통해 점검 및 진단할 수 있습니다.

#### 자가 진단 툴
진단 가능한 문제는 대역폭 이용률이 지나치게 높은 경우, 외부 네트워크 대역폭이 0인 경우, 서버 고부하인 경우, 보안 그룹 규칙이 부적합한 경우, DDoS 공격을 막은 경우, 보안 격리 및 계정 연체 등을 포함합니다.

#### 보안 그룹(포트) 진단 툴
보안 그룹과 포트 관련 장애를 점검합니다. 보안 그룹 설정에 문제가 있으면, 해당 툴의 **원클릭 오픈**기능을 통해 모든 보안 그룹 상용 인터페이스를 오픈할 수 있습니다.
툴을 통해 원인을 진단한 경우, 그에 따라 상응하는 장애 처리를 진행하시기 바랍니다.

### 인스턴스 재시작
점검 툴을 통해 상응하는 장애를 판단 및 처리한 후, 또는 점검 툴을 통해서도 로그인할 수 없는 원인을 진단할 수 없는 경우 모두 인스턴스 재시작을 통해 원격 연결을 다시 시도해 연결에 성공했는지 조회할 수 있습니다.
인스턴스 재시작 작업은 [인스턴스 재시작](http://intl.cloud.tencent.com/document/product/213/4928)을 참조할 수 있습니다.

### 흔히 발생하는 기타 로그인 문제의 원인
위의 처리 단계를 통해서도 문제의 원인을 진단할 수 없거나 CVM에 로그인할 때 사용자가 직접 다음 유형의 오류 메시지를 출력할 경우, 다음 솔루션을 참조할 수 있습니다.

#### Windows 인스턴스
- [Windows 인스턴스: 원격 데스크톱 서비스 로그인 권한 없는 경우](https://intl.cloud.tencent.com/document/product/213/32420)
- [Windows 인스턴스: Mac 원격 로그인 비정상](https://intl.cloud.tencent.com/document/product/213/32422)
- [Windows 인스턴스: 인증 오류 발생](https://intl.cloud.tencent.com/document/product/213/32421)
- [Windows 인스턴스: 원격 데스크톱이 원격 컴퓨터로 연결할 수 없는 경우](https://intl.cloud.tencent.com/document/product/213/32404)

#### Linux 인스턴스
- [Linux 인스턴스: CPU 또는 메모리의 높은 점유율로 인해 로그인할 수 없는 경우](https://intl.cloud.tencent.com/document/product/213/32387)

## 후속 작업

위의 단계를 통해서도 원격 로그인할 수 없는 문제를 해결할 수 없는 경우, 관련 로그와 자가 점검 결과를 저장한 후 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 피드백 및 해결할 수 있습니다.
