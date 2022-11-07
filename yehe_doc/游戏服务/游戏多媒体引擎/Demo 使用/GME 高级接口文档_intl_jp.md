開発者がTencent Cloud Gaming Multimedia Engine (GME)製品APIのデバッグとアクセスを容易にするために、ここでGME SDKの高度なインターフェースを紹介します。

<dx-alert infotype="alarm" title="调用须知">
このドキュメントインターフェースは高度なインターフェースであり、必要がない場合は呼び出す必要はありません。インターフェースを呼び出す前に、GME開発者に相談してください。
</dx-alert>

## オーディオ関連の高度なインターフェース

### iOSオーディオ関連インターフェース

この部分のインターフェースは、ルームに入る前にSetAdvanceParamsインターフェースを使用して呼び出されます。 

```
[[ITMGContext GetInstance] SetAdvanceParams:keyString value:_value]
```

| パラメータ      | 意味                            |
| --------- | ------------------------------- |
| keyString | 異なるキーは異なる機能を表します       |
| value     | <li> 0：オフを表します<li>1：オンを表します |

#### Key 

異なるキーは異なる機能を表します。パラメータKeyに入力できるフィールドは次のとおりです。

- **OptionMixWithOthers**
  リミックスタブ。オンにすると、バックグラウンドで再生されている音楽とフォアグラウンドで通話している音声を同時に再生できます。
- **OptionDuckOthers**
  バックグラウンドサウンドを下げます。OptionMixWithOthersが有効な場合、この機能をオンにすると、スピーカーをオンにして音声を再生するときに、他のバックグラウンドサウンドが下げられます。
- **ReleaseAudioFoucus**
  オーディオフォーカスをリリースします。
- オンにすると、退室後にオーディオフォーカスがリリースされ、システムはバックグラウンドで他のオーディオ関連アプリケーションをリカバーします。たとえばQQ音楽。
- オフにすると、退室後に他のオーディオ関連アプリケーションがリカバーされません。

### iPhoneのミュートキーがオンになっているかどうかの確認

<dx-alert infotype="explain" title="説明">
このインターフェースは、GME2.8.4以降のSDKで有効になります。
</dx-alert>

####  関数のプロトタイプ

```
CheckDeviceMuteState();
```

戻り値0は物理ミュートキーがオフであることを意味し、戻り値1は物理ミュートキーがオンであることを意味します。

### マイクデバイスのステータスの確認

<dx-alert infotype="explain" title="説明">
このインターフェースは、GME2.8.4以降のSDKで有効になります。
</dx-alert>

####  関数のプロトタイプ

```
TestMic();
```

#### 戻り値の処理

| 戻り値                               | 意味                | 処理                                                         |
| ------------------------------------ | ------------------- | ------------------------------------------------------------ |
| ITMG_TEST_MIC_STATUS_AVAILABLE = 0   | 通常利用可能            | 処理不要                                                     |
| ITMG_TEST_MIC_STATUS_NO_GRANTED = 2  | 承認権限を未取得/拒否 | マイクをオンにする前に権限を取得してください                               |
| ITMG_TEST_MIC_STATUS_INVALID_MIC = 3 | 利用可能なデバイスなし      | 通常、PCデバイスでは、利用可能なマイクデバイスがない場合にこのエラーが表示されます。ヘッドセットまたはマイクを挿入するように提示してください。 |
| ITMG_TEST_MIC_STATUS_NOT_INIT = 5    | 未初期化          | Init後にEnableMicインターフェースを呼び出します                                |

### Android Bluetoothデバイスアダプテーションの設定

<dx-alert infotype="explain" title="説明">
このインターフェースは、GME2.8.4以降のSDKで有効になります。
</dx-alert>

このインターフェースを呼び出すことで、Bluetoothヘッドセットがマイクのオン/オフを切り替えるときに音漏れする問題や、Bluetoothヘッドセットを接続した後にAndroidデバイスが接続状態を切り替えることによって発生するスピーカーからの再生の問題を解決できます。

```
SetAdvanceParams(「BluetoothUseMedia」, 「1」);
```

### リミックスの最大チャネル数の設定

SetRecvMixStreamCountインターフェースを使用することで、リミックスの最大チャネル数を設定できます。ルームに入る前に呼び出されます。すべてのプラットフォームがこのインターフェースを持っています。以下ではPC端末を例に取ります。

```
virtual int SetRecvMixStreamCount(int nCount) = 0;
```

**パラメータの説明** 

| パラメータ   | 意味               |
| ------ | ------------------ |
| nCount | リミックスのチャネル数、最大20 |



## ルーム関連の高度なインターフェース

### ルームオーディオタイプの設定

ルームに入る前にSetForceUseMediaVolを使用すると、メディアボリュームを滑らかな音質のルームまたは標準的な音質のルームで使用できます。

```
[[ITMGContext GetInstance] SetAdvanceParams:SetForceUseMediaVol value:1]
```

#### value

次のように、異なるvalueは異なる機能を表します：
- 0：ルームタイプ1と2の音声ルームは、マイクをオンにすると通話音量に戻ります。
- 1：ルームタイプ1の音声ルームは、マイクをオンにした後にメディア音量（元の通話音量）に設定されます。
- 2：ルームタイプ2の音声ルームは、マイクをオンにした後にメディア音量（元の通話音量）に設定されます。

### ルーム内メンバーの発言音量の取得

TrackingVolumeインターフェースを呼び出した後、`TIMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_USER_VOLUMES`イベントをモニタリングし、内部のキー値のペアはuin-volumeで、このインターフェースを介して、ルーム内の特定のuinの発言音量に従って対応するエネルギーヒストグラムを描画できます。

取得できなくなった場合は、StopTrackingVolumeインターフェースを呼び出してください。

```
//TMGAudioCtrl
public int TrackingVolume(float fTrackingTimeS)
public int StopTrackingVolume();
```

| パラメータ           | タイプ  | 意味                        |
| -------------- | ----- | --------------------------- |
| fTrackingTimeS | float | モニタリング秒数。0.5fに設定することをお勧めします |

## 汎用の高度なインターフェース
### openidは文字列をサポートする
>! このインターフェースは、GME2.9.3以降のSDKで有効になります。

現在、GME SDKは、文字列の形式でSDKに渡す数値のみをサポートします。openidを文字列の形式で渡す必要がある場合は、Initインターフェースを呼び出す前に、次のインターフェースを呼び出してください：
```
SetAdvanceParams("StringOpenID", "1");
``` 

### 印刷ログのサイズを変更する

<dx-alert infotype="explain" title="説明">
このインターフェースは、GME2.8.4以降のSDKで有効になります。
</dx-alert>

このインターフェースは、GME Init初期化インターフェースの前に呼び出され、デフォルトのログファイルサイズを変更するときに使用されます。現在、1つのログファイルは50mで、最大3つのログファイルがあります。

####  関数のプロトタイプ

```
SetAdvanceParams（const char* key, const char* object）
```

| パラメータ   | タイプ        | 意味                                                         |
| ------ | ----------- | ------------------------------------------------------------ |
| key    | const char* | MAX_LOG_FILE_SIZE_MBとMAX_LOG_FILE_COUNTは、それぞれ1つのログのサイズとログの数を表します。|
| object | const char* | keyがMAX_LOG_FILE_SIZE_MBの場合、objectはLogファイルサイズのデフォルト値で、値の範囲（単位M）：5～50。keyがMAX_LOG_FILE_COUNTの場合、objectはLogファイル数のデフォルト値で、値の範囲：1～3。|

<dx-alert infotype="notice" title="参数范围">
入力されたobjectが値の範囲の上限を超えた場合は上限値に設定され、入力されたobjectが値の範囲の下限を下回った場合は下限値に設定されます。
</dx-alert>

####  サンプルコード

```
SetAdvanceParams("MAX_LOG_FILE_SIZE_MB", "5");
SetAdvanceParams("MAX_LOG_FILE_COUNT", "1");
```

## 高度な機能インターフェース

### テキスト翻訳インターフェース

このインターフェースを呼び出すことで、中国語を英語に翻訳するなど、テキストを翻訳することができます。インターフェースを呼び出した後、翻訳結果がコールバックを介して返されます。ここでC++インターフェースを例に取ります。

>!このインターフェースは、ホワイトリストに登録されたユーザーのみが利用でき、SDK291以降でのみ使用できます。必要に応じて、[チケットを提出](https://console.cloud.tencent.com/workorder/category)して、サービスのお申し込みはスタッフにお問い合わせください。

#### 関数のプロトタイプ

```
virtual int TranslateText(const char* text, const char* sourceLanguage, const char* translateLanguage) = 0;
```

| パラメータ              | タイプ        | 意味                                                         |
| ----------------- | ----------- | ------------------------------------------------------------ |
| text              | const char* | 翻訳するテキストを空にすることはできません。最大長は5000文字です                     |
| sourceLanguage    | const char* | 翻訳するテキストの言語を指定します。空にすることもできます。バックグラウンドでは自動的に音声を検出します               |
| translateLanguage | const char* | テキストが翻訳された後の言語を指定します。空にすることはできません。「cmn-Hans-CN,en-GB」、「cmn-Hans-CN」など、英語のカンマで区切ります |

言語パラメータについては、[言語パラメータリスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。

#### コールバックインターフェース

| パラメータ       | タイプ                            | 意味                                                         |
| ---------- | ------------------------------- | ------------------------------------------------------------ |
| code       | int                             | エラーコードで、0は成功を意味します。その他の戻り値については、[エラーコード](https://intl.cloud.tencent.com/document/product/607/33223)を参照して解決してください |
| targetText | jason(Unityでstring形式が返される) | 翻訳後のターゲットテキストです。たとえば     {"target_text":[{"target_language_code":"cmn-Hans-CN","target_text":"我是中国人"},{"target_language_code":"de-DE","target_text":"Ich bin Chinese"}]} |

#### Unityプロジェクトのサンプルコード

1. モニタリングの追加
```
ITMGContext.GetInstance().GetPttCtrl().OnTranslateTextComplete+= OnTranslateTextComplete;
```

2. インターフェースの呼び出し
```
private void OnTranslateTextBtn()
{
     mTargetText.text = "";
    int ret = ITMGContext.GetInstance().GetPttCtrl().TranslateText(mSourceText. text, mSourceLanguageText.text, mTargetLanguageText.text);
    if (0 != ret)
    {
         mTargetText.text = "Invalid Atgument";
    }
}
```

3. コールバックの処理
```
void OnTranslateTextComplete(int code, string targetText)
{
    if (0 == code)
    {
        mTargetText.text = targetText;
    }
    else
    {
        mTargetText.text = String.Format(
            "Translate Text Error, Error Code:{0}", code);
    }
}
```

4. モニタリングのキャンセル
```
ITMGContext.GetInstance().GetPttCtrl().OnTranslateTextComplete-= OnTranslateTextComplete;
```

### テキストツーボイス変換のインターフェース

このインターフェースを呼び出すと、テキストを対応する音声に変換できます。インターフェースを呼び出した後、音声fileidがコールバックを介して返され、音声が音声インターフェースのダウンロードを介してダウンロードされます。ここでC++インターフェースを例に取ります。

>!このインターフェースは、ホワイトリストに登録されたユーザーのみが利用でき、SDK291以降でのみ使用できます。必要に応じて、[チケットを提出](https://console.cloud.tencent.com/workorder/category)して、サービスのお申し込みはスタッフにお問い合わせください。

####  関数のプロトタイプ

```
virtual int TextToSpeech(const char* text, const char* voiceName,const char* languageCode, float speakingRate) = 0;
```

| パラメータ         | タイプ        | 意味                                           |
| ------------ | ----------- | ---------------------------------------------- |
| text         | const char* | 元のテキストを空にすることはできません。最大長は5000文字です            |
| voiceName    | const char* | 音声タイプです。英語と北京語で例を提供します。他の言語が必要な場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してお問い合わせください |
| languageCode | const char* | ターゲット言語を指定します。空にすることはできません                         |
| speakingRate | float       | 音声速度です。値の範囲は[0.6-1.5]で、1は正常な速度を表します     |

voiceNameの説明は次のとおりです：

| 音声タイプ | 性別 | 言語 |
|---------|---------|---------|
| cmn-CN-Standard-A | 女性 | 北京語 |
| cmn-CN-Standard-B | 男性 | 北京語 |
| en-US-Neural2-A | 女性 | 英語 |
| en-US-Neural2-B | 男性 | 英語 |

言語パラメータについては、[言語パラメータリスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。

#### コールバックインターフェース

| パラメータ   | タイプ   | 意味                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| code   | int    | エラーコードで、0は成功を意味します。その他の戻り値については、[エラーコード](https://intl.cloud.tencent.com/document/product/607/33223)を参照して解決してください |
| isCos  | bool   | ファイルがCOSにアップロードされているかどうか                                            |
| fileID | string | ファイルIDで、ダウンロードインターフェースの入力パラメータを提供します。DownloadRecordedFileインターフェースを介して音声をダウンロードできます |

#### Unityプロジェクトのサンプルコード

1. モニタリングの追加
```
ITMGContext.GetInstance().GetPttCtrl().OnTextToSpeechComplete += new QAVTextToSpeechCallback(TextToSpeechComplate);
```

2. インターフェースの呼び出し
```
void OnTextToSpeech()
{
    float fSpeakingRate;
    if (!float.TryParse(mSpeakingRate.text, out fSpeakingRate))
    {
        mReturnData.text = "SpeakingRate invalid";
         return;
    }

    int iRet = ITMGContext.GetInstance().GetPttCtrl().TextToSpeech(
        mSouceText.text, mVoiceName.text,
        mLanguageCode.text, fSpeakingRate);

    Debug.Log(string.Format("TextToSpeech Code:{0}", iRet));

    if (0 != iRet)
    {
        mReturnData.text = string.Format("TextToSpeech Error, errorCode:{0}", iRet);
        return;
    }
}
```

3. コールバックの処理
```
void TextToSpeechComplate(int code, bool isCos, string fileID)
{
    Debug.Log(string.Format("TextToSpeechComplate Code:{0}", code));

    if (0 != code)
    {
        mReturnData.text = string.Format("TextToSpeech Error, errorCode:{0}", code);
        return;
    }

    mReturnData.text = string.Format("code:{0}\r\nisCos:{1}\r\nfileID:{2}", code, isCos, fileID);
    mDownloadUrl.text = fileID;
}
```

4. モニタリングのキャンセル
```
ITMGContext.GetInstance().GetPttCtrl().OnTextToSpeechComplete -= new QAVTextToSpeechCallback(TextToSpeechComplate);
```
