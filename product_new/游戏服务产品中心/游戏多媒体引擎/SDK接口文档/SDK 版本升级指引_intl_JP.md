開発者がTencent Cloud Gaming Multimedia Engine製品APIのデバッグやアクセスを行いやすいように、開発向けのインターフェースアップグレード技術ドキュメント（GME 2.2がらGME 2.3.5へ）について説明させていただきます。

## SDKの変更
### 新規追加機能
- リアルタイム音声チャット中のオフライン音声利用を対応します。
- リアルタイム音声チャットのフィルタリングを対応し、暴力、テロ、エロチック、政治的なコンテンツを識別することができます。
- H5リアルタイム音声チャットを対応し、オールプラットフォーム間のリアルタイム音声相互通信を実現しています。
- Android v8aアーキテクチャの対応を新規に追加しています。
- Androidでの低レイテンシーキャプチャーと再生を対応します。

### 機能の最適化
- SDK範囲音声機能のインターフェースを最適化し、アクセスするハードルを下げています。
- 音声ノイズ低減の効果を最適化しています。
- SDKのメモリ消費量を大幅に下げています。

## 主なインターフェースの変更
### EnterRoom 
入室操作は同期コールから非同期コールに変更しました。戻り値が0である場合、非同期デリバリーが成功し、コールバック関数による処理を待つことを示します。戻り値が0でない場合、非同期デリバリーが失敗したことを示します。

```
public abstract int EnterRoom();
```

### ExitRoom 
退室操作は同期コールから非同期コールに変更しました。RoomExitCompleteコールバック関数の処理を参照し、戻り値がAV_OKである場合、非同期デリバリーが成功したことを示します。

>!アプリケーション作動中に退室してから直ちに入室するケースがある場合、インターフェースの呼び出しプロセスで、開発者はExitRoomのコールバックRoomExitComplete通知を待つ必要がなく、インターフェースを直接に呼び出せばよいです。

```
public abstract int EnterRoom();
```

## エラーコードの変更
すべてのエラーコードを一括処理する場合は、!AV_OKを使ってください。 

タイプごとにエラーを処理するには、インターフェースから戻されたエラータイプに注意してください。エラーコード「1」は明確な意味がなく、かつ2.3.5以降のバージョンでは戻されなくなったため、削除しました。


## その他インターフェースの変更
### PauseAudio/ResumeAudio 

```
public int PauseAudio()
public int ResumeAudio()
```

2.3以前のバージョンにおけるSDKインターフェース呼び出しプロセスでは、ITMGAudioCtrl::PauseAudio/ResumeAudioという2つのインターフェースを呼び出す場合は、下記の表を参照しバージョンを比較してください。


|2.3以前のバージョン|2.3バージョンへのアップグレード|
|---|---|
|使用目的は他のモジュールと相互排他することである|PauseAudioを Pauseに、ResumeAudioをResumeに変更してください|
|使用目的はリアルタイム音声チャット中のオフライン音声利用である|PauseAudioとResumeAudioを削除してください|


### SetLogLevelインターフェースパラメータの変更

#### 元インターフェース
```
ITMGContext virtual void SetLogLevel(int logLevel, bool enableWrite, bool enablePrint)
```

#### 新しいインターフェース
```
ITMGContext virtual void SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### パラメータの意味

|パラメータ|タイプ|意味|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|ログに書き込むレベルを設定する。TMG_LOG_LEVEL_NONEは書き込まないことを示す|
|levelWrite|ITMG_LOG_LEVEL|ログをプリントするレベルを設定する。TMG_LOG_LEVEL_NONEはプリントしないことを示す|

#### ITMG_LOG_LEVEL タイプ

|ITMG_LOG_LEVEL|意味|
|-------------------------------|-------------|
|TMG_LOG_LEVEL_NONE=0|ログをプリントしない|
|TMG_LOG_LEVEL_ERROR=1|エラーログをプリントする（デフォルト）|
|TMG_LOG_LEVEL_INFO=2|ヒントログをプリントする|
|TMG_LOG_LEVEL_DEBUG=3|開発デバッグログをプリントする|
|TMG_LOG_LEVEL_VERBOSE=4|多発ログをプリントする|
