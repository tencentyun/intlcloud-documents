開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグ・アクセスを行いやすいように、ここで、Gaming Multimedia Engineリアルタイム音声伴奏のインポート技術ドキュメントを説明させていただきます。

## リアルタイム音声伴奏の関連インターフェース
|インターフェース     | インターフェースの意味   |
| ------------- |:-------------:|
|StartAccompany           |伴奏再生を開始します。|
|StopAccompany       |伴奏再生を停止します。|
|IsAccompanyPlayEnd|伴奏再生が終わっているかどうか。|
|PauseAccompany    |伴奏再生を一時停止します。|
|ResumeAccompany|伴奏再生を再開します。|
|SetAccompanyVolume |伴奏ボリュームを設定します。|
|GetAccompanyVolume|伴奏再生ボリュームを取得します。|
|SetAccompanyFileCurrentPlayedTimeByMs |再生進捗を設定します。|


>リアルタイム音声伴奏を利用する必要がある場合は、 GME SDK をアクセスし、且つリアルタイムの音声通話を行える必要があります。

### フローチャート
ソーシャルタイプAPPの呼び出しフローチャートは下図の通りです。
![](https://main.qcloudimg.com/raw/cdcd069530545ed560f99985b15edcc9.png)


### 伴奏再生を開始する
StartAccompany インターフェースを呼び出し伴奏再生を開始します。m4a、wav、mp3 の3種類のフォーマットをサポートしています。このAPIを呼び出すと、ボリュームがリセットされます。

####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int StartAccompany(const char* filePath, bool loopBack, int loopCount, int msTime) 
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| filePath    |char\* |伴奏を再生するパスです。|
| loopBack  |bool|ミキシングで発送するかどうかは、一般的にはtrueにします、即ち、ほかの人たちも伴奏が聞こえることです。|
| loopCount|int    |循環回数です。数値が-1の場合、無限循環を示しています。|
| msTime|int   |ディレー時間です。|

####  サンプルコード  
```
//Windowsコード
ITMGContextGetInstance()->GetAudioEffectCtrl()->StartAccompany(filePath,true,-1,0);
//Androidコード
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StartAccompany(filePath,true,loopCount,0);
//iOSコード
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StartAccompany:path loopBack:isLoopBack loopCount:loopCount msTime:0];
```

### 伴奏再生のコールバック
伴奏再生が終わった後に、コールバック関数が OnEventを呼び出します。イベントメッセージがITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISHであり、OnEvent関数でイベントメッセージを判断します。
渡されるパラメータdataには resultと file_pathの二つの情報が含まれています。
####  サンプルコード  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//処理します
		break;
	   	}
		...
        case ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH:
		{
		//処理します
		break;
		}
	}
}
```

### 伴奏再生を停止する
StopAccompanyインターフェースを呼び出し、伴奏再生を停止します。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int StopAccompany(int duckerTime)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| duckerTime|int             |フェードアウト時間です。|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAccompany(0);
```

### 伴奏再生が終わっているかどうか
再生が終わった場合は、戻り値がtrueです。再生が終わっていない場合は、戻り値が falseです。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual bool IsAccompanyPlayEnd()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->IsAccompanyPlayEnd();
```


### 伴奏再生を一時停止する
 PauseAccompany インターフェースを呼び出し伴奏再生を一時停止します。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int PauseAccompany()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAccompany();
```


### 伴奏再生を再開する
ResumeAccompany インターフェースは伴奏再生の再開に使われています。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int ResumeAccompany()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAccompany();
```

### 自分に伴奏が聞こえるかどうかを設定する
このインターフェースは自分に伴奏が聞こえるかどうかを設定することに使われます。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int EnableAccompanyPlay(bool enable)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|--------------|
| enable    |bool             |聞こえるかどうか。|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->EnableAccompanyPlay(false);
```

### 他人にも伴奏が聞こえるかどうかを設定します
他人にも伴奏が聞こえるかどうかを設定します。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int EnableAccompanyLoopBack(bool enable)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|--------------|
| enable    |bool             |聞こえるかどうか。|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->EnableAccompanyLoopBack(false);
```

### 伴奏ボリュームを設定する
SetAccompanyVolume インターフェースを呼び出し伴奏ボリュームを設定します、ボリュームのデフォルト値が100です。数値が100以上の場合はゲインを上げ、数値が100以下の場合はゲインを下げます。数値範囲が0-200です。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int SetAccompanyVolume(int vol)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| vol    |int             |ボリュームの数値です。|

####  サンプルコード  
```
int vol=100;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetAccompanyVolume(vol);
```

### 伴奏再生のボリュームを取得する
GetAccompanyVolume インターフェースは伴奏ボリュームの取得に使われています。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int GetAccompanyVolume()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyVolume();
```

### 伴奏再生進捗を取得する
下記の二つのインターフェースは伴奏再生進捗の取得に使われています。注意事項：Current / Total = 現在循環回数、Current % Total = 現在再生循環の位置。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int GetAccompanyFileTotalTimeByMs()
ITMGAudioEffectCtrl virtual int GetAccompanyFileCurrentPlayedTimeByMs()
```
####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyFileTotalTimeByMs();
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyFileCurrentPlayedTimeByMs();
```


### 再生進捗を設定する
SetAccompanyFileCurrentPlayedTimeByMs インターフェースは再生進捗の設定に使われています。
####  関数のプロトタイプ  
```
ITMGAudioEffectCtrl virtual int SetAccompanyFileCurrentPlayedTimeByMs(unsigned int time)
```
|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| time    |int                |再生進捗はミリ秒を単位とします。|

####  サンプルコード  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetAccompanyFileCurrentPlayedTimeByMs(time);
```


## エラーコードリスト

|エラーコードの名|エラーコードの値|エラーコードの意味|解決方法|
|------|------|------|-----|
|QAV_ERR_ACC_OPENFILE_FAILED        |4001|ファイルを開くことに失敗しました|ファイルパス及びファイルが存在しているかどうかを確認し、ファイルにアクセスする権限があるかどうかを確認します。|
|QAV_ERR_ACC_FILE_FORAMT_NOTSUPPORT |4002|未対応のファイル形式です|ファイル形式が正しいかどうかを確認します。|
|QAV_ERR_ACC_DECODER_FAILED         |4003|デコードに失敗しました|ファイル形式が正しいかどうかを確認します。|
|QAV_ERR_ACC_BAD_PARAM              |4004|パラメータエラー|コードにおけるパラメータが正しいかどうかを確認します。|
|QAV_ERR_ACC_MEMORY_ALLOC_FAILED    |4005|メモリの割り当てに失敗しました|システムリソースが使い切られています、このエラーコードが続く場合、開発者に連絡してください。|
|QAV_ERR_ACC_CREATE_THREAD_FAILED   |4006|スレッドの作成は失敗しました|システムリソースが使い切られています、このエラーコードが続く場合、開発者に連絡してください。|
|QAV_ERR_ACC_STATE_ILLIGAL          |4007|不正な状態です|ある状態でないことです。この状態でないと呼び出せないインターフェースを呼び出した場合は、このエラーが発生します。|
