본문은 고급 라이브 스트리밍 기능을 프로그램으로 가져오는 방법을 설명합니다.

## AV1 비디오 재생
AV1은 로열티가 없는 오픈 소스 비디오 압축 형식입니다. 이전 H.265[HEVC] 인코딩과 비교하여 동일한 수준의 화질을 유지하면서 비트레이트를 30% 이상 더 줄일 수 있습니다. 이는 동일한 대역폭에서 더 높은 이미지 품질을 제공할 수 있음을 의미합니다. 현재 CSS는 AV1 인코딩을 지원합니다. 그러나 AV1 비디오를 재생하려면 플레이어가 AV1 형식 디코딩을 지원해야 합니다.
다음과 같이 자체 플레이어에서 AV1 디코딩을 구현할 수 있습니다.

### 컨테이너 형식 및 배포 프로토콜
Tencent Cloud는 AV1 in FLV에 대한 독점 확장(in T-FFmpeg)을 구현했습니다. 플레이어를 수정하려면 T-FFmpeg의 [Patch 파일](https://github.com/tencentyun/AV1/tree/main/patch)을 기반으로 코드를 확장할 수 있습니다. 자세한 내용은 [tencentyun/AV1](https://github.com/tencentyun/AV1)을 참고하십시오.

### 디코딩
- **하드웨어 디코딩**
PC에서 AMD, Intel 및 Nvidia GPU의 거의 모든 새 모델은 AV1 하드웨어 디코딩을 지원합니다.
AV1 하드웨어 디코딩을 지원하는 장치 모델은 다음과 같습니다.
<table>
<thead>
<tr>
<th>유형</th>
<th>브랜드</th>
<th>프로세서</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=23>휴대폰</td>
<td>realme X7 Pro</td><td>Dimensity 1000+</td>
</tr><tr>
<td>oppo reno 5 pro</td><td>Dimensity 1000+</td>
</tr><tr>
<td>HONOR v40</td><td>Dimensity 1000+</td>
</tr><tr>
<td>Redmi k30 Ultra</td><td>Dimensity 1000+</td>
</tr><tr>
<td>vivo iQOO Z1</td><td>Dimensity 1000+</td>
</tr><tr>
<td>Redmi Note 10 Pro</td><td>Dimensity 1000+</td>
</tr><tr>
<td>vivo S9</td><td>Dimensity 1100</td>
</tr><tr>
<td>realme Q3 Pro</td><td>Dimensity 1100</td>
</tr><tr>
<td>vivo s10</td><td>Dimensity 1100</td>
</tr><tr>
<td>vivo s12</td><td>Dimensity 1100</td>
</tr><tr>
<td>vivo s12 pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>OPPO Reno6 Pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>OPPO Reno7 Pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>Redmi K40 pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>realme GT Neo</td><td>Dimensity 1200</td>
</tr><tr>
<td>HONOR X20</td><td>Dimensity 1200</td>
</tr><tr>
<td>OnePlus Nord 2</td><td>Dimensity 1200</td>
</tr><tr>
<td>realme GT Neo2</td><td>Dimensity 1200</td>
</tr><tr>
<td>OPPO K9 Pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>OPPO Find X5 Pro Dimensity 버전</td><td>Dimensity 9000</td>
</tr><tr>
<td>Redmi K50</td><td>Dimensity 9000</td>
</tr><tr>
<td>Galaxy S21(삼성 Exynos 버전)</td><td>Exynos 2100</td>
</tr><tr>
<td>Galaxy S22(삼성 Exynos 버전)</td><td>Exynos 2200</td>
</tr><tr>
<td>TV</td><td>삼성 Q950TS QLED 8K TV</td><td>-</td>
</tr>
</tbody></table>

- **소프트웨어 디코딩**
	- av1d (Tencent Cloud의 최적화된 AV1 디코더로 dav1d를 능가하며 폐쇄 소스 라이브러리를 제공할 수 있습니다. [av1d 통합 가이드](https://doc.weixin.qq.com/doc/w3_APEAMQbpAEs1nkQ8rfiR02j8K8srn?scode=AJEAIQdfAAo21jd3VvAPEAMQbpAEs&version=4.0.8.6617&platform=win)의 지침에 따라 통합할 수 있습니다. T-FFmpeg는 통합할 FFmpeg Patch와 av1d 라이브러리를 제공합니다.
	- [dav1d](https://code.videolan.org/videolan/dav1d) 
	- libgav1
	- Android 10.0은 AV1 디코더를 통합합니다
	- Chrome 제품군은 AV1 디코딩을 지원합니다

### 브라우저 지원
Chrome 제품군은 AV1 디코딩을 지원하지만 iOS의 브라우저는 지원하지 않습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5e2045b9c9f721306675c3f812a52d04.png)
>! 상기 정보는 2022년 7월에 [AVI 웹사이트](https://caniuse.com/?search=AV1)에서 수집한 것입니다. 최신 정보를 보려면 웹사이트를 방문하십시오.

## MediaConnect SDK (TMIO SDK)
TMIO SDK는 SRT 및 QUIC와 같은 스트리밍 미디어 프로토콜을 사용자 지정, 캡슐화 및 최적화합니다. 업스트림을 보호하고 높은 패킷 손실 방지율, 다중 연결 전송 최적화 및 RTO(재전송 시간 초과) 메커니즘으로 지연 시간이 짧은 전송을 구현합니다. 높은 데이터 소스 안정성과 장거리 전송이 필요한 시나리오에서 폭넓은 적용을 약속합니다.

### 기능 소개
- TMIO SDK는 장거리 전송 및 라디오 및 TV 산업에 적합합니다.
- TMIO SDK는 Android, iOS, Windows, MacOS 및 Linux를 포함한 주요 플랫폼을 지원합니다.

### 통합 방식
[TMIO SDK](https://www.tencentcloud.com/document/product/267/51158)의 안내에 따라 SDK를 연동할 수 있습니다.


## libLebConnection SDK
libLebConnection SDK는 기본 WebRTC를 기반으로 업그레이드된 전송 기능을 제공합니다. 몇 가지 간단한 수정만으로 기존 플레이어를 LEB에 연결할 수 있습니다. LVB 호환 스트림 푸시 및 클라우드 기반 미디어 처리 기능을 기반으로 높은 동시성에서도 저지연 라이브 스트리밍을 구현할 수 있으므로 표준 LVB 스트리밍에서 지연 시간이 짧은 LEB 스트리밍으로 원활하게 마이그레이션할 수 있습니다. 최신 RTC(실시간 통신) 시나리오의 대형 회의실의 경우 저렴한 비용과 낮은 대기 시간으로 릴레이된 라이브 스트리밍을 신속하게 구현하는 데 도움이 될 수도 있습니다.

### 기능 소개
- libLebConnection SDK는 약한 네트워크 조건에서도 짧은 대기 시간으로 오디오/비디오 스트림을 가져올 수 있습니다.
- B 프레임이 있는 H.264, H.265 및 AV1 비디오를 재생하고 각각 H.264/H.265 및 AV1 입력 비디오에 대한 AnnexB 및 OBU 파일과 같은 원시 비디오 프레임 데이터로 출력할 수 있습니다.
- AAC 및 OPUS 오디오를 재생하고 원시 오디오 프레임 데이터로 출력할 수 있습니다.
- Android, iOS, Windows, Linux 및 Mac을 지원합니다.

### 통합 방식
[플레이어에 libLebConnection SDK 통합](https://www.tencentcloud.com/document/product/267/51159#.E6.8E.A5.E5.85.A5.E6.96.B9.E5.BC.8F)의 지침에 따라 libLebConnection SDK를 통합할 수 있습니다.

### 특수 효과 및 뷰티 필터
뷰티 필터와 특수 효과를 통합하고 라이브 스트리밍 중에 뷰티 필터, 이미지 필터 및 스티커를 가져오려면 Tencent Cloud · Tencent 특수 효과 엔진(Tencent Effect) SDK를 통합할 수 있습니다.

### App에 통합
[여기](https://www.tencentcloud.com/document/product/1143/45377)에서 Tencent 특수 효과 엔진(Tencent Effect) SDK를 다운로드하고 [iOS](https://www.tencentcloud.com/document/product/1143/45387) & [Android](https://www.tencentcloud.com/document/product/1143/45388) 통합 가이드의 지침에 따라 통합합니다.


## 더 보기
[Tencent Effect SDK](https://www.tencentcloud.com/document/product/1143/45377)를 사용하면 요금이 발생합니다. 자세한 내용은 [가격 리스트](https://www.tencentcloud.com/document/product/1143/45371)를 참고하십시오.