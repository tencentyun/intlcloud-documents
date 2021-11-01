본문은 멀티미디어 품질, 딜레이, 원활성, 안정성 및 CPU, 메모리, 전력 소모, 발열 등 개발자가 중요하게 여기는 핵심 지표를 중심으로, **정상**, **약한 네트워크 환경** 및 **다양한 실시간 인터랙션 시나리오(1v1, 1vN 등)**에서 객관적인 테스트 및 분석으로 결론을 도출합니다.

## 손실이 없는 약한 네트워크 환경에서의 효과 품질

### 테스트 시나리오

영상 통화 및 온라인 라이브 방송의 멀티미디어 시나리오와 음성 통화 시나리오.

### 매개변수 설정
- **영상 통화: **
<table><tr><th>매개변수 유형</th><th>설정 정보</th></tr>
<tr><td>해상도</td><td>368 × 640</td></tr>
<tr><td>비트 레이트</td><td>400Kbps</td>
</tr><tr>
<td>프레임 레이트</td><td>15</td>
</tr></table>
- **ILVB: **
<table><tr><th>매개변수 유형</th><th>설정 정보</th></tr>
<tr><td>해상도</td><td>720 × 1280</td></tr>
<tr>
<td>비트 레이트</td><td>1200Kbps</td>
</tr><tr>
<td>프레임 레이트</td><td>15</td>
</tr></table>



### 극한 네트워크 저항력 테스트 데이터
극한 네트워크 저항력 테스트는 각종 네트워크 손실 환경에서 SDK가 견딜 수 있는 최대 네트워크 손실을 테스트하는 것을 가리킵니다.
![](https://main.qcloudimg.com/raw/363a7f800bd4720c96cc8656a0eb6491.png)

>? 구체적인 손실 지표 및 의미는 [부록1: 멀티미디어 품질 지표 설명](#appendix1)을 참고하십시오.

### 약한 음성 네트워크 MOS 값
데이터 해석: TRTC는 매우 열악한 네트워크 환경에서 딜레이 시간이 더 짧아짐과 동시에 높은 음질을 보장합니다.
다음은 약한 네트워크 환경에서 진행한 객관적인 TRTC MOS 평가 결과입니다.
![](https://main.qcloudimg.com/raw/f7580010ffae2342bbba22967c9e514b.png)



## 클라이언트 SDK 성능 데이터

### 테스트 디바이스 정보
|  디바이스 유형  |  프로세서 유형 |   메모리  |
| ------------ | ----------- | ---- |
| Android 디바이스1 | Snapdragon 835-8코어 | 6G   |
| Android 디바이스2 | Kirin 980-8코어 | 8G   |
| iOS 디바이스1     | A8-듀얼코어     | 3G   |
| iOS 디바이스2     | A13-6코어     | 4G   |

### 테스트 매개변수 설정

| 매개변수 유형 | 설정 정보 |
| ------ | ------- |
| 해상도 | 240 × 320 |
| 비트 레이트   | 100kbps |
| 프레임 레이트   | 15      |

### 테스트 솔루션 설명

- **테스트 시나리오**: 1v1, 1v2, 1v3, 1v4, 1v8.
- **테스트 시간**: 각 시나리오 평균 30분.
- **테스트 솔루션**: Linux 푸시 스트리밍으로 다중 사용자 시나리오를 구성하여 모든 테스트 디바이스를 독립적으로 테스트합니다.

### 테스트 결과

데이터 해석: TRTC SDK는 CPU 사용률, 메모리 점유율, 발열, 전력 소모 등 각 항목의 성능이 좋아 비교적 점유율이 적은 하드웨어 리소스로 고품질의 멀티미디어 서비스를 제공할 수 있습니다.

- **App CPU 사용률: **
![](https://main.qcloudimg.com/raw/de4f28684d93db2964e4a97b6dcc9f7a.png)
- **App 메모리 사용률: **
![](https://main.qcloudimg.com/raw/a30a5ad382d3870db62a18c255dafc28.png)
- **시스템 총 CPU 사용률: **
![](https://main.qcloudimg.com/raw/d2dfc3d66296a38753002dc0982da26b.png)
- **시스템 총 메모리 사용률: **
![](https://main.qcloudimg.com/raw/f9446367302bf4d7afa14e2cbab7c64d.png)
- **30분 실행 전력 소모량: **
![](https://main.qcloudimg.com/raw/a9f18fae1440d7eaafc97adabc2ba888.png)
- **30분 실행 발열 증분: **
![](https://main.qcloudimg.com/raw/33b73b2194ef0cae9aba51b2e52f21b8.png)


[](id:appendix1)
## 부록1: 멀티미디어 네트워크 손실 지표 설명

<table>
<tr><th width="17%">네트워크 손실 지표</th><th width="50%">설명</th><th>예시</th>
</tr><tr>
<td>Loss</td>
<td>네트워크 패킷 손실</td>
<td>50% Loss는 10개의 패킷 중 5개의 손실을 의미</td>
</tr><tr>
<td>Delay</td>
<td>딜레이</td>
<td>200ms Delay, 즉 SDK 발송 패킷이 200ms 경과 후 네트워크로부터 발송됨</td>
</tr><tr>
<td>Jitter</td>
<td>지터</td>
<td>300 Jitter, 즉 SDK 발송 패킷은 임의로 20ms, 280ms, 50ms, 250ms 딜레이되어 발송될 확률이 있습니다. 최대 딜레이 시간 300ms, 평균 딜레이 시간 150ms입니다.</td>
</tr></table>

[](id:appendix2)
## 부록2: 네트워크 손실 시 성능 데이터 설명
<table>
<tr><th width="17%">성능 데이터</th><th width="50%">설명</th>
</tr><tr>
<td>MOS 값</td>
<td>통신 시스템 음성 품질 측정에 자주 사용되는 중요 지표로, 객관적인 MOS 값은 Spirent Nomad 디바이스를 도입하여 POLQA 점수를 매기며 점수가 높을수록 음질이 좋습니다.</td>
</tr><tr>
<td>end to end 딜레이</td>
<td>end to end 딜레이는 발신측 음성 수집부터 수신측에 재생될 때까지의 시간을 의미</td>
</tr><tr>
<td>극한 멀티미디어 저항력 테스트 표준</td>
<td>네트워크 손실 후 Spirent Nomad 디바이스를 사용한 <a href="#POLQA">POLQA</a> 점수와 foreman을 사용한 비디오를 순서대로 발송하여 수신측에서 프레임 간격을 검증합니다. 10분 이상 모니터링을 지속하며 30개의 데이터 지점을 획득합니다. <strong>3분 동안 3회 이상 오류가 감지되거나 </strong><strong>비교적 긴 시간 동안 사용할 수 없는 현상이 1회</strong> 발생할 경우 저항력이 초과되었다고 볼 수 있습니다.</td>
</tr></table>

>! POLQA(객관적인 음성 품질 감지 평가) 표준, 즉 ITU P.863 국제 표준을 기준으로 점수를 매긴 후 목소리 측정에 적용합니다. POLQA는 전 세계에서 통용되는 각종 네트워크 시나리오에 대한 음성 품질 분석 표준입니다. [](id:POLQA)


[](id:appendix3)
## 부록3: SDK 성능 지표 설명

<table>
<tr><th width="16%">지표 유형</th><th colspan=2>설명</th>
</tr><tr>
<td rowspan=2>App CPU 사용률</td>
<td>Android</td>
<td>App CPU는 프로세스에서 CPU 사용률을 표준화하지 않았음을 의미합니다. 통계 결과는 Android Studio Profiler와 일치합니다.</td>
</tr><tr>
<td>iOS</td>
<td>App CPU는 프로세스의 CPU 사용률을 의미합니다. 통계 결과는 Xcode와 일치합니다. <br><code>PerfDog 사용률 = Xcode 사용률 / 코어 수</code>.</td>
</tr><tr>
<td rowspan=2>시스템 CPU 사용률</td>
<td>Android</td>
<td>Total CPU는 기기에서 CPU 사용률을 표준화하지 않았음을 의미합니다. 통계 결과는 Android Studio Profiler와 일치합니다.</td>
</tr><tr>
<td>iOS</td>
<td>Total CPU는 기기의 CPU 사용률을 의미합니다. 통계 결과는 Xcode와 일치합니다. <br><code>PerfDog 사용률 = Xcode 사용률 / 코어 수</code>.</td>
</tr><tr>
<td rowspan=2>메모리 사용률</td>
<td>Android</td>
<td>PSS Memory, 통계 결과는 Android Java API 표준 결과와 일치하며, Meminfo와도 일치합니다.</td>
</tr><tr>
<td>iOS</td>
<td>Xcode Memory, XCode Debug gauges 통계 방식입니다.</td>
</tr><tr>
<td>전력 소모량</td>
<td colspan=2>테스트 시 모니터링 전력량이 100%에서 99%로 떨어지는 때부터 기록합니다. 종료 전력량 값을 설정하여 비율에 따라 30분간 소모되는 전력량을 계산합니다.</td>
</tr><tr>
<td>발열 증분</td>
<td colspan=2>App을 실행하지 않은 상태에서 온도계로 현재 온도를 측정하고, App 실행 후 시나리오마다 30분간 실행합니다. <br><code>발열 증분 = 30분 후의 온도 - App을 실행하지 않았을 때의 온도</code>.</td>
</tr></table>
