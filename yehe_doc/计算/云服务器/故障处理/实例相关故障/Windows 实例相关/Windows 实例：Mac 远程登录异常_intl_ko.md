본 문서는 사용자의 Mac이 Microsoft Remote Desktop을 통해 Windows에 원격 로그인 시 흔히 볼 수 있는 장애 현상 및 솔루션을 소개합니다.
## 장애 현상

- Mac이 Microsoft Remote Desktop을 통해 Windows에 원격 로그인 시, "The certificate couldn't be verified back to a root certificate."라는 알림이 뜹니다.
<img src="https://main.qcloudimg.com/raw/070b9c862d6928988768b266461bc816.png" data-nonescope="true" />
- Mac 원격 데스크탑 연결(Remote Desktop Connection) 시, "원격 데스크탑에서 귀하가 연결하고자 하는 컴퓨터를 인증할 수 없습니다"라고 알림이 뜹니다.
<img src="https://main.qcloudimg.com/raw/32f0444a47b2e4c90f6657ec9686afcb.png" height="180" width="550" />

## 장애 처리
> 다음 작업은 Windows Server 2016을 예로 듭니다.
>

### VNC 방식을 통해 CVM에 로그인

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. "Instances" 페이지에서 목표 CVM 인스턴스를 찾고 [Log In]을 클릭합니다. 
3. 팝업된 "Windows 인스턴스 로그인" 창에서 [Alternative login methods(VNC)]을 선택하고 [Log In Now]을 클릭하여 CVM에 로그인합니다.
4. 팝업된 로그인 창 왼쪽 상단의 "원격 명령어 발송"을 선택하고 **Ctrl-Alt-Delete**를 클릭하여 시스템 로그인 인터페이스에 접속합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### 인스턴스 로컬 그룹 정책 수정

1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">를 클릭하고 **gpedit.msc**를 입력하고 **Enter**를 눌러 “로컬 그룹 정책 에디터”를 엽니다.
> 단축키 "Win+R"를 사용하여 실행 인터페이스를 열 수도 있습니다.
>
2. 왼쪽 메뉴에서 [컴퓨터 설정]>[템플릿 관리]>[Windows 컴포넌트]>[원격 데스크탑 서비스]>[원격 데스크탑 세션 호스트]>[보안]을 선택하고 [원격(RDP) 연결에 지정된 보안 레이어 사용 요청]을 더블클릭합니다. 

3. 열린 "원격(RDP)연결에 지정된 보안 레이어 사용 요청" 창에서 [활성화]를 선택하고 [보안 레이어]를 [RDP]로 설정합니다. 

4. [확인]을 클릭하여 설정을 완료합니다.
5. 인스턴스를 재시작하여 성공적으로 연결되었는지 다시 시도합니다. 여전히 연결 실패일 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2)을 통해 피드백해 주시기 바랍니다.
