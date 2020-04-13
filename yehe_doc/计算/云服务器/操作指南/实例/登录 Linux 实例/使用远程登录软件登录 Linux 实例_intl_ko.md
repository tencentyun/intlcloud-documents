## 작업 시나리오

본 문서는 PuTTY 프로그램을 예로 들어 Windows 시스템의 로컬 컴퓨터에서 원격 로그인 프로그램을 사용해 Linux 인스턴스에 로그인하는 방법에 대해 소개합니다.


## 로컬 운영 체제에 적용

Windows

## 인증 방식

**비밀번호** 또는 **키**

## 전제 조건
- 인스턴스에 로그인할 수 있는 관리자 계정 및 비밀번호(또는 키)를 획득한 상태.
 - 시스템의 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)에 이동하여 획득 바랍니다.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호 리셋](http://intl.cloud.tencent.com/document/product/213/16566)하세요.
- 사용자의 CVM 인스턴스가 공용 IP를 구매하였고, 해당 인스턴스가 이미 CVM 인스턴스의 22번 포트를 활성화한 상태(빠른 구성을 통해 구매한 CVM 인스턴스는 기본적으로 활성화 상태입니다).


## 작업 순서

### 비밀번호를 사용하여 로그인

1. Windows 원격 로그인 프로그램, 즉 PuTTY를 다운로드합니다.
PuTTY의 획득 방식:[획득](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
2. [putty.exe]를 더블 클릭하여 PuTTY 클라이언트를 실행합니다.
3. PuTTY Configuration 창에서 다음 내용을 입력합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
매개변수 예시 설명은 아래와 같습니다.
 - Host Name(or IP address): CVM의 공인 IP([CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하여 리스트 페이지 및 상세 페이지에서 공인 IP를 획득할 수 있습니다).
 - Port: CVM의 포트이며 반드시 22로 설정해야 합니다.
 - Connect type: "SSH"를 선택합니다.
 - Saved Sessions: 세션 이름을 입력합니다. 예시: test.
 "Host Name"을 설정한 후 "Saved Sessions"을 설정하여 저장하면 이후 사용부터 "Saved Sessions" 아래에 저장한 세션 이름을 더블 클릭하여 바로 서버에 로그인할 수 있습니다.
3. [Open]을 클릭하여 "PuTTY"의 운행 인터페이스에 접속하면 "login as:" 제시어가 표시됩니다.
4. "login as" 뒤에 사용자 이름을 입력한 후 **Enter**를 누릅니다.
5. "Password" 뒤에 비밀번호를 입력한 후 **Enter**를 누릅니다.
로그인을 하면 명령 프롬프트 왼쪽에 현재 CVM 로그인 정보가 표시됩니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)

### 키를 사용하여 로그인

1. Windows 원격 로그인 프로그램, 즉 PuTTy를 다운로드합니다.
putty.exe와 puttygen.exe 프로그램을 각각 다운로드하세요. PuTTy의 획득 방식: [이곳을 클릭하여 획득](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)。
2. [puttygen.exe]를 더블 클릭하여 PuTTy Key 클라이언트를 실행합니다.
3. [Load]를 클릭하여 이미 다운받은 프라이빗 키 저장 디렉터리를 선택하고 엽니다. 아래 이미지 참조
예시, 파일명이 david인 프라이빗 키 파일을 선택하고 엽니다.
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. PuTTY Key Generator 창에서 키 이름과 암호화된 프라이빗 키의 비밀번호를 입력한 다음 [Save private key]를 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. 팝업된 창에서 키를 저장한 디렉터리를 선택하고 파일명 입력란에 “키 이름.ppk”를 입력한 후 [저장]을 클릭합니다. 예시, david 프라이빗 키 파일을 david.ppk 키 파일로 다른 이름으로 저장합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/44df54ca77069356a26c51e2a4db7643.png)
6. [putty.exe]를 더블 클릭하여 PuTTY 클라이언트를 실행합니다.
7. 왼쪽 메뉴에서 [Connection]>[SSH]>[Auth]를 선택하여 Auth 설정 인터페이스에 접속합니다.
8. [Browse]를 클릭하여 키의 저장 디렉터리를 선택하고 엽니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
8. Session 설정 인터페이스로 전환한 후 서버의 IP, 포트 및 연결 유형을 설정합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - Host Name (IP address): CVM의 공인 IP. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하여 리스트 페이지 및 상세 페이지에서 공인 IP를 획득할 수 있습니다.
 - Port: CVM의 포트로 반드시 22를 입력해야 합니다.
 - Connect type: "SSH"를 선택합니다.
 - Saved Sessions: 세션 이름을 입력합니다. 예시: test.
 "Host Name"을 설정한 후 "Saved Sessions"을 설정하여 저장하면 이후 사용부터 "Saved Sessions" 아래에 저장한 세션 이름을 더블 클릭하여 바로 서버에 로그인할 수 있습니다.
9. [Open]을 클릭하여 로그인 요청을 합니다.


