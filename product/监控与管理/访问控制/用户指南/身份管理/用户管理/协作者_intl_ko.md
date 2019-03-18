## 개요
협력자는 서브 계정의 사용자 유형으로 주로 기본 계정에 클라우드 리소스 및 서브 계정을 관리하는 데 도움이 됩니다. 협력자는 리소스에 로그인하여 접근할 수 있을 뿐만 아니라 메시지 알림을 받을 수 있습니다.

## 작업 가이드

### 협력자 생성

1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 [사용자 생성]을 클릭한 다음 [협력자]를 선택합니다.
![](https://main.qcloudimg.com/raw/ac5cf81c6d781e7dca12b7efe234d092.png)

2. 관련 사용자 정보를 입력합니다. 로그인 보호 및 민감한 조작 보호를 활성화하는 것을 권장합니다.

3. 권한을 설정합니다. 다음과 같은 세 가지 방법으로 생성된 협력자에 대한 권한을 설정할 수 있습니다. 전략이 연결된 후에 협력자가 전략에서 설명한 대로 권한을 획득합니다.
 -  그룹을 사용하는 것은 작업 기능별로 사용자 권한을 관리하는 데 가장 좋은 방법입니다. 그룹에 연결되면 해당 권한을 획득할 수 있기 때문에 기존 또는 새로 생성된 사용자 그룹에 협력자를 추가하면 협력자는 그룹에 따라 첨부된 전략과 연결할 수 있습니다.
 ![](https://main.qcloudimg.com/raw/4a6b738e3748aeecc50ed0623ecfd9eb.png)
 -  기존 사용자의 권한을 복사하면 협력자와 해당 전략을 연결할 수 있습니다. [기존 사용자 권한 복사]를 클릭하고 복사해야 하는 사용자를 선택하면 협력자는 복사된 사용자에게 첨부된 전략과 연결될 수 있습니다.
 ![](https://main.qcloudimg.com/raw/908a5e4531f0b35b61f7d1db79638068.png)
 -  전략 리스트에서 권한을 부여합니다. [전략 리스트에서 권한 부여]를 클릭하고 연결할 전략을 선택합니다.
 ![](https://main.qcloudimg.com/raw/82fc1abeb724a84eba9855022fc69bfe.png)
 
4. [완료]를 클릭하여 협력자 생성을 완료합니다.

### 협력자에게 전략 연결 권한 부여

#### 직접 연결
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 전략 권한을 부여해야 하는 협력자를 찾은 다음 조작 열에서 [권한 부여]를 클릭합니다.
![](https://main.qcloudimg.com/raw/aa5e5efa2674742134ad0a100f43fc80.png)
2. 권한을 부여할 전략을 선택하고 [확인]을 클릭하여 협력자에게 전략 연결에 대한 권한 부여를 완료합니다.
![](https://main.qcloudimg.com/raw/651a1c0e8181f64a34d597e2bcd48cdc.png)

#### 그룹에 따라 연결
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 전략 권한을 부여해야 하는 협력자를 찾은 다음 조작 열에서 [기타]>[그룹에 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/34ba527220e06d8344cd9dc4dbdd0441.png)
2. 협력자를 추가할 사용자 그룹을 선택하고 [확인]을 클릭하여 그룹에 추가하여 그룹에 따른 전략 연결을 완료합니다.

### 협력자의 연결된 전략 삭제
#### 직접 해제
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 연결된 전략을 삭제하려는 협력자를 찾은 다음 협력자 이름을 클릭하여 협력자 세부 정보 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/2648266a7986476740ab2bef1006c091.png)
2. [연결된 전략]을 클릭하고 리스트에서 삭제할 전략을 찾은 다음 오른쪽의 [해제]를 클릭합니다.
![](https://main.qcloudimg.com/raw/70941b2c1281d828e7c5ca608ee462a3.png)
3. [해제 확인]을 클릭하여 협력자의 연결된 전략 삭제를 완료합니다.

#### 그룹에서 협력자 제거
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 연결된 전략을 삭제하려는 협력자를 찾은 다음 협력자 이름을 클릭하여 협력자 세부 정보 페이지로 이동합니다
![](https://main.qcloudimg.com/raw/2648266a7986476740ab2bef1006c091.png)
2. [연결한 전략]을 클릭하고 리스트에서 삭제할 그룹에 따라 연결된 전략을 찾은 다음 오른쪽의 [해제]를 클릭합니다.
![](https://main.qcloudimg.com/raw/c1566f7e4b28fd1eef8e401afb2996dc.png)
3. [해제 확인]을 클릭하여 협력자를 사용자 그룹에서 제거하고 그룹과 연결된 전략이 해제됩니다.

### 협력자를 위한 메시지 구독
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 메시지 구독하려는 협력자를 찾은 다음 조작 열에서 [기타]>[메시지 구독]을 클릭합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/79139119ca274cea6f32148bad2c31df.png)

2. 구독할 메시지 유형을 선택하고 [확인]을 클릭하여 협력자를 위한 메시지 구독을 완료합니다.
![](https://main.qcloudimg.com/raw/c527d42e456bbf72034f038fc1bad31c.png)

### 도로어로 협력자 정보 확인
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 확인해야 하는 협력자를 찾은 다음 왼쪽의 세부 정보 아이콘을 클릭합니다. 다음 그림과 같습니다.![](https://main.qcloudimg.com/raw/24cd11e8ea5094e390938b68736ec9f6.png)
>여기서 서브 사용자의 메시지 구독, 비고, 마지막 로그인 시간, 마지막 로그인 방법 및 MFA 상태 등 정보를 확인할 수 있습니다.

### 검색란을 통해 협력자 찾기
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 오른쪽 상단의 검색란에 키워드를 입력하고 검색 아이콘을 클릭하여 관련 협력자를 검색할 수 있습니다. 
![](https://main.qcloudimg.com/raw/336d924fa1ed9fc07ecf4294a54729b8.png)
>검색란은 다중 키워드 검색을 지원합니다(키워드 사이에 공백을 둠). 사용자 이름, ID, 휴대폰, 이메일 주소 및 비고 등 키워드를 통해 관련 협력자를 검색할 수 있습니다.


### 협력자 삭제
#### 단일 협력자 삭제
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 삭제할 협력자를 찾은 다음 조작 열에서 [기타]>[삭제]를 클릭합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/dc58ed07235b00038f049d22b2bec191.png)

2. [삭제 확인]을 클릭하여 협력자 삭제를 완료합니다.

#### 여러 협력자 삭제
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 왼쪽에서 삭제할 협력자를 선택하고 왼쪽 상단의 [삭제]를 클릭합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/a274a4888c8e7c00cda091538445ec54.png)
2. [삭제 확인]을 클릭하여 협력자 삭제를 완료합니다.


