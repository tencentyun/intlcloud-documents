본 문서에서는 Tencent Cloud 라이브 화면 캡처 혹은 음란물 감지 데이터를 Tencent Cloud 객체 스토리지에 저장함으로써, 버킷(COS Bucket)을 통해 CSS 캡처 또는 음란물 감지 데이터를 저장하는 것에 대해 소개합니다. 먼저 COS Bucket을 생성한 후, COS Bucket을 통해 CSS에 권한을 부여하고 라이브 방송 콘솔에서 라이브 방송 화면 캡처 및 음란물 감지를 설정해 CSS 화면 캡처 혹은 음란물 감지 데이터를 지정된 COS Bucket(새 버전 콘솔 기능)에 입력할 수 있습니다.
### COS Bucket 생성
1. 객체 스토리지 콘솔에 로그인해 [[버킷 리스트]](https://console.cloud.tencent.com/cos5/bucket)를 선택합니다.
2. [버킷 생성]을 클릭한 뒤 팝업창에 해당 정보를 입력하고 [확인]을 클릭하면 버킷(COS Bucket)이 생성됩니다.
![](https://main.qcloudimg.com/raw/423beefad19658e0cec8cdd28d6d25e1.png)
>!
> - Bucket name은 buckettest123이며, -1259222427은 포함하지 않습니다.  
> - 위 정보는 모두 비즈니스에 따라 필요한 설정입니다.
3. 비즈니스 니즈에 따라 COS bucket의 CDN 가속을 활성화하고 기 생성된 버킷 이름 혹은 [설정 관리]를 클릭합니다. 왼쪽의 [도메인 및 전송 관리]>[기본 CDN 가속 도메인]을 클릭한 후, [기본 CDN 가속 도메인] 설정 항목 중 [편집]을 클릭하고 현재 상태 설정을 활성화한 후 아래 옵션을 설정합니다. 구체적인 설정 방법은 [기본 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31505)를 참조하십시오. 설정 완료 후 [저장]을 클릭하면 CDN 가속이 활성화됩니다.
![](https://main.qcloudimg.com/raw/097144cf7c6d1df5923d406b0301f93e.png)

 

### CSS의 화면 캡처 저장 권한 부여
1. Tencent Cloud 화면 캡처 스토리지 활성화를 위해 데이터 입력 권한을 받습니다. 권한을 받은 루트 계정 ID는 3508645126입니다.
	1. 버킷의 [버킷 리스트](https://console.cloud.tencent.com/cos5/bucket)>[권한 관리]>[버킷 액세스 권한]에서 사용자를 추가합니다. 사용자 유형은 루트 계정으로 선택하고 **루트 계정 ID: 3508645126을 입력합니다.**
	>! **계정 ID에 루트 계정 ID: 3508645126을 입력하여 권한을 받아야 합니다. (루트 계정 ID: 3508645126은 CSS 서비스로, 3508645126을 그대로 입력하면 됩니다)**.
	![](https://main.qcloudimg.com/raw/37362cc7a0b945e79899e24f84f33dab.png)
	
	2. 버킷 액세스 권한 설정 API는 [PUT Bucket acl 문서](https://intl.cloud.tencent.com/document/product/436/7737)를 참조하십시오.
2. 권한을 받은 COS Bucket 정보
	1. 버킷의 [기본 설정]>[기본 정보]에서 COS의 모든 정보를 조회할 수 있습니다. 액세스 도메인(원본 서버 도메인)에는 bucket name과 cos appid, bucket region이 포함되어 있습니다.
	![](https://main.qcloudimg.com/raw/b84d288cf37b40ed548ca4a25863742a.png)
	 - bucket name: buckettest123
	 - cos appid: 1259200900
	 - bucket region: ap-chengdu
	2. 위 3개 필드 정보를 제출하면 시스템에서 라이브 방송 화면 캡처 데이터를 권한을 받은 COS Bucket에 저장합니다.
