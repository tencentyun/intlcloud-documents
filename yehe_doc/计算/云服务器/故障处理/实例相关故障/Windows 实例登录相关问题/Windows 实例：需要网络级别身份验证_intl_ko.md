본 문서는 Windows 인스턴스에 원격 연결할 때 "네트워크 수준 인증이 필요합니다" 등의 알림이 표시되는 경우에 대한 처리 방법을 소개합니다.

## 장애 현상
Windows 시스템 자체의 원격 데스크톱 연결을 사용하면, 가끔 원격 컴퓨터에 연결할 수 없는 문제가 나타나며 "네트워크 수준 인증이 필요합니다"와 같은 알림이 표시됩니다.
![](https://main.qcloudimg.com/raw/409b3259fa13220e8cde0790aa87488b.jpg)

## 장애 처리

>? 다음 작업은 Windows Server 2016을 예로 듭니다.
>

### VNC 방식을 통해 CVM에 로그인
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 타깃 CVM 인스턴스를 찾아 [Log In]을 클릭합니다. 아래 이미지 참조
![CVM 리스트 페이지](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. 팝업된 "Windows 인스턴스 로그인" 창에서 [Alternative login methods(VNC)]]을 선택하고 [Log In Now]을 클릭하여 CVM에 로그인합니다.
4. 팝업된 로그인 창 왼쪽 상단의 "원격 명령어 발송"을 선택하고 **Ctrl-Alt-Delete**를 클릭하여 시스템 로그인 인터페이스에 접속합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### 레지스트리 수정

1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>를 클릭하고 **regedit**를 입력한 후 **Enter**를 눌러 레지스트리 편집기를 엽니다.
2. 왼쪽 메뉴에서 차례대로 [컴퓨터]>[HKEY_LOCAL_MACHINE]>[SYSTEM]>[CurrentControlSet]>[Control]>[Lsa] 디렉터리를 열고 오른쪽 창에서 [Security Packages]를 찾습니다. 아래 이미지 참조
![Security Packages](https://main.qcloudimg.com/raw/db037b5131ff44af72b560fbac4931e1.png)
3. [Security Packages]를 더블 클릭하여 [다중 문자열 편집] 창을 엽니다.
4. "다중 문자열 편집" 창에서 [tspkg] 문자를 추가하고 [확인]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/cca2bce345b48569d45fd391ee65bc51.png)
5. 왼쪽 메뉴에서 차례대로 [컴퓨터]>[HKEY_LOCAL_MACHINE]>[SYSTEM]>[CurrentControlSet]>[Control]>[SecurityProviders] 디렉터리를 열고 우측 창에서 [SecurityProviders]를 찾습니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/14e84c77ae1d1d3c5bc2ab091543a957.png)
6. [SecurityProviders]를 더블 클릭하여 [문자열 편집] 창을 엽니다.
7. "문자열 편집" 창의 [값 데이터] 말미에 `, credssp.dll`을 추가하고 [확인]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/34b98c226c359b070e2f03c2ff1c6e42.png)
8. 레지스트리 편집기를 닫고 인스턴스를 재시작하면 바로 원격 로그인할 수 있습니다.

