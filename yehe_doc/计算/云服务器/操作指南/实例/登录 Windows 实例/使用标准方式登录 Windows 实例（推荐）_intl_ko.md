## 작업 시나리오
본문은 표준 로그인 방법(WebRDP)을 사용하여 Windows 인스턴스에 로그인하는 방법을 설명합니다. 

<dx-alert infotype="explain" title="">
이 방법은 로컬 시스템 운영 체제를 구분하지 않으며 콘솔을 통한 Windows 인스턴스 직접 로그인을 지원합니다.
</dx-alert>



## 전제 조건[](id:Prerequisites)
- Windows 인스턴스 원격 로그인을 위해 필요한 인스턴스의 관리자 계정 및 비밀번호를 획득한 상태여야 합니다.
 - 로그인 비밀번호가 설정되어 있는 경우 해당 비밀번호를 사용하여 로그인하시기 바랍니다. 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.
 - 인스턴스 생성 시 시스템에서 비밀번호 랜덤 생성을 선택했다면 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 초기 비밀번호를 받으시기 바랍니다.
- CVM 인스턴스에서 공용 IP를 구매하였고, WebRDP 프록시 IP가 소스인 원격 로그인 포트(기본값: 3389)가 인스턴스와 연결된 보안 그룹에서 인터넷 개방되어있어야 합니다.
 - 빠른 구성을 통해 CVM을 구매하시면 기본적으로 이미 활성화되어 있습니다.
 - 사용자 정의 설정을 통해 CVM을 구매한 경우 [RDP를 통한 Windows CVM 원격 연결 허용](https://intl.cloud.tencent.com/document/product/213/32369)을 참고하여 수동으로 인터넷 개방하십시오.
- 인스턴스의 공용 네트워크 대역폭이 5Mbit/s 이상인지 확인하십시오. 그렇지 않다면 원격 데스크톱에 랙이 발생됩니다. 네트워크 대역폭 조정은 [네트워크 구성 변경](https://intl.cloud.tencent.com/document/product/213/15517)을 참고하십시오.


## 작업 단계

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작업합니다.
<dx-tabs>
::: 리스트 뷰
아래 이미지와 같이 로그인하려는 Windows CVM 우측의 **로그인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: 탭 뷰
2. 아래 이미지와 같이 로그인하려는 Windows CVM 탭을 선택하고 **로그인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>
3. ‘표준 로그인 | Windows 인스턴스’ 창에서 실제 상황에 따라 로그인 정보를 입력합니다.
 - **포트**: 기본값은 3389이며 필요에 따라 입력하십시오.
 - **사용자 이름**: Windows 인스턴스 사용자 이름은 기본적으로 `Administrator`이며 필요에 따라 입력하십시오.
 - **비밀번호**: [전제 조건](#Prerequisites) 단계에서 얻은 로그인 비밀번호를 입력합니다.
5. **로그인**을 클릭하여 Windows 인스턴스에 로그인합니다.
보안 주체는 운영 체제가 Windows Server 2016 데이터 센터 버전의 64비트 영어 버전인 CVM에 로그인되어 있다고 가정합니다. 로그인에 성공하면 아래 이미지와 같이 인터페이스가 표시됩니다.
![](https://main.qcloudimg.com/raw/60abc6a9f51ae33ea95aa11edc53e009.jpg)


## 관련 문서
- [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)
- [네트워크 구성 변경](https://intl.cloud.tencent.com/document/product/213/15517)
