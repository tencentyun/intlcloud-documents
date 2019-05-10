크로스 계정 VPC를 연결하려면 계정 간 VPC에서 신청해야 하며, CCN 소개 계정이 신청을 동의/거절하면 됩니다. 
구체적인 프로세스는 다음 그림과 같습니다.
![0](https://main.qcloudimg.com/raw/60807add361682ba1472ce05ec9095df.png)
## CCN 가입 신청(VPC 계정 작업)
1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고 [클라우드 제품]>[클라우드 컴퓨팅과 네트워크]>[VPC]를 선택하여 VPC 콘솔에 진입합니다. 
2. 왼쪽 목록에서 [VPC]를 클릭하여 리스트에서 CCN에 가입할 VPC를 찾은 뒤, 해당 ID를 클릭하여 세부 정보 페이지에 진입합니다. 
3. [CCN 가입]을 클릭합니다.
 ![1](https://main.qcloudimg.com/raw/51fc0718b592f123049a94620567f533.png)
4. 팝업창에 상대 계정 ID와 CCN ID를 입력한 뒤 [확인]을 클릭하고 신청을 제출합니다.
 ![2](https://main.qcloudimg.com/raw/0045ac1991be1bb335a1966814d22686.png)

## 신청 동의(CCN 계정 작업)
1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고 [클라우드 제품]>[클라우드 컴퓨팅과 네트워크]>[VPC]를 선택하여 VPC 콘솔에 진입합니다. 
2. 왼쪽 목록에서 [CCN]을 클릭하여 리스트에서 동의 예정인 신청 CCN 인스턴스를 찾고 해당 ID를 클릭하여 세부 정보 페이지에 진입합니다. 
3. [인스턴스 연결] 페이지에 동의 예정인 VPC 정보가 나타납니다. [동의]를 클릭하고 확인하면 해당 VPC를 CCN에 추가할 수 있습니다. 
 ![3](https://main.qcloudimg.com/raw/f63b5f1497e372515521e75f3467eb59.png)

## 라우팅 테이블 검사(선택 가능)
신청에 동의하고 연결에 성공한 뒤, 해당 인스턴스와 CCN에 있는 기존 인스턴스가 IP 주소 범위 충돌로 인해 라우팅 효력이 발생하지 않는 상황이 일어나지 않도록 라우팅 테이블을 검사해야 합니다. 
관련 작업은 [라우팅 테이블 검사](https://cloud.tencent.com/document/product/877/18766)를 참조하십시오.

## 지역 간 상호 연결 대역폭 설정(선택 가능)
관련 작업은 [지역 간 상호 연결 대역폭 설정](https://cloud.tencent.com/document/product/877/18759)을 참조하십시오.

