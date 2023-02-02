본문은 개발자가 쉽게 통합하고 디버깅할 수 있도록 음성 채팅의 이퀄라이저용 Game Multimedia Engine(GME) API에 대해 설명합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/72bd34689aed95d320d1e655a5f1a049.png" width="80%" >



## 시나리오

GME 이퀄라이저 기능은 GME SDK에서 실시간으로 캡처한 오디오 스트림의 이퀄라이저를 조정할 수 있습니다. 이 기능은 온라인 노래방 시나리오에 적용할 수 있습니다. 플레이어가 노래를 시작한 후 **GME SDK**의 **이퀄라이저** API를 호출하여 플레이어의 실시간 오디오 스트림을 조정합니다.


## 전제 조건

- **음성 채팅 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME SDK에 액세스**: 핵심 API 및 음성 채팅 API에 대한 액세스를 포함합니다. 자세한 내용은 [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.


## Demo

## Demo 다운로드

[다운로드 주소 >>](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.8.4/Windows/PC_Release_ForTest.zip)

이 무료 Demo는 Windows 실행 프로그램입니다.

![](https://qcloudimg.tencent-cloud.cn/raw/f00d59d614ce32aa6ae1e702f6a3cc6b.png)


### 매개변수 구성

입력 상자에 GME AppID 및 Key를 입력할 수 있습니다.

대상 방 ID와 OpenID를 입력할 수도 있습니다.

### 사용 방법

1. 다음 단계에 따라 마이크와 스피커를 엽니다. Init > EnterRoom > EnableCapture > EnablePlay > EnableSend > EnableRecv.
2. 방에 성공적으로 입장한 후 **EnableLoopBack**을 활성화하면 음성을 들을 수 있습니다.
3. **EQ**를 조정합니다. (EQ는 주파수 구간 게인, Exditor 및 Reverb는 리버브레이터)




## 이퀄라이저 기능 통합
방에 성공적으로 입장한 후에야 API가 로컬에서 캡처한 사운드에 이퀄라이저를 사용할 수 있습니다.

###  함수 프로토타입  
```
int SetKaraokeType(ITMG_VOICE_TYPE_EQUALIZER* pEqualizer, ITMG_VOICE_TYPE_REVERB* pReverb)
```

|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| pEqualizer|ITMG_VOICE_TYPE_EQUALIZER|주파수 밴드 게인|
| pReverb|ITMG_VOICE_TYPE_REVERB|HARMONIC 및 REVERB 커버|

### 구조 세부 정보
**ITMG_VOICE_TYPE_EQUALIZER의 구조 구성원은 float 유형입니다. 값 범위는 -12에서 12까지입니다.**

|ITMG_VOICE_TYPE_EQUALIZER      |설명|
| ------------- |:-------------:|
|EQUALIZER_32HZ|32HZ 밴드에 적용되는 게인|
|EQUALIZER_64HZ|64HZ 밴드에 적용되는 게인|
|EQUALIZER_128HZ        |128HZ 밴드에 적용되는 게인|
|EQUALIZER_250HZ        |250HZ 밴드에 적용되는 게인|
|EQUALIZER_500HZ        |500HZ 밴드에 적용되는 게인|
|EQUALIZER_1KHZ         |1KHZ 밴드에 적용되는 게인|
|EQUALIZER_2KHZ         |2KHZ 밴드에 적용되는 게인|
|EQUALIZER_4KHZ         |4KHZ 밴드에 적용되는 게인|
|EQUALIZER_8KHZ         |8KHZ 밴드에 적용되는 게인|
|EQUALIZER_16KHZ        |16KHZ 밴드에 적용되는 게인|
|EQUALIZER_MASTER_GAIN  |전체 볼륨|

**ITMG_VOICE_TYPE_REVERB의 구조 구성원은 float 유형입니다. 값 범위는 0에서 1까지입니다.**


|ITMG_VOICE_TYPE_REVERB      |
|-------------|
|HARMONIC_GAIN				|
|HARMONIC_START_FREQUENCY	|
|HARMONIC_BASS_CONTROL		|
|REVERB_SIZE				|
|REVERB_DEPTH				|
|REVERB_GAIN				|
|REVERB_ECHO_DEPTH			|


### 예시 코드

```
void CTMGSDK_For_AudioDlg::OnVScroll(UINT nSBCode, UINT nPos, CScrollBar* pScrollBar)
{
	if ((CWnd*)pScrollBar == (CWnd*)&m_SliderEQ1 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ2 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ3 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ4 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ5 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ6 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ7 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ8 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ9 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ10 || 
		(CWnd*)pScrollBar == (CWnd*)&m_SliderEQ11 ||
		(CWnd*)pScrollBar == (CWnd*)&m_SliderExGain ||
		(CWnd*)pScrollBar == (CWnd*)&m_SliderExStartFrequency ||
		(CWnd*)pScrollBar == (CWnd*)&m_SliderExBaseCtrl ||
		(CWnd*)pScrollBar == (CWnd*)&m_SliderReverbSize ||
		(CWnd*)pScrollBar == (CWnd*)&m_SliderReverbDepth ||
		(CWnd*)pScrollBar == (CWnd*)&m_SliderReverbGain ||
		(CWnd*)pScrollBar == (CWnd*)&m_SliderReverbEchoDepth
		)
	{
		ITMG_VOICE_TYPE_EQUALIZER equalizer = {
			(m_SliderEQ1.GetPos() - 50)  * 24.0f / 100,
			(m_SliderEQ2.GetPos() - 50)  * 24.0f / 100,
			(m_SliderEQ3.GetPos() - 50)  * 24.0f / 100,
			(m_SliderEQ4.GetPos() - 50)  * 24.0f / 100,
			(m_SliderEQ5.GetPos() - 50)  * 24.0f / 100,
			(m_SliderEQ6.GetPos() - 50)  * 24.0f / 100,
			(m_SliderEQ7.GetPos() - 50)  * 24.0f / 100,
			(m_SliderEQ8.GetPos() - 50)  * 24.0f / 100,
			(m_SliderEQ9.GetPos() - 50)  * 24.0f / 100,
			(m_SliderEQ10.GetPos() - 50) * 24.0f / 100,
			(m_SliderEQ11.GetPos() - 50) * 24.0f / 100
		};

		ITMG_VOICE_TYPE_REVERB reverb = {
			(m_SliderExGain.GetPos())            * 1.0f / 100.0f,
			(m_SliderExStartFrequency.GetPos())  * 1.0f / 100.0f,
			(m_SliderExBaseCtrl.GetPos())        * 1.0f / 100.0f,
			(m_SliderReverbSize.GetPos())        * 1.0f / 100.0f,
			(m_SliderReverbDepth.GetPos())       * 1.0f / 100.0f,
			(m_SliderReverbGain.GetPos())        * 1.0f / 100.0f,
			(m_SliderReverbEchoDepth.GetPos())   * 1.0f / 100.0f
		};

		m_pTmgContext->GetAudioEffectCtrl()->SetKaraokeType(&equalizer, &reverb);

	}
	CDialogEx::OnVScroll(nSBCode, nPos, pScrollBar);
}
```

## 이퀄라이저 사용 가이드

>!이 문서는 가이드용으로만 제공됩니다.

사람이 들을 수 있는 소리의 범위는 대략 20HZ에서 20KHZ 사이입니다. 각 주파수 밴드의 인식은 로그 관계를 나타내므로 믹싱 프로젝트는 종종 사람이 들을 수 있는 주파수 대역을 10옥타브로 나누고 다음 영역으로 나뉩니다.

| 밴드 | 영역 | 설명 |
|---------|---------|---------|
|  20HZ - 32HZ | 초저주파 및 서브우퍼 영역 | 이 영역에 있는 대부분의 주파수 대역은 사람이 들을 수 있는 하한선보다 낮습니다. 초대형 파이프 오르간의 음악과 폭발 및 영화의 천둥 음향 효과는 이 주파수에 도달할 수 있지만 사람의 목소리는 도달할 수 없습니다. 일반적으로 VOIP 통화는 DC 간섭을 제거하고 다른 주파수 대역에 대한 신호 에너지를 남기기 위해 z 최소로 조정하는 것이 좋습니다.|
|  32HZ - 64HZ | <nobr>헤비 베이스 영역</nobr> | 주로 드럼과 베이스의 다이브를 조절하는데 사용합니다. 톤이 명확하지 않아 바리톤의 일부가 도달할 수 있습니다. 산업용 주파수 간섭을 제거하고 다른 주파수 대역에 에너지를 남겨두기 위해 VOIP 통화를 낮추는 것이 좋습니다.|
| 64HZ - 125HZ | 베이스 영역 | 타악기의 강도를 결정하는 대부분의 오케스트라 악기의 기본 클럭 범위입니다.|
|  <nobr>125HZ - 250HZ</nobr> | 베이스 영역 | 사람 목소리 톤의 인식을 결정하는 것은 사람 목소리의 기본 클럭 범위입니다. 너무 무거우면 뭉개지는 소리가 납니다.|
|  250HZ - 500HZ | 미드베이스 영역 | 주파수 대역에서 톤의 중요한 하모닉스를 포함하고 있어 톤을 조절하는 데 사용할 수 있으며 이 섹션의 강화는 톤을 따뜻하고 두껍게 만드는 반면 과도한 강화는 톤을 뭉개지게 만듭니다.|
|  500HZ - 1KHZ | 미드레인지 | 여성의 목소리 톤을 조절하여 더 풍성하게 만들 때 사용합니다. 너무 높으면 무거운 비음으로 이어지니 주의하십시오. 휴대 전화 및 기타 모바일 재생 장치의 공진 피크는 이 대역에서 최대이므로 너무 높게 설정하지 마십시오.|
|  1KHZ - 2KHZ | 미드레인지 | 인간 귀의 민감한 부분입니다. 이 값은 음량과 현장감에 영향을 미치므로 강화하는 것이 좋습니다.|
|  2KHZ - 4KHZ | 소프라노 영역 | 인간의 귀에서 가장 민감한 부분입니다. 향상은 목소리의 크기를 증가시키고 명료도를 향상시킬 수 있습니다. 너무 높으면 치찰음이 무거울 수 있습니다.|
|  4KHZ - 8KHZ | 소프라노 영역 | 예를 들어 심벌즈 및 현악기와 같은 고주파 악기의 세부 정보를 표시할 수 있습니다. 게다가, 순치음과 마찰음과 같은 음성의 세부 사항을 결정할 수 있습니다. 조정은 권장하지 않습니다.|
|  8KHZ - 16KHZ | 초고음 및 초음성 영역 | 악기의 고주파 오버톤 영역입니다. 조정은 음성에 거의 영향을 미치지 않습니다.|


자세한 내용은 다음을 참고하십시오.
![](https://main.qcloudimg.com/raw/4f56ccddf718bfd04633d85f19f35468.png)




