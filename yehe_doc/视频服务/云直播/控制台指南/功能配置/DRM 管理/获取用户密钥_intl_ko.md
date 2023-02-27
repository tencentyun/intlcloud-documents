CSS에서 DRM 암호화의 라이선스 서비스는 타사 공급업체인 SDMC 및 DRMtoday에서 제공합니다. SDMC 또는 DRMtoday에 액세스하려면 사용자 키를 제공해야 합니다. 이 문서는 SDMC 또는 DRMtoday 사용자 키를 가져오는 방법을 보여줍니다.

## SDMC
### 작업 단계
1. [SDMC DRM 서비스](https://www.xmediacloud.com/contact-us/)에 등록합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e92825b46f81fce995a115c0905915cb.png)
2. 정보를 입력하고 **send message**를 클릭합니다. 몇 시간 내에 SDMC로부터 승인 이메일을 받게 되며 회사의 영업 사원이 귀하의 정보를 확인하기 위해 연락할 것입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/73ca49235b99ef7c42c97514a46f47c8.png)
3. SDMC에서 신청서를 검토하고 DRM 콘솔 주소와 초기 비밀번호를 이메일로 보내드립니다.
4. 받은 계정과 비밀번호로 [SDMC DRM 콘솔](https://sso.multidrm.tv/login)에 로그인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1833a48650c8ba607ad57701839b6d33.png)
5. **DRM SETTING**을 클릭하여 UID, SecretID 및 SecretKey를 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/59b1edb28e121521e9806b0d062b7495.png)
6. CSS 콘솔의 [DRM 관리](https://console.cloud.tencent.com/live/config/drm)로 이동하여 획득한 정보를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8b1e5a5214c518aa387157921cd9acf6.png)

## DRMtoday
### 작업 단계
1. [DRMtoday 웹사이트](https://castlabs.com/free-trials/drmtoday/)를 방문하여 필요한 정보를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e775679d700c980bf41e998af8d7fb25.png)
2. 입력 완료 후, **send**를 클릭합니다. 일반적으로 몇 시간 후에 drmtoday에서 시스템 이메일을 받게 됩니다. 이로부터 일정 시간 경과 후 계정 로그인 이메일을 받게 됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/dd40958e4ac33287ca764587cecdbe0a.png)
3. 그 직후 DRMtoday에서 계정 세부 정보가 포함된 다른 이메일을 보내드립니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6392ffb43cf33a2180aed06a3a8c51fa.png)
4. [DRMtoday 로그인 페이지](https://login.castlabs.com/login?response_type=code&client_id=1fc7irb6c3cumm1004dpv8fbs1&scope=openid%20profile%20email&state=bvqz7MJ1DQ4A-X_dzYZDflN3BT_O_jRF6OFxpL3fnvE%3D&redirect_uri=https://fe.staging.drmtoday.com/login/oauth2/code/&nonce=gVEoLbgH7RDiR-EXX6PiAvEgqx3UIg8fCBfDniiHZAY)에 로그인하여 계정을 입력하고 비밀번호를 생성하여 로그인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d5355f8f48e0f6056b89cdc0cb2ab108.png)
5. drmtoday 대시보드로 들어갑니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e6da9e6ff0b15e423f77ede1fbf69879.png)
6. API를 클릭합니다. 판매자 이름과 uuid를 기록해 둡니다. (merchantName\merchantUUID)
![](https://qcloudimg.tencent-cloud.cn/raw/e79ec6a6287cb6ae4ae646e312a88209.png)
7. Users 페이지로 이동합니다. API 계정을 추가하고 권한을 부여하고 암호를 기록해 둡니다.
>! 비밀번호는 한 번만 나타납니다. 판매자 API 이름과 암호를 기록해 두어야 합니다. (merchantAPIname/merchantAPIpassword)

![](https://qcloudimg.tencent-cloud.cn/raw/48d71df6591557ff51d8dc911c9d60bf.png)
생성한 API 계정을 활성화합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d59f5b5cbbaff1fcca550c6962ddaff8.png)
8. Configuration의 Ingest settings으로 이동합니다. key(keySeedID) 및 iv(ivSeedID)를 생성하는 키 시드를 추가합니다.
>? key seed에 의해 생성된 키는 여러 번 볼 수 있습니다. DRM 암호화 공급자에게 제공할 수 있습니다. HMAC SHA512를 사용한 단순 암호화의 경우 key seed 및 keyId를 사용하여 HMAC SHA512 문자열을 생성하고 문자열의 처음 16자를 key 또는 iv로 사용할 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/5fa20f0cd056e6e91cb8b4df7548ca5c.png)
9. merchantName, merchantUUID, merchantAPIname, merchantAPIpassword 및 keySeedID, ivSeedID를 가져온 후 CSS 콘솔의 DRM 관리에 해당 정보를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e648c01c8f7892252932ef8a7a6024c4.png)
>? DRM, SDMC 및 DRMtoday를 연결하는 동안 문제가 발생하면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하십시오. 전체 프로세스를 책임지고 도와드리겠습니다.