## 작업 시나리오

본문에서는 PuTTY 소프트웨어를 사례로 Windows 시스템 로컬 컴퓨터에서 원격 로그인 소프트웨어를 사용한 Linux 인스턴스 로그인 방법을 소개합니다.


## 로컬 운영 체제에 적용

Windows

## 인증 방식

**비밀번호**또는**보안키**

## 전제 조건
- 인스턴스에 로그인할 수 있는 관리자 계정 및 비밀번호(또는 보안키) 보유
 - 시스템 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)로 접속하여 획득 바랍니다.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.
- CVM 인스턴스가 이미 공인 IP를 구매 및 획득하였고, 해당 인스턴스가 이미 CVM 인스턴스의 22번 포트를 활성화함(빠른 구성을 통해 구매한 CVM 인스턴스는 기본적으로 활성화 상태임)


## 작업 순서

### 비밀번호를 사용하여 로그인하기

1. Windows 원격 로그인 소프트웨어(즉, PuTTY)를 다운로드합니다.
PuTTY 획득 방법: [여기 클릭](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
2. [putty.exe]를 더블 클릭하여 PuTTY 클라이언트를 실행합니다.
3. PuTTY Configuration 창에 다음 내용을 입력합니다. (다음 이미지 참고)
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
매개변수 예시 설명:
 - Host Name(or IP address): CVM의 공인 IP([CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 후 리스트 페이지 및 상세 정보 페이지에서 공인 IP 획득 가능)
 - Port: CVM 포트 반드시 22로 설정
 - Connect type: “SSH” 선택
 - Saved Sessions: 세션명 기입, 예: test
 “Host Name” 설정 후 다시 “Saved Sessions”을 설정 및 저장하면, 이후 사용 시 “Saved Session”에 저장한 세션명을 더블 클릭해 서버에 바로 로그인할 수 있습니다.
4. [Open]을 클릭해 “PuTTY” 실행 인터페이스로 들어가면 “login as:”가 표시됩니다.
5. “login as” 에 사용자 이름을 입력한 후 **Enter**키를 누릅니다.
6. “Password”에 비밀번호를 입력한 후 **Enter**키를 누릅니다.
비밀번호 입력 시 화면에는 표시되지 않습니다. (다음 이미지 참고)
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
로그인되면 명령 프롬프트 왼쪽에 현재 로그인한 CVM 정보가 표시됩니다.

### 보안키를 사용하여 로그인하기

1. Windows 원격 로그인 소프트웨어(즉, PuTTy)를 다운로드합니다.
putty.exe와 puttygen.exe 소프트웨어를 각각 다운로드 합니다. PuTTy 획득 방법: [여기 클릭](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
2. [puttygen.exe]를 더블 클릭하여 PuTTy Key 클라이언트를 실행합니다.
3. 다음 이미지와 같이 [Load]를 클릭하여 미리 다운로드한 프라이빗 키 저장 경로를 선택 및 오픈합니다.
예: 파일명이 david인 프라이빗 키를 선택 및 오픈하는 경우
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. <span id="Step4"></span>다음 이미지와 같이 PuTTY Key Generator 창에 보안키 이름을 입력하고 프라이빗 키 암호화에 사용할 PuTTY 비밀번호를 설정합니다(선택 사항). 설정 완료 후 [Save private key]를 클릭합니다.
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. 다음 이미지와 같이 팝업된 창에서 보안키를 저장한 경로를 선택하고 파일명 란에 “보안키 이름.ppk”를 입력한 후 [저장]버튼을 클릭합니다. 예: david 프라이빗 키 파일을 david.ppk 보안키 파일로 다른 이름으로 저장하는 경우
![](https://main.qcloudimg.com/raw/44df54ca77069356a26c51e2a4db7643.png)
6. [putty.exe]를 더블 클릭하여 PuTTY 클라이언트를 실행합니다.
7. 왼쪽 메뉴에서 [Connection] > [SSH] > [Auth]를 선택하여 Auth 설정 인터페이스로 들어갑니다.
8. 다음 이미지와 같이 [Browse]를 클릭하여 보안키 저장 경로를 선택 및 오픈합니다.
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
8. 다음 이미지와 같이 Session 설정 인터페이스로 전환한 후 서버 IP와 포트, 연결 유형을 설정합니다.
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - Host Name(IP address): CVM의 공인 IP([CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 후 리스트 페이지 및 상세페이지에서 공인 IP 획득 가능)
 - Port: CVM 포트 반드시 22로 기입
 - Connect type: “SSH” 선택
 - Saved Sessions: 세션명 기입, 예: test
 “Host Name” 설정 후 다시 “Saved Sessions”을 설정 및 저장하면, 이후 사용 시 “Saved Session”에 저장한 세션 이름을 더블 클릭해 서버에 바로 로그인할 수 있습니다.
9. [Open]을 클릭해 “PuTTY” 실행 인터페이스로 들어가면 “login as:”가 표시됩니다.
10. “login as” 에 사용자 이름을 입력한 후 **Enter**키를 누릅니다.
11. [순서 4](#Step4)에 따라 프라이빗 키의 비밀번호 암호화 설정을 완료한 경우 “Passphrase for key "imported-openssh-key":”에서 비밀번호를 입력한 후 **Enter**를 누릅니다.
비밀번호 입력 시 화면에는 표시되지 않습니다. (다음 이미지 참고)
![](https://main.qcloudimg.com/raw/89b2ef5f04a6402f0b1832301fa811cb.png)
로그인되면 명령 프롬프트 왼쪽에 현재 로그인한 CVM 정보가 표시됩니다.



## 후속 작업

CVM에 로그인 성공하면, Tencent CVM에서 개인 사이트, 포럼을 구축할 수 있으며 다른 작업 또한 진행할 수 있습니다. 관련 작업 방법은 아래의 내용을 참조하십시오.
- [WordPress 개인 사이트 구축](https://intl.cloud.tencent.com/document/product/213/8044)
- [Discuz! 포럼 구축](https://intl.cloud.tencent.com/document/product/213/8043)

