## 概要説明
LEB転送レイヤーSDK (libLebConnection)はネイティブWebRTCエンハンス版をベースにした転送機能を提供します。ユーザは既存のプレイヤーを簡単に改造するだけで、LEBに迅速に導入できます。LVBのプッシュ、クラウド側のメディア処理機能と完全な互換性を持った上で、高並列低遅延のストリーミングを実装しています。これにより、ユーザは既存のLVBからスムーズにLEBに移行できるだけではなく、既存のRTCシーンでコストの低いビッグルーム低遅延バイパスライブストリーミングを速やかに実装することもできます。


## 機能説明

- オーディオビデオプル。低遅延の性能と遅くて安定しないネットワーク対策機能を備えています
- ビデオはH.264、H.265、AV1をサポートします。Bフレームをサポートします。ビデオ出力フォーマットはビデオフレームの生データです（H.264/H.265はAnnexB、AV1はOBU）
- オーディオはAACとOPUSをサポートします。オーディオ出力フォーマットはオーディオフレームの生データです
- Android、iOS、Windows、Linux、Macをサポートします


## 導入方法

### 基本インターフェースの説明

- LEB接続を作成します
```java
LEB_EXPORT_API LebConnectionHandle* OpenLebConnection(void* context, LebLogLevel loglevel);
```
- コールバック関数を登録します
```java
LEB_EXPORT_API void RegisterLebCallback(LebConnectionHandle* handle, const LebCallback* callback);
```
-  接続してプルします
```java
LEB_EXPORT_API void StartLebConnection(LebConnectionHandle* handle, LebConfig config);
```
- 接続を停止します
```java
LEB_EXPORT_API void StopLebConnection(LebConnectionHandle* handle);
```
- 接続を終了します
```java
LEB_EXPORT_API void CloseLebConnection(LebConnectionHandle* handle);
```

### コールバックインターフェースの説明
```java
typedef struct LebCallback {
  // ログのコールバック
  OnLogInfo onLogInfo;
  // ビデオ情報のコールバック
  OnVideoInfo onVideoInfo;
  // オーディオ情報のコールバック
  OnAudioInfo onAudioInfo;
  // ビデオデータのコールバック
  OnEncodedVideo onEncodedVideo;
  // オーディオデータのコールバック
  OnEncodedAudio onEncodedAudio;
  // メタデータのコールバック
  OnMetaData onMetaData;
  // 集計情報のコールバック
  OnStatsInfo onStatsInfo;
  // エラーのコールバック
  OnError onError;
} LebCallback;
```

>! データ構造の定義については、ヘッダーファイル`leb_connection_api.h`をご参照ください。


### インターフェースの呼出しフロー
1. **LEB接続を作成**：OpenLebConnection()
2. **各コールバック関数を登録**：RegisterXXXXCallback()
3. **接続してプルを開始**：StartLebConnection()
4. **オーディオビデオ生データをコールバックして出力**：
  - OnEncodedVideo()
  - OnEncodedAudio()
5. **接続を停止**：StopLebConnection()
6. **接続を終了する**：CloseLebConnection


### 導入例
この[例](https://mp.weixin.qq.com/s/f3ct29ydzAjdJ1fIdOmHmQ) では、Androidで広く使用されている代表的なオープンソースプレイヤーijkplayerを使用し、LEB転送レイヤーSDKに迅速に導入する方法とその流れを説明します。他のOSについては、この例を参考にして統合を実施してください。

### 最新SDKのダウンロード
LEB転送レイヤーlibLebConnection SDKについては、[SDKのダウンロード](https://github.com/tencentyun/libLebConnectionSDK/tree/main/libs)をご参照ください。

## 統合に関するよくあるご質問

### ラグ集計機能の開発
bufferingを無効にしているため、レンダリング更新時間の間隔を集計することで、ラグパラメータを集計できます。ビデオのレンダリング時間の間隔が閾値を超えると、1回のラグとしてカウントし、ラグ時間も累計します。
以下では、ijkplayerを例として、ラグ集計機能を実装するフローを説明します。

1. **ソースコードの修正**
   1. VideoState構造体とFFPlayer構造体に、ラグ集計に必要な変数を追加します。

```diff
diff --git a/ijkmedia/ijkplayer/ff_ffplay_def.h b/ijkmedia/ijkplayer/ff_ffplay_def.h
index 00f19f3c..f38a790c 100755
--- a/ijkmedia/ijkplayer/ff_ffplay_def.h
+++ b/ijkmedia/ijkplayer/ff_ffplay_def.h
@@ -418,6 +418,14 @@ typedef struct VideoState {
     SDL_cond  *audio_accurate_seek_cond;
     volatile int initialized_decoder;
     int seek_buffering;
+
+    int64_t stream_open_time;
+    int64_t first_frame_display_time;
+    int64_t last_display_time;
+    int64_t current_display_time;
+    int64_t frozen_time;
+    int frozen_count;
+    float frozen_rate;
 } VideoState;
 
 /* options specified by the user */
@@ -720,6 +728,14 @@ typedef struct FFPlayer {
     char *mediacodec_default_name;
     int ijkmeta_delay_init;
     int render_wait_start;

     int low_delay_playback;
+    int frozen_interval;
     int high_level_ms;
     int low_level_ms;

     int64_t update_plabyback_rate_time;
     int64_t update_plabyback_rate_time_prev;
 } FFPlayer;
 
 #define fftime_to_milliseconds(ts) (av_rescale(ts, 1000, AV_TIME_BASE))
@@ -844,6 +860,15 @@ inline static void ffp_reset_internal(FFPlayer *ffp)
     ffp->pf_playback_volume             = 1.0f;
     ffp->pf_playback_volume_changed     = 0;
 
     ffp->low_delay_playback             = 0;
 
     ffp->high_level_ms                  = 500;
     ffp->low_level_ms                   = 200;
+    ffp->frozen_interval                = 200;
 
     ffp->update_plabyback_rate_time      = 0;
     ffp->update_plabyback_rate_time_prev = 0;

     av_application_closep(&ffp->app_ctx);
     ijkio_manager_destroyp(&ffp->ijkio_manager_ctx);
```

    2. **ラグ集計ロジックの追加**

```diff
diff --git a/ijkmedia/ijkplayer/ff_ffplay.c b/ijkmedia/ijkplayer/ff_ffplay.c
index 714a8c9d..c7368ff5 100755
--- a/ijkmedia/ijkplayer/ff_ffplay.c
+++ b/ijkmedia/ijkplayer/ff_ffplay.c
@@ -874,6 +874,25 @@ static void video_image_display2(FFPlayer *ffp)
     VideoState *is = ffp->is;
     Frame *vp;
     Frame *sp = NULL;
+    int64_t display_interval = 0;
+
+    if (!is->first_frame_display_time){
+        is->first_frame_display_time = SDL_GetTickHR() - is->stream_open_time;
+    }
+    
+    is->last_display_time = is->current_display_time;
+    is->current_display_time = SDL_GetTickHR() - is->stream_open_time;
+    display_interval = is->current_display_time - is->last_display_time;
+    av_log(NULL, AV_LOG_DEBUG, "last_display_time:%"PRId64" current_display_time:%"PRId64" display_interval:%"PRId64"\n", is->last_display_time, is->current_display_time, display_interval);
+
+    if (is->last_display_time > 0) {
+        if (display_interval > ffp->frozen_interval) {
+            is->frozen_count += 1;
+            is->frozen_time += display_interval;
+        }
+    }
+    is->frozen_rate = (float) is->frozen_time / is->current_display_time;
+    av_log(NULL, AV_LOG_DEBUG, "frozen_interval:%d frozen_count:%d frozen_time:%"PRId64" is->current_display_time:%"PRId64" frozen_rate: %f ", ffp->frozen_interval, is->frozen_count, is->frozen_time, is->current_display_time, is->frozen_rate);
 
     vp = frame_queue_peek_last(&is->pictq);
```

>! この例では、ラグの閾値frozen_intervalを`200(ms)`に初期化しています。必要に応じて調整してください。

2. **ラグパラメータ集計テスト**
QNETを使用し遅くて安定しないネットワークをシミュレートしてテストを実施します。具体的な手順は以下のとおりです：：
   1. [QNETネットワークテストツール](https://wetest.qq.com/product/qnet/)をダウンロードします。
   2. QNETを起動し、**追加** > **テンプレートタイプ** > **カスタムテンプレート**をクリックし、必要に応じて遅くて安定しないネットワークのテンプレートとパラメータを設定します（下図に示す設定は、下りリンクで30%のランダムパケットドロップ率です）。
   3. プログラムリストからテストプログラムを選択します。
   4. 遅くて安定しないネットワークを有効にしてテストを始めます。

>! 簡単にテストするために、上記のラグパラメータに対する変更は、jniを使用しデータをJavaレイヤーに転送して表示できます。

### 再生中にノイズがある問題の解決方法（Android soundtouchの最適化）

buffer水位に応じて再生レートを変更するのは、soundtouchを使用しオーディオの速度を変更することで実装します。しかし、フリピングが大きく、buffer水位を頻繁に調整するには、速度を複数回変更する必要があります。ネイティブijkplayerがsoundtouchを呼び出すことにより、ノイズが発生する可能性があります。以下のソースコードを参考にして最適化してください：

soundtouchを呼び出して速度を変更する時、低遅延再生モードの場合、すべてのbufferはsoundtouchでtranslateを行います。

```diff
diff --git a/ijkmedia/ijkplayer/ff_ffplay.c b/ijkmedia/ijkplayer/ff_ffplay.c
index 714a8c9d..c7368ff5 100755
--- a/ijkmedia/ijkplayer/ff_ffplay.c
+++ b/ijkmedia/ijkplayer/ff_ffplay.c
@@ -2579,7 +2652,7 @@ reload:
         int bytes_per_sample = av_get_bytes_per_sample(is->audio_tgt.fmt);
         resampled_data_size = len2 * is->audio_tgt.channels * bytes_per_sample;
 #if defined(__ANDROID__)
-        if (ffp->soundtouch_enable && ffp->pf_playback_rate != 1.0f && !is->abort_request) {
+        if (ffp->soundtouch_enable && (ffp->pf_playback_rate != 1.0f || ffp->low_delay_playback) && !is->abort_request) {
             av_fast_malloc(&is->audio_new_buf, &is->audio_new_buf_size, out_size * translate_time);
             for (int i = 0; i < (resampled_data_size / 2); i++)
             {

```

### MediaCodecを有効にした場合、MediaCodecを使用してH.265形式のビデオをデコードしない問題の解決方法
H.265形式のビデオストリームをサポートするのは、LEB転送レイヤーの特徴です。しかし、ネイティブijkplayerは、**Settings**で`Using MediaCodec`にチェックを入れて有効にした後、MediaCodecを使用してH.265形式のビデオストリームをデコードしません。以下のソースコードを参考にして最適化してください：
```diff
diff --git a/ijkmedia/ijkplayer/ff_ffplay_options.h b/ijkmedia/ijkplayer/ff_ffplay_options.h
index b021c26e..958b3bae 100644
--- a/ijkmedia/ijkplayer/ff_ffplay_options.h
+++ b/ijkmedia/ijkplayer/ff_ffplay_options.h
@@ -178,8 +178,8 @@ static const AVOption ffp_context_options[] = {
         OPTION_OFFSET(vtb_handle_resolution_change),    OPTION_INT(0, 0, 1) },
 
     // Android only options
-    { "mediacodec",                             "MediaCodec: enable H.264 (deprecated by 'mediacodec-avc')",
-        OPTION_OFFSET(mediacodec_avc),          OPTION_INT(0, 0, 1) },
+    { "mediacodec",                             "MediaCodec: enable all_videos (deprecated by 'mediacodec_all_videos')",
+        OPTION_OFFSET(mediacodec_all_videos),   OPTION_INT(0, 0, 1) },
     { "mediacodec-auto-rotate",                 "MediaCodec: auto rotate frame depending on meta",
         OPTION_OFFSET(mediacodec_auto_rotate),  OPTION_INT(0, 0, 1) },
     { "mediacodec-all-videos",                  "MediaCodec: enable all videos",
```