FairPlay DRM(FPS) 기술을 사용하려면 Apple FPS 배포 패키지에 요청해야 합니다. 본문에서는 이 패키지와 다음 정보를 얻는 방법을 안내합니다.

- FairPlay Streaming(FPS) 인증서(형식: .cer)
- 프라이빗 키 파일(형식: .pem)
- 프라이빗 키 암호
- ASK（Application Secret Key）

## 1단계: FairPlay Streaming Deployment Package 요청

1. [Apple FairPlay 페이지](https://developer.apple.com/streaming/fps/)로 이동하여 맨 아래로 스크롤한 다음 `Request FPS Deployment Package`를 클릭하면 양식이 팝업됩니다.

>! Apple 개발자 계정으로 로그인해야 합니다.

![image-20220426181021189](https://qcloudimg.tencent-cloud.cn/raw/c8533ed9e4cf2b7961058eb9e5cd502a.png)

2. 양식을 작성하여 제출하십시오.

![image-20220426181021190](https://qcloudimg.tencent-cloud.cn/raw/5f905c0a865990ba4f1705fabdcdd652.png)

3. 요청이 승인되면 `FPS_Deployment_Package.zip` 패키지가 발행됩니다.

  >? KSM(키 보안 모듈)을 구현하고 테스트했는지 묻는 메시지가 표시되면 이에 대해 다음과 같이 답할 수 있습니다. 
   > ```
   > I am using a 3rd party DRM company and the company has already built and tested KSM
   > ```

## 2단계: 프라이빗 키 및 인증서 서명 요청(CSR, Certificate Signing Request) 생성

`FPS_Deployment_Package.zip`의 압축을 풀고 패키지의 가이드 문서(.pdf)에 설명된 대로 암호로 보호된 프라이빗 키 파일과 CSR 파일을 만듭니다.

>! 이 프로세스가 수행되는 컴퓨터 또는 서버 환경에 OpenSSL이 설치되어 있는지 확인하십시오. 

1. 아래 명령을 실행하여 프라이빗 키 파일(`privatekey.pem`)을 생성합니다.

   ```shell
openssl genrsa -aes256 -out privatekey.pem 2048
   ```
   프라이빗 키에 대한 암호(32자 이하 권장)를 설정해야 합니다. 나중에 사용할 수 있도록 암호를 기록해 두십시오.
   
   ![image-20220421115813168](https://staticintl.cloudcachetci.com/yehe/backend-news/ksBs652_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16723902163742.png)
   
2. 아래 명령을 실행하여 CSR 파일(`certreq.csr`)을 생성합니다.

   ```shell
   openssl req -new -sha1 -key privatekey.pem -out certreq.csr -subj "/CN=SubjectName/OU=OrganizationalUnit/O=Organization/C=US"
   ```
   프라이빗 키 암호를 입력해야 합니다.
   
   ![image-20220421115929084](https://qcloudimg.tencent-cloud.cn/raw/25c7097a4633a2429b0f7173c0f255b6.png)
   

## 3단계: FPS 인증서 생성(FairPlay Streaming Certificate)

[Apple 개발자 페이지](https://developer.apple.com/account)에서 FPS 인증서와 ASK를 받으십시오.

1. [Apple 개발자 페이지](https://developer.apple.com/account)로 이동하여 왼쪽 사이드바에서 `Certificates, Identifiers & Profiles`를 클릭합니다.

   ![image-20220419113745847](https://qcloudimg.tencent-cloud.cn/raw/29e8bb1b63a60c877f17dd0c39d9e8d5.png)

2. `+`를 클릭합니다.

   ![image-20220419113637808](https://qcloudimg.tencent-cloud.cn/raw/4b88b93e4450b7171f09a3b75e2cb2bc.png)

3. `FairPlay Streaming Certificate`를 선택하고 `Continue`를 클릭합니다.

   ![image-20220419114215512](https://qcloudimg.tencent-cloud.cn/raw/00fa1494b1256c9b4e1d769356450721.png)

4. `Choose File`을 클릭하고 2단계에서 생성한 `certreq` 파일을 선택한 다음 `Continue`를 클릭합니다.

   ![image-20220419114506263](https://qcloudimg.tencent-cloud.cn/raw/52c2834bf36f4074e7f9f731aefc8948.png)

5. `Application Secret Key (ASK)`를 복사 및 백업하고 아래 입력 필드에 입력하고 `Continue`를 클릭합니다.

   ![image-20220419114920781](https://qcloudimg.tencent-cloud.cn/raw/8e55fb6e817a2279f6b2cea3418506f7.png)

6. `ASK`를 저장했는지 확인하는 창이 나타납니다. 확인 후 `Generate`를 클릭합니다.

   >! ASK 사본을 저장했는지 확인하십시오. 이후에는 볼 수 없습니다.

   ![image-20220419115103618](https://qcloudimg.tencent-cloud.cn/raw/808347b36d824de46b6cbb84654d20c8.png)

7. 상기 단계가 완료되면 생성된 FPS 인증서(유형: `FairPlay Streaming`)가 인증서 목록에 나타납니다.

   ![image-20220419115340087](https://qcloudimg.tencent-cloud.cn/raw/ee831cfc5c26f37bdc09c9a50bab5ef5.png)

8. `Download`를 클릭하여 FPS 인증서(`fairplay.cer`)를 다운로드합니다.

   ![image-20220419115536031](https://qcloudimg.tencent-cloud.cn/raw/d7e7ad03c0168b61db084cfee762f6cc.png)

## 결론

이제 필요한 `FairPlay` 인증서 정보 신청을 완료했습니다.
