## 문제 설명

Windows 운영 체제의 로컬 컴퓨터가 RDP 프로토콜(MSTSC 등)를 통해 원격 데스크톱 접속으로 Windows CVM에 로그인 시, 다음의 에러가 표시됩니다.
자격 증명은 작동할 수 없습니다, `XXX.XXX.XXX.XXX` 접속에 사용된 자격 증명은 작동하지 않았습니다. 새 자격 증명을 입력하세요.
![](https://main.qcloudimg.com/raw/47a299873e3df8f1f160c1594fc56644.png)

## 처리 순서
>? Windows Server 2012 운영 체제의 Tencent Cloud CVM를 예로 들면, 운영 체제의 버전이 다르기 때문에, 자세한 조작 절차는 조금 다릅니다.
> 다음 절차에 따라 문제를 진단하세요, 각 절차를 다 실행한 후, Windows CVM에 재연결해 문제가 해결되었는지 확인합니다. 문제가 해결되지 않은 경우는 다음 절차에 따라 진행하세요.

### 절차1：네트워크 접근 정책 변경
1. [VNC를 사용하여 Windows 인스턴스에 로그인합니다](https://intl.cloud.tencent.com/document/product/213/32496).
2. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;">클릭 후,“Windows PowerShell”창을 여십시오.
3.“Windows PowerShell”창에서 **gpedit.msc**를 입력한 후 **Enter**를 눌러 "로컬 그룹 정책 편집기"를 여십시오.
4. 왼쪽 메뉴에서【컴퓨터 구성】>【Windows 설정】>【보안 설정】>【로컬 정책】>【보안 옵션】디렉터리를 차례로 클릭해서 여십시오.
5.【보안 옵션】의 【네트워크 액세스: 로컬 계정의 공유와 보안 모델】을 찾아서 여십시오. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/4ffb48c55d2f4aeedee127d97a4378ee.png)
6.【클래식 - 로컬 사용자 인증 시 원래 신분을 바꾸지 않음】을 선택한 후 【확인】을 클릭하세요. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/0f460bef7a7e35e1295149bb1f5f0d03.png)
7. Windows CVM에 재연결하여 연결에 성공했는지 확인하세요.
 - 네, 작업이 종료됐습니다.
 - 아니요, 절차2 (자격 증명 위임 변경)을 실행하세요.

### 절차2 : 자격 증명 위임 변경
1. “로컬 그룹 정책 편집기”의 왼쪽 메뉴에서,【컴퓨터 구성】>【관리 템플릿】>【시스템】>【자격 증명 위임】 디렉터리를 차례로 클릭해서 여십시오.
2. 【자격 증명 위임】의 【NTLM 서버만의 인증으로 저장된 자격 증명 위임을 허가하기】를 찾아서 여십시오. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/7643737fdfa2be299c21f6bc82b0165b.png)
3. 열린 창에서 【활성화됨】을 선택하고 "옵션" 의 【표시】에 `TERMSRV/*`를 입력하고 【확인】을 클릭하세요. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/6a9af6aa4c3c3b3c4d1b9eba53d202b1.png)
4. 【확인】을 클릭하세요.
5. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;">클릭 후,“Windows PowerShell”창을 여십시오.
6. “Windows PowerShell”창에서 **gpupdate /force**를 입력하고 **Enter**키를 눌러 그룹 정책을 새로 고칩니다. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/98d0b757e65e3617145c05513ba652dc.png)
7. Windows CVM에 재연결하여 연결에 성공했는지 확인하세요.
 -네, 작업 종료됐습니다.
 -아니요, 절차3 (로컬 CVM의 자격 증명 설정)을 실행하세요.

### 절차3 : 로컬 CVM의 자격 증명 설정
1. 운영 체제 인터페이스에서,<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > 【제어판】>【사용자 계정】을 클릭해,【자격 증명 관리자】의【Windows 자격 증명 관리】를 선택하여, Windows 자격 증명 인터페이스에 들어갑니다. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/2726e3d109fdaadd1d90a1f3e692601a.png)
2. Windows 자격 증명 아래에 현재 로그인하고 있는 CVM의 자격 증명가 있는지 확인하세요.
 - 없으면 다음 단계로 넘어가서 Windows 자격 증명을 추가하세요.
 - 있으면 절차4 (CVM 비밀번호 보호 공유 비활성화)를 실행하세요.
3. 【Windows 자격 증명 추가】를 클릭하고, Windows 자격 증명 추가 인터페이스에 들어갑니다. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/87077862379ea7d9e86d5fdc7e0af1da.png)
4. 현재 로그인하고 있는 CVM의 IP 주소, 사용자 이름과 비밀번호를 입력하고, 【확인】을 클릭하세요.
>?
> - CVM의 IP 주소는 CVM 공인 IP 주소입니다. 상세한 내용은 [공인 IP 주소 취득](https://intl.cloud.tencent.com/document/product/213/17940)을 참조 바랍니다.
> - Windows 인스턴스의 기본 사용자 이름은 `Administrator`이며 비밀번호는 인스턴스 생성 시 설정됩니다. 로그인 비밀번호를 잊어버린 경우 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.
>
5. Windows CVM에 재연결하여 연결에 성공했는지 확인하세요.
 - 네, 작업 종료됐습니다.
 - 아니요, 절차4 (CVM 비밀번호 보호 공유 비활성화)를 실행하세요.

### 절차4：CVM 비밀번호 보호 공유 비활성화
1. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > 【제어판】>【네트워크 및 인터넷】>【네트워크 및 공유 센터】>【고급 공유 설정 변경】을 클릭하고 고급 공유 설정 변경 인터페이스에 들어갑니다. 아래 그림과 같습니다.
![](https://main.qcloudimg.com/raw/d1cc8fd023642654091d1b152bb67ef1.png)
2.【모든 네트워크】탭을 펼치고, 【비밀번호 보호 공유】에서 【비밀번호 보호 공유 비활성화】를 선택하고, 【변경 저장】을 클릭하세요.
3. Windows CVM에 재연결하여 연결에 성공했는지 확인하세요.
 - 네, 작업 종료됐습니다.
 - 아니요, [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6andlevel2_id=7andsource=0anddata_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVMandstep=1)하고 피드백을 요청하십시오.


