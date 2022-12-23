## 개요
libLebConnection SDK는 네이티브 WebRTC를 기반으로 업그레이드된 전송 기능을 제공합니다. 몇 가지 간단한 수정만으로 기존 플레이어를 LEB에 연결할 수 있습니다. LVB 호환 스트림 푸시 및 클라우드 기반 미디어 처리 기능을 기반으로 높은 동시성에서도 저지연 라이브 스트리밍을 구현할 수 있으므로 표준 LVB 스트리밍에서 지연 시간이 짧은 LEB 스트리밍으로 원활하게 마이그레이션할 수 있습니다. 최신 RTC(실시간 통신) 시나리오의 대형 회의실의 경우 저렴한 비용과 낮은 대기 시간으로 릴레이된 라이브 스트리밍을 신속하게 구현하는 데 도움이 될 수도 있습니다.


## 기능 소개

- libLebConnection SDK는 약한 네트워크 조건에서도 짧은 대기 시간으로 오디오/비디오 스트림을 가져올 수 있습니다.
- B 프레임이 있는 H.264, H.265 및 AV1 비디오를 재생하고 각각 H.264/H.265 및 AV1 입력 비디오에 대한 AnnexB 및 OBU 파일과 같은 원시 비디오 프레임 데이터로 출력할 수 있습니다.
- AAC 및 OPUS 오디오를 재생하고 원시 오디오 프레임 데이터로 출력할 수 있습니다.
- Android, iOS, Windows, Linux 및 Mac을 지원합니다.


## 통합 방식

### 기본 API 설명

- LEB 연결을 생성합니다
```java
LEB_EXPORT_API LebConnectionHandle* OpenLebConnection(void* context, LebLogLevel loglevel);
```
- 콜백 함수를 등록합니다
```java
LEB_EXPORT_API void RegisterLebCallback(LebConnectionHandle* handle, const LebCallback* callback);
```
-  스트림을 가져오기 위해 연결을 시작합니다
```java
LEB_EXPORT_API void StartLebConnection(LebConnectionHandle* handle, LebConfig config);
```
- 연결을 중지합니다
```java
LEB_EXPORT_API void StopLebConnection(LebConnectionHandle* handle);
```
- 연결을 닫습니다
```java
LEB_EXPORT_API void CloseLebConnection(LebConnectionHandle* handle);
```

### 콜백 API 설명
```java
typedef struct LebCallback {
  // 로그 콜백
  OnLogInfo onLogInfo;
  // 비디오 정보 콜백
  OnVideoInfo onVideoInfo;
  // 오디오 정보 콜백
  OnAudioInfo onAudioInfo;
  // 비디오 데이터 콜백
  OnEncodedVideo onEncodedVideo;
  // 오디오 데이터 콜백
  OnEncodedAudio onEncodedAudio;
  // MetaData 콜백
  OnMetaData onMetaData;
  // 통계 콜백
  OnStatsInfo onStatsInfo;
  // 오류 콜백
  OnError onError;
} LebCallback;
```

>! 데이터 구조의 자세한 정의는 `leb_connection_api.h`를 참고하십시오.


### API 호출 프로세스
1. **LEB 연결 생성**: OpenLebConnection()
2. **다양한 콜백 함수 등록**: RegisterXXXXCallback()
3. **스트림을 가져오기 위한 연결 시작**: StartLebConnection()
4. **원시 오디오/비디오 데이터를 콜백하고 출력**:
  - OnEncodedVideo()
  - OnEncodedAudio()
5. **연결 중지**: StopLebConnection()
6. **연결 닫기**: CloseLebConnection


### 통합 예시
이 [예시](https://mp.weixin.qq.com/s/f3ct29ydzAjdJ1fIdOmHmQ)는 Android 기기에서 널리 사용되는 일반적인 오픈 소스 플레이어 ijkplayer에 libLebConnection을 통합하는 방법을 설명합니다. 다른 플랫폼에 통합하는 방법은 예시 코드를 참고할 수도 있습니다.

### 최신 SDK 버전
[여기](https://github.com/tencentyun/libLebConnectionSDK/tree/main/libs)에서 libLebConnection SDK를 다운로드할 수 있습니다.

## 통합에 대한 FAQ

### 랙 통계 기능 개발
버퍼링이 비활성화되었으므로 이제 비디오 렌더링 간격을 기반으로 랙 통계를 수집할 수 있습니다. 비디오 렌더링 간격이 특정 임계값을 초과하면 랙으로 간주되고 랙 기간이 총 랙 기간에 추가됩니다.
ijkplayer를 예로 들면 다음과 같이 랙 통계 기능을 개발할 수 있습니다.

1. **코드 수정**
   1. 랙 통계 수집에 필요한 변수를 VideoState 및 FFPlayer 구조에 추가합니다.

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

    2. **랙 통계 로직 추가**

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

>! 이 예시에서 랙 임계값(frozen_interval)의 초기 값은 `200(ms)`이며 필요에 따라 조정할 수 있습니다.

2. **테스트 랙 통계 수집**
QNET을 사용하여 다음과 같이 약한 네트워크 조건을 시뮬레이션하여 테스트를 진행합니다.
   1. [여기](https://wetest.qq.com/product/qnet/)에서 QNET을 다운로드합니다.
   2. QNET을 열고 **추가** > **템플릿 유형** > **사용자 지정 템플릿**을 클릭하고 필요에 따라 약한 네트워크 조건에 대한 템플릿과 매개변수를 구성합니다(다음은 다운스트림 중 30% 임의 네트워크 패킷 손실).
   3. 프로그램 목록에서 프로그램을 선택합니다.
   4. 테스트를 위해 약한 네트워크 조건 구성을 활성화합니다.

>! 테스트를 용이하게 하기 위해 상기 랙 매개변수를 수정하고 데이터를 jni를 통해 Java 레이어에 전달하여 표시할 수 있습니다.

### 재생 중 노이즈 문제 해결(Android soundtouch 최적화)

buffer 워터마크를 기반으로 재생 속도를 조정하려면 soundtouch를 사용하여 오디오 속도를 조정해야 합니다. 그러나 네트워크 변동이 많은 경우 buffer 워터마크를 자주 조정하므로 여러 속도 조정이 필요하며, 이는 네이티브 ijkplayer가 soundtouch를 호출할 때 노이즈가 발생할 수 있습니다. 이 경우 최적화를 위해 다음 코드를 참고할 수 있습니다.

저지연 재생 모드에서 속도 조정을 위해 soundtouch가 호출되면 모든 버퍼가 soundtouch에 의해 translate됩니다.

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

### MediaCodec이 활성화된 후 H.265 비디오를 디코딩할 수 없는 이유는 무엇입니까?
libLebConnection SDK는 H.265 비디오 스트림을 지원하지만 네이티브 ijkplayer의 **Settings**에서 `Using MediaCodec`을 활성화하면 H.265 비디오 스트림이 MediaCodec에 의해 디코딩되지 않습니다. 이 경우 다음 코드를 참고하여 최적화할 수 있습니다.
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