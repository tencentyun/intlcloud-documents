본 문서는 Tencent Cloud 라이브 화면 캡처 혹은 Tencent Cloud 객체 스토리지에 음란물 감지 데이터를 저장하고, 버킷(COS Bucket)를 통한 클라우드 라이브 화면 캡처 혹은 음란물 감지 데이터 저장에 관해 소개합니다. 먼저 COS Bucket을 생성한 후, CSS에 COS Bucket의 권한을 부여하고 라이브 방송 콘솔에서 라이브 방송 화면 캡처 음란물 감지를 설정해 CSS 화면 캡처 혹은 음란물 감지 데이터를 지정된 COS Bucket(새 버전 콘솔 기능)에 입력할 수 있습니다.
### COS Bucket 생성
1. 객체 스토리지 콘솔에 로그인해 [버킷 리스트](https://console.cloud.tencent.com/cos5/bucket)를 선택합니다.
2. [버킷 생성]을 클릭하면 해당 정보가 팝업창이 뜨며, [확인]을 클릭하면 버킷 COS Bucket을 생성할 수 있습니다.
 ![](https://main.qcloudimg.com/raw/423beefad19658e0cec8cdd28d6d25e1.png)
>!
> - Bucket name은 examplebucket으로 하며, 오른쪽 숫자는 포함하지 않습니다.  
> - 위 정보는 모두 서비스에 필요한 설정입니다.
3. 서비스 요구사항에 따라 COS bucket의 CDN 가속을 활성화하고 이미 생성된 버킷 이름 혹은 [관리 설정]을 클릭합니다. 왼쪽의 [도메인 및 전송 관리]>[기본 CDN 가속 도메인]을 클릭한 후, [기본 CDN 가속 도메인] 설정 페이지에서 [편집]을 클릭합니다. 현재 상태 설정을 활성화로 한 후 아래 옵션을 설정합니다. 구체적인 설정 방법은 [기본 CDN 가속 도메인](https://intl.cloud.tencent.com/zh/document/product/436/31505)을 참조하십시오. 설정 완료 후 [저장]을 클릭하면 CDN 가속이 활성화됩니다.
![](https://main.qcloudimg.com/raw/097144cf7c6d1df5923d406b0301f93e.png)



### CSS의 화면 캡처 저장 권한 부여
1. Tencent Cloud 화면 캡처 활성화를 위해 데이터 입력 권한을 받습니다. 권한을 받은 루트 계정 ID는 3508645126입니다.
	1. 버킷의 [버킷 리스트](https://console.cloud.tencent.com/cos5/bucket)>[권한 관리]>[버킷 액세스 권한]에서 사용자를 추가합니다. 사용자 유형은 루트 계정으로 선택하고 **루트 계정 ID: 3508645126**을 입력합니다.
	>! **계정 ID는 루트 계정 ID: 3508645126를 입력해서 권한을 받아야 합니다. 루트 계정 ID: 3508645126는 CSS 서비스로, 3508645126를 입력하면 됩니다**.
	![](https://main.qcloudimg.com/raw/37362cc7a0b945e79899e24f84f33dab.png)
	
	2. 버킷 액세스 권한 설정 API는 [PUT Bucket acl 문서](https://intl.cloud.tencent.com/document/product/436/7737)를 참조하십시오.
2. 권한을 받은 COS Bucket 정보
	1. 버킷의 [기본 설정]>[기본 정보]에서 COS의 모든 정보를 조회할 수 있습니다. 액세스 도메인(원본 서버 도메인)에는 bucket name, cos appid, bucket region이 포함되어 있습니다.
	![](https://main.qcloudimg.com/raw/b84d288cf37b40ed548ca4a25863742a.png)
	 - bucket name: examplebucket。
	 - cos appid: 125****900。
	 - bucket region: ap-chengdu
	2. 위 3개 필드 정보를 제출하면 시스템에서 라이브 방송 화면 캡처 데이터를 권한을 받은 COS Bucket에 저장합니다.
