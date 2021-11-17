본 문서에서는 Tencent Cloud 라이브 화면 캡처 혹은 음란물 감지 데이터를 Tencent Cloud COS에 저장함으로써, 버킷(COS Bucket)을 통해 CSS 캡처 또는 음란물 감지 데이터를 저장하는 방법에 대해 소개합니다. 먼저 COS Bucket을 생성한 후, COS Bucket을 통해 CSS에 권한을 부여하고 라이브 방송 콘솔에서 라이브 방송 화면 캡처 및 음란물 감지를 설정해 CSS 화면 캡처 혹은 음란물 감지 데이터를 지정된 COS Bucket(신규 버전 콘솔 기능)에 입력할 수 있습니다.

### COS Bucket 생성
1. COS 콘솔에 로그인해 [ **버킷 리스트** ](https://console.cloud.tencent.com/cos5/bucket)를 선택합니다.
2. **버킷 생성**을 클릭하고 팝업 페이지에 해당 정보를 입력한 후 **다음 단계**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a447693216193809de86e422149f5a25.png)
3. 필요에 따라 고급 옵션 설정을 선택하고 완료되면 **다음 단계**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/29fe705f2b98c29bc7ae913e39fc99d0.png)
4. 설정 정보를 확인하고 **생성**을 클릭하여 COS Bucket 버킷 생성을 완료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fb2c3a34e7502234600b93cfff7900b6.png)

>!
>- Bucket name은 test로 하며, `-130****592`은 포함하지 않습니다.  
>- 위 정보는 모두 실제 비즈니스 니즈에 따라 설정할 수 있습니다.

5. 비즈니스 니즈에 따라 COS bucket의 CDN 가속을 활성화하고 기존 생성된 버킷 이름 혹은 **설정 관리**를 클릭합니다. 왼쪽의 **도메인 및 전송 관리**> **기본 CDN 가속 도메인**을 클릭한 후, **기본 CDN 가속 도메인** 설정 항목 중 **편집**을 클릭하고 현재 상태를 활성화로 설정한 뒤, 아래 옵션을 설정합니다. 자세한 설정 방법은 [기본 가속 도메인 이름 사용](https://intl.cloud.tencent.com/document/product/436/31505)을 참고하십시오. 설정 완료 후 **저장**을 클릭하면 CDN 가속이 활성화됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/dc7a8ff49c0832d2322d03a0714d2f76.png)


### CSS의 화면 캡처 저장 권한 부여

1. Tencent Cloud 화면 캡처 스토리지의 데이터 입력 권한을 활성화합니다. 권한 부여 루트 계정 ID: `3508645126`.
   1. 버킷의 **[버킷 리스트](https://console.cloud.tencent.com/cos5/bucket)**에서 권한을 받은 버킷을 선택하고 오른쪽의 **설정 관리**를 클릭하여 해당 버킷 설정 관리 인터페이스로 이동한 뒤 **권한 관리**> **[버킷 액세스 권한](https://console.cloud.tencent.com/cos5/bucket/setting?type=aclconfig&anchorType=accessPermission&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)**을 선택해 사용자를 추가합니다. 사용자 유형은 루트 계정으로 선택하고 **루트 계정 ID: `3508645126`을 입력합니다**. **저장**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f31e4a9251f1c959954b958b284bfb44.png)
![](https://qcloudimg.tencent-cloud.cn/raw/8c8b4331c37cfb3f07169eb8726017df.png)
또는 **인증 관리**를 클릭하여 인증 관리 인터페이스로 이동하고 권한을 부여할 버킷을 확인한 다음 **공개 권한** 및 **사용자 권한** 버튼을 열어 사용자를 추가합니다. 사용자 유형으로 루트 계정을 선택하고 **루트 계정 ID: `3508645126`을 입력합니다**. **저장** 및 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3af1130fae59890e7658d4681aadf844.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0025f6d26a3cf83f7e213c32e7f7eddf.png)
>! **계정 ID에 루트 계정(메인 계정) ID: `3508645126`을 입력하여 권한을 부여합니다. (루트 계정 ID: `3508645126`은 CSS APPID로, `3508645126`을 입력하면 됩니다)**.

   2. 버킷 액세스 권한 설정 API는 [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737)을 참고하십시오.
2. 권한을 받은 COS Bucket 정보 가져옵니다.
   1. 버킷의 **[개요](https://console.cloud.tencent.com/cos5/bucket/setting?type=bucketoverview&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)**에서 COS의 모든 정보를 조회할 수 있습니다. 액세스 도메인(원본 서버 도메인)에는 bucket name과 cos appid, bucket region이 포함되어 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2b1fa50e6551966b3a7fe946f59d6260.png)
    - bucket name: `test`
    - cos appid: `130****592`
    - bucket region: `eu-moscow`
   2. 위 3개 필드 정보를 제출하면 시스템에서 라이브 방송 화면 캡처 데이터를 권한을 받은 COS Bucket에 저장합니다.
