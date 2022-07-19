FairPlay로 콘텐츠를 암호화하려면 Apple에서 FairPlay Streaming(FPS) 배포 패키지를 가져와 다음 파일을 SDMC 서버에 업로드해야 합니다.
- FPS 인증서 파일(`.der 또는 `.cer`)
- 개인 키 파일(`.pem`)
- 개인 키 비밀번호 파일(`.txt`)
- 애플리케이션 비밀 키(ASK) 파일(`.txt`)

## 작업 단계
 [](id:step1)
### 1단계: Apple 개발자 계정 생성 및 FPS 패키지 요청
1. [Apple 개발자 계정](https://developer.apple.com/support/enrollment/)을 생성합니다.
2. [FairPlay Streaming](https://developer.apple.com/streaming/fps/) 페이지 하단의 ‘[Request FPS Deployment Package](https://developer.apple.com/contact/fps/)’를 클릭하고 Apple 개발자 계정으로 로그인합니다.
3. 양식을 작성하여 제출하십시오. 요청이 승인되면 Apple에서 FPS 인증서 생성 가이드가 포함된 패키지를 보내드립니다.

>! KSM(키 보안 모듈)을 구현하고 테스트했는지 묻는 메시지가 표시되면 이에 대해 다음과 같이 답할 수 있습니다.
```
I am using a 3rd party DRM company and the company has already built and tested KSM
```

 [](id:step2)
### 2단계: 개인 키 및 인증서 서명 요청(CSR) 생성
FPS 인증서 생성 가이드의 지침에 따라 개인 키 파일(`privatekey.pem`)과 CSR 파일(`certreq.csr`)을 생성합니다. 다음은 가이드의 OpenSSL 방법을 설명합니다.
>! 이 프로세스가 수행되는 컴퓨터 또는 서버 환경에 OpenSSL이 설치되어 있는지 확인하십시오.

1. **개인 키 파일(privatekey.pem) 생성**:
	1. 아래 명령을 실행하여 개인 키 파일을 생성합니다.[](id:step1_1)
```
openssl genrsa -aes256 -out privatekey.pem 1024
```
	2. 개인 키의 비밀번호(32자 이내)를 설정합니다. 나중에 사용할 수 있도록 메모해 두십시오.
2. **CSR 파일 생성**:
	1. 아래 명령을 실행합니다(`-subj`를 수정할 수 있음).
```
openssl req -new -sha1 -key privatekey.pem -out certreq.csr -subj "/CN=SubjectName/OU=OrganizationalUnit/O=Organization/C=US"
```
	2. [이전 단계](#step1_1)에서 설정한 개인 키 비밀번호를 입력하십시오.

[](id:step3)
### 3단계: Apple Developer Portal에서 FPS 인증서 생성
1. [Apple Developer Portal](https://developer.apple.com/)에 로그인한 후 [Certificates, IDs, & Profiles](https://developer.apple.com/account/ios/certificate/)를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3c2963e1317986b25f05014042f120de.png)
2. **+**를 클릭하여 Create a New Certificate 페이지로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/79a02a3d039ae6bfe40144e2d90b0d44.png)
3. **FairPlay Streaming Certificate**를 선택하고 **Continue**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fef15cd65ddf3c21752c3b71c37b9b04.png)
4. **Choose File**을 클릭하고 생성된 `certreq.csr` 파일을 선택한 다음 **Continue**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d179f0554b61453a51e2a6efa83338e9.png)
5. Application Secret Key (ASK)를 복사하여 저장하고 아래 입력 필드에 붙여넣고 **Continue**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3a69ea9e79824df5d39213373830c8a2.png)
6. ASK를 저장했는지 확인하는 창이 나타납니다. **Generate**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1a9471e089b5224e393b8efecd5a77c7.png)
7. 상기 단계가 완료되면 FairPlay Streaming type으로 생성된 FPS 인증서가 Certificate 목록에 나타납니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0a0a4fa58cb43e811b21f34bfa91823e.png)
8. **Download**를 클릭하여 FPS 인증서(`fairplay.cer`)를 다운로드합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/dcc1be70e6c01658348920c8856ec6c2.png)

[](id:step4)
### 4단계: 인증서를 SDMC 플랫폼에 업로드
1. [SDMC의 DRM 콘솔](https://www.xmediacloud.com/contact-us/)에 로그인하여 메뉴에서 DRM 설정을 찾습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3147f0f1b675351dfdde217fc5449ceb.png)
2. **DRM 설정** > **설정 메뉴**로 이동하여 FPS 인증서 등록을 찾아 업데이트를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b6e7c92bab1dc0c7efa7b8bbfc179303.png)
3. FPS 인증서, 개인 키 파일, 개인 키 암호 파일, ASK 파일을 업로드하고 **OK**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c318449d607d21ed74d2aaaa89119f9e.png)
