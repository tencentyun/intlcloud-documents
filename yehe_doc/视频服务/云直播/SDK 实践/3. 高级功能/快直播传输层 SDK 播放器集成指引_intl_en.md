## Overview
The libLebConnection SDK provides upgraded transfer capabilities based on the native WebRTC. It allows you to connect your existing player to LEB with just a few simple modifications. Based on LVB-compatible stream push and cloud-based media processing capabilities, it can implement live streaming at a low latency even under high concurrency, so as to help you smoothly migrate from standard LVB streaming to low-latency LEB streaming. For large rooms in modern real-time communication (RTC) scenarios, it can also help you quickly implement relayed live streaming at low costs and low latency.


## Feature Description

- The libLebConnection SDK can pull audio/video streams at a low latency even under poor network conditions.
- It can play back H.264. H.265, and AV1 videos with B frames and output them as raw video frame data such as Annex B and OBU files for H.264/H.265 and AV1 input videos respectively.
- It can play back AAC and Opus audios and output them as raw audio frame data.
- It supports Android, iOS, Windows, Linux, and macOS.


## Integration Method

### Basic API description

- Create a LEB connection.
```java
LEB_EXPORT_API LebConnectionHandle* OpenLebConnection(void* context, LebLogLevel loglevel);
```
- Register a callback function.
```java
LEB_EXPORT_API void RegisterLebCallback(LebConnectionHandle* handle, const LebCallback* callback);
```
- Start the connection to pull the stream.
```java
LEB_EXPORT_API void StartLebConnection(LebConnectionHandle* handle, LebConfig config);
```
- Stop the connection.
```java
LEB_EXPORT_API void StopLebConnection(LebConnectionHandle* handle);
```
- Close the connection.
```java
LEB_EXPORT_API void CloseLebConnection(LebConnectionHandle* handle);
```

### Callback API description
```java
typedef struct LebCallback {
  // The log callback
  OnLogInfo onLogInfo;
  // The video information callback
  OnVideoInfo onVideoInfo;
  // The audio information callback
  OnAudioInfo onAudioInfo;
  // The video data callback
  OnEncodedVideo onEncodedVideo;
  // The audio data callback
  OnEncodedAudio onEncodedAudio;
  // The `MetaData` callback
  OnMetaData onMetaData;
  // The statistics callback
  OnStatsInfo onStatsInfo;
  // The error callback
  OnError onError;
} LebCallback;
```

>! For the detailed definitions of data structures, see `leb_connection_api.h`.


### API call process
1. **Create an LEB connection**: `OpenLebConnection()`
2. **Register various callback functions**: `RegisterXXXXCallback()`
3. **Start the connection to pull the stream**: `StartLebConnection()`
4. **Call back and output the raw audio/video data**:
  - OnEncodedVideo()
  - OnEncodedAudio()
5. **Stop the connection**: `StopLebConnection()`
6. **Close the connection**: `CloseLebConnection`


### Integration sample
This [sample](https://mp.weixin.qq.com/s/f3ct29ydzAjdJ1fIdOmHmQ) describes how to integrate libLebConnection into the typical open-source player ijkplayer widely used on Android devices. For how to integrate it on other platforms, you can also refer to the sample code.

### Latest SDK version
You can download the libLebConnection SDK [here](https://github.com/tencentyun/libLebConnectionSDK/tree/main/libs).

## FAQs on Integration

### How do I develop the lag statistics collection feature?
As buffering is disabled, you can now collect lag statistics based on the video rendering interval. If the video rendering interval exceeds a certain threshold, it will be counted as a lag, and the lag duration will be added to the total lag duration.
Taking ijkplayer as an example, you can develop the lag statistics feature as follows:

1. **Modify the code**
   1. Add the variables required by lag statistics collection to the `VideoState` and `FFPlayer` structures.

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

    2. **Add the logic for lag statistics collection**

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

>! In this sample, the initial value of the lag threshold (`frozen_interval`) is `200(ms)`, which can be adjusted as needed.

2. **Test lag statistics collection**
Use QNET to simulate poor network conditions for the test as follows:
   1. Download QNET [here](https://wetest.qq.com/product/qnet/).
   2. Open QNET, click **Add** > **Template Type** > **Custom Template** and configure a template and parameters for poor network conditions as needed (the following is 30% random network packet loss during downstreaming).
   3. Select a program from the program list.
   4. Enable the configuration of poor network conditions for testing.

>! To facilitate testing, you can modify the above lag parameters and deliver the data to the Java layer through JNI to display it.

### How do I eliminate the noise during playback? (optimization of SoundTouch for Android)

To adjust the playback rate based on the buffer watermarks, you need to use SoundTouch to adjust the audio speed. However when many network fluctuations occur, multiple speed adjustments are required as the buffer watermarks are frequently adjusted, which may cause noise when the native ijkplayer calls SoundTouch. In this case, you can refer to the following code for optimization:

When SoundTouch is called for speed adjustment in low-latency playback mode, all the buffer is translated by SoundTouch.

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

### Why can't MediaCodec decode H.265 videos after it is enabled?
The libLebConnection SDK supports H.265 video streams, but if you enable `Using MediaCodec` in **Settings** in the native ijkplayer, H.265 video streams won't be decoded by MediaCodec. In this case, you can refer to the following code for optimization:
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