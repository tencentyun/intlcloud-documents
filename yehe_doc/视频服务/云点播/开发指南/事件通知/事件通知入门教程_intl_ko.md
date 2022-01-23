이 튜토리얼은 ‘일반 콜백’ 및 ‘신뢰할 수 있는 콜백’ 모드에서 VOD 이벤트 알림을 사용하는 방법을 안내합니다.

## 전제 조건

- [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 및 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증이 되지 않은 사용자는 중국 본토 VOD 인스턴스를 구매할 수 없습니다.
- 일반 콜백을 위한 Python 2.7 런타임 환경이 필요합니다.

## 일반 콜백
### 콜백 수신 서비스 배포

[일반 콜백](https://intl.cloud.tencent.com/document/product/266/33948)을 통해 이벤트 알림을 받기 위해서는 공용 IP가 있는 서버에 콜백 수신 서비스를 배포해야 합니다. 다음은 예를 들어 CVM 인스턴스에 이러한 서비스를 배포하는 방법을 설명합니다.

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에서 인스턴스 목록 페이지를 입력하고 [생성]을 클릭합니다.
2. [빠른 구성] 메뉴를 선택하고 [이미지]에 ‘**Ubuntu Server**’ 또는 ‘**CentOS**’를 선택하고 [공용 네트워크 대역폭]에 ‘**1Mbps**’를 선택하고 ‘**무료 공용 IP 할당**’을 선택한 다음 [즉시 구매]를 클릭합니다.
3. [인스턴스 목록](https://console.cloud.tencent.com/cvm/index) 페이지로 다시 들어가 성공적으로 생성된 CVM 인스턴스를 찾아 [기본 IP 주소](본 예시에서는 **134.XXX.XXX.167**)에서 공용 IP를 복사합니다.
![](https://main.qcloudimg.com/raw/89e8b56123b9155e880658bad20eec1e.png)
4. 구입한 CVM 인스턴스에 로그인하여 [소스 코드 패키지](http://document-1251659802.coscd.myqcloud.com/NotificationTuition.zip)를 다운로드하고 작업 디렉터리에 압축을 풀고 다음 명령을 실행합니다.
		python NotificationReceiveServer.py
명령이 실행된 후 CVM 인스턴스의 표준 출력은 서비스 프로세스가 시작되었고 포트 8080에서 수신 대기 중임을 나타내는 `Started httpserver on port 8080`가 출력됩니다.
5. 브라우저에 `http://134.XXX.XXX.167:8080`을 입력하면 CVM 인스턴스의 표준 출력은 다음 HTTP 요청 정보를 출력합니다.
![](https://main.qcloudimg.com/raw/4e7eaffe641002f9b0307244e4bec8dc.png)

### 일반 콜백 설정
1. [VOD 콘솔](https://console.cloud.tencent.com/vod/overview)에 로그인하고 왼쪽 사이드바에서 [콜백 설정]을 클릭합니다.
2. [설정]을 클릭합니다.
	- 콜백 모드: ‘**일반 콜백**’을 선택합니다.
	- 콜백 URL: http://134.XXX.XXX.167:8080을 입력합니다.
	- 콜백 이벤트: ‘**비디오 업로드 완료 시 콜백**’을 선택합니다.
3. [확인]을 클릭하여 설정을 완료합니다.

### 일반 콜백 시작 및 수신

시작하려면 [데모 비디오](http://1255566954.vod2.myqcloud.com/ca75586fvodgzp1255566954/484c46995285890788305672872/xUCHV5kOGyIA.wmv)를 로컬 파일 시스템에 다운로드하십시오.
1. 왼쪽 사이드바에서 [미디어 자산]을 클릭하고 [업로드됨]을 선택한 다음 [비디오 업로드]를 클릭합니다.
![](https://main.qcloudimg.com/raw/4724951966b46c801498efed4b6ebec9.png)
2. ‘**비디오 업로드**’ 대화 상자가 나타나면 [로컬 업로드]를 선택하고 [비디오 선택]을 클릭한 후 **데모 비디오**를 VOD 플랫폼에 업로드합니다.
![](https://main.qcloudimg.com/raw/e0eb51db29de59e948b332ad05a069db.png)
 업로드 작업을 수행한 후 ‘**업로드 중**’ 열에 비디오 업로드 진행률이 표시됩니다.
![](https://main.qcloudimg.com/raw/7f072f0e67b4f3be6907ff1f5a414848.png)
 업로드가 완료되면 ‘**업로드 완료**’ 열의 비디오 목록에 업로드된 동영상과 해당 ID(예: FileId)가 표시됩니다.
![](https://main.qcloudimg.com/raw/6c18e73eb8576fc120fe903fc0848927.png)
3. CVM 인스턴스를 확인합니다. 표준 출력은 [비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33950) 알림의 내용을 출력합니다.
 <img src="https://main.qcloudimg.com/raw/f6439edcd8ae59cab1d393987382e136.png" width="818">
4. [미디어 자산]의 ‘**업로드됨**’ 열에서 방금 업로드한 비디오를 선택하고 [비디오 처리](https://intl.cloud.tencent.com/document/product/266/33892)를 클릭합니다. [처리 유형]에 대해 ‘**트랜스코딩 템플릿 수동 선택**’ 옵션을 선택하고, [트랜스코딩 템플릿]에서 ‘**MP4-LD-FLU(10)**’를 선택하고, [비디오 커버]를 선택한 상태로 유지하고 [확인]을 클릭합니다.
5. 10분 동안 기다린 후 CVM 인스턴스를 확인하면 해당 표준 출력은 트랜스코딩 결과(`Type`이 `Transcode`) 및 커버 생성을 위한 시점 화면 캡처(`Type`이 `CoverBySnapshot`) 결과를 포함한 [태스크 플로우 상태 변경](https://intl.cloud.tencent.com/document/product/266/33953)에 대한 알림 내용을 출력합니다.
 <img src="https://main.qcloudimg.com/raw/4e577e7feb5524ff82e8a82c8e1cbdd2.png" width="818">

이렇게 비디오를 업로드하고 트랜스코딩 작업을 수행했습니다. 업로드 및 트랜스코딩이 완료된 후 콜백 수신 서비스는 ‘**비디오 업로드 완료**’ 및 ‘**태스크 플로우 상태 변경**’에 대한 알림을 수신했습니다.

## 신뢰할 수 있는 콜백

1. [VOD 콘솔](https://console.cloud.tencent.com/vod/overview)에 로그인하고 왼쪽 사이드바에서 [콜백 설정]을 클릭합니다.
2. [설정]을 클릭합니다.
	- 콜백 모드: ‘**신뢰할 수 있는 콜백**’을 선택합니다.
	- 콜백 이벤트: ‘**비디오 업로드 완료 콜백**’을 선택합니다.
3. [확인]을 클릭하여 설정을 완료합니다.

### 신뢰할 수 있는 콜백 시작

1. 왼쪽 사이드바에서 [미디어 자산]을 클릭하고 [업로드됨]을 선택한 다음 [비디오 업로드]를 클릭합니다.
![](https://main.qcloudimg.com/raw/4724951966b46c801498efed4b6ebec9.png)

2. ‘**비디오 업로드**’ 대화 상자가 나타나면 [로컬 업로드]를 선택하고 [비디오 선택]을 클릭한 후 **데모 비디오**를 VOD 플랫폼에 업로드합니다.
![](https://main.qcloudimg.com/raw/e0eb51db29de59e948b332ad05a069db.png)

 업로드 작업을 수행한 후 ‘**업로드 중**’ 열에 비디오 업로드 진행률이 표시됩니다.
![](https://main.qcloudimg.com/raw/7f072f0e67b4f3be6907ff1f5a414848.png)

 업로드가 완료되면 ‘**업로드 완료**’ 열의 비디오 목록에 업로드된 동영상과 해당 ID(예: FileId)가 표시됩니다.
![](https://main.qcloudimg.com/raw/6c18e73eb8576fc120fe903fc0848927.png)

3. [미디어 자산]의 ‘**업로드됨**’ 열에서 방금 업로드한 비디오를 선택하고 [[비디오 처리]](https://intl.cloud.tencent.com/document/product/266/33892)를 클릭합니다. [처리 유형]에 대해 ‘**트랜스코딩 템플릿 수동 선택**’ 옵션을 선택하고, [트랜스코딩 템플릿]에서 ‘**MP4-LD-FLU(10)**’를 선택하고, [비디오 커버]를 선택한 상태로 유지하고 [확인]을 클릭합니다.

이렇게 비디오를 다시 업로드하고 해당 비디오에 대한 트랜스코딩 작업을 시작했습니다. 이러한 작업으로 인해 이벤트 알림이 트리거됩니다.

### 신뢰할 수 있는 콜백 가져오기

이벤트 알림이 트리거된 후 신뢰할 수 있는 콜백을 능동적으로 가져와야 합니다. [API 툴](https://intl.cloud.tencent.com/document/product/266/34183)을 통해 'PullEvents' 명령을 실행하여 소비할 이벤트 알림을 쿼리할 수 있으며 구체적인 단계는 다음과 같습니다.
1. [VOD PullEvents 명령용 API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=PullEvents&SignVersion=)를 입력하고 ‘**개인 키**’([키 조회]를 클릭하여 [API 키 관리 콘솔](https://console.cloud.tencent.com/cam/capi)에서 가져올 수 있음).
2. 오른쪽 열에서 [온라인 호출]을 선택하고 [요청 발송]을 클릭합니다.

요청을 보낸 후 반환된 결과에서 이벤트 목록 'EventSet'을 관찰합니다. 이벤트 목록에는 ‘**비디오 업로드 완료**’ 및 ‘**태스크 플로우 상태 변경**’의 두 가지 이벤트 알림이 포함되어 있으며 해당 이벤트 핸들은 각각 '8078360634045903972' 및 '8078360634045903972'입니다.
	 <img src="https://main.qcloudimg.com/raw/1497a3fd83ce599ef0a03437df53b6b4.png" width="579">
 <img src="https://main.qcloudimg.com/raw/9bf358ef2231a05237fe226cadebe136.png" width="579">

이렇게 신뢰할 수 있는 콜백 메소드에서 ‘**비디오 업로드 완료**’ 및 ‘**태스크 플로우 상태 변경**’이라는 두 가지 알림을 가져왔습니다. 다음으로 가져온 이벤트 알림을 즉시 확인해야 합니다.

### 신뢰할 수 있는 콜백 확인

가져온 신뢰할 수 있는 콜백은 **30초 이내** 에 확인되어야 합니다. 그렇지 않으면:

* 이벤트 핸들에서 30초 경과 후 확인을 위해 API를 호출하면 호출이 실패합니다.
* 이벤트가 30초 이상 확인되지 않으면 다음 신뢰할 수 있는 콜백이 풀링될 때 다시 풀링됩니다.

[API 툴](https://intl.cloud.tencent.com/document/product/266/34184)을 통해 `ConfirmEvents` 명령을 실행하여 소비할 이벤트 알림을 쿼리할 수 있으며 구체적인 단계는 다음과 같습니다.

1. [VOD ConfirmEvents 명령용 API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ConfirmEvents&SignVersion=)로 이동하여 ‘**개인 키**’를 입력합니다.

2. ‘**EventHandles.N**’ 입력 창에 이벤트 알림을 가져올 때 얻은 이벤트 핸들을 입력합니다.

3. 오른쪽 열에서 [온라인 호출]을 선택하고 [요청 발송]을 클릭합니다.

 요청 성공 시 다음 정보가 반환됩니다.

실패 시 다음을 확인하십시오.
- 이벤트 핸들이 잘못 입력되었는지 여부.
- 이벤트가 30초 이상 당겨졌는지 여부.
4. 5분 후 [API 툴](https://intl.cloud.tencent.com/document/product/266/34183)을 다시 사용하여 'PullEvents' 명령을 실행하고 이벤트 알림을 가져옵니다.

​      **ResourceNotFound** 오류가 반환되면 가져올 수 있는 알림이 더 이상 없다는 의미입니다.



