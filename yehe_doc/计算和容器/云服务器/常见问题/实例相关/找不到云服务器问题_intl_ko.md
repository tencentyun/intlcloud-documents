## 문제 설명
구매한 CVM 인스턴스를 CVM 콘솔에서 찾을 수 없습니다.


## 가능한 원인
[1. 인스턴스가 현재 리전에 없습니다](#1)
[2. 올바른 콘솔에 로그인하지 않았습니다](#2)
[3. 현재 계정에서 사용 가능한 인스턴스가 없습니다](#3)
[4. 연체 또는 만료로 인해 인스턴스가 릴리스되었습니다](#4)
[5. 스팟 인스턴스가 자동으로 회수되었습니다](#5)
[6. 리소스 부족으로 인해 환불되었습니다](#6)


## 솔루션
[](id:1)
### 1. 인스턴스가 현재 리전에 없습니다
인스턴스가 있는 리전으로 전환하지 않으면 인스턴스를 찾을 수 없습니다. 다음 방법으로 확인할 수 있습니다.
[CVM 인스턴스 페이지](https://console.cloud.tencent.com/cvm/instance) 상단에서 리전을 전환합니다. 인스턴스가 다른 리전에 있는 경우 대상 리전으로 전환하여 조회합니다. 
<img src="https://qcloudimg.tencent-cloud.cn/raw/9f3877ec56c7a19adf8c3e5594d5038f.png" width="500px"/>

[](id:2)

### 2. 올바른 콘솔에 로그인하지 않았습니다
CVM 인스턴스 대신 [Lighthouse 인스턴스](https://console.cloud.tencent.com/lighthouse/instance) 또는 다른 인스턴스를 구입했고 올바른 콘솔에 로그인하지 않았을 수 있습니다.
- 방법1: [콘솔 개요](https://console.cloud.tencent.com/) > **주문 관리**에서 최근 3개월 간의 선불 / 후불 주문을 확인합니다. 오래 전에 인스턴스를 구매한 경우 **[전체 기간](https://console.cloud.tencent.com/expense/deal)** 을 클릭하십시오. 
<img src="https://qcloudimg.tencent-cloud.cn/raw/435aaa01910882ffd0edf1a1dd94a1e0.png" width="500px"/>                                       	

- 방법2: [콘솔 개요](https://console.cloud.tencent.com/) > **내 리소스**를 클릭하여 현재 계정에 있는 모든 리소스를 확인합니다.  
<img src="https://qcloudimg.tencent-cloud.cn/raw/0b159468504385294580b4485235f976.png" width="500px"/>              



[](id:3)

### 3. 현재 계정에서 사용 가능한 인스턴스가 없습니다
- CVM과 관련하여 수신한 SMS에서 계정 ID를 찾을 수 있습니다.
- 본인 명의의 계정으로 인스턴스를 구매하지 않았을 수 있습니다. 

[](id:4)

### 4. 연체 또는 만료로 인해 인스턴스가 릴리스되었습니다
인스턴스가 만료되었거나 결제가 연체된 경우 릴리스되므로 콘솔에서 찾을 수 없습니다.

- 폐기된 인스턴스는 복구할 수 없습니다. <선불 서비스 만료 및 중단 공지>는 [메시지 센터](https://console.cloud.tencent.com/message/index)를 통해 확인하실 수 있습니다. 메시지 센터에서 관련 메시지를 받지 못한 경우 알림 수신을 거부했을 수 있습니다.
- 계정의 결제가 연체된 경우 [연체 설명](https://intl.cloud.tencent.com/document/product/213/2181)을 참고하여 CVM 인스턴스 및 공중망 대역폭의 상태를 확인하십시오.

[](id:5)

### 5. 스팟 인스턴스가 자동으로 회수되었습니다
할당된 [스팟 인스턴스](https://intl.cloud.tencent.com/document/product/213/17816)는 가격 또는 수요와 공급의 관계에 따라 회수될 수 있습니다.

스팟 인스턴스가 종료되기 전에 메시지 센터 또는 metadata를 통해 알림을 받게 됩니다. <스팟 인스턴스 회수 공지>는 [메시지 센터](https://console.cloud.tencent.com/message/index)를 통해 확인할 수 있습니다. 메시지 센터에서 관련 메시지를 받지 못한 경우 알림 수신을 거부했을 수 있습니다. 

[](id:6)

### 6. 리소스 부족으로 인해 환불되었습니다
콘솔에서 새로 구매한 인스턴스를 찾을 수 없다면 리소스 부족으로 인해 환불되었기 때문일 수 있습니다.

[주문 관리](https://console.cloud.tencent.com/expense/deal)에서 환불 관련 정보 확인 후 다른 리전 또는 가용존에서 재구매 가능합니다.
