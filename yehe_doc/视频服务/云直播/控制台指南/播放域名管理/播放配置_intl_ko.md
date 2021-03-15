## 작업 시나리오
도메인 푸시 스트리밍 완료 후, CSS 콘솔로 이동해 재생 주소 생성기를 이용하여 푸시 스트리밍 주소 StreamName과 동일한 StreamName을 입력한 후 해당 스트리밍의 재생 주소를 생성하면 해당 재생 주소를 통해 라이브 방송 화면을 확인할 수 있습니다.

## 전제 조건
 - [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 합니다.
 - **재생 도메인**이 추가되어 있어야 합니다.

## 작업 순서
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **재생 도메인** 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Playback Configuration]>[Playback Address Generator]를 선택하여 다음과 같이 설정합니다.
	1. 만료 시간을 선택합니다. (예시: `2019-02-28 23:59:59`)
	2. 사용자 정의 스트림 이름 StreamName을 입력합니다(예: `liveteststream`). 재생 주소 StreamName은 푸시 스트리밍 주소 StreamName과 반드시 일치해야 해당 스트림을 재생할 수 있습니다.
	3. [ Generate Playback Address]을 클릭합니다.
![](https://main.qcloudimg.com/raw/6bea977acb754ec9c36422aef3189f39.png)
3. 재생 도메인의 재생 인증이 비활성화 상태인 경우, [Playback Configuration]>[Playback Address] 탭에서 해당 재생 도메인의 RTMP, FLV, HLS 세 가지 재생 주소를 확인할 수 있습니다. 재생 주소 상의 StreamName(스트림 이름)이 변경되어 푸시 스트리밍 주소와 연결됩니다. 연결된 후에는 재생 주소로 라이브 방송 화면을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/8d8a9ee63dc12045da418c1539051eb6.png)

>- 라이브 방송에 관한 자세한 내용은 [라이브 방송](https://intl.cloud.tencent.com/document/product/267/31559)을 참조하십시오.




## 재생 주소
### 1. 재생 주소 생성 규칙
```
RTMP 포맷: rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
FLV 포맷: http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
M3U8 포맷: http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- **domain**: ICP비안을 받은 외부 재생 도메인
- **AppName**: 애플리케이션 이름. 기본값은 live로 설정되어 있으며, 사용자 정의가 필요한 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 설정해야 합니다.
- **StreamName**: 스트림 이름. 사용자 정의가 가능하며 라이브 방송 스트림을 식별하는 데 사용됩니다.
- **txSecret**: 재생 인증을 활성화하면 생성되는 인증 문자열
- **txTime**: 재생 주소에 설정된 타임스탬프. 콘솔 재생 주소의 유효 시간입니다.

>
>-도메인 인증을 활성화한 경우 실제 만료 시간은 txTime + 인증 유효시간입니다.
>
>- 콘솔에서는 사용 편의를 위해 설정하는 시간이 곧 실제 만료시간이 됩니다. 도메인 인증을 활성화한 경우 재생 주소 연산 시 공식에 따라 txTime을 역산출합니다.

### 2. 트랜스 코딩 후의 라이브 방송 주소
라이브 방송 도메인에 트랜스 코딩 템플릿을 설정하고 트랜스 코딩 후의 라이브 방송 스트림을 재생해야 하는 경우, 트랜스 코딩 재생 주소는 원본 재생 주소 상의 StreamName 뒤에 `_트랜스 코딩 템플릿 이름`을 추가하는 방식으로 조합됩니다.

예를 들어 원본 재생 주소가 `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`이고 연결된 트랜스 코딩 템플릿 이름이 `hd`인 경우, 트랜스 코딩 재생 주소는 `http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`이 됩니다.

### 3. H.265 재생 주소
H.265를 이용하는 푸시 스트리밍이고, 동시에 H.265의 라이브 방송 스트림을 재생하는 경우 StreamName 뒤에 `_h265`를 추가하여 재생 주소를 새로 생성해야 합니다.
>
>- `_h265`를 추가하지 않는 경우 H.264 라이브 방송 스트림 재생 시 트랜스 코딩 비용이 발생합니다.
>- StreamName에 `_h265`를 추가한 후에는 다시 재생 주소를 생성해야 하며, 이미 생성한 재생 주소에 추가할 수 없고 해당 주소는 사용할 수 없습니다.

예를 들어 원본 재생 주소가 `http://domain/AppName/StreamName1.flv?txSecret=Md5(key+StreamName1+hex(time))&txTime=hex(time)`이고 H.265를 이용하는 푸시 스트리밍인 경우, `StreamName1_h265`을 사용하여 생성된 재생 주소는 `http://domain/AppName/StreamName1_h265.flv?txSecret=Md5(key+StreamName1_h265+hex(time))&txTime=hex(time)`이 됩니다.
