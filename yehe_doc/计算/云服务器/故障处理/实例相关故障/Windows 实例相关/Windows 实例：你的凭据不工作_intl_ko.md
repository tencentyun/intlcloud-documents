## 문제 설명

Windows 운영 체제의 로컬 컴퓨터가 MSTSC 방식과 같은 RDP 프로토콜을 통해 원격 데스크톱으로 Windows CVM에 로그인할 시, 다음과 같은 오류가 발생합니다.
자격 증명이 작동하지 않습니다. `XXX.XXX.XXX.XXX`에 연결할 때 사용한 자격 증명이 작동하지 않습니다. 새 자격 증명을 입력하십시오.
![](https://main.qcloudimg.com/raw/47a299873e3df8f1f160c1594fc56644.png)

## 작업 순서
>? Windows Server 2012 운영 체제를 예시로 사용하며, 자세한 작업 순서는 운영 체제의 버전에 따라 다를 수 있습니다.
> 다음의 작업을 차례대로 실행하여 문제를 해결해 주시기 바랍니다. 각 단계의 작업이 완료될 때마다 Windows CVM에 재연결하여 인증 문제가 해결되었는지 확인한 뒤, 아직 해결되지 않았다면 다음 단계를 진행하시기 바랍니다.
>

### 1단계: 네트워크 액세스 정책 수정
1. [VNC를 사용하여 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32496)합니다.
2. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> 클릭 후, 'Windows PowerShell' 창을 엽니다.
3. 'Windows PowerShell' 창에서 **gpedit.msc**를 입력하고, **Enter**를 눌러 '로컬 그룹 정책 편집기'를 엽니다.
4. 왼쪽 메뉴에서 [컴퓨터 구성]>[Windows 설정]>[보안 설정]>[로컬 정책]>[보안 옵션] 순서대로 디렉터리를 펼칩니다.
5. 아래 이미지와 같이 [보안 옵션]에서 [네트워크 액세스: 로컬 계정에 대한 공유 및 보안 모델]을 찾아서 엽니다.
![](https://main.qcloudimg.com/raw/4ffb48c55d2f4aeedee127d97a4378ee.png)
6. 아래 이미지와 같이 [일반 - 로컬 사용자를 그대로 인증]을 선택한 뒤 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/0f460bef7a7e35e1295149bb1f5f0d03.png)
7. Windows CVM에 재연결하여 인증에 성공했는지 확인합니다.
 - 성공한 경우, 작업을 종료합니다.
 - 실패한 경우, 2단계로 넘어가 자격 증명 위임 수정을 진행합니다.

### 2단계: 자격 증명 위임 수정
1. '로컬 그룹 정책 편집기'의 왼쪽 메뉴에서 [컴퓨터 구성]>[관리 템플릿]>[시스템]>[자격 증명 위임] 순서대로 디렉터리를 펼칩니다.
2. 아래 이미지와 같이 [자격 증명 위임]에서 [서버 인증이 NTLM 전용일 경우 저장된 자격 증명 허용]을 찾아서 엽니다.
![](https://main.qcloudimg.com/raw/7643737fdfa2be299c21f6bc82b0165b.png)
3. 아래 이미지와 같이, 열린 창에서 [활성화]를 선택한 다음 '옵션'의 [표시]에 `TERMSRV/*` 입력 후, [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/6a9af6aa4c3c3b3c4d1b9eba53d202b1.png)
4. [확인]을 클릭합니다.
5. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> 클릭 후, 'Windows PowerShell' 창을 엽니다.
6. 아래 이미지와 같이 'Windows PowerShell' 창에서 **gpupdate /force**를 입력하고, **Enter**를 눌러 정책을 업데이트합니다.
![](https://main.qcloudimg.com/raw/98d0b757e65e3617145c05513ba652dc.png)
7. Windows CVM에 재연결하여 인증에 성공했는지 확인합니다.
 - 성공한 경우, 작업을 종료합니다.
 - 실패한 경우, 3단계로 넘어가 로컬 CVM의 자격 증명 설정을 진행합니다.

### 3단계: 로컬 서버의 자격 증명 설정
1. 아래 이미지와 같이 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > [제어판]>[사용자 계정]을 클릭한 후, [자격 증명 관리자]의 [Windows 자격 증명 관리]를 선택하여 Windows 자격 증명 인터페이스에 들어갑니다.
![](https://main.qcloudimg.com/raw/2726e3d109fdaadd1d90a1f3e692601a.png)
2. Windows 자격 증명에 현재 로그인한 CVM의 자격 증명이 있는지 확인합니다.
 - 자격 증명이 없다면, 다음 단계를 통해 Windows 자격 증명을 추가합니다.
 - 자격 증명이 있다면, 4단계로 넘어가 CVM의 암호 보호 공유 끄기를 진행합니다.
3. 아래 이미지와 같이 [Windows 자격 증명 추가]를 클릭한 뒤, Windows 자격 증명 추가 인터페이스에 진입합니다.
![](https://main.qcloudimg.com/raw/87077862379ea7d9e86d5fdc7e0af1da.png)
4. 현재 로그인한 CVM의 IP 주소 및 사용자 이름과 암호를 입력한 뒤, [확인]을 클릭합니다.
5. Windows CVM에 재연결하여 인증에 성공했는지 확인합니다.
 - 성공한 경우, 작업을 종료합니다.
 - 실패한 경우, 4단계로 넘어가 CVM의 암호 보호 공유 비활성화를 진행합니다.

### 4단계: CVM의 암호 보호 공유 비활성화
1. 아래 이미지와 같이 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > [제어판]>[네트워크 및 인터넷]>[네트워크 및 공유 센터]>[고급 공유 설정 변경]을 클릭하여, 고급 공유 설정 인터페이스로 들어갑니다.
![](https://main.qcloudimg.com/raw/d1cc8fd023642654091d1b152bb67ef1.png)
2. [모든 네트워크] 탭을 펼쳐 [암호로 보호된 공유]에서 [암호 보호 공유 끄기]를 선택한 뒤, [변경 내용 저장]을 클릭합니다.
3. Windows CVM에 재연결하여 인증에 성공했는지 확인합니다.
 - 성공한 경우, 작업을 종료합니다.
 - 실패한 경우, [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 해주시기 바랍니다.


