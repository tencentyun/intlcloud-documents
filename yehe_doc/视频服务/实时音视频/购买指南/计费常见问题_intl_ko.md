<span id="que1"></span>
### 무료 베타 패키지는 어떻게 획득하나요?
2019년 10월 11일부터 [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 처음으로 애플리케이션을 생성하는 Tencent Cloud 계정에 10,000분 무료 베타 패키지를 증정합니다. 무료 패키지는 [영상 통화](https://intl.cloud.tencent.com/document/product/647/39788), [음성 통화](https://intl.cloud.tencent.com/document/product/647/39787), [비디오 ILVB](https://intl.cloud.tencent.com/document/product/647/39786), [음성 ILVB](https://intl.cloud.tencent.com/document/product/647/39785) 서비스 용량을 차감하는 방식으로 사용할 수 있습니다. 자세한 내용은 [무료 베타 테스트](https://intl.cloud.tencent.com/document/product/647/39784)를 참조하십시오.
)。

<span id="que2"></span>
### 청구서와 차감 상세 내역은 어떻게 조회하나요?
[과금 센터 > 청구서 상세 내역](https://console.cloud.tencent.com/expense/bill/summary)에서 자세한 청구서와 차감 내역을 조회할 수 있습니다.

<span id="que3"></span>
### 과금 사용량의 상세 내역은 어떻게 조회/확인하나요?
- 실시간 사용량: TRTC 콘솔 - [사용량 통계](https://console.cloud.tencent.com/trtc/statistics) 페이지에서 사용량 그래프와 상세한 데이터를 조회할 수 있습니다. 당일 조회는 5분 단위의 상세 내역을, 기간 조회는 일별 취합 내역을 확인할 수 있습니다(분 단위 표시).
- 청구서 사용량: Tencent Cloud 과금 센터에서 청구서에 해당하는 상세 사용 내역을 [다운로드](https://console.cloud.tencent.com/expense/bill/dosageDownload)할 수 있습니다. 다운로드 결과는 Excel 파일로 저장되며, 5분 단위의 상세 내역과 일별 세부 내역을 확인할 수 있습니다(초 단위 표시).
- 서버 API: 더 자세한 과금 사용량 데이터는 서버 API에서 확인할 수 있습니다. 조회 기간이 1일 이하일 경우 5분 단위의 데이터가 반환되며, 1일을 초과할 경우 일별 취합 데이터가 반환됩니다(초 단위 표시).

>!사용량 데이터는 실시간으로 변하므로 최종 결산된 사용량과 소폭 차이가 있을 수 있습니다. **청구서 사용량을 기준으로 하십시오**.

<span id="que4"></span>
### 패키지 잔여 시간은 어떻게 조회하나요?
패키지는 실시간 차감 방식을 사용해 5분마다 잔여 시간이 업데이트됩니다. [패키지 관리](https://console.cloud.tencent.com/trtc/package) 페이지에서 잔여 시간을 조회할 수 있습니다.

<span id="que5"></span>
### 초 단위로 과금되는데 잔여 시간이 1분 미만일 때 1분으로 계산되면, 패키지 이용 시 시간이 더 많이 차감되는 것 아닌가요?
아닙니다. 패키지 사용 시간 차감 시 당일 누적 시간을 기준으로 하므로, 중복으로 차감되지 않습니다.
다음은 패키지 시간 차감에 관한 예시입니다.

|통계 구간|구간 서비스 사용량|누적 서비스 사용량|누적 과금 시간|구간 차감 시간|누적 차감 시간|
|---|---|---|---|---|---|
|00:00:00 - 00:04:59|30초|30초|1분|1분 차감|1분 차감|
|00:05:00 - 00:09:59|20초|50초|1분|0분 차감|1분 차감|
|00:10:00 - 00:14:59|40초|90초|2분|1분 차감|2분 차감|


<span id="que6"></span>
### 새로 구매한 패키지에서 차감된 시간이 제가 패키지를 구매한 후의 사용량을 초과하는 이유가 무엇인가요?

새 패키지가 적용되면, 구매일 0시 이후 차감되지 않은 다른 패키지의 사용량이 차감됩니다. TRTC 콘솔의 [사용량 통계](https://console.cloud.tencent.com/trtc/statistics) 페이지에서 새로 구매한 패키지의 당일 사용 현황을 조회할 수 있습니다.

<span id="que15"></span>
### 구매한 음성/표준 화질/고화질 패키지를 범용 패키지로 전환할 수 있나요?
가능합니다. 전환 기준은 다음과 같습니다.
- **음성 패키지** 1분 = 범용 패키지 1분
- **표준 화질 패키지** 1분 = 범용 패키지 2분
- **고화질 패키지** 1분 = 범용 패키지 4분

전환 권한이 없습니다. 필요한 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 도움을 요청하십시오. 

<span id="que7"></span>
### 범용 패키지 구매 불가 메시지가 뜨는 이유는 무엇인가요?
2019년 10월 11일부터 TRTC의 과금 기준이 음성, 비디오 통합 단가(이하 기존 과금 방식)에서 음성, 표준 화질, 고화질, 초고화질 차등 단가(이하 신규 과금 방식)로 변경되었습니다. 신규 과금 패키지는 새로운 과금 방식에서만 사용할 수 있습니다.
- 2019년 10월 11일 이후 가입한 Tencent Cloud 계정은 기본적으로 신규 과금 방식이 적용됩니다.
- 2019년 10월 11일 이전에 가입한 Tencent Cloud 계정은 기존 과금 방식이 적용된 패키지를 모두 사용하거나, 기간 만료일의 다음 달에 신규 과금 패키지를 구매할 수 있습니다. 신규 과금 패키지를 구매하면 신규 과금 방식으로 자동 업그레이드됩니다.

기존 과금 방식이 적용된 패키지도 계속 [구매](https://intl.cloud.tencent.com/zh/document/product/647/35440)할 수 있습니다. 기존 과금 패키지를 모두 사용하지 않았거나 기간이 만료되지 않았는데 신규 과금 방식으로 업그레이드하려면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 도움을 요청하십시오.



<span id="que8"></span>
### 영상 통화 또는 비디오 ILVB를 사용했는데 왜 음성 시간이 집계되나요?
사용자가 멀티미디어 스트림을 구독하는 경우, 일반적으로 음성 및 비디오 데이터가 모두 포함됩니다. 발신 측에서 카메라를 비활성화하거나 수신 측에서 비디오 화면을 비활성화한 경우, 수신 측 네트워크에 이상이 있거나 방에 혼자 있는 경우에는 사용자가 비디오 화면을 수신하지 못합니다. TRTC는 사용자의 요금 절감을 위해 비디오 화면을 수신하지 못한 경우 음성 시간으로 사용량을 통계합니다.

<span id="que9"></span>
### 화면 공유는 어떻게 과금되나요?
화면 공유는 개별적인 비디오 스트림 채널입니다. 사용자가 화면 공유한 비디오 스트림을 구독하고 비디오 화면을 수신하면, 비디오의 길이에 따라 과금됩니다.

<span id="que10"></span>
### 클라우드 녹화는 어떻게 과금되나요?
TRTC는 릴레이 푸시 스트림을 통해 [CSS](https://intl.cloud.tencent.com/document/product/267) 시스템에서 녹화를 진행하며, 녹화한 파일은 [VOD](https://intl.cloud.tencent.com/document/product/266) 플랫폼에 저장해 언제든지 재생할 수 있습니다.
>- 2020년 7월 1일부터 TRTC 콘솔에서 처음으로 애플리케이션을 생성한 Tencent Cloud 계정의 경우, 클라우드 녹화 기능 사용으로 발생하는 녹화 요금은 [클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385)의 과금 규정을 기준으로 합니다.
- 2020년 7월 1일 이전에 TRTC 콘솔에서 애플리케이션을 생성한 적이 있는 Tencent Cloud 계정의 경우, 애플리케이션 생성 일자와 상관없이 클라우드 녹화 기능 사용으로 발생하는 요금은 기본적으로 [CSS > 라이브 방송 녹화](https://intl.cloud.tencent.com/document/product/267/39605)의 과금 규정을 적용합니다.
- 클라우드 녹화 완료 후 출력되는 녹화 파일은 기본적으로 VOD 플랫폼에 저장되며, VOD는 사용 현황에 따라 스토리지 요금과 재생 요금이 부과됩니다. 자세한 내용은 [클라우드 녹화 > 관련 요금](https://intl.cloud.tencent.com/document/product/647/35426)을 참조하십시오.
- 클라우드 녹화 전 CSS의 클라우드 혼합 스트림 기능을 사용한 경우 [라이브 방송 트랜스 코딩 > 표준 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/39604) 요금이 추가로 부과됩니다.


<span id="que11"></span>
### CDN 라이브 방송 시청은 어떻게 과금되나요?
TRTC는 릴레이 푸시 스트림을 통한 [CSS](https://intl.cloud.tencent.com/document/product/267)를 사용해 CDN 라이브 방송 시청 기능을 제공합니다. TRTC 요금은 청구되지 않으며, **CSS**는 실제 사용 현황에 따라 [CDN 라이브 방송 시청 > 관련 요금](https://intl.cloud.tencent.com/document/product/647/35242)을 청구합니다.

<span id="que12"></span>
### 방에 혼자 있어도 과금되나요?
방에 혼자 있는 경우, 푸시 스트림을 하지 않더라도(업스트림 데이터가 발생하지 않음) TRTC 클라우드 서비스 리소스를 차지합니다. 방에 혼자 있으면 다른 사람의 멀티미디어 스트림을 구독할 수 없어 비디오 화면을 수신할 수 없으므로, **음성 시간**으로 서비스 사용량을 통계합니다.

<span id="que13"></span>
### 후불을 직접 활성화할 수 없나요?
 [영상 통화](https://intl.cloud.tencent.com/document/product/647/39788), [음성 통화](https://intl.cloud.tencent.com/document/product/647/39787), [비디오 ILVB](https://intl.cloud.tencent.com/document/product/647/39786) 및 [음성 ILVB](https://intl.cloud.tencent.com/document/product/647/39785) 등 서비스의 후불은 구매한 패키지를 모두 사용하거나 기간이 만료된 경우에만 자동으로 활성화되며, 수동으로 활성화할 수 없습니다. Tencent Cloud의 영업 담당자와 후불로 계약하신 경우 영업 담당자에게 활성화를 요청하십시오.
