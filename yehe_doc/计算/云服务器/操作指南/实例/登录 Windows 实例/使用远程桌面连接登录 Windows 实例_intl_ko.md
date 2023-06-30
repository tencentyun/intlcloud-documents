## 작업 시나리오
본 문서는 Windows 시스템의 로컬 컴퓨터에서 원격 데스크톱을 통해 Windows 인스턴스에 로그인하는 방법을 소개합니다.

## 지원 운영 체제

Windows

## 전제 조건[](id:Preconditions)

- Windows 인스턴스 원격 로그인을 위해 필요한 인스턴스의 관리자 계정 및 비밀번호를 획득한 상태여야 합니다.
 - 시스템 기본 설정 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)에 접속하여 획득 바랍니다.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.
- CVM 인스턴스가 이미 공용 IP를 구매했고, 해당 인스턴스가 CVM 인스턴스의 3389번 포트를 활성화한 상태여야 합니다(빠른 구성을 통해 구매한 CVM 인스턴스는 기본으로 활성화되어 있습니다).

## 작업 순서


<dx-alert infotype="explain" title="">
다음 작업 순서는 Windows 7 운영 체제를 예로 듭니다.
</dx-alert>

1. 로컬 Windows 컴퓨터에서 <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: -5px 0px;width: 35px;">을(를) 클릭하고 **프로그램 및 파일 검색**에서 **mstsc**를 입력한 후 **Enter**를 눌러 원격 데스크톱 연결 창을 엽니다. 아래 이미지 참고:
![](https://main.qcloudimg.com/raw/d8a4b0f70f876f6c0edc6e995a02c37d.png)
2. ‘컴퓨터’에서 Windows 서버의 공용 IP를 입력하고 **연결**을 클릭합니다. [공용 IP 주소 가져오기](https://intl.cloud.tencent.com/document/product/213/17940)를 참고하여 서버의 공용 IP를 가져옵니다.
3. 팝업된 ‘Windows 보안’ 창에서 인스턴스의 관리자 계정과 비밀번호를 입력합니다. 아래 이미지 참고:
<dx-alert infotype="explain" title="">
 - ‘이 원격 연결을 신뢰하십니까?’라는 창이 팝업되면 ‘이 컴퓨터로의 연결을 다시 묻지 않음’을 선택하고 **연결**을 클릭합니다.
 - Windows CVM 인스턴스의 기본 관리자 계정은 'Administrator'이며, 비밀번호는 [전제 조건](#Preconditions)을 참고하여 가져옵니다.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/5d3d89e3ec4616a367b80ba377a3f541.png"/>
4. **확인**을 클릭하면 바로 Windows 인스턴스에 로그인할 수 있습니다.

