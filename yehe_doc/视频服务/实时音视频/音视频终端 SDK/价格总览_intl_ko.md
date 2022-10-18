## 과금 방식

Tencent Cloud의 Media SDK(RT-Cube) 기능을 사용하려면 해당 License 리소스를 구매해야 합니다.

>! SDK의 기능에 대한 자세한 내용은 [SDK 다운로드](https://www.tencentcloud.com/document/product/647/34615)를 참고하십시오.

<table>
<thead>
<tr>
<th colspan="2" width="40%">과금 항목</th>
<th>과금 관련 설명</th>
<th width="22%">결제 방식</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="4">SDK License</td>
<td>라이브 스트림 게시 License</td>
<td>이 License는 <b>라이브 스트림 게시 + 동영상 재생</b> 기능을 활성화할 수 있습니다.</td>
<td><ul style="margin:0">
<li><a href="#live_license">라이브 스트림 게시 License 요금</a><br></li></td>
</tr>
<tr>
<td>UGSV License</td>
<td>이 License는 <b>UGSV + 동영상 재생</b> 기능을 활성화할 수 있습니다.</td>
<td><ul style="margin:0">
<li><a href="#ugsv_license">UGSV License 요금</a><br></li></td>
</tr>
<tr>
<td>동영상 재생 License</td>
<td>이 License는 <b>동영상 재생</b> 기능을 활성화할 수 있습니다.</td>
<td><ul style="margin:0">
<li><a href="#play_license">동영상 재생 License 요금</a></li></td>
</tr>
</tbody></table>

Media SDK와 함께 Tencent Cloud 서비스를 사용하는 경우에도 요금이 발생합니다.

<table>
<thead>
<tr>
<th colspan="2" width="40%">과금 항목</th>
<th>과금 관련 설명</th>
<th width="22%">결제 방식</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="4">Tencent Cloud 서비스</td>
<td>Cloud Streaming Services(CSS)</td>
<td>CSS를 Media SDK의 라이브 스트림 게시 및 동영상 재생 기능과 함께 사용하여 실시간 스트림을 클라우드에 신속하게 게시하여 처리 및 전달하는 경우 CSS 서비스 요금이 발생합니다.</td>
<td><a href="https://www.tencentcloud.com/document/product/267/2819">CSS 가격 리스트</a></td>
</tr>
<tr>
<td>Tencent Real-Time Communication(TRTC)</td>
<td>음성/영상 통화, 그룹 회의 및 양방향 라이브 스트리밍과 같은 기능을 구현하기 위해 Media SDK를 사용하는 경우 TRTC 서비스 요금이 발생합니다.</td>
<td><a href="https://www.tencentcloud.com/document/product/647/34610">TRTC 가격 리스트</a></td>
</tr>
<tr>
<td>Video on Demand(VOD)</td>
<td>VOD를 Media SDK와 함께 사용하여 라이브 녹화, 재생, 단편 동영상 편집, 동영상 저장, 동영상 배포 등의 기능을 구현하는 경우 VOD 서비스 요금이 발생합니다.</td>
<td><a href="https://www.tencentcloud.com/document/product/266/2838">VOD 가격 리스트</a></td>
</tr>
<tr>
<td>Instant Messaging(IM)</td>
<td>Tencent Cloud의 IM 서비스를 Media SDK와 함께 사용하여 방 관리, 화면 댓글, 홍바오/선물하기 및 메시지와 같은 기능을 구현하는 경우 IM 서비스 요금이 발생합니다.</td>
<td><a href="https://www.tencentcloud.com/document/product/1047/34349">IM 가격 리스트</a></td>
</tr>
</tbody></table>

[](id:license)

## SDK License

### 기본 서비스 요금

License를 사용하여 Media SDK의 다양한 기능 모듈에 대한 액세스를 관리합니다. 현재 **라이브 스트림 게시**, **UGSV** 및 **동영상 재생** 기능을 사용하려면 라이선스가 필요합니다. **UGSV의 경우 UGSV Standard 및 UGSV Lite의 두 가지 유형의 라이선스를 제공합니다.**

- 라이브 스트림 게시 License는 **라이브 스트림 게시 및 동영상 재생** 기능을 활성화할 수 있습니다.
- UGSV License는 **UGSV 및 동영상 재생** 기능을 활성화할 수 있습니다.
- 동영상 재생 License는 **동영상 재생** 기능을 활성화할 수 있습니다.

**License를 구매**하여 해당 기능을 활성화할 수 있습니다. 구매한 License는 **애플리케이션에 바인딩한 후 1년 동안 유효하며 1년 후의 익일 00:00:00에 만료됩니다**. 또는 **패키지를 구매하면 라이브 방송 License, UGSV License 또는 동영상 재생 License를 무료로 받을 수 있습니다**. 이러한 License는 **패키지를 구매한 후 1년 동안 유효합니다(1년 후의 익일 00:00:00에 만료됨)**.

>! 동영상 재생 License는 Media SDK 10.1 버전(2022년 5월 말 출시)에 도입되었습니다.

#### 라이브 스트림 게시 License 가격[](id:live_license)

<table>
<thead>
<tr>
<th>License 유형</th>
<th>유효 기간</th>
<th>기능</th>
<th>가격(USD)</th>
<th>획득 방법</th>
</tr>
</thead>
<tbody><tr>
<td>라이브 방송 License <br>(<b>평가판</b>)</td>
<td>28일</td>
<td rowspan=2>라이브 스트림 게시 + 동영상 재생</td>
<td>0</td>
<td><a href="https://console.tencentcloud.com/vod/license">무료 신청</a></td>
</tr>
<tr>
<td >라이브 스트림 게시 License</td>
<td >1년</td>
<td>5,988</td>
<td r><a href="https://buy.tencentcloud.com/license">구매하기</a></td>
</tbody></table>



#### UGSV License 가격[](id:ugsv_license)

<table>
<thead>
<tr>
<th>License 유형</th>
<th>유효 기간</th>
<th>능력</th>
<th>가격(USD)</th>
<th>획득 방법</th>
</tr>
</thead>
<tbody><tr>
<td>UGSV Standard License <br>(<strong>평가판</strong>)</td>
<td>28일</td>
<td>UGSV(Standard) + 동영상 재생</td>
<td>0</td>
<td><a href="https://console.tencentcloud.com/vod/license">무료 신청</a></td>
</tr>
<tr>
<td>UGSV Lite License</td>
<td>1년</td>
<td>UGSV(Lite) + 동영상 재생</td>
<td>1,899</td>
<td rowspan=3><a href="https://buy.tencentcloud.com/license">구매하기</a></td>
</tr>
<tr>
</tr>
<tr>
<td rowspan=2>UGSV Standard License</td>
<td rowspan=2>1년</td>
<td rowspan=2>UGSV(Standard) + 동영상 재생</td>
<td>9,999</td>
</tr>
</tbody></table>

>? UGSV Standard는 필터, 특수 효과 및 전환 효과와 같은 추가 기능을 제공하여 모바일 장치용 쇼트 비디오 애플리케이션을 쉽게 구축할 수 있도록 도와줍니다. 자세한 내용은 [Different Editions of the UGSV SDK](https://www.tencentcloud.com/document/product/1069/37914)를 참고하십시오.

#### 동영상 재생 License 가격[](id:play_license)

**동영상 재생** License는 모바일 장치(Android & iOS & Flutter)용 Media SDK 10.1 버전(2022년 5월 말 출시)에 도입되었습니다.

- **App이 이미 라이브 방송 License(기존 라이브 스트림 게시 License) 또는 UGSV License에 바인딩되어 있는 경우 v10.1로 업데이트한 후에도 해당 기능을 계속 사용할 수 있습니다**.
- 애플리케이션이 라이브 방송 License(기존 라이브 스트림 게시 License) 또는 UGSV License에 바인딩되지 않은 경우 **새 SDK의 라이브 또는 VOD 재생 기능을 사용하려면 동영상 재생 License를 구매해야 합니다**. 자세한 내용은 [기능 활성화](#warrant)를 참고하십시오.
- 동영상 재생 기능을 사용하지 않거나 SDK를 업데이트하지 않는 경우 변경 사항의 영향을 받지 않습니다.

<table>
<thead>
<tr>
<th width=15%>License 유형</th>
<th>유효 기간</th>
<th>능력</th>
<th width=10%>가격<br>(USD/년)</th>
<th>획득 방법</th>
</tr>
</thead>
<tbody><tr>
<td>동영상 재생(평가판)</td>
<td>28일</td>
<td rowspan=2>동영상 재생</td>
<td rowspan=2>0</td>
<td rowspan=2><a href="https://console.tencentcloud.com/vod/license">무료 신청</a></td>
</tr>
<tr>
<td>동영상 재생(정식 버전)</td>
<td>1년</td>
</tr>
</tbody></table>

[](id:warrant)

#### 기능 활성화

10.1 버전(2022년 5월 말 출시) 이상 버전에서는 라이브 방송(기존 라이브 스트림 게시 License), UGSV 또는 동영상 재생 세 가지 License 중 **임의의** License를 사용하여 **동영상 재생** 기능(라이브 및 VOD 재생)을 활성화할 수 있습니다. **임의의 1개의** License를 구입하여 신규 버전 SDK의 라이브 방송 및 VOD 재생 기능을 정상적으로 사용할 수 있습니다. 각 License별 활성화할 수 있는 기능에 대한 자세한 내용은 아래 표를 참고하십시오.

<table>
<thead>
<tr>
<th rowspan="2" width=20%>License</th>
<th colspan="3">기능</th>
<th rowspan="2">획득 방법</th>
</tr><tr>
<th>라이브 스트림 게시</th>
<th>UGSV</th>
<th>동영상 재생</th>
</tr>
</thead>
<tbody>
<tr>
<td>라이브 스트림 게시 License</td>
<td>&#10003; </td>
<td>-</td>
<td>&#10003; </td>
<td><ul style="margin:0">
<li>라이브 방송 License 구매(1년 동안 유효)</li></ul></td>
</tr>
<tr>
<td>UGSV License</td>
<td>-</td>
<td>&#10003; </td>
<td>&#10003; </td>
<td><ul style="margin:0">
<li>UGSV License 구매(1년 동안 유효)</li></ul></td>
</tr>
<tr>
<td>동영상 재생 License</td>
<td>-</td>
<td>-</td>
<td>&#10003; </td>
<td><ul style="margin:0">
<li>동영상 재생 License 무료 신청(1년 유효)</li></ul></td>
</tr>
</tbody></table>

#### 과금 설명

- 각 Tencent Cloud 계정은 라이브 방송 License 1개, UGSV License 1개, 동영상 재생 License 1개를 **1회 무료 신청**하여 해당 기능을 시험해 볼 수 있습니다. 평가판 License는 14일 동안 유효합니다. 콘솔에서 유효 기간을 14일 더 연장할 수 있습니다(총 28일).
- License는 새 애플리케이션에 바인딩되거나 기존 License를 대체할 수 있습니다. 교체 후 새 License의 만료 시간이 적용됩니다. 원래 License는 애플리케이션에서 자동으로 바인딩 해제됩니다. 유효 기간은 변경되지 않습니다.
- 유효성 정보:
  - 패키지를 구매하시면 패키지 소진 여부와 관계없이 **구매일로부터** 1년 동안(1년 후의 익일 00:00:00 만료) 유효합니다. 트래픽 패키지의 소진은 바인딩된 라이선스의 사용에 영향을 미치지 않으며 바인딩된 리소스 패키지를 변경하여 License를 갱신할 수 있습니다.
  - License를 구매한 후에는 애플리케이션에 바인딩할 때까지 License가 비활성화됩니다. 구매한 License는 **애플리케이션에 바인딩한 후** 1년 동안 유효합니다(1년 후의 익일 00:00:00에 만료됨).
- **각 License는 개발 환경에서 사용하든 프로덕션 환경에서 사용하든 상관없이 하나의 iOS Bundle ID와 하나의 Android Package Name으로 바인딩될 수 있습니다.** Media SDK를 여러 애플리케이션과 함께 사용하려면 여러 License를 구매해야 합니다.

- **패키지 구매 후, 패키지에 포함된 License만 환불할 수 없습니다. License는 애플리케이션에 바인딩되면 사용된 것으로 간주되며 패키지에는 5일 무조건 환불 정책이 더 이상 적용되지 않습니다.**
- **구매한 License는 애플리케이션에 바인딩된 후에는 환불되지 않습니다.**

>! 패키지는 사용한 후(소진 여부) 또는 구매 후 5일이 지난 경우 환불되지 않습니다.


### 부가 서비스 요금

[](id:value)

**License 요금 외에도 Media SDK를 사용하면 다음과 같은 서비스 요금이 발생할 수 있습니다. 필요에 따라 사용 및 구입하시기 바랍니다.**

## Cloud Streaming Services(CSS)

Media SDK의 라이브 스트림 게시 및 동영상 재생 기능은 백엔드에 의존하여 라이브 스트림을 수신, 처리 및 제공합니다. [CSS](https://www.tencentcloud.com/products/css) 사용을 권장합니다.

CSS는 라이브 스트림 수신, 온-클라우드 녹화, 라이브 트랜스코딩, 라이브 화면 캡처, 라이브 스트림 전달 및 재생을 포함한 기능을 제공합니다.

- CSS를 사용하여 라이브 스트림을 수신 및 전달하는 경우 기본 서비스 요금이 발생하며, 이는 소비된 트래픽/대역폭에 따라 부과됩니다.
- 라이브 트랜스코딩(스트림 믹싱 및 워터마킹 포함), 라이브 녹음, 라이브 화면 캡처, RTC 기반 공동 앵커링 및 CDN으로 중계와 같은 CSS 기능을 사용하면 부가 서비스 요금이 발생합니다.

>? CSS 과금에 대한 자세한 내용은 [가격 리스트](https://www.tencentcloud.com/document/product/267/2819)를 참고하십시오.


## Tencent Real-Time Communication(TRTC)

[TRTC](https://www.tencentcloud.com/products/trtc) Media SDK를 사용하여 음성/영상 통화, 그룹 회의, 양방향 라이브 스트리밍 등의 기능을 구현하는 경우 서비스 요금이 발생합니다.

TRTC 과금:

- 기본 서비스 요금은 음성/영상 라이브 스트리밍 세션 또는 음성/영상 통화 시간에 따라 부과됩니다.
- 온클라우드 레코딩, 온클라우드 믹스 트랜스코딩 등의 TRTC 서비스 이용 시 부가 서비스 요금이 발생합니다.

>? TRTC 결제에 대한 자세한 내용은 [과금 개요](https://www.tencentcloud.com/document/product/647/34610)를 참고하십시오.

## Video on Demand(VOD)

Tencent Cloud의 [VOD](https://www.tencentcloud.com/products/vod) 서비스를 이용하여 라이브 스트림을 녹화 및 재생하거나 편집 후 쇼트 비디오를 저장 및 배포할 수 있습니다.

VOD 과금:

- VOD에 업로드된 파일 및 트랜스코딩 출력에 사용된 저장 공간에 따라 스토리지 요금이 부과됩니다.
- VOD에 저장된 파일을 트랜스코딩하는 경우 대상 파일의 사양 및 지속 시간에 따라 트랜스코딩 요금이 부과됩니다.
- VOD의 가속 서비스를 이용하여 동영상을 전송하는 경우 재생에 소모된 트래픽에 따라 가속 요금이 부과됩니다.

>? VOD 결제에 대한 자세한 내용은 [과금 개요](https://www.tencentcloud.com/document/product/266/2838)를 참고하십시오.

## Instant Messaging(IM)

Tencent Cloud의 [IM](https://www.tencentcloud.com/products/im) 을 사용하여 방 관리, 화면 댓글, 홍바오/선물 보내기 및 메시지와 같은 기능을 구현할 수 있습니다. 결제에 대한 자세한 내용은 [과금 개요](https://www.tencentcloud.com/document/product/1047/34349)를 참고하십시오.

>!
>- 메시징 기능은 IM의 오디오/비디오 그룹(AvChatRoom) 기능에 의존합니다. 생성할 수 있는 오디오/비디오 그룹의 최대 수는 구매하는 IM 플랜 및 부가 서비스에 따라 다릅니다.
>- Tencent Cloud의 IM을 사용하여 화면 댓글, 메시지, 홍바오/선물 보내기와 같은 기능을 구현할 수 있습니다. 자체 솔루션을 개발하거나 타사 서비스를 사용할 수도 있습니다.
>- IM에는 기능을 시험해 볼 수 있는 무료 버전이 있습니다. 실제 필요에 따라 요금제 또는 부가 서비스를 구매할 수 있습니다.
