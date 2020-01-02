開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグ・アクセスを手軽に実行できるように、ここで、Gaming Multimedia Engineリアルタイム音声サウンドエフェクトのアクセス技術ドキュメントについて説明させていただきます。


## リアルタイム音声サウンドエフェクトの関連インターフェース
|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|PlayEffect    |サウンドエフェクトを再生します。|
|PauseEffect    |サウンドエフェクト再生を一時停止します。|
|PauseAllEffects|すべてのサウンドエフェクトを一時停止します。|
|ResumeEffect    |サウンドエフェクト再生を再開します。|
|ResumeAllEffects|すべてのサウンドエフェクト再生を再開します。|
|StopEffect |サウンドエフェクト再生を停止します。|
|StopAllEffects|すべてのサウンドエフェクト再生を停止します。|
|SetVoiceType |ボイス・チェンジの特殊効果音です。|
|SetKaraokeType |カラオケの特殊効果音です。|
|GetEffectsVolume|サウンドエフェクト再生のボリュームを取得します。|
|SetEffectsVolume |サウンドエフェクト再生のボリュームを設定します。|


### サウンドエフェクトの再生
PlayEffectインターフェイスはサウンドエフェクトを再生するために使用されます。パラメータのサウンドエフェクトIDはApp側で管理される必要があり、IDは独立の再生イベントを表します。後でこの再生はこのIDに基づいて制御できます。ファイルはm4a、wav、mp3の3種類の形式をサポートします。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int PlayEffect(int soundId,  const char* filePath, bool loop, double pitch, double pan, double gain)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| soundId    |int    |サウンドエフェクトのIDです。|
| filePath    |char\*     |サウンドエフェクトのパスです。|
| loop    |bool  |繰り返し再生するかどうか。|
| pitch    |double|再生の周波数はデフォルトで1.0です。この値が小さいほど再生スピードが遅く、時間が長くなります。|
| pan    |double|サウンドチャンネルは値の範囲が-1.0～1.0で、-1.0が左チャンネルのみをオンにすることを表します。|
| gain    |double|ゲイン音量は値の範囲が0.0～1.0で、デフォルト値で1.0になっています。|

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
| soundId    |int                    |サウンドエフェクトのIDです。|

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
| soundId    |int                    |サウンドエフェクトのIDです。|

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
| soundId    |int                    |サウンドエフェクトのIDです。|

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
| type    |int                    |ローカルオーディオのボイス・チェンジタイプを示します。|



|タイプパラメータ     |パラメータ代表|意味|
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND  |0|地声です。|
| ITMG_VOICE_TYPE_LOLITA    |1|ロリっ子ボイスです。|
| ITMG_VOICE_TYPE_UNCLE  |2|おじさんボイスです。|
| ITMG_VOICE_TYPE_INTANGIBLE    |3|透明感のある声です。|
| ITMG_VOICE_TYPE_DEAD_FATBOY  |4|オタクボイスです。|
| ITMG_VOICE_TYPE_HEAVY_MENTA|5|ヘビーメタル感の声です。|
| ITMG_VOICE_TYPE_DIALECT |6|外国人のようになまりがある声です。|
| ITMG_VOICE_TYPE_INFLUENZA |7|インフルエンザにかかったような声です。|
| ITMG_VOICE_TYPE_CAGED_ANIMAL |8|エルキングの声です。|
| ITMG_VOICE_TYPE_HEAVY_MACHINE|9|重型機械のような声です。|
| ITMG_VOICE_TYPE_STRONG_CURRENT|10|大電流を交えている声です。|
| ITMG_VOICE_TYPE_KINDER_GARTEN|11|幼稚園生みたいな声です。|
| ITMG_VOICE_TYPE_HUANG |12|ミニオンのような声です。|

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
|ITMG_KARAOKE_TYPE_ORIGINAL |0|オリジナルサウンドです。|
|ITMG_KARAOKE_TYPE_POP |1|ポップエフェクトです。|
|ITMG_KARAOKE_TYPE_ROCK |2|ロックンロールエフェクトです。|
|ITMG_KARAOKE_TYPE_RB |3|ヒップホップエフェクトです。|
|ITMG_KARAOKE_TYPE_DANCE |4|舞曲エフェクトです。|
|ITMG_KARAOKE_TYPE_HEAVEN |5|透明感エフェクトです。|
|ITMG_KARAOKE_TYPE_TTS |6|音声合成エフェクトです。|

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
| volume    |int                    |ボリューム値です。|

####  サンプルコード  
```
int volume=1;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetEffectsVolume(volume);
```

