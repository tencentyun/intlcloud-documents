## 일반 공인 IP 관련 문제

### CVM에 공인 IP가 없을 경우 공용 네트워크에 어떻게 액세스하나요?
기기 구매 시 공인 IP를 구매하지 않았거나 공인 IP를 이미 반환한 경우, [EIP 콘솔](https://console.cloud.tencent.com/cvm/eip)에서 EIP를 신청한 후 기기에 바인딩해 공용 네트워크에 액세스할 수 있습니다.

### 공인 IP 주소를 변경할 수 있나요?

사용자의 CVM에서 공인 IP를 변경할 수 있습니다. 자세한 작업 방식은 [인스턴스의 공인 IP 변경](https://intl.cloud.tencent.com/document/product/213/16642)를 참조 바랍니다.

### 어떻게 해야 공인 IP 주소를 그대로 유지할 수 있나요?

계정의 특정 공인 IP를 유지하려면 먼저 공인 IP를 EIP로 전환하여 디바이스에 바인딩하고, 해당 IP를 사용하여 공용 네트워크에 액세스할 수 있습니다. **릴리스** 작업을 진행하지 않는 한, EIP는 사용자의 계정에 계속 보관됩니다.
자세한 내용은 [EIP](https://intl.cloud.tencent.com/document/product/213/16586)를 참조 바랍니다.

### 공인 IP 주소란 무엇인가요?
공인 IP 주소란 Internet에 접속할 수 있는 권한을 가진 주소로, 공인 IP 주소를 가진 CVM은 Internet상의 다른 컴퓨터와 상호 액세스할 수 있습니다.
더 자세한 내용은 [공용 네트워크 서비스](https://intl.cloud.tencent.com/document/product/213/5224)를 참조 바랍니다.

### 인스턴스의 공인 IP 주소는 어떻게 획득하나요?
자세한 작업 방식은 [공인 IP 주소 획득](https://intl.cloud.tencent.com/document/product/213/17940)을 참조 바랍니다.

### 인스턴스 공인 IP는 어떻게 변경하나요?
자세한 작업 방법은 [공인 IP 주소 변경](https://intl.cloud.tencent.com/document/product/213/16642)을 참조 바랍니다.

### 공용망 게이트웨이와 공인 IP를 가진 CVM의 차이점은 무엇인가요?
공용망 게이트웨이는 이미지의 공용 네트워크 트래픽을 라우팅으로 포워딩하는 기능이 활성화되어 있지만, 공인 IP를 가진 CVM에는 기본적으로 트래픽 포워딩 기능이 없습니다. Windows 이미지의 트래픽 포워딩 기능이 비활성화되어 있으므로, Windows의 공용 이미지 CVM은 공용망 게이트웨이를 사용할 수 없습니다.

### CVM의 공인 IP를 변경할 수 없습니다.
예상 원인은 다음과 같습니다.
- CVM 인스턴스가 종료되었고, 종료 시 미과금으로 설정된 경우.
- CVM의 공인 IP를 변경했던 경우.


### 인스턴스 생성 시 독립된 공인 IP(IPv4)를 할당하지 않았다면, 이후에 공인 IP 주소는 어떻게 획득해야 하나요?
- EIP를 신청하여 바인딩하는 방식으로 획득할 수 있습니다. 자세한 내용은 [EIP](https://intl.cloud.tencent.com/document/product/213/16586)를 참조 바랍니다.

## 개인 IP 관련 문제

### 개인 IP 주소란 무엇인가요?
개인 IP 주소는 Internet을 통해 액세스할 수 없는 IP 주소이며, Tencent Cloud의 내부 네트워크 서비스를 구현하는 하나의 형식입니다.
자세한 내용은 [내부 네트워크 서비스](https://intl.cloud.tencent.com/document/product/213/5225)를 참조 바랍니다.

### 인스턴스의 개인 IP 주소는 어떻게 획득하나요?
자세한 작업 방식은 [인스턴스의 개인 IP 주소 획득](https://intl.cloud.tencent.com/document/product/213/17941)을 참조 바랍니다.

### 공인 IP 주소를 변경하지 않고 개인 IP 주소만 변경할 수 있나요?
가능합니다. 자세한 작업 방식은 [개인 IP 주소 수정](https://intl.cloud.tencent.com/document/product/213/16561)을 참조 바랍니다.

