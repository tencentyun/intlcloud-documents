애플리케이션 생성 완료 후, [기능 설정]에서 현재 애플리케이션의 [릴레이 푸시 스트림](#bypass), [클라우드 녹화](#record), [고급 권한 제어](#purview) 기능을 활성화할 수 있으며, 해당 페이지에서 모든 기능 설정을 수정한 후 적용하는데 약 5분의 시간이 소요됩니다.

[](id:bypass)
## 릴레이 푸시 스트림 설정

### 주의사항

- UDP 전송 프로토콜을 기반으로 한 Tencent Real-Time Communication(TRTC) 서비스로, 프로토콜 전환을 통해 멀티미디어 스트림을 [Cloud Streaming Services](https://intl.cloud.tencent.com/document/product/267) 시스템에 연결합니다. 이 프로세스를 ‘릴레이 푸시 스트림’이라고 합니다.
- 릴레이 푸시 스트림 기능은 기본적으로 비활성화되어 있으며, 활성화 시 먼저 CSS 서비스를 활성화해야 합니다.
- 릴레이 푸시 스트림은 [CDN 라이브 방송 시청 실행](https://intl.cloud.tencent.com/document/product/647/35242) 시, CSS에서 라이브 방송 시청에 따라 발생하는 다운스트림 트래픽/대역폭 관련 요금을 부과하는데 사용되며, 자세한 내용은 [CSS > 트래픽/대역폭 과금](https://intl.cloud.tencent.com/document/product/267/2818) 설명을 참고하십시오.
- 릴레이 푸시 스트림은 [클라우드 녹화 및 재생](https://intl.cloud.tencent.com/document/product/647/35426) 시 발생하는 녹화 및 녹화 파일 저장 등의 요금을 부과하는데 사용되며, 자세한 내용은 [클라우드 녹화 및 재생 > 관련 요금](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8) 설명을 참고하십시오.
- [CSS 콘솔](https://console.cloud.tencent.com/live/domainmanage)에서 릴레이 푸시 스트림에 사용하는 푸시 도메인(`xxxx.livepush.myqcloud.com`)에 녹화, 트랜스 코딩, 음란물 감지 화면 캡처, 워터마크 등의 유료 기능 템플릿을 바인딩한 경우, 릴레이 푸시 스트림 사용 시 템플릿에 해당하는 [부가 요금](https://intl.cloud.tencent.com/document/product/267/2819)이 발생합니다.

[](id:open_bypass)
### 릴레이 푸시 스트림 기능 활성화
1. TRTC 콘솔에 접속하여 [[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)]를 선택합니다.
2. 기능 설정 수정이 필요한 애플리케이션을 선택하고 타깃 애플리케이션의 [기능 설정]을 클릭합니다.
 ![](https://main.qcloudimg.com/raw/f302931ec709c205bd6c4e2378cd14b3.png)
3. [릴레이 푸시 스트림 설정]에서 [릴레이 푸시 스트림 활성화] 오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/19050dd982abfe75080843148f3abbc4.png)
4. 팝업된 [릴레이 푸시 스트림 기능 활성화] 창에서 **리스크 설명을 꼼꼼히 읽은 후** [릴레이 푸시 스트림 기능 활성화]를 클릭하면 활성화가 완료됩니다.
![](https://main.qcloudimg.com/raw/0c81b0ef96e7e07f9fba0d7f8827c7f8.png)

[](id:select)
### 릴레이 푸시 스트림 방식 선택
[릴레이 푸시 스트림 기능 활성화](#open_bypass) 후 실제 작업 상황에 따라 릴레이 푸시 스트림 방식을 선택할 수 있습니다.
![](https://main.qcloudimg.com/raw/98b5a33c06846dc755a1e1b6a2853048.png)

- **지정 스트림 릴레이**: ‘지정 스트림 릴레이’를 선택한 후, 혼합 스트림 트랜스 코딩이 필요 없는 경우, 클라이언트 SDK [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a7cbe48ea2cd3fb05a5b10350b6d81265) 인터페이스를 호출하여 직접 릴레이 푸시 스트림을 실행할 수 있습니다. 혼합 스트림 트랜스 코딩이 필요한 경우에는 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618) 문서 가이드에 따라 진행하면 혼합 스트림 트랜스 코딩 후 자동으로 푸시 스트림을 릴레이 합니다.
- **전체 자동 릴레이**: '전체 자동 릴레이'를 선택하면 TRTC의 모든 업스트림 멀티미디어 스트림은 자동으로 CSS 시스템에 릴레이 푸시 스트림됩니다.


[](id:close__bypass)
### 릴레이 푸시 스트림 기능 비활성화
릴레이 푸시 스트림 기능을 비활성화하고 싶은 경우, 다음과 같이 설정합니다.
1. [[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)]를 클릭하여 기능 설정 수정이 필요한 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
3. [릴레이 푸시 스트림 설정]에서 [릴레이 푸시 스트림 활성화] 오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/8abcab1e53ca628b274576c597e6fcb6.png)
4. [릴레이 푸시 스트림 기능 비활성화] 팝업창에 보이는 **리스크 설명을 자세히 읽습니다.** 비활성화 하려면 [릴레이 푸시 스트림 기능 비활성화]를 클릭합니다.
![](https://main.qcloudimg.com/raw/42501fc7a48d9384fa271280fad9fb50.png)


[](id:record)
## 클라우드 녹화 설정

### 주의사항
- TRTC 서비스는 릴레이 푸시 스트림을 통해 [Cloud Streaming Services](https://intl.cloud.tencent.com/document/product/267)로 전 과정 클라우드 녹화 기능을 제공하며 녹화한 파일을 [Video on Demand](https://intl.cloud.tencent.com/document/product/266) 플랫폼에 저장합니다.
- 녹화 기능은 CSS 서비스를 이용하여 CSS의 라이브 방송 녹화 요금이 발생하며, 당월 라이브 방송 녹화 피크 동시 접속 수를 청구 기준으로 합니다. 자세한 과금 규정은 [CSS > 라이브 방송 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/267/39605)을 참고하십시오.
- 녹화 후의 파일은 VOD 플랫폼에 저장되며 VOD 저장 요금이 발생합니다. 녹화 파일이 저장된 VOD 플랫폼의 저장 용량을 기준으로 과금되며, 과금 규정에 대한 자세한 사항은 [VOD > 비디오 스토리지(일 결산) 과금 설명](https://intl.cloud.tencent.com/document/product/266/14666)을 참고하십시오.
- 녹화한 비디오 파일을 재생 또는 다운로드하는 경우 VOD 서비스의 트래픽(비디오 가속) 요금이 발생하며, 다운스트림 가속 트래픽에 따라 과금됩니다. 자세한 과금 규정은 [VOD > 비디오 가속(일 결산) 과금 설명](https://intl.cloud.tencent.com/document/product/266/14666)을 참고하십시오.
- 클라우드 녹화 기능은 기본적으로 비활성화되어 있으며, 활성화 시 먼저 CSS 및 VOD 서비스를 활성화해야 합니다.
- 클라우드 녹화는 릴레이 푸시 스트림에 종속되므로, 먼저 [릴레이 푸시 스트림](#open_bypass)을 활성화해야 합니다.


[](id:open_record)
### 클라우드 녹화 기능 활성화
TRTC의 클라우드 녹화는 각 방마다 사용자별 멀티미디어 스트리밍을 독립 파일로 녹화할 수 있습니다. 클라우드 녹화 기능 활성화의 자세한 작업 가이드는 [클라우드 녹화 및 재생](https://intl.cloud.tencent.com/document/product/647/35426#open)을 참고하십시오.

[](id:change_record)
### 클라우드 녹화 설정 수정
>! 클라우드 녹화 설정을 변경하는 경우 현재 온라인에서 실행되고 있는 작업 데이터에 영향을 미칠 수 있습니다. 리스크를 확인한 후 신중하게 변경하시기 바랍니다.

1. [[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)]에서 클라우드 녹화 설정 수정이 필요한 애플리케이션을 선택해 타깃 애플리케이션에서 수행하는 [기능 설정]을 클릭합니다.
3. [기능 설정] > [클라우드 녹화 활성화]에서 오른쪽에 있는 [편집]을 클릭하여 클라우드 녹화 설정 수정 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/1c46c6d6f7d87928536ab576975cdcd3.png)
4. 실제 상황에 따라 [설정 정보](https://intl.cloud.tencent.com/document/product/647/35426#recordType)를 수정하고 [확인]을 누르면 수정 사항이 저장됩니다.


[](id:close_record)
### 클라우드 녹화 기능 비활성화
클라우드 녹화를 비활성화하면 현재 온라인에서 실행 중인 작업에 대해 수동 녹화 및 자동 녹화를 포함한 모든 클라우드 녹화를 진행할 수 없습니다. 작업에 클라우드 녹화 기능이 필요 없는지 확인 후 비활성화하시기 바랍니다.

1. [[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)]를 클릭하여 기능 설정 변경이 필요한 애플리케이션을 선택한 후, 타깃 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
2. [기능 설정] > [클라우드 녹화 설정]에서 [클라우드 녹화 활성화] 오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/72893310f197830b468292b9d0062458.png)
3. 비활성화 진행 후의 영향에 대해 자세히 읽습니다. 클라우드 녹화 비활성화를 하려면 [클라우드 녹화 비활성화]를 클릭합니다.
![](https://main.qcloudimg.com/raw/b1a41cf54dad0c5cd48f65d2a250e56d.png)



[](id:purview)
## 고급 권한 제어
입장 혹은 마이크 켜짐 권한을 제한하고 싶은 경우 지정 사용자만 입장하고 마이크를 켤 수 있도록 허용할 수 있습니다. 클라이언트 권한에 대한 크래킹 공격이 걱정되는 경우 [고급 권한 제어 기능 활성화](https://intl.cloud.tencent.com/document/product/647/35157)를 고려해볼 수 있습니다.
![](https://main.qcloudimg.com/raw/78882ea4eac56c347c89a4e8113d706a.png)


### 주의사항
고급 권한 제어 기능을 활성화하면 현재 SDKAppID의 모든 사용자가 TRTCParams에 privateMapKey 매개변수를 정확하게 전송해야만 방에 입장할 수 있습니다. 해당 SDKAppID의 사용자가 온라인 상태인 경우 이 기능을 쉽게 활성화해서는 안 됩니다.


### 고급 권한 제어 기능 활성화
1. [애플리케이션 관리]를 클릭하여 고급 권한 제어 기능을 활성화할 애플리케이션을 선택한 후, 타깃 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
2. [기능 설정] > [고급 권한 제어 기능]에서 [고급 권한 제어 기능 활성화] 오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/d5de4b300cf71969244239d821414db6.png)

### 고급 권한 제어 기능 비활성화
1. [애플리케이션 관리]를 클릭하여 고급 권한 제어 기능을 비활성화할 애플리케이션을 선택하고 타깃 애플리케이션 라인에서 [기능 설정]을 클릭합니다.
2. [기능 설정] > [고급 권한 제어]에서 [고급 권한 제어 비활성화] 오른쪽에 있는 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/b1a41cf54dad0c5cd48f65d2a250e56d.png)

## 관련 문서
- 신규 애플리케이션 생성에 대한 자세한 방법은 [애플리케이션 생성](https://intl.cloud.tencent.com/document/product/647/39077)을 참고하십시오.
- 애플리케이션 리스트에서 관련 애플리케이션을 검색하는 자세한 방법은 [애플리케이션 검색](https://intl.cloud.tencent.com/document/product/647/39078)을 참고하십시오.
- 애플리케이션 기본 정보 조회에 대한 자세한 방법은 [애플리케이션 정보](https://intl.cloud.tencent.com/document/product/647/39079)를 참고하십시오.
- 클라우드에서 혼합 스트림 트랜스 코딩 시 사용자 정의 배경 이미지 설정이 필요한 경우 리소스 관리에서 상응하는 이미지 리소스를 추가할 수 있으며, 자세한 방법은 [리소스 관리](https://intl.cloud.tencent.com/document/product/647/39081)를 참고하십시오.
- 애플리케이션 빠른 실행 관련 Demo 소스 코드에 대한 자세한 내용은 [퀵 스타트](https://intl.cloud.tencent.com/document/product/647/39082)를 참고하십시오.



