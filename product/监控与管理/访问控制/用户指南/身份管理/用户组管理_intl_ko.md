## 개요
같은 기능을 가진 사용자를 동일한 사용자 그룹에 추가하고 이 사용자 그룹에 적절한 전략을 연결하여 다른 권한을 할당해 생산성을 높일 수 있습니다.
전략이 사용자 그룹과 연결되면 사용자 그룹의 모든 사용자가 전략에서 설명한 권한을 부여받기 때문에 일괄 권한 부여 시나리오에 매우 적합합니다.

## 작업 가이드
### 사용자 그룹 생성

1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview )에 로그인하고 왼쪽 네비게이션에서 [사용자 그룹 관리]를 클릭하여 해당 페이지로 들어갑니다.
2. [사용자 그룹 생성]을 클릭하여 사용자 그룹 이름과 비고를 입력하고 [다음]을 클릭합니다(예: 예제 그룹 생성).
![](https://main.qcloudimg.com/raw/3d0df07232ad5255564915341ca56bd2.png)
>사용자 그룹 리스트에서 사용자 그룹 이름이나 비고를 검색하고 여러 사용자 그룹에서 해당 사용자 그룹을 신속하고 정확하게 찾을 수 있습니다.

3. (옵션)연결 전략을 선택(선택하지 않아도 사용자 그룹 생성 작업을 완료할 수 있음)하고 [다음]을 클릭하여 검토 단계로 들어갑니다.
![](https://main.qcloudimg.com/raw/28a7fe34644cfd986f0fc3fe29331a04.png)
4. 검토 단계에서 사용자 그룹의 관련 설정을 확인하고 오류가 있는 경우 수정할 수 있습니다. 오류가 없는지 확인한 후 [완료]를 클릭하여 사용자 그룹 생성을 완료합니다.
![](https://main.qcloudimg.com/raw/7dac4da14cb82e38355200b2a878b1b1.png)

### 사용자 그룹에 사용자 추가
#### 단일 사용자 그룹에 사용자 추가
1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview )에 로그인하고 왼쪽 네비게이션에서 [사용자 그룹 관리]를 클릭하여 해당 페이지로 들어갑니다. 사용자 그룹 리스트에서 사용자 추가할 사용자 그룹을 찾은 다음 오른쪽에 있는 [사용자 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/8d46923017c61ec74dcf901e3e97109e.png)
2. 추가할 사용자를 선택하고 [확인]을 클릭하여 사용자 그룹에 사용자 추가를 완료합니다.
![](https://main.qcloudimg.com/raw/7824db271abb280599476a4709a91ed3.png)

#### 여러 사용자 그룹에 사용자 추가
1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview )에 로그인하고 왼쪽 네비게이션에서 [사용자 그룹 관리]를 클릭하여 해당 페이지로 들어갑니다. 사용자 그룹 리스트에서 사용자 추가할 사용자 그룹을 선택한 다음 [사용자 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/34b96460336cc44e22fba290d9f0b8a7.png)

2. 추가할 사용자를 선택하고 [확인]을 클릭하여 사용자 그룹에 사용자 추가를 완료합니다.
![](https://main.qcloudimg.com/raw/7824db271abb280599476a4709a91ed3.png)

### 사용자 그룹에서 사용자 삭제
#### 사용자 그룹에서 단일 사용자 삭제
1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview )에 로그인하고 왼쪽 네비게이션에서 [사용자 그룹 관리]를 클릭하여 해당 페이지로 들어갑니다. 사용자 그룹 이름을 클릭하여 사용자 그룹 세부 정보 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/6cdce4885bb299c758130fa480af0f92.png)

2. [추가된 사용자]를 클릭여 사용자 리스트에서 삭제할 사용자를 하나씩 찾은 다음 오른쪽의 [그룹에서 제거]를 클릭하여 단일 사용자를 삭제합니다.
![](https://main.qcloudimg.com/raw/e7ab8520de2aa75deef2b307e45dcdc9.png)

3. [사용자 제거]를 클릭하여 사용자 그룹에서 사용자 삭제를 완료합니다.

#### 사용자 그룹에서 여러 사용자 삭제
1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview )에 로그인하고 왼쪽 네비게이션에서 [사용자 그룹 관리]를 클릭하여 해당 페이지로 들어갑니다. 사용자 그룹 이름을 클릭하여 사용자 그룹 세부 정보 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/6cdce4885bb299c758130fa480af0f92.png)

2. [추가된 사용자]를 클릭하고 삭제할 여러 사용자를 선택한 다음 왼쪽 상단의 [사용자 제거]를 클릭합니다.
![](https://main.qcloudimg.com/raw/9106a51eb41ea9d949ebd47fb8c66c23.png)

3. [제거 확인]을 클릭하여 사용자 그룹에서 사용자 삭제를 완료합니다.

### 사용자 그룹에 전략 추가

1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview )에 로그인하고 왼쪽 네비게이션에서 [사용자 그룹 관리]를 클릭하여 해당 페이지로 들어갑니다. 사용자 그룹 이름을 클릭하여 사용자 그룹 세부 정보 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/750507c3c3bff9e82746366d0b4f9961.png)
2. [연결된 전략]>[전략 연결]을 클릭합니다.
 ![](https://main.qcloudimg.com/raw/752a908e7a8f69b31e3b4257a5d506fc.png)
3. 팝업 창에서 추가할 전략을 선택하고 [확인]을 클릭하여 사용자 그룹에 전략 추가를 완료합니다.
![](https://main.qcloudimg.com/raw/0ae6e0b78f0ed7e6147a0c0bc2dba2eb.png)

### 사용자 그룹에서 전략 삭제

1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview )에 로그인하고 왼쪽 네비게이션에서 [사용자 그룹 관리]를 클릭하여 해당 페이지로 들어갑니다. 사용자 그룹 이름을 클릭하여 사용자 그룹 세부 정보 페이지로 이동합니다.

 ![](https://main.qcloudimg.com/raw/750507c3c3bff9e82746366d0b4f9961.png)

2. 리스트에서 삭제할 전략을 찾은 다음 오른쪽의 [해제]를 클릭합니다. 다음 그림과 같습니다.

 ![](https://main.qcloudimg.com/raw/ac114903444a8b9d5a81e9cd560fe143.png)

3. 전략을 확인한 후 [해제 확인]을 클릭하여 사용자 그룹에서 전략 삭제를 완료합니다.

### 사용자 그룹 삭제

1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview )에 로그인하고 왼쪽 네비게이션에서 [사용자 그룹 관리]를 클릭하여 해당 페이지로 들어갑니다. 삭제할 사용자 그룹을 선택한 다음 [삭제]를 클릭합니다. 다음 그림과 같습니다.

 ![](https://main.qcloudimg.com/raw/a4a3cfa9b48052ba6656bba59d26a9df.png)

2. 사용자 그룹을 확인한 후 [삭제 확인]을 클릭하여 사용자 그룹 삭제를 완료합니다.
