開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、このドキュメントではGMEリアルタイムなサウンドイコライザの導入を紹介します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/72bd34689aed95d320d1e655a5f1a049.png" width="80%" >



## シナリオ

GMEイコライザ機能は、GME SDKで収集したオーディオストリームをリアルタイムでイコライザ調整することができます。この機能はオンラインのカラオケシーンに使用されます。プレイヤーが歌い始めた後、**GME SDK**の**イコライザ**インターフェースを呼び出して、プレイヤーのリアルタイムの音声ストリームに対し音の美化効果を調整することができます。


##  前提条件

- **リアルタイムボイスサービスを有効にしました：[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GME SDK導入済み**：コアインターフェースとリアルタイム音声インターフェースの導入が含まれます。詳細については、[Native SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/40858)、[Unity SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44544)、[Unreal SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44545)をご参照ください。


## Demo体験

### Demoのダウンロード

[ダウンロードアドレス>>](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.8.4/Windows/PC_Release_ForTest.zip)

この体験Demoは、次のような画面を持つWindows実行可能プログラムです。

![](https://qcloudimg.tencent-cloud.cn/raw/f00d59d614ce32aa6ae1e702f6a3cc6b.png)


### 構成パラメータ

AppidとKeyの入力ボックスに自分が申請したGME AppIDとKeyを記入します。

必要に応じて、ターゲットのルーム番号とOpenIDを入力することもできます。

### 使用方法

1.　ルームに入ってマイクスピーカーをオンにする手順は、Init > EnterRoom > EnableCapture > EnablePlay > EnableSend > EnableRecvです。
2.　ルームに入ると、**EnableLoopBack**をオンにして自分の声を聞くことができます。
3.　赤枠の**EQ**イコライザ（EQは帯域利得、ExditorとReverbはリバーブ）を調整します。




##　イコライザ機能の導入
このインターフェースを使用してローカル側で収音されたサウンドのイコライザ調整を行うには、入室が成功している状態が必要です。

### 関数プロトタイプ  
```
int SetKaraokeType(ITMG_VOICE_TYPE_EQUALIZER* pEqualizer, ITMG_VOICE_TYPE_REVERB* pReverb)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| pEqualizer|ITMG_VOICE_TYPE_EQUALIZER|帯域利得|
| pReverb|ITMG_VOICE_TYPE_REVERB| HARMONICとREVERBを含む|

###　構造体の詳細
**ITMG_VOICE_TYPE_EQUALIZERの構造体メンバーはfloatタイプで、数値の範囲は-12から12です。**

|ITMG_VOICE_TYPE_EQUALIZER      |意味|
| ------------- |:-------------:|
|EQUALIZER_32HZ			|32HZ帯域に加えた利得|
|EQUALIZER_64HZ			|64HZ帯域に加えた利得|
|EQUALIZER_128HZ        |128HZ帯域に加えた利得|
|EQUALIZER_250HZ        |250HZ帯域に加えた利得|
|EQUALIZER_500HZ        |500HZ帯域に加えた利得|
|EQUALIZER_1KHZ         |1KHZ帯域に加えた利得|
|EQUALIZER_2KHZ         |2KHZ帯域に加えた利得|
|EQUALIZER_4KHZ         |4KHZ帯域に加えた利得|
|EQUALIZER_8KHZ         |8KHZ帯域に加えた利得|
|EQUALIZER_16KHZ        |16KHZ帯域に加えた利得|
|EQUALIZER_MASTER_GAIN  |全体的な音量|

**ITMG_VOICE_TYPE_REVERBの構造体メンバーはfloatタイプで、数値の範囲は0~1です。**


|ITMG_VOICE_TYPE_REVERB      |
|-------------|
|HARMONIC_GAIN				|
|HARMONIC_START_FREQUENCY	|
|HARMONIC_BASS_CONTROL		|
|REVERB_SIZE				|
|REVERB_DEPTH				|
|REVERB_GAIN				|
|REVERB_ECHO_DEPTH			|


####  サンプルコード

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

## イコライザ使用ガイド

>!　ここでは簡単な使い方を示しています。高級のEQ効果を使用する場合は、専門の調律師に依頼してください。

人間の耳に聞こえる音の範囲はだいたい20Hz～20KHzであり、人間の耳は各周波数帯に対して対数関係にあるので、ミキシングプロジェクトでは人間の可聴周波数帯を10オクターブに分けて調整することがよくあり、調律は大きく次のように分けられます。

| 帯域 | 領域 | 説明 |
|---------|---------|---------|
|  20HZ - 32HZ | サブサウンドと超低音域 | 大部分の周波数帯は人の耳の聴覚の下限を下回って、触覚で感知することが多い。音楽の超大型パイプオルガンと映画の中の爆発と雷の効果音はこの周波数に達することができ、人の声はこの周波数帯に達することができません。一般的なVOIP通話はzの最低に調整し、直流の干渉を除去し、信号のエネルギーを他の周波数帯に残すことをお勧めします。|
|  32HZ - 64HZ | <nobr>重低音域</nobr> | 主にドラムとベースのダウンを調整するために使用され、音調が目立たないように感じられ、一部のバス音域はこの周波数帯に達することができます。VoIP通話の人の声の調律は一般的に低くし、周波数干渉を除去し、エネルギーを他の周波数帯に残すことをお勧めします。|
| 64HZ - 125HZ | 低音域 | ほとんどの管弦楽器の基本周波数の範囲です。打楽器の強さも決定します。|
|  <nobr>125HZ - 250HZ</nobr> | 低音域 | 人の声の基本周波数の範囲です。人の声のトーンの知覚を決定します。重すぎると音が濁ることがあります。|
|  250HZ - 500HZ | 中低音域 | 人の声色の重要な低次高調波がある周波数帯を含み、男性の声の音色を調整するために使用され、これを適当に強化して人の声色を温かく、重厚になり、強めすぎて音が濁ります。|
|  500HZ - 1KHZ | 中音域 | 女声の音色を調整し、それをより豊かにします。高すぎると鼻音が重くなります。携帯電話などのモバイル再生機器のフォルマントはこの周波数帯にあり、調整が高すぎて構造振動雑音が発生しやすいことを避けることをお勧めします。|
|  1KHZ - 2KHZ | 中音域 | 人の耳の敏感な領域で、響きと臨場感に影響し、適切に増強することができます。|
|  2KHZ - 4KHZ | 中高音域 | 人の耳が最も敏感な領域で、この判断を高めることで音の響きを高め、音声の理解度の相関を高めることができ、調整が高すぎると歯音が重すぎることになます。|
|  4KHZ - 8KHZ | 高音域 | チャイナシンバルなどの高周波楽器や弦楽器の摩擦音などの音の細かい部分を表現します。唇歯音、摩擦音など、人の声の高周波数のディテールを決定します。通常増強しないでください。|
|  8KHZ - 16KHZ | 超高音や超音波領域 | 楽器の高周波オーバトーンです。調整が音声にあまり影響しません。|


調整の詳細については、次の図をご参照ください。
![](https://main.qcloudimg.com/raw/4f56ccddf718bfd04633d85f19f35468.png)




