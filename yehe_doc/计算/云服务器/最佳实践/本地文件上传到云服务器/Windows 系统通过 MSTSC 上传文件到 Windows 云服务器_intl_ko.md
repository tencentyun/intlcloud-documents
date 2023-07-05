## 작업 시나리오

Windows CVM에 파일 업로드 시 일반적으로 MSTSC 원격 데스크톱 연결(Microsoft Terminal Services Client) 방식을 사용합니다. 본 문서에서는 로컬 Windows 컴퓨터에서 원격 데스크톱 연결을 통해 Windows CVM에 파일을 업로드하는 방법을 안내합니다.

## 전제 조건

Windows CVM이 공용 네트워크에 액세스할 수 있어야 합니다.

## 작업 단계
<dx-alert infotype="explain" title="">
다음의 작업 순서는 Windows 7 운영 체제를 사용하는 로컬 컴퓨터를 예로 들어 설명합니다. 운영 체제에 따라 세부 작업 순서에 약간의 차이가 있습니다.
</dx-alert>


### 공용 IP 획득
[CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 후, 인스턴스 리스트 페이지에서 파일을 업로드할 CVM의 공용 IP를 다음 이미지와 같이 기록합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/43f0fa221ab8a5483f1aa7a2698e4cf1.png)

### 파일 업로드
1. 로컬 컴퓨터에서 단축 키 **Windows + R**을 사용해 ‘실행’ 창을 엽니다.
2. 팝업된 ‘실행’ 창에 **mstsc**를 입력한 후 **확인**을 클릭하여 ‘원격 데스크톱 연결’ 창을 엽니다.
3. ‘원격 데스크톱 연결’ 대화 상자에 CVM 공용 IP 주소를 입력한 후 **옵션**을 클릭합니다.
4. **일반** 탭에 CVM 공용 IP 주소 및 사용자 이름 Administrator를 입력합니다.
5. **로컬 리소스** 탭을 선택한 후 **세부 정보**를 클릭합니다.
6. 아래 이미지와 같이 ‘로컬 디바이스 및 리소스’ 팝업 창에서 **드라이버**를 선택한 후 Windows CVM에 업로드할 파일이 있는 로컬 디스크를 선택한 다음 **확인**을 클릭합니다.
7. 로컬 설정을 마친 후, **연결**을 클릭하여 ‘Windows 보안’ 팝업 창에 인스턴스의 로그인 비밀번호을 입력하여 Windows CVM에 원격 로그인합니다.
8. Windows CVM에서 <img src="https://main.qcloudimg.com/raw/ef8fb18be7880d8b48ce402b973f22dc.png" style="margin:-3px 0px">을(를) 선택합니다. 열린 창에서 **내 PC**를 클릭하면 CVM에 마운트된 로컬 디스크를 확인할 수 있습니다.
9. 더블 클릭하여 마운트된 로컬 디스크를 열고, 복사할 로컬 파일을 Windows CVM의 기타 디스크에 복사해 넣으면 파일 업로드 작업이 완료됩니다.
예: 로컬 디스크(F)의 A 파일을 Windows CVM의 C: 드라이브에 복사합니다.

### 파일 다운로드
Windows CVM의 파일을 로컬 컴퓨터에 다운로드할 경우, 파일 업로드 작업을 참고할 수 있습니다. 다운로드할 파일을 Windows CVM에서 마운트된 로컬 디스크에 복사해 파일 다운로드 작업을 완료합니다.

