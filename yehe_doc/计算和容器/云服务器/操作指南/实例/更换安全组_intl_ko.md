## 작업 시나리오

보안 그룹은 스테이트풀 패킷 필터링 가상 방화벽의 일종으로 단일 또는 다중 CVM의 네트워크 액세스 제어 설정에 사용되며, Tencent Cloud에서 제공하는 주요 네트워크 보안 격리 수단입니다. CVM 인스턴스를 생성할 때 인스턴스에 반드시 보안 그룹을 설정해야 하며, Tencent Cloud에서는 CVM 인스턴스를 생성한 후, 사용자의 인스턴스 보안 그룹 변경을 지원합니다.
>! 인스턴스에 새로운 보안 그룹을 설정하고 싶을 경우, 먼저 보안 그룹을 생성해야 합니다. 자세한 작업 방식은 [보안 그룹 생성](https://intl.cloud.tencent.com/document/product/213/34271)을 참조 바랍니다.

## 전제 조건

[CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인되어 있어야 합니다.

## 작업 순서

### 설정된 보안 그룹 변경

더 편리한 CVM 콘솔 사용을 위해, 인스턴스 관리 페이지를 통한 설정과 인스턴스 상세 페이지를 통한 설정 등 두 가지 보안 그룹 설정 루트가 제공됩니다.

#### 인스턴스 관리 페이지에서의 보안 그룹 설정

1. 아래 이미지와 같이, 인스턴스 관리 페이지에서 새로운 보안 그룹을 할당할 CVM을 선택한 뒤 [More]>[Security Groups]>[Configure Security Groups]를 클릭합니다.
![](https://main.qcloudimg.com/raw/68a30faac347446e57d87e8a1c30ef11.png)
2. 팝업된 "Configure Security Groups" 창에서 새로운 보안 그룹 이름을 체크한 뒤(다중 선택 가능), [OK]를 클릭하면 보안 그룹 변경 작업이 완료됩니다.
 
#### 인스턴스 상세 페이지에서의 보안 그룹 설정
 
1. 인스턴스 관리 페이지에서 보안 그룹을 변경할 CVM 인스턴스의 ID/인스턴스 이름을 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 아래 이미지와 같이, 인스턴스 상세 페이지에서 우측 상단의 [More actions]>[Configure Security Groups]를 클릭합니다.
![](https://main.qcloudimg.com/raw/c7a1d76159feaa66f52eb16c7787432d.png)
3. 팝업된 "Configure Security Groups" 창에서 새로운 보안 그룹 이름을 체크한 뒤(다중 선택 가능), [확인]을 클릭합니다.

### 바인딩된 보안 그룹 변경

1. 인스턴스 관리 페이지에서 보안 그룹을 바인딩할 CVM 인스턴스의 ID/인스턴스 이름을 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 아래 이미지와 같이, 인스턴스 상세 페이지에서 [Security Groups] 탭을 선택한 뒤 "Bound to security group" 란에서 [Bind]를 클릭합니다.
![](https://main.qcloudimg.com/raw/2ea553a1f2f589c6202245addfd62523.png)
3. 아래 이미지와 같이, 팝업된 "Configure Security Groups" 창에서 실제 필요에 따라 바인딩할 보안 그룹을 체크한 뒤, [OK]를 클릭하면 바인딩이 완료됩니다.
![](https://main.qcloudimg.com/raw/ac58322e8b11db8497d79eb54ecc67f6.png)
