## 작업 시나리오
Tencent Cloud의 네트워크는 [classic network and VPC](https://intl.cloud.tencent.com/document/product/215/31807)로 구분되며, 사용자에게 다양한 고품질 서비스를 제공하고 있습니다. 이를 바탕으로 네트워크 연결을 쉽게 관리할 수 있도록 아래와 같이 보다 유연한 서비스를 제공합니다.
- **네트워크 스위치**
  - 클래식 네트워크에서 VPC로 전환: 단일 TencentDB 원본 인스턴스를 클래식 네트워크에서 VPC로 전환할 수 있습니다.
  - VPC A에서 VPC B로 전환: 단일 TencentDB 원본 인스턴스를 VPC A에서 VPC B로 전환할 수 있습니다.
- **사용자 정의 IP 포트**
  - 사용자 정의 원본 인스턴스 IP 및 포트: 콘솔의 인스턴스 세부 정보 페이지에서 원본 인스턴스의 IP 및 포트를 사용자 정의할 수 있습니다.
  - 사용자 정의 읽기 전용 인스턴스 IP 및 포트: 읽기 전용 인스턴스의 IP 및 포트는 콘솔의 인스턴스 세부 정보 페이지에서 사용자 정의할 수 있습니다.

## 주의 사항
- 클래식 네트워크에서 VPC로 전환한 후 동일한 VPC에 있는 클라이언트만 서로 연결할 수 있습니다. VPC IP 범위를 [설정](https://intl.cloud.tencent.com/document/product/215/31805)하여 VPC IP를 클래식 네트워크 IP와 동일하게 유지할 수 있습니다.
- 기존 IP 주소의 보관 시간은 기본 24시간이며, 최대 168시간까지 지원됩니다. 기존 IP 주소의 회수 시간을 0시간으로 설정하면 네트워크 전환 후 기존 IP 주소가 즉시 릴리스됩니다.
- 클래식 네트워크에서 VPC로의 전환은 되돌릴 수 없습니다. VPC로 전환한 후 TencentDB 인스턴스는 다른 VPC 또는 클래식 네트워크의 Tencent Cloud 서비스와 통신할 수 없습니다.
- 원본 인스턴스의 네트워크를 전환한 후 원본 인스턴스와 연결된 읽기 전용 인스턴스 또는 재해 복구 인스턴스의 네트워크는 자동으로 전환되지 않습니다. 수동으로 전환해야 합니다.

## 서브넷 설명
- 서브넷은 VPC의 논리적 네트워크 공간입니다. 기본적으로 사설망을 통해 서로 통신하는 동일한 VPC의 서로 다른 가용존에 서브넷을 생성할 수 있습니다.
- 네트워크를 선택하면 선택한 인스턴스의 AZ에 있는 서브넷 IP가 기본적으로 표시됩니다. 인스턴스 리전의 다른 가용존에서 서브넷 IP를 선택할 수도 있습니다. 비즈니스 연결은 근거리 액세스를 채택하므로 네트워크 대기 시간이 증가하지 않습니다.

## 작업 단계
### 네트워크 스위치
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 인스턴스 리스트에서 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 인스턴스 기본 정보의 **네트워크**에서 네트워크 간 전환 유형에 따라 **VPC로 스위치** 또는 **네트워크 변경**을 클릭합니다.
3. 팝업 창에서 VPC 및 해당 서브넷을 선택한 후 **확인**을 클릭합니다.
>?
>- IP 주소가 지정되지 않은 경우 시스템에서 자동으로 할당합니다.
>- 인스턴스 리전에서만 VPC를 선택할 수 있지만 모든 AZ에서 서브넷을 선택하고 해당 IP 범위를 볼 수 있습니다.
>- CVM이 있는 리전의 VPC를 선택하시길 권장합니다. 그러지 않으면, CVM에서는 내부 네트워크를 통해 TencentDB for MySQL(2개의 VPC 사이에 [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827) 또는 [CCN](https://intl.cloud.tencent.com/document/product/1003/30049)을 생성한 경우는 제외)에 액세스할 수 없습니다.
>
   - **클래식 네트워크에서 VPC로 전환**
![](https://main.qcloudimg.com/raw/ba78ed608b83c2f553cb72350b726491.png)
   - **VPC A에서 VPC B로 전환**
![](https://qcloudimg.tencent-cloud.cn/raw/82c30b3269695e6428de87d2c2c06cc0.png)
4. 인스턴스 상세 페이지로 돌아가면 인스턴스의 네트워크를 확인할 수 있습니다.

### RO 그룹 네트워크 스위치
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 인스턴스 리스트에서 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 읽기 전용 인스턴스의 **RO 그룹 정보**에서 네트워크 스위치 유형(클래식 네트워크에서 VPC 또는 VPC에서 VPC)에 따라 **서브넷 변경** 또는 **VPC로 스위치**를 클릭합니다.
3. 팝업 창에서 VPC와 서브넷을 선택한 후 **확인**을 클릭합니다.
>?
>- IP 주소가 지정되지 않은 경우 시스템에서 자동으로 할당합니다.
>- 인스턴스 리전에서만 VPC를 선택할 수 있지만 모든 AZ에서 서브넷을 선택하고 해당 IP 범위를 볼 수 있습니다.
>- CVM이 있는 리전의 VPC를 선택하시길 권장합니다. 그러지 않으면, CVM에서는 내부 네트워크를 통해 TencentDB for MySQL(2개의 VPC 사이에 [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827) 또는 [CCN](https://intl.cloud.tencent.com/document/product/1003/30049)을 생성한 경우는 제외)에 액세스할 수 없습니다.

### IP 및 포트 사용자 정의
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 인스턴스 리스트에서 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 인스턴스 기본 정보의 내부 네트워크 주소 및 포트에서 <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;">을(를) 클릭합니다.
>!내부 네트워크 주소와 포트를 변경하면 현재 액세스 중인 데이터베이스 작업에 영향을 줍니다.
3. 팝업 창에서 IP와 포트를 사용자 정의하고, 오류가 없는지 확인한 다음 **확인**을 클릭합니다.
