

開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、このドキュメントではGMEのボイス・チェンジ効果音の導入方法を紹介します。


## シナリオ


![](https://qcloudimg.tencent-cloud.cn/raw/d7d75633180f90d9357650a7d7493f4d.png)

##  前提条件

- **リアルタイムボイスサービスを有効にしました：[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
-　**ボイスツーテキスト変換サービスを有効にしました**：[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GME SDK導入済み**：コアインターフェースとリアルタイム音声インターフェースの導入が含まれます。詳細については、[Native SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/40858)、[Unity SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44544)、[Unreal SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44545)をご参照ください。
-　**GME SDKライブラリファイルlibgmesoundtouchを導入しました**：libgmesoundtouchがプロジェクトライブラリファイルに含まれていることを確認する必要があります。具体的には、[ライブラリファイル対応機能](https://intl.cloud.tencent.com/document/product/607/32363)をご参照ください。

## リアルタイム音声のボイス・チェンジの導入

###　ボイス・チェンジインターフェース
入室に成功し、マイクがオンになっている場合、SetVoiceTypeインターフェースを呼び出してボイスオーバー効果を設定します。インターフェースが0を返した場合、呼び出しに成功したことを示します。この場合、ルームにいる人は自端末からボイス・チェンジ効果のある音声を聞くことができます。ボイス・チェンジをセルフテストする場合は、インイヤ・モニタリング機能（インターフェース：EnableLoopBack）を使用します。

####  関数のプロトタイプ  


<dx-codeblock>
::: Android java
    public static class ITMG_VoiceType {
        public static final int ITMG_VOICE_TYPE_ORIGINAL_SOUND = 0;
        public static final int ITMG_VOICE_TYPE_LOLITA = 1;   
        public static final int ITMG_VOICE_TYPE_UNCLE = 2;  
        public static final int ITMG_VOICE_TYPE_INTANGIBLE = 3; 
        public static final int ITMG_VOICE_TYPE_DEAD_FATBOY = 4; 
        public static final int ITMG_VOICE_TYPE_HEAVY_MENTAL = 5;
        public static final int ITMG_VOICE_TYPE_DIALECT = 6; 
        public static final int ITMG_VOICE_TYPE_INFLUENZA = 7;
        public static final int ITMG_VOICE_TYPE_CAGED_ANIMAL = 8; 
        public static final int ITMG_VOICE_TYPE_HEAVY_MACHINE = 9;
        public static final int ITMG_VOICE_TYPE_STRONG_CURRENT = 10;
        public static final int ITMG_VOICE_TYPE_KINDER_GARTEN = 11; 
        public static final int ITMG_VOICE_TYPE_HUANG = 12;
    };
    public abstract int SetVoiceType(int type);
:::
::: iOS objectc
-(QAVResult)SetVoiceType:(ITMG_VOICE_TYPE) type 
:::
::: Unity C#		
public abstract class ITMGAudioEffectCtrl{
	public static int VOICE_TYPE_ORIGINAL_SOUND = 0;
	public static int VOICE_TYPE_LOLITA = 1;		
	public static int VOICE_TYPE_UNCLE = 2;			
	public static int VOICE_TYPE_INTANGIBLE = 3;	
	public static int VOICE_TYPE_DEAD_FATBOY = 4;	
	public static int VOICE_TYPE_HEAVY_MENTAL = 5;	 
	public static int VOICE_TYPE_DIALECT = 6;		
	public static int VOICE_TYPE_INFLUENZA = 7;		
	public static int VOICE_TYPE_CAGED_ANIMAL = 8;	
	public static int VOICE_TYPE_HEAVY_MACHINE = 9;	
	public static int VOICE_TYPE_STRONG_CURRENT = 10;
	public static int VOICE_TYPE_KINDER_GARTEN = 11;
	public static int VOICE_TYPE_HUANG = 12;
	public abstract int SetVoiceType(int voiceType);
}
:::
::: C++ c++
class ITMGAudioEffectCtrl {
public:
    virtual ~ITMGAudioEffectCtrl(){};
    virtual int SetVoiceType(ITMG_VOICE_TYPE voiceType) = 0;
}
:::
</dx-codeblock>


|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| type    |int                    |ローカル側のボイス変更タイプを示す|


|タイプパラメータ     |パラメータ代表|意味|
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND  		|0	|原音			|
|ITMG_VOICE_TYPE_LOLITA    				|1	|ロリ			|
| ITMG_VOICE_TYPE_UNCLE  				|2	|おじさん			|
|ITMG_VOICE_TYPE_INTANGIBLE    			|3	|ファンタジー			|
| ITMG_VOICE_TYPE_DEAD_FATBOY  			|4	|オタク		|
|ITMG_VOICE_TYPE_HEAVY_MENTA			|5	|ヘビーメタル			|
| ITMG_VOICE_TYPE_DIALECT |6|外国人のようになまりがある声です。|
| ITMG_VOICE_TYPE_INFLUENZA 				|7	|風邪			|
|ITMG_VOICE_TYPE_CAGED_ANIMAL 			|8	|絶望			|
| ITMG_VOICE_TYPE_HEAVY_MACHINE		|9	|ヘビーマシン			|
|ITMG_VOICE_TYPE_STRONG_CURRENT			|10	|強電流			|
| ITMG_VOICE_TYPE_KINDER_GARTEN			|11	|幼稚園			|
| ITMG_VOICE_TYPE_HUANG 					|12	|ミニオン|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->setVoiceType(0);
```


## 音声メッセージのボイス・チェンジ導入

### 音声メッセージボイス・チェンジ手順
![](https://qcloudimg.tencent-cloud.cn/raw/490623c6f98fa3d2378a3946d818adc0.png)

音声メッセージのボイス・チェンジは元のオーディオ情報に影響を与えず、再生時にボイス・チェンジ効果が反映されます。

#### 音声メッセージ再生

ボイス・チェンジパラメータ付きの音声メッセージ再生インターフェース。

<dx-codeblock>
::: Android java
public abstract int PlayRecordedFile(String filePath,int voicetype);
:::
::: iOS objectc
-(int)PlayRecordedFile:(NSString*)filePath VoiceType:(ITMG_VOICE_TYPE) type
:::
::: Unity c#
ITMGPTT PlayRecordedFile(string filePath,int voiceType);
:::
::: C++ c++
public abstract int PlayRecordedFile(string filePath,int voiceType);
:::
</dx-codeblock>

| パラメータ          | タイプ                    | 意味                                                  |
| --------- | :----: | ------------------------------------------------------------ |
| filePath  | string | ローカル音声ファイルのパス                                           |
| voicetype |  int   | ボイス・チェンジタイプ |

#### エラーコード

| エラーコード | 原因       | 解決策                       |
| -------- | ---------- | ------------------------------ |
|20485  |再生が開始されていません|ファイルがあるかどうか、及びファイルパスの正当性を確認します|
