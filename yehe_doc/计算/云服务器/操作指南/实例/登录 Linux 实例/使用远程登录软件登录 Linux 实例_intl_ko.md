## 작업 시나리오

본 문서는 PuTTY 소프트웨어를 사례로 Windows 시스템 로컬 컴퓨터에서 원격 로그인 소프트웨어를 사용한 Linux 인스턴스 로그인 방법을 설명합니다.


## 로컬 운영 체제에 적용

Windows

## 인증 방식

**비밀번호** 또는 **키**

## 전제 조건
- 인스턴스에 로그인할 수 있는 관리자 계정 및 비밀번호(또는 키)를 보유하고 있습니다.
 - 시스템 기본 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)로 접속하여 획득 바랍니다.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.
- CVM 인스턴스가 이미 공용 IP를 구매 및 획득하였고, 해당 인스턴스가 이미 CVM 인스턴스의 22번 포트를 활성화하였습니다(빠른 구성을 통해 구매한 CVM 인스턴스는 기본적으로 활성화 상태).


## 작업 순서
<dx-tabs>
::: 비밀번호로\s로그인[](id:passwordLogin)
1. Windows 원격 로그인 소프트웨어(PuTTY)를 다운로드합니다.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe" target="_blank" style="color: white; font-size:16px;">클릭하여 PuTTY 획득하기</a></div>
2. [putty.exe]를 더블 클릭하여 PuTTY 클라이언트를 엽니다.
3. PuTTY Configuration 창에 다음 내용을 입력합니다(아래 이미지 참고).
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
매개변수 예시 설명:
 - **Host Name(or IP address)**: CVM의 공용 IP([CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 후 리스트 페이지 및 상세 정보 페이지에서 공용 IP 획득 가능)
 - **Port**: CVM 포트는 반드시 22로 설정
 - **Connect type**: 'SSH' 선택
 - **Saved Sessions**: 세션 이름 입력(예: test)
 'Host Name' 설정 후 다시 'Saved Sessions'를 설정 및 저장하면, 이후 사용 시 'Saved Sessions'에 저장한 세션 이름을 더블 클릭해 바로 서버에 로그인할 수 있습니다.
4. [Open]을 클릭해 'PuTTY' 실행 인터페이스로 들어가면 'login as:'가 표시됩니다.
5. 'login as' 에 사용자 이름을 입력한 후 **Enter**키를 누릅니다.
6. 'Password'에 비밀번호를 입력한 후 **Enter**키를 누릅니다.
비밀번호 입력 시 화면에는 표시되지 않습니다(아래 이미지 참고).
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
로그인 후 명령 프롬프트 왼쪽에 현재 로그인한 CVM 정보가 표시됩니다.
:::
::: 키\s로그인[](id:keyLogin)
1. Windows 원격 로그인 소프트웨어(PuTTy)를 다운로드합니다. putty.exe와 puttygen.exe 소프트웨어를 각각 다운로드하십시오. 획득 방식은 다음과 같습니다.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;margin:5px;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe" target="_blank" style="color: white; font-size:16px;"> 클릭하여 PuTTY 획득하기</a></div><div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;margin:5px;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe" target="_blank" style="color: white; font-size:16px;"> 클릭하여 PuTTYgen 획득하기</a></div>
2. [puttygen.exe]를 더블 클릭하여 PuTTy Key 클라이언트를 엽니다.
3. [Load]를 클릭하고, 다운로드한 개인키 스토리지 경로를 선택하여 엽니다. 개인키는 생성 시 다운로드되었으며 사용자 개인이 보관합니다. 자세한 내용은 [SSH 키 관리](https://intl.cloud.tencent.com/document/product/213/16691)를 참조하십시오.
예들 들어, 아래의 이미지와 같이 파일명이 david인 개인키 파일을 선택하여 엽니다.
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. <span id="Step4"></span> 아래의 이미지와 같이 PuTTY Key Generator 창에 키 이름을 입력하고, 개인키 암호화에 사용할 PuTTY 비밀번호를 설정합니다(옵션). 설정 완료 후 [Save private key]를 클릭합니다.
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. 팝업된 창에서 키를 저장한 경로를 선택하고 파일명 란에 '키 이름.ppk'를 입력한 후 [저장] 버튼을 클릭합니다. 예를 들어, 아래의 이미지와 같이 david 개인키 파일을 다른 이름으로 저장하기를 통해 david.ppk 키 파일로 저장합니다.
![](https://main.qcloudimg.com/raw/fad925e85923ac1d41afacde4a9c690c.png)
6. [putty.exe]를 더블 클릭하여 PuTTY 클라이언트를 엽니다.
7. 왼쪽 메뉴에서 [Connection]>[SSH]>[Auth]를 선택하여 Auth 설정 인터페이스로 들어갑니다.
8. 아래의 이미지와 같이 [Browse]를 클릭하여 키 스토리지 경로를 선택하고 엽니다.
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
8. 아래의 이미지와 같이 Session 설정 인터페이스로 전환한 후 서버 IP와 포트, 연결 유형을 설정합니다.
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - **Host Name(IP address)**: CVM의 공용 IP([CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 후 리스트 페이지 및 상세페이지에서 공용 IP 획득 가능)
 - **Port**: CVM 포트는 반드시 22 입력
 - **Connect type**: 'SSH' 선택
 - **Saved Sessions**: 세션 이름 입력(예: test)
 'Host Name' 설정 후 다시 'Saved Sessions'를 설정 및 저장하면, 이후 사용 시 'Saved Sessions'에 저장한 세션 이름을 더블 클릭해 바로 서버에 로그인할 수 있습니다.
9. [Open]을 클릭해 'PuTTY' 실행 인터페이스로 들어가면 'login as:'가 표시됩니다.
10. 'login as' 에 사용자 이름을 입력한 후 **Enter**키를 누릅니다.
11. [순서 4](#Step4)에 따라 개인키의 비밀번호 암호화 설정을 완료한 경우 'Passphrase for key'imported-openssh-key':'에서 비밀번호를 입력한 후 **Enter**를 누릅니다.
비밀번호 입력 시 화면에는 표시되지 않습니다(아래 이미지 참고).
![](https://main.qcloudimg.com/raw/89b2ef5f04a6402f0b1832301fa811cb.png)
로그인 후 명령 프롬프트 왼쪽에 현재 로그인한 CVM 정보가 표시됩니다.
:::
</dx-tabs>

## 후속 작업

CVM 로그인에 성공하면 Tencent Cloud CVM에서 개인 사이트나 포럼을 구축할 수 있으며 다른 작업 또한 진행할 수 있습니다. 관련 작업은 아래의 내용을 참조하십시오.
- [WordPress 개인 사이트 구축](https://intl.cloud.tencent.com/document/product/213/33469)
- [Discuz! 포럼 구축](https://intl.cloud.tencent.com/document/product/213/34278)

