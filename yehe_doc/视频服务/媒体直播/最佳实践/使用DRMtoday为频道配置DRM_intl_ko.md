### 1단계: 계정 신청

1. DRMtoday 신청

   a. [DRMtoday 제품 페이지](https://castlabs.com/drmtoday/)로 이동하여 DRMtoday를 신청합니다.
   ![img](https://main.qcloudimg.com/raw/b1fa760d75f68f27c4470bf52f81b800.png)

   b.신청 완료 후 DRMtoday 계정, 비밀번호, Dashboard 웹 사이트 주소를 얻을 수 있습니다.

2. Fairplay 인증서 신청

   a. [Apple Fairplay 공식 홈페이지](https://developer.apple.com/streaming/fps/)로 이동합니다.

   b. [Request FPS Deployment Package](https://idmsa.apple.com/IDMSWebAuth/signin.html?path=%2Fcontact%2Ffps%2F&appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757)를 클릭하여 관련 정보를 입력 및 제출합니다.
   ![img](https://main.qcloudimg.com/raw/9592e1021494896689ad0d7135f26560.png)

   c. FPS_Deployment_Package.zip 파일을 가져옵니다.

   d. FPS_Deployment_Package.zip의 압축 해제 문서를 참고하여 비밀번호로 보호된 개인 키와 CSR(인증서 서명 요청)을 로컬에서 생성합니다.

   e. FPS_Deployment_Package.zip의 압축 해제 문서를 참고하여 CSR을 Apple에 업로드합니다. 페이지가 ASK를 반환합니다. 잘 보관하시기 바랍니다.

   f. 공식적으로 생성된 FairPlay Certificate(인증서)를 로컬에 다운로드합니다.


## 2단계: DRMtoday에 Fairplay 인증서 업로드

DRMtoday Dashboard 웹 사이트로 이동하여 Configuration-DRMsettings을 선택합니다.
![img](https://main.qcloudimg.com/raw/352f6e951f0ca3252c5bf346ad19464b.png)
매개변수:

- **Default IV**: 비워둘 수 있습니다.

**Update certificate and keys** 선택 후, 다음 매개변수를 설정합니다.

   - **Application secret key(ASK)**: Fairplay 인증서 신청 시 5단계에서 받은 ASK를 hex 인코딩 형식으로 입력합니다.
    
   - Provider certificate: 6단계에서 다운로드한 FairPlay Certificate(인증서)입니다. Fairplay 인증서 신청 시 업로드된 인증서 유형은 PEM 형식이어야 하며, linux에서 openssl 툴을 사용하여 전환할 수 있습니다. 예시: 인증서 이름이 Fairplay.cer 일 때, 전환 명령은 다음과 같습니다.

  ```
  openssl x509 -inform der -in fairplay.cer -out fairplay.pem
  ```

- Provider private key: 사용자가 키로 보호되는 개인키를 생성하고 업로드 키 유형은 linux에서 openssl 툴을 사용하여 전환할 수 있는 PKCS #8 PEM 형식이어야 합니다. 예시: 개인키 파일 이름이 privatekey.pem 일 때, 전환 명령은 다음과 같습니다.

  ```
  openssl rsa -in privatekey.pem -outform PEM -out out.pem
  ```



## 3단계: DRMtoday API를 통해 Widevine 또는 Fairplay 키 설정

다음 작업은 DRMtoday 공식 홈페이지에서 제공하는 작업 문서를 참고하시기 바랍니다. 원본 문서는 [DRMtoday Key Ingestion](https://fe.staging.drmtoday.com/frontend/documentation/integration/key_ingestion.html)을 참고하십시오.

1. CAS 인증
   DRMtoday는 CAS(Central Authentication Service)를 사용하여 API를 승인되지 않은 무단 액세스로부터 보호합니다. 원본 문서는 [DRMtoday CAS Authentication](https://fe.staging.drmtoday.com/frontend/documentation/integration/cas_authentication.html)을 참고하십시오.

   a. CAS Login: Login 주소로 HTTP POST 요청을 보냅니다.

   예시:

   ```
   curl -v 'https://auth.staging.drmtoday.com/cas/v1/tickets' -H 'Content-Type: application/x-www-form-urlencoded' -XPOST -d 'username=${username}&amp;password=${password}'
   ```

   매개변수:

   - **username, password**: DRMtoday의 계정 비밀번호를 사용하거나 DRMtoday에서 생성한 API 계정과 비밀번호를 사용합니다. [DRMtoday API 계정 생성 문서](https://fe.staging.drmtoday.com/frontend/documentation/integration/dashboard.html?dummy#adding-accounts)

   b. CAS Ticket Retrieval: CAS Login 요청 후 반환된 header의 Location 주소로 HTTP POST 요청을 보냅니다.

   예시:

   ```
   curl -v 'https://auth.staging.drmtoday.com/cas/v1/tickets/xxx' -H 'Content-Type: application/x-www-formurlencoded'-XPOST -d 'service=https://fe.staging.drmtoday.com/frontend/api/keys/v2/ingest/${merchantApiName}'
   ```

   매개변수:

   - **service**: Dashboard-API 페이지의 Ingest key에 해당하는 Endpoint로, 아래 이미지와 같습니다.
     ![img](https://main.qcloudimg.com/raw/299f6fdcdfd5016a48c4b41f530e277a.png)

2. 키 설정
   인증 완료 후 Ingest key API를 통해 Widevine 또는 Fairplay 키를 설정합니다. 인터페이스 사용 문서는 [DRMtoday Key Ingestion](https://fe.staging.drmtoday.com/frontend/documentation/integration/key_ingestion.html)을 참고하십시오.
   예시:

   ```
   curl -v 'https://fe.staging.drmtoday.com/frontend/api/keys/v2/ingest/${merchant}?ticket=${ticket}' -H 'Content-Type: application/json' -H 'Accept: application/json' -XPOST -d '{"assets":[{"type":"CENC","assetId":"assettest","variantId":"varianttest","ingestKeys":[{"streamType":"VIDEO_AUDIO","algorithm":"AES","keyId":"MDAwMDAwMDAwMDAwMDAwMA==","key":"MDAwMDAwMDAwMDAwMDAwMA==","iv":"MDAwMDAwMDAwMDAwMDAwMA=="}]}]}'
   ```

   매개변수:

   - **merchant**: Dashboard의 Ingest key에 해당하는 Endpoint입니다.
   - **ticket**: CAS Ticket Retrieval에서 반환된 Body 콘텐츠입니다.
   - **type**: CENC로 설정하면 Widevine, Fairplay 지원 가능합니다. Widevine 암호화는 keyId 및 key를 설정해야 하고 Fairplay 암호화는 key 및 iv를 설정해야 합니다.
   - **keyId, key, iv**: base64 인코딩 형식으로 설정합니다. “MDAwMDAwMDAwMDAwMDAwMA==” 해당 hex 문자열은 30303030303030303030303030303030 입니다.



## 4단계: StreamLive에서 DRM 키 설정

StreamLive 콘솔 작업 가이드의 출력 그룹 설정(*여기서 ‘출력 그룹 설정’은 링크로 리디렉션하여 ‘StreamLive 채널 관리’ Ⅲ. 출력 그룹 설정 페이지로 이동해야 합니다.)을 참고하여 StreamLiveDRM 키를 설정합니다.

- **DRM**: 활성화
- **Scheme**: Custom DRM Keys

Fairplay 키:
![img](https://main.qcloudimg.com/raw/d1fd0abc8a2c4b1aa970f74160641731.png)

- **ContentId**: 3-2단계 키 설정에서 설정된 assetId로, hex 문자열로 입력합니다.
- **Key**: 3-2단계 키 설정에서 설정된 key로, hex 문자열로 입력합니다.
- **Iv**: 3-2단계 키 설정에서 설정된 iv로, hex 문자열로 입력합니다.

Widevine 키:
![img](https://main.qcloudimg.com/raw/d65d6a93e13b12d8014558a601a21692.png)

- **ContentId**: 3-2단계 키 설정에서 설정된 assetId로, hex 문자열로 입력합니다.
- **KeyId**: 3-2단계 키 설정에서 설정된 keyId로, hex 문자열로 입력합니다.
- **Key**: 3-2단계 키 설정에서 설정된 key로, hex 문자열로 입력합니다.


## 5단계: 재생 테스트 

StreamLive 매뉴얼에 따라 재생 주소를 설정한 후(예를 들어 [StreamPackage의 Channel로 라이브 스트림을 출력](https://intl.cloud.tencent.com/document/product/1048/41760#6.-output-content-to-streampackage-through-streamlive)하고, StreamPackage의 [Endpoint 노드를 통해 재생 주소를 가져오기]([콘솔 가이드 | Tencent Cloud(tencent.com)](https://intl.cloud.tencent.com/document/product/1063/41787))할 수 있습니다. [DRMtoday 재생 페이지](https://players.castlabs.com/presto/6.1.2/#/player/config)를 사용하여 테스트할 수 있습니다.
![img](https://main.qcloudimg.com/raw/5b8b559d838497dd5b75cf9c7cedf363.png)
![img](https://main.qcloudimg.com/raw/77249ddf9131bc9578bdb28fc3c37fb4.png)
매개변수:

- **Content URL**: 재생 콘텐츠 URL. 
- **DRM Environment**: 실제 상황에 따라 선택하십시오.
- **Merchant**: DRMtoday 상의 사용자 이름은 일반적으로 merchantApiName과 동일합니다.
- **User ID, Session ID**: [설정 문서](https://fe.staging.drmtoday.com/frontend/documentation/integration/dashboard.html#uisetting-Test_dummy)(License Delivery Authorization 유형이 Test_dummy인 경우)를 참고하십시오.
- **Asset ID**: 3-2단계 키 설정에서 설정된 assetId.
- **Variant ID**: 3-2단계 키 설정에서 설정된 variantId.
