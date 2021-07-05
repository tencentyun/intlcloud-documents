본 문서에서는 Tencent Cloud 라이브 화면 캡처 혹은 음란물 감지 데이터를 Tencent Cloud 객체 스토리지에 저장함으로써, 버킷(COS Bucket)을 통해 CSS 캡처 또는 음란물 감지 데이터를 저장하는 것에 대해 소개합니다. 먼저 COS Bucket을 생성한 후, COS Bucket을 통해 CSS에 권한을 부여하고 라이브 방송 콘솔에서 라이브 방송 화면 캡처 및 음란물 감지를 설정해 CSS 화면 캡처 혹은 음란물 감지 데이터를 지정된 COS Bucket(새 버전 콘솔 기능)에 입력할 수 있습니다.

### COS Bucket 생성
1. 객체 스토리지 콘솔에 로그인해 [[버킷 리스트]](https://console.cloud.tencent.com/cos5/bucket)를 선택합니다.
2. [버킷 생성]을 클릭한 뒤 팝업창에 해당 정보를 입력하고 [확인]을 클릭하면 버킷(COS Bucket)이 생성됩니다.
![](https://main.qcloudimg.com/raw/422f9ca892a0a9a46cc411712fbb1c06.png)
>!
>- Bucket name은 test로 하며, `-125****577`은 포함하지 않습니다 .  
>- 위 정보는 모두 실제 비즈니스 니즈에 따라 설정할 수 있습니다.
3. 비즈니스 니즈에 따라 COS bucket의 CDN 가속을 활성화하고 기 생성된 버킷 이름 혹은 [설정 관리]를 클릭합니다. 왼쪽의 [도메인 및 전송 관리]>[기본 CDN 가속 도메인]을 클릭한 후, [기본 CDN 가속 도메인] 설정 항목 중 [편집]을 클릭하고 현재 상태를 활성화로 설정한 뒤, 아래 옵션을 설정합니다. 자세한 설정 방법은 [기본 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31505)를 참조하십시오. 설정 완료 후 [저장]을 클릭하면 CDN 가속이 활성화됩니다.
![](https://main.qcloudimg.com/raw/96538f69d6de9e987f206aa8b26bfa5d.png)

 

### CSS의 화면 캡처 저장 권한 부여

1. Tencent Cloud 화면 캡처 스토리지 활성화를 위해 데이터 입력 권한을 받습니다. 권한을 받은 루트 계정 ID는 `-125****577`입니다.
   1. 버킷의 [[버킷 리스트](https://console.cloud.tencent.com/cos5/bucket)]에서 권한을 받은 버킷을 선택하고 오른쪽의 [설정 관리]를 클릭하여 해당 버킷 설정 관리 인터페이스로 이동한 뒤 [권한 관리]>[[버킷 액세스 권한](https://console.cloud.tencent.com/cos5/bucket/setting?type=aclconfig&anchorType=accessPermission&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)]을 선택해 사용자를 추가합니다. 사용자 유형은 루트 계정으로 선택하고 <b>루트 계정 ID: `-125****577`을 입력합니다</b>. [저장]을 클릭합니다.
![](https://main.qcloudimg.com/raw/76b93786e2d54c9166fcf0ed63b12d97.png)
![](https://main.qcloudimg.com/raw/b00fcba492552d1a7105132d1f69e714.png)
또는 [권한 관리]를 클릭해 권한 관리 인터페이스로 이동하여 권한을 부여할 버킷을 선택하고 [공용 권한]과 [사용자 권한] 버튼을 활성화하여 사용자를 추가합니다. 사용자 유형으로 루트 계정을 선택하고, <b>루트 계정 ID: `-125****577`을 입력합니다</b>. [저장] 및 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/b00fcba492552d1a7105132d1f69e714.png)
![](https://main.qcloudimg.com/raw/75667a8ec647a60700ce6ff5557c0f46.png)
>! <b>계정 ID에 루트 계정(메인 계정) ID: `125****577`를 입력하여 권한을 부여합니다. (루트 계정 ID: `125****577`은 Tencent Cloud 서비스 APPID로, `125****577`를 입력하시면 됩니다)</b>.
  
   2. 버킷 액세스 권한 설정 API는 [PUT Bucket acl 문서](https://intl.cloud.tencent.com/document/product/436/7737)를 참조하십시오.
2. 권한을 받은 COS Bucket 정보
   1. 버킷의 [[개요](https://console.cloud.tencent.com/cos5/bucket/setting?type=bucketoverview&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)]에서 COS의 모든 정보를 조회할 수 있습니다. 액세스 도메인(원본 서버 도메인)에는 bucket name과 cos appid, bucket region이 포함되어 있습니다.
![](https://main.qcloudimg.com/raw/d533e4b8c386454085d1e8604503d892.png)
    - bucket name: `test`
    - cos appid: `125****577`
    - bucket region: `ap-nanjing`

   2. 위 3개 필드 정보를 제출하면 시스템에서 라이브 방송 화면 캡처 데이터를 권한을 받은 COS Bucket에 저장합니다.
