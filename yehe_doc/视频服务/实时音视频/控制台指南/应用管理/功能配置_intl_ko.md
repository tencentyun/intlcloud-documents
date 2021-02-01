애플리케이션 생성 완료 후, [기능 설정]을 통해 현재 애플리케이션에 대한 [릴레이 푸시 스트리밍](#bypass), [클라우드 녹화](#record), [고급 권한 제어](#purview) 기능을 활성화할 수 있으며, 해당 페이지에서 설정을 수정한 후에는 약 5분 후 설정이 적용됩니다.

[](id:bypass)
## 릴레이 푸시 스트리밍 설정

### 주의사항

- UDP 전송 프로토콜을 기반으로 한 TRTC 서비스로, 프로토콜 전환을 통해 멀티미디어 스트림을 [LVB](https://intl.cloud.tencent.com/zh/document/product/267) 시스템으로 연결하며, 해당 프로세스를 “릴레이 푸시 스트리밍”이라고 합니다.
- 릴레이 푸시 스트리밍 기능은 기본적으로 비활성화되어 있으며, 활성화 시 먼저 LVB 서비스를 활성화해야 합니다.
- 릴레이 푸시 스트리밍은 [CDN 라이브 방송 보기](https://intl.cloud.tencent.com/document/product/647/35242) 시 LVB에서 라이브 방송 보기에 따라 발생하는 다운 스트림 트래픽/대역폭 관련 요금을 부과하는데 사용되며, 자세한 내용은 [LVB>트래픽/대역폭 과금](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) 설명을 참조하십시오.
- 릴레이 푸시 스트리밍은 [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/35426) 시 발생하는 녹화 및 녹화 파일 저장 등의 비용 부과에 사용되며, 자세한 내용은 [클라우드 녹화 및 재생>관련 요금](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8) 설명을 참조하십시오.
- [LVB 콘솔](https://console.cloud.tencent.com/live/domainmanage)에서 릴레이 푸시 스트리밍에 사용하는 푸시 스트리밍 도메인(`xxxx.livepush.myqcloud.com`)에 녹화, 트랜스 코딩, 음란물 감지 화면 캡처, 워터마크 등의 유료 기능을 바인딩한 경우, 릴레이 푸시 스트리밍 시 템플릿에 상응하는 [부가 요금](https://intl.cloud.tencent.com/zh/document/product/267/2819#.E5.A2.9E.E5.80.BC.E6.9C.8D.E5.8A.A1.E8.B4.B9.E7.94.A8)이 발생합니다.

[](id:open_bypass)
### 릴레이 푸시 스트리밍 기능 활성화
1. TRTC 콘솔에서 [Application Management](https://console.cloud.tencent.com/trtc/app)를 선택합니다.
2. 기능 설정 수정이 필요한 애플리케이션을 선택하고 대상 애플리케이션 라인에서 [Function Configuration]을 클릭합니다.
3. [릴레이 푸시 스트리밍 설정]에서 [릴레이 푸시 스트리밍 활성화] 오른쪽에 있는 버튼을 클릭합니다.
4. 팝업된 [릴레이 푸시 스트리밍 기능 활성화] 창에서 **리스크 설명을 잘 읽어주시고**, [릴레이 푸시 스트리밍 기능 활성화]를 클릭하면 활성화가 완료됩니다.

[](id:select)
### 릴레이 푸시 스트리밍 방식 선택
[릴레이 푸시 스트리밍 기능 활성화](#open_bypass) 후 실제 비즈니스 상황에 따라 릴레이할 푸시 스트리밍 방식을 선택할 수 있습니다.

- **지정 스트림 릴레이**: “지정 스트림 릴레이”를 선택한 후 혼합 스트리밍 트랜스 코딩이 필요 없는 경우, 클라이언트 SDK [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) 인터페이스를 호출하여 직접 릴레이 푸시 스트리밍을 실행할 수 있습니다. 혼합 스트리밍 트랜스 코딩이 필요한 경우에는 [클라우드 혼합 스트리밍 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618) 문서 가이드에 따라 진행하면 혼합 스트리밍 트랜스 코딩 후 자동으로 푸시 스트리밍을 자동으로 릴레이 합니다.
- **전체 자동 릴레이**: “전체 자동 릴레이”를 선택하면 TRTC의 모든 멀티미디어 업스트림이 자동으로 LVB 시스템에 릴레이 푸시 스트리밍됩니다.


[](id:close__bypass)
### 릴레이 푸시 스트리밍 기능 비활성화
릴레이 푸시 스트리밍 기능을 비활성화하고 싶은 경우, 다음과 같이 설정합니다.
1. [Application Management](https://console.cloud.tencent.com/trtc/app)를 클릭하여 기능 설정 수정이 필요한 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [Function Configuration]을 클릭합니다.
2. [릴레이 푸시 스트리밍 설정]에서 [릴레이 푸시 스트리밍 활성화] 오른쪽에 있는 버튼을 클릭합니다.
3. 팝업된 [릴레이 푸시 스트리밍 기능 비활성화] 창에서 **리스크 설명을 잘 읽어주시고**, [릴레이 푸시 스트리밍 기능 비활성화]를 클릭하면 비활성화가 완료됩니다.


[](id:record)
## 클라우드 녹화 설정

### 주의사항
- TRTC 서비스는 릴레이 푸시 스트리밍 방식으로 [LVB](https://intl.cloud.tencent.com/zh/document/product/267) 기능을 이용해 전체 과정을 녹화할 수 있으며, 녹화한 파일은 [VOD](https://intl.cloud.tencent.com/zh/document/product/266)에 저장됩니다.
- 녹화 기능은 LVB 서비스를 이용하여 LVB의 라이브 방송 녹화 요금이 발생하며, 당월 라이브 방송 녹화 동시 피크 채널 수를 청구 기준으로 합니다. 자세한 과금 규정은 [LVB>라이브 방송 녹화 요금 설명](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6)을 참조하십시오.
- 녹화 후 파일은 VOD 플랫폼에 저장되며, VOD 스토리지 요금이 발생합니다. VOD 플랫폼 스토리지 용량에 따라 과금되며, 자세한 과금 규정은 [VOD>비디오 스토리지(일 결산) 요금 설명](https://intl.cloud.tencent.com/document/product/266/14666)을 참조하십시오.
- 녹화한 비디오 파일을 재생 또는 다운로드하는 경우 VOD 서비스의 트래픽(비디오 가속) 비용이 발생하며, 업스트림 가속 트래픽에 따라 과금됩니다. 자세한 과금 규정은 [VOD>비디오 가속(일 결산) 요금 설명](https://intl.cloud.tencent.com/document/product/266/14666)을 참조하십시오.
- 클라우드 녹화 기능은 기본적으로 비활성화되어 있으며, 활성화 시 먼저 LVB 및 VOD 서비스를 활성화해야 합니다.
- 클라우드 녹화는 릴레이 푸시 스트리밍에 종속되므로, 먼저 [릴레이 푸시 스트리밍](#open_bypass)을 활성화해야 합니다.


[](id:open_record)
### 클라우드 녹화 기능 활성화
TRTC의 클라우드 녹화는 방 안 모든 사용자의 멀티미디어 스트림을 하나의 독립된 파일로 저장할 수 있습니다. 클라우드 녹화 기능 활성화 방법에 대한 자세한 가이드는 [클라우드 녹화 및 재생](https://intl.cloud.tencent.com/document/product/647/35426#open)을 참조하십시오.

[](id:change_record)
### 클라우드 녹화 설정 수정
>! 클라우드 녹화 설정을 수정하는 경우 현재 온라인에서 실행되고 있는 서비스 데이터에 영향이 미칠 수 있습니다. 리스크를 확인한 후 신중하게 수정하시기 바랍니다.

1. [Application Management](https://console.cloud.tencent.com/trtc/app)를 클릭하여 클라우드 녹화 기능 수정이 필요한 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [Function Configuration]을 클릭합니다.
2. [Function Configuration]>[On-cloud Recording Configuration]에서 오른쪽에 있는 [Edit]을 클릭하여 클라우드 녹화 설정 수정 페이지로 이동합니다.
4. 실제 상황에 따라 [설정 정보](https://intl.cloud.tencent.com/document/product/647/35426#recordType)를 수정하고 [OK]를 누르면 수정 사항이 저장됩니다.


[](id:close_record)
### 클라우드 녹화 기능 비활성화
클라우드 녹화를 비활성화하면 수동 녹화 및 자동 녹화를 포함한 현재 온라인에서 실행되고 있는 서비스에 대해 클라우드 녹화를 진행할 수 없습니다. 비즈니스에 클라우드 녹화 기능이 정말 필요 없는지 확인한 후 비활성화하시기 바랍니다.

1. [Application Management](https://console.cloud.tencent.com/trtc/app)를 클릭하여 기능 설정 수정이 필요한 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [Function Configuration]을 클릭합니다.
2. [Function Configuration]>[On-cloud Recording Configuration]에서 [Enable On-Cloud Recording]오른쪽에 있는 버튼을 클릭합니다.
3. 비활성화 후 미치는 영향을 자세히 읽어주시고, [클라우드 녹화 비활성화]를 클릭하면 클라우드 녹화가 비활성화됩니다.



[](id:purview)
## 고급 권한 제어
어떤 방에 방 입장 제한 또는 마이크 켜짐 제한을 추가하고 싶은 경우, 즉 지정한 사용자만 입장하거나 마이크를 켤 수 있도록 허용하고 싶고 클라이언트측에서 권한을 판단할 경우 쉽게 크래킹 공격을 당할 수 있다고 우려되는 경우 [고급 권한 제어 활성화](https://intl.cloud.tencent.com/document/product/647/35157)를 고려할 수 있습니다.


### 주의사항
고급 권한 제어를 활성화하면 현재 SDKAppID의 모든 사용자가 TRTCParams에 privateMapKey 매개변수를 정확하게 전송해야만 방에 입장할 수 있습니다. 현재 해당 SDKAppID의 사용자가 온라인 상태인 경우 해당 기능 활성화 시 신중히 고려하십시오.


### 고급 권한 제어 활성화
1. [Application Management]를 클릭하여 고급 권한 제어를 활성화할 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [Function Configuration]을 클릭합니다.
2. [Function Configuration]>[Advanced Permission Control]에서 [고급 권한 제어 활성화] 오른쪽에 있는 버튼을 클릭합니다.

### 고급 권한 제어 비활성화
1. [Application Management]를 클릭하여 고급 권한 제어를 활성화할 애플리케이션을 선택한 후, 대상 애플리케이션 라인에서 [Function Configuration]을 클릭합니다.
2. [Function Configuration]>[Advanced Permission Control]에서 [고급 권한 제어 비활성화] 오른쪽에 있는 버튼을 클릭합니다.

## 관련 문서
- 애플리케이션 리스트에서 관련 애플리케이션을 검색하는 자세한 방법은 [애플리케이션 검색](https://intl.cloud.tencent.com/zh/document/product/647/39078)을 참조하십시오.
- 클라우드에서 혼합 스트리밍 트랜스 코딩 시 사용자 정의 배경 이미지 설정이 필요한 경우 리소스 관리에서 해당하는 이미지 리소스를 추가할 수 있으며, 자세한 방법은 [리소스 관리](https://intl.cloud.tencent.com/zh/document/product/647/39081)를 참조하십시오.
- 애플리케이션 빠른 실행 관련 Demo 소스 코드에 대한 자세한 내용은 [퀵 스타트](https://intl.cloud.tencent.com/zh/document/product/647/39082)를 참조하십시오.





