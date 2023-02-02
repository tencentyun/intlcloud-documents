開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグ・アクセスを手軽に実行できるように、ここで、Gaming Multimedia Engineリアルタイム音声サウンドエフェクトのアクセス技術ドキュメントについて説明させていただきます。


##  前提条件

- **リアルタイムボイスサービスを有効にしました：[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GME SDK導入済み**：コアインターフェースとリアルタイム音声インターフェースの導入が含まれます。詳細については、[Native SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/40858)、[Unity SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44544)、[Unreal SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44545)をご参照ください。
-　GMEリアルタイムボイス機能を使用して音声ルームへの参加に成功し、マイク（EnableMic）、スピーカー（EnableSpeaker）をオンにしました。


## リアルタイム音声サウンドエフェクトの関連インターフェース
|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|PlayEffect    		|効果音の再生|
|PauseEffect    	|効果音再生の一時停止|
|PauseAllEffects	|すべての効果音の一時停止|
|ResumeEffect    	|効果音再生の再開|
|ResumeAllEffects	|すべての効果音再生の再開|
|StopEffect 		|効果音再生の停止|
|StopAllEffects		|すべての効果音再生を停止|
|SetVoiceType 		|ボイス変更特効|
|SetKaraokeType 		|カラオケ特別効果音|
|GetEffectsVolume	|効果音再生音量の取得|
|SetEffectsVolume 	|効果音再生音量の設定|


### サウンドエフェクトの再生
PlayEffectインターフェイスはサウンドエフェクトを再生するために使用されます。パラメータのサウンドエフェクトIDはApp側で管理される必要があり、IDは独立の再生イベントを表します。後でこの再生はこのIDに基づいて制御できます。ファイルはm4a、wav、mp3の3種類の形式をサポートします。

####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int PlayEffect(int soundId,  const char* filePath, bool loop, double pitch, double pan, double gain)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId  	|int        	|効果音ID						|
| filePath    	|char\*     	|効果音パス						|
| loop    		|bool  	|繰り返し再生の要否						|
| pitch    	|double	|再生頻度。デフォルトが1.0です。値が小さいほど、再生速度は遅くなり、時間は長くなります		|
| pan    		|double	|チャンネル、値の範囲は-1.0～1.0です。-1.0は左チャンネルのみがオンになっていることを意味します	|
| gain    		|double	|音量ゲイン。値の範囲は0.0～1.0です。デフォルトが1.0です		|

####  サンプルコード  
```
double pitch = 1.0;
double pan = 0.0;
double gain = 0.0;
//Windows
ITMGContextGetInstance()->GetAudioEffectCtrl()->PlayEffect(soundId,filepath,true,pitch,pan,gain);
//Android
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PlayEffect(soundId,filePath,loop);
//iOS
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PlayEffect:soundId filePath:path loop:isLoop];
```


### サウンドエフェクトの再生を一時停止する
PauseEffectインターフェースはサウンドエフェクトの再生を一時停止することに使用されます。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int PauseEffect(int soundId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId  	|int        	|効果音ID						|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseEffect(soundId);
```

### すべてのサウンドエフェクトを一時停止する
PauseAllEffectsインターフェースを呼び出してすべてのサウンドエフェクトを一時停止します。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int PauseAllEffects()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAllEffects();
```

### サウンドエフェクトの再生を再開する
ResumeEffectインターフェースはサウンドエフェクトの再生を再開することに使用されます。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int ResumeEffect(int soundId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId  	|int        	|効果音ID						|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeEffect(soundId);
```



### すべてのサウンドエフェクトの再生を再開する
ResumeAllEffectsインターフェースを呼び出してすべてのサウンドエフェクトの再生を再開します。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int ResumeAllEffects()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAllEffects();
```


### サウンドエフェクト再生を停止する
StopEffectインターフェースはサウンドエフェクト再生を停止することに使用されます。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int StopEffect(int soundId)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId  	|int        	|効果音ID						|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopEffect(soundId);
```

### すべてのサウンドエフェクト再生を停止する
StopAllEffectsインターフェースを呼び出してすべてのサウンドエフェクト再生を停止します。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int StopAllEffects()
```


####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAllEffects();
```



### ボイス・チェンジの特殊効果音
SetVoiceTypeインターフェースを呼び出してボイス・チェンジの特殊効果音を設定します。
####  関数のプロトタイプ  
```
TMGAudioEffectCtrl int setVoiceType(int type)
```

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

###カラオケサウンドエフェクトの特殊効果音
SetKaraokeTypeインターフェースを呼び出してカラオケサウンドエフェクトの特殊効果音を設定します。
####  関数のプロトタイプ  
```
TMGAudioEffectCtrl int SetKaraokeType(int type)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| type    |int                    |ローカルオーディオのボイス・チェンジタイプを示します。|


|タイプパラメータ     |パラメータ代表|意味|
| ------------- |-------------|------------- |
|ITMG_KARAOKE_TYPE_ORIGINAL 		|0	|原音			|
|ITMG_KARAOKE_TYPE_POP 				|1	|流行			|
|ITMG_KARAOKE_TYPE_ROCK 			|2	|ロック			|
|ITMG_KARAOKE_TYPE_RB 				|3	|ヒップホップ			|
|ITMG_KARAOKE_TYPE_DANCE 			|4	|舞曲			|
|ITMG_KARAOKE_TYPE_HEAVEN 			|5	|ファンタジー			|
|ITMG_KARAOKE_TYPE_TTS 				|6	|ボイス合成		|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetKaraokeType(0);
```

### サウンドエフェクト再生のボリュームを取得する
GetEffectsVolumeインターフェイスを呼び出してサウンドエフェクト再生のボリューム（リニアボリューム）を取得します。デフォルト値は100で、値が100以上になるとゲイン効果で、100未満の値がデバフ効果です。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int GetEffectsVolume()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetEffectsVolume();
```

### サウンドエフェクト再生のボリュームを設定する
SetEffectsVolumeインターフェイスを呼び出してサウンドエフェクト再生のボリュームを設定します。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int SetEffectsVolume(int volume)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| volume    |int                    |音量値|

####  サンプルコード  
```
int volume=1;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetEffectsVolume(volume);
```
