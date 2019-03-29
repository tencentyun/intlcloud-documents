## 개요
서브 사용자는 루트 계정에 의해 생성한 개체로 명확한 신분 ID 및 ID 자격 증명을 가지고 있으며 콘솔에 로그인할 수 있고 독립적으로 콘솔을 설정할 수 있습니다. 또한 API 접근 권한도 가지고 있습니다.

## 작업 가이드

### 서브 사용자 생성
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 [사용자 생성] > [서브 사용자]를 클릭합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/ea2c83f453f040868d74cebde326ece2.png)

2. 사용자 정보를 입력합니다. 이 단계에서 서브 사용자를 일괄 생성하거나 접근 유형 및 콘솔 비밀번호를 설정할 수 있습니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/4af2c64e456a66c71aeba544237c5aaa.png)

3. 권한을 설정합니다. 다음과 같은 세 가지 방법으로 생성된 서브 사용자에게 권한을 설정할 수 있습니다. 전략이 연결된 후에 서브 사용자가 전략에서 설명한 대로 권한을 획득합니다.
 - 그룹에 서브 사용자를 할당하는 것은 작업 기능별로 사용자 권한을 관리하는 데 가장 좋은 방법입니다. 그룹에 연결되면 해당 권한을 획득할 수 있기 때문에 기존 또는 새로 생성된 사용자 그룹에 서브 사용자를 추가하면 서브 사용자는 그룹에 따라 첨부된 전략과 연결할 수 있습니다.
![](https://main.qcloudimg.com/raw/42203e02f8db3e3f380d7b41b133885b.png)
 - 기존 사용자의 권한을 복사하면 서브 사용자와 해당 전략을 연결할 수 있습니다. [기존 사용자 권한 복사]를 클릭하고 복사해야 하는 사용자를 선택하면 서브 사용자는 복사된 사용자에게 첨부된 전략과 연결될 수 있습니다.
![](https://main.qcloudimg.com/raw/e144d026b601ef06f0b678905ec9dbaa.png)
 - 전략 리스트에서 권한을 부여합니다. [전략 리스트에서 권한 부여]를 클릭하고 연결할 전략을 선택합니다.
 ![](https://main.qcloudimg.com/raw/ec45ef82b8f31d6707d8873cc5485155.png)
4. 이메일로 전체 정보를 이메일 주소에 보내거나 excel 파일로 일부 정보를 로컬에 저장할 수 있습니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/5538d2b037b8d0299c6f96185e85f828.png)

5. [완료]를 클릭하여 서브 사용자 생성을 완료합니다.

### 서브 사용자에게 전략 연결 권한 부여

#### 직접 연결
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 전략 연결 권한을 부여해야 하는 서브 사용자를 찾은 다음 조작 열에서 [권한 부여]를 클릭합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/def984e04ba312d066f5ced32996cb99.png)
2. 권한을 부여할 전략을 선택하고 [확인]을 클릭하여 서브 사용자에게 전략 연결에 대한 권한 부여를 완료합니다.
![](https://main.qcloudimg.com/raw/0ed5b135fe498eb017552a9014b29893.png)

#### 그룹에 따라 연결
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 전략 연결 권한을 부여해야 하는 서브 사용자를 찾은 다음 조작 열에서 [기타]>[그룹에 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/ccd8ed71ab1e2414adccc07d699bbe54.png)
2. 서브 사용자를 추가할 사용자 그룹을 선택하고 확인을 클릭하여 그룹에 추가하여 그룹에 따른 전략 연결을 완료합니다.


### 서브 사용자의 연결된 전략 삭제

#### 직접 해제
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 연결된 전략을 삭제해야 하는 서브 사용자를 찾은 다음 서브 사용자 이름을 클릭하여 서브 사용자 세부 정보 페이지로 이동합니다
![](https://main.qcloudimg.com/raw/7acf69885801de4d444955f3315fe4cf.png)
2. [연결된 전략]을 클릭하고 리스트에서 삭제할 전략을 찾은 다음 오른쪽의 [해제]를 클릭합니다.
![](https://main.qcloudimg.com/raw/8f39787d4168aca9cb49856f0b2579be.png)
3. [해제 확인]을 클릭하여 서브 사용자의 연결 전략 삭제를 완료합니다.

#### 그룹에서 제거
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 연결된 전략을 삭제해야 하는 서브 사용자를 찾은 다음 서브 사용자 이름을 클릭하여 서브 사용자 세부 정보 페이지로 이동합니다
![](https://main.qcloudimg.com/raw/7acf69885801de4d444955f3315fe4cf.png)
2. [연결한 전략]을 클릭하고 리스트에서 삭제할 그룹에 따라 연결된 전략을 찾은 다음 오른쪽의 [해제]를 클릭합니다.
![](https://main.qcloudimg.com/raw/bf4de0304257aab985745b7e456c40c7.png)
3. [해제 확인]을 클릭하여 서브 사용자를 사용자 그룹에서 제거하고 그룹과 연결된 전략이 해제됩니다.

### 서브 사용자를 위한 메시지 구독
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 메시지 구독하려는 서브 사용자를 찾은 다음 조작 열에서 [기타]>[메시지 구독]을 클릭합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/110fe3ebd376969a1b18f81f287ee88b.png)
2. 구독할 메시지 유형을 선택하고 [확인]을 클릭하여 서브 사용자를 위한 메시지 구독 설정을 완료합니다.
![](https://main.qcloudimg.com/raw/1eac93c0efd19c26e0ca1e3a1e637b75.png)

### 드로어로 서브 사용자 정보 확인
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 확인할 서브 사용자를 찾은 다음 왼쪽의 세부 정보 아이콘을 클릭합니다. 다음 그림과 같습니다.![](https://main.qcloudimg.com/raw/4413929aa2d843861a5512da4a27d437.png)
>여기서 서브 사용자의 메시지 구독, 비고, 마지막 로그인 시간, 마지막 로그인 방법 및 MFA 상태 등 정보를 확인할 수 있습니다.

### 검색란을 통해 서브 사용자 찾기
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 오른쪽 상단의 검색란에 키워드를 입력하고 검색 아이콘을 클릭하여 관련 서브 사용자를 검색할 수 있습니다. 
![](https://main.qcloudimg.com/raw/21545d7d3da888f878dda5d82c75a8e9.png)
>검색란은 다중 키워드 검색을 지원합니다(키워드 사이에 공백을 둠). 사용자 이름, ID, 휴대폰, 이메일 주소 및 비고 등 키워드를 통해 관련 서브 사용자를 검색할 수 있습니다.



### 서브 사용자 삭제

#### 단일 서브 사용자 삭제
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 삭제할 서브 사용자를 찾은 다음 조작 열에서 [기타]>[삭제]를 클릭합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/fc3a8a73f4ef0f53f8ad3a2a7b8d4cd2.png)

2. [삭제 확인]을 클릭하여 서브 사용자 삭제를 완료합니다.


#### 여러 서브 사용자 삭제
1. Tencent Cloud 콘솔에 로그인하고 [사용자 관리](https://console.cloud.tencent.com/cam)로 이동하여 사용자 리스트에서 삭제할 서브 사용자를 선택하고 왼쪽 상단의 [삭제]를 클릭합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/983a54ffdf83dcd0d4b9da6a7f746f27.png)

2. [삭제 확인]을 클릭하여 서브 사용자 삭제를 완료합니다.

