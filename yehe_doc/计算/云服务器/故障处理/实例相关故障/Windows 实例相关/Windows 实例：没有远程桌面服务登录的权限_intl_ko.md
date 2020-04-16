## 장애 현상

<span id="FaultPhenomenon1"></span>
### 상황 설명(1)
Windows가 원격 데스크탑으로 Windows 인스턴스에 연결할 때 "사용자 계정에 원격 로그인 권한이 없기 때문에 연결이 거부되었습니다."라는 메시지가 뜹니다.

<span id="FaultPhenomenon2"></span>
### 상황 설명(2)
Windows가 원격 데스크탑으로 Windows 인스턴스에 연결할 때 "원격 로그인을 하려면 사용자가 원격 데스크탑 서비스로 로그인을 할 수 있는 권한이 필요합니다. 원격 데스크탑 사용자 그룹의 멤버에게는 이 권한이 기본으로 부여되어 있습니다. 단, 사용자가 소속된 그룹에 이 권한이 없거나 원격 데스크탑 사용자 그룹에서 이 권한을 삭제했을 경우엔 수동으로 부여해야 합니다."라고 메시지가 뜹니다.

## 장애 원인

이 사용자는 원격 데스크탑 연결 방식을 통해 Windows 인스턴스에 로그인이 허용되지 않았습니다.

## 솔루션
- 원격 데스크탑을 통해 Windows 인스턴스에 연결할 때 [상황 설명(1)](#FaultPhenomenon1)의 경우가 발생했을 때 사용자 계정을 Windows 인스턴스가 설정한 원격 데스크탑 서비스를 통한 로그인 허용 리스트에 추가해야 합니다. 자세한 작업 순서는 [원격 로그인 권한 허용 설정](#ConfigurationToAllowAccess)을 참조하십시오.
- 사용자가 원격 데스크탑을 통해 Windows 인스턴스에 연결할 때 [상황 설명(2)](#FaultPhenomenon2)의 경우가 발생했을 때 사용자 계정을 Windows 인스턴스가 설정한 원격 데스크탑 서비스를 통한 로그인 거부 리스트에서 삭제해야 합니다. 자세한 작업 순서는 [원격 로그인의 권한 거부 수정](#ModifyLoginAuthority)을 참조하십시오.

## 프로세스 순서

### VNC 방식을 통해 CVM에 로그인
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 목표 CVM 인스턴스를 찾은 후 [Log In]을 클릭합니다.
3. 팝업된 "Windows 인스턴스 로그인" 창에서 [Alternative login methods(VNC)]을 선택하고 [Log In Now]을 클릭하여 CVM에 로그인합니다.
4. 팝업된 로그인 창에서 좌측 상단의 "원격 명령어 발송"을 선택하고 **Ctrl-Alt-Delete**를 클릭해 시스템 로그인 인터페이스에 접속합니다.

<span id="ConfigurationToAllowAccess"></span>
### 원격 로그인을 허용하는 권한 설정

> 다음 작업은 Windows Server 2016를 예로 듭니다.
>
1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"> 클릭하고 **gpedit.msc**를 입력한 후 **Enter**를 눌러 "로컬 그룹 정책 에디터"를 엽니다.
2. 왼쪽 메뉴에서 [컴퓨터 설정]>[Windows 설정]>[보안 설정]>[로컬 정책]>[사용자 권한 할당]을 선택하고 [원격 데스크탑 서비스를 통한 로그인 허용]을 더블 클릭하여 엽니다.
3. 열린 "원격 데스크탑 서비스를 통한 로그인 허용 속성" 창에서 원격 데스크탑 서비스를 통한 로그인 허용 사용자 리스트에 로그인해야 하는 계정이 존재하는지 점검합니다.
 - 해당 사용자가 원격 데스크탑 서비스를 통한 로그인 허용 리스트에 없으면 [4단계](#step04)를 실행하십시오.
 - 해당 사용자가 원격 데스크탑 서비스를 통한 로그인 허용 리스트에 있으면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2)을 통해 피드백하십시오.
4. <span id="step04">[사용자 또는 그룹 추가]를 클릭하고 “사용자 또는 그룹 선택” 창을 엽니다.</span>
5. 원격 로그인을 해야 하는 계정을 입력하고 [확인]을 클릭합니다.
6. [확인]을 클릭하고 로컬 그룹 정책 에디터를 닫습니다.
7. 인스턴스를 재시작하고 이 계정 원격 데스크탑을 사용해 Windows 인스턴스에 연결을 재시도합니다.

<span id="ModifyLoginAuthority"></span>
### 원격 로그인을 거부하는 권한 수정

> 다음 작업은 Windows Server 2016를 예로 듭니다.
>
1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"> 클릭하고 **gpedit.msc**를 입력한 후 **Enter**를 눌러 "로컬 그룹 정책 에디터"를 엽니다.
2. 왼쪽 메뉴에서 [컴퓨터 설정]>[Windows 설정]>[보안 설정]>[로컬 정책]>[사용자 권한 할당]을 선택하고 더블 클릭으로 [원격 데스크탑 서비스를 통한 로그인 거부]를 엽니다.
3. 열린 "원격 데스크탑 서비스를 통한 로그인 거부 속성" 창에서 원격 데스크탑 서비스를 통한 로그인 거부 사용자 리스트에 로그인해야 하는 계정이 존재하는지 점검합니다.
 - 해당 사용자가 원격 데스크탑 서비스를 통한 로그인 거부 리스트에 있으면 로그인해야 하는 계정을 리스트에서 삭제하고 인스턴스를 재시작하십시오.
 - 사용자가 원격 데스크탑 서비스를 통한 로그인 거부 리스트에 없으면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2)을 통해 피드백하십시오.
