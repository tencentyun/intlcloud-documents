## 절차 1: CCN 유형의 직접 연결 게이트웨이 생성
1. [VPC 콘솔](https://console.cloud.tencent.com/vpc/vpc?rid=1)에 로그인하고 왼쪽 디렉터리에서 [직접 연결 게이트웨이]를 클릭하여 관리 페이지에 들어갑니다.
2. [생성]을 클릭합니다.
3. 팝업창에 게이트웨이 이름을 입력하고 연결 네트워크를 [CCN]으로 선택하며 CCN 인스턴스는 [잠시 연결하지 않음]을 선택한 후 [확인]을 클릭합니다.
 ![1](https://main.qcloudimg.com/raw/1c2c8a3989764a9eafd3c2f82a5eb5f4.png)
 
## 절차 2: 직접 연결 게이트웨이에 IDC IP 주소 범위 추가
1. 직접 연결 게이트웨이의 리스트에서 조절할 인스턴스 “dcg-\***”를 찾아내고 해당 ID를 클릭하여 세부 정보 페이지에 들어갑니다.
2. 탭의 [IDC IP 주소 범위]를 클릭합니다.
3. [추가]를 클릭하고 사용자의 IDC IP 주소 범위를 입력합니다.
![2](https://main.qcloudimg.com/raw/1652cfec77d76f9aadecd551942e1e01.png)

## 절차 3: CCN 인스턴스 생성
자세한 조작 절차는 CCN 문서 [CCN 인스턴스 생성](https://cloud.tencent.com/document/product/877/18752)을 참조하십시오.

## 절차 4: 전용 채널을 생성하고 CCN 직접 연결 게이트웨이에 연결
1. [DC 콘솔](https://console.cloud.tencent.com/dc/dc)에 로그인하고 왼쪽 디렉터리에서 [전용 채널]을 클릭하여 관리 페이지에 들어갑니다.
2. [+ 생성]을 클릭합니다.
3. 팝업창에 페이지 프롬프트에 따라 관련 정보를 입력합니다. 액세스 네트워크를 [CCN]으로 선택하며 직접 연결 게이트웨이를 방금 생성한 CCN 직접 연결 게이트웨이 “dcg-\***”를 선택합니다.
![3](https://main.qcloudimg.com/raw/aa80ea33e85fe2fb4c6ba73683e6ace8.png)

## 절차 5: 네트워크 인스턴스 연결
상호 연결할 네트워크 인스턴스(VPC 와 직접 연결 게이트웨이 포함, 갯수 제한 없음)를 CCN 인스턴스에 로딩하면 CCN 내의 네트워크 인스턴스의 상호 연결을 구현할 수 있습니다. 자세한 조작은 CCN 문서 [네트워크 인스턴스 연결](https://cloud.tencent.com/document/product/877/18747)을 참조하십시오.

