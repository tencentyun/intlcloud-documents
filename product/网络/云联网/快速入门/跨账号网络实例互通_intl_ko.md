본문은 CCN을 통해 CCN으로 계정 간 VPC를 연결하는 기능을 설명합니다.

## 전제 조건
- 모든 계정(본문은 계정 A와 계정 B를 예로 함)은 CCN 내부 테스트 자격을 지니고 있습니다.
- 상호 연결해야 할 VPC가 이미 생성되었습니다.
- 상호 연결해야 할 VPC별 서브넷 IP 주소 범위, IDC IP 주소 범위는 충돌되지 않습니다.


## 절차 1: 계정 A CCN 인스턴스 생성
1. 계정 A를 사용하여 [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고 [클라우드 제품]>[클라우드 컴퓨팅과 네트워크]>[VPC]를 선택하여 VPC 콘솔에 진입합니다.
2. 왼쪽 목록에서 [CCN]을 클릭하여 CCN 관리 페이지에 진입합니다.
3. [생성]을 클릭합니다. 
 ![](https://main.qcloudimg.com/raw/4189c3d3af70c389a81159a12198a21c.png)
4. 팝업창에 CCN 인스턴스 이름, 비고를 입력합니다.
![](https://main.qcloudimg.com/raw/8609a7bff509a7630938714730d472be.png)
5. 네트워크 인스턴스 1개를 연결합니다(또는 CCN 생성 후 다시 연결 가능).
6. [확인]을 클릭하여 CCN 인스턴스를 생성합니다.

## 절차 2: VPC 소속 계정 B CCN 연결 신청
1. 계정 B를 사용하여 [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고 [클라우드 제품]>[클라우드 컴퓨팅과 네트워크]>[VPC]를 선택하여 VPC 콘솔에 진입합니다.
2. VPC 리스트에서 CCN에 연결해야 할 VPC의 ID를 클릭하여 세부 정보 페이지에 진입합니다.
3. [바로 연결]을 클릭합니다.
![](https://main.qcloudimg.com/raw/0ed0b142be6116cf4cf9fa4aff81c611.png)
4. 팝업창에서 [기타 계정]을 선택하고 계정 A의 계정 ID, CCN 인스턴스 ID를 입력합니다.
![](https://i.imgur.com/SYNWnBZ.png)
5. [확인]을 클릭하면 CCN 소속 계정에 연결 신청이 발송됩니다.

## 절차 3: CCN 계정 A가 계정 B 연결 신청 동의
1. 계정 A를 사용하여 [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고 [클라우드 제품]>[클라우드 컴퓨팅과 네트워크]>[VPC]를 선택하여 VPC 콘솔에 진입합니다. 
2. 왼쪽 목록에서 [CCN]을 클릭하여 리스트에서 동의 예정인 신청 CCN 인스턴스를 찾고 해당 ID를 클릭하여 세부 정보 페이지에 진입합니다. 
3. [인스턴스 연결] 페이지에 동의 예정인 VPC 정보가 나타납니다. [동의]를 클릭하고 확인하면 해당 VPC를 CCN에 추가할 수 있습니다. 
 ![3](https://main.qcloudimg.com/raw/f63b5f1497e372515521e75f3467eb59.png)

## 절차 4: 라우팅 테이블 검사
연결한 네트워크 인스턴스 IP 주소 범위에 충돌이 발생한 경우, 무효 라우팅을 생성하게 됩니다. 다음과 같이 하십시오.

1. CCN 리스트에서 조회할 라우팅의 CCN ID를 클릭하여 세부 정보 페이지에 진입합니다.
2. [라우팅 테이블]을 클릭하여 해당 CCN 라우팅 테이블을 조회합니다.
3. 무효 상태의 라우팅 전략이 존재하는지 검사합니다.
 ![](https://main.qcloudimg.com/raw/ae2fb3be44f2f56ab64a257f505b2b4e.png)
4. 라우팅 충돌에 대한 세부 정보는 [라우팅 제한](https://cloud.tencent.com/document/product/877/18679#.E8.B7.AF.E7.94.B1.E9.99.90.E5.88.B6)을 참조하십시오. 충돌된 라우팅을 사용해야 할 경우 [라우팅 활성화](https://cloud.tencent.com/document/product/877/18750)를 참조하십시오.

## 절차 5: 크로스 지역 대역폭 한도 설정(선택 가능)

1. CCN 리스트에서 설정해야 할 대역폭의 CCN ID를 클릭하여 세부 정보 페이지에 진입합니다.
2. [모니터링] 탭을 클릭하여 해당 CCN의 모니터링 정보를 확인합니다.
3. 아웃바운드 대역폭 한도를 설정할 지역을 선택합니다.
4. 각 지역의 아웃바운드 대역폭 한도를 설정합니다(기본 1G).
 ![](https://main.qcloudimg.com/raw/e92d2cef0bdf5366054f7fd71415f24a.png)

>?CCN 인스턴스 간 통신은 비용이 발생될 수 있습니다. 세부 정보는 [요금제 개요](https://cloud.tencent.com/document/product/877/18676)를 참조하십시오.

