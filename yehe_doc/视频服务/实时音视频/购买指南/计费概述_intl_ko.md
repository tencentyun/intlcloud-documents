TRTC 서비스 항목은 유형에 따라 크게 **기본 서비스**와 **부가 서비스**로 나뉩니다.

## 기본 서비스

응용 시나리오에 따라 음성 ILVB, 비디오 ILVB, 음성 통화, 영상 통화로 나뉩니다. 4가지 기본 서비스는 개별적으로 사용할 수도 있고, 중복하여 사용할 수도 있습니다. 다음은 4가지 기본 서비스에 대한 과금 설명입니다.

<table>
<tr><th>서비스</th><th>서비스 설명</th><th>과금 설명</th></tr>
<tr>
<td>음성 ILVB</td>
<td><ul style="margin:0">
<li>호스트와 시청자의 마이크를 통한 음성 인터랙션을 지원합니다.</li>
<li>호스트 크로스 룸(라이브 룸 간) PK를 지원합니다.</li>
<li>매끄러운 마이크 On/Off 전환을 지원합니다. 호스트 딜레이는 300ms 미만입니다.</li>
<li>방의 마이크 수는 무제한으로 연결이 가능하며, 최대 30명까지 마이크 동시 연결이 가능합니다.</li>
<li>저 딜레이 라이브 방송 모드에서 시청자 10만 명의 동시 재생을 지원합니다. 재생 딜레이는 1000ms 수준입니다.</li>
<li>CDN 릴레이 라이브 방송 모드에서 시청자 수는 무제한입니다.</li>
</ul></td>
<td><a href="https://cloud.tencent.com/document/product/647/44248">음성 ILVB 과금 설명</a></td>
</tr>
<tr>
<td>비디오 ILVB</td>
<td><ul style="margin:0">
<li>호스트와 시청자의 비디오와 마이크를 통한 인터랙션을 지원합니다.</li>
<li>호스트 크로스 룸(라이브 룸 간) PK를 지원합니다.</li>
<li>매끄러운 마이크 On/Off 전환을 지원합니다. 호스트 딜레이는 300ms 미만입니다.</li>
<li>방의 마이크 수는 무제한으로 연결이 가능하며, 최대 30명까지 마이크 동시 연결이 가능합니다.</li>
<li>저 딜레이 라이브 방송 모드에서 시청자 10만 명의 동시 재생을 지원합니다. 재생 딜레이는 1000ms 수준입니다.</li>
<li>CDN 릴레이 라이브 방송 모드에서 시청자 수는 무제한입니다.</li>
</ul></td>
<td><a href="https://cloud.tencent.com/document/product/647/44247">비디오 ILVB 과금 설명</a></td>
</tr>
<tr>
<td>음성 통화</td>
<td><ul style="margin:0">
<li>2인 이상의 그룹 음성 통화는 48kHz와 스테레오 사운드 채널을 지원합니다.</li>
<li>방은 최대 300명의 동시 접속이 가능하며, 최대 30명이 동시에 마이크를 활성화할 수 있습니다.</li>
</ul></td>
<td><a href="https://cloud.tencent.com/document/product/647/44226">음성 통화 과금 설명</a></td>
</tr>
<tr>
<td>영상 통화</td>
<td><ul style="margin:0">
<li>2인 이상의 그룹 영상 통화는 720P, 1080P의 고화질을 지원합니다.</li>
<li>방은 최대 300명의 동시 접속이 가능하며, 최대 30명이 동시에 카메라를 활성화할 수 있습니다.</li></ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39788">영상 통화 과금 설명</a></td>
</tr>
</table>

## 부가 서비스

부가 서비스는 기본 네 가지 서비스에 추가 제공되는 서비스로, 단독으로는 사용할 수 없으며 서비스 사용 시 추가 요금을 지불해야 합니다. TRTC는 부가 서비스로 **클라우드 녹화**와 **클라우드 혼합 스트림 트랜스 코딩** 서비스를 제공합니다. 다음은 부가 서비스에 대한 과금 설명입니다.

| 서비스                                                              | 서비스 설명                                                      | 과금 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/35426) | 릴레이 푸시 스트림 방식으로 **CSS** 기능을 사용해 전체 과정에 대한 클라우드 녹화(녹음/녹화) 기능을 제공합니다. 녹화 파일은 **VOD**에 저장되며, 언제든지 다운로드 또는 재생할 수 있습니다. |[클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385) |
| [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618) | MCU 클러스터를 사용해 TRTC 방의 각 채널에서 업스트림한 멀티미디어 스트림을 필요에 따라 혼합 스트림 트랜스 코딩합니다. 트랜스 코딩 후 출력된 멀티미디어 스트림은 릴레이 푸시 스트림을 통해 CSS에서 **클라우드 녹화** 또는 **CDN 라이브 방송 시청**이 가능합니다. | [클라우드 혼합 스트림 트랜스 코딩 과금 설명](https://intl.cloud.tencent.com/document/product/647/38929) |

## 무료 베타 테스트

2019년 10월 11일부터 [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 처음으로 애플리케이션을 생성하는 Tencent Cloud 계정에 10,000분 무료 베타 패키지를 증정합니다. 무료 패키지는 [영상 통화](https://intl.cloud.tencent.com/document/product/647/39788), [음성 통화](https://intl.cloud.tencent.com/document/product/647/39787), [비디오 ILVB](https://intl.cloud.tencent.com/document/product/647/39786), [음성 ILVB](https://intl.cloud.tencent.com/document/product/647/39785) 서비스 용량을 차감하는 방식으로 사용할 수 있습니다. 자세한 내용은 [무료 베타 테스트](https://intl.cloud.tencent.com/document/product/647/39784)를 참조하십시오.
