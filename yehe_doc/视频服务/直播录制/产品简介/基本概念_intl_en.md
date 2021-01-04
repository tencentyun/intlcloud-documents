### Recording Template

When a live stream is recorded into VOD, VOD will use this template to transcode the video.

### Recording Rule

You can bind the recording template to a rule at the specified level. Then, when the push starts, the bound rule will be executed for recording.

### Recording Task

You can create a recording task with custom time settings to achieve flexible recording.

### Automatic Splicing and Resuming

When a live stream is recorded in HLS format, you can enable the automatic splicing and resuming feature and enter the value of the resuming timeout period for stream interruption. Then, if the interruption duration does not exceed the timeout period, the live streams before and after the interruption will be automatically spliced into one recording file.

> ! After the automatic splicing and resuming feature is enabled, the system will wait for the resuming timeout period to elapse before starting to generate a recording file, which will lead to a longer time for getting the recording file.

### Automatic Transcoding

After the video is recorded into VOD, a transcoding task will be automatically triggered.

### Manual Transcoding

After the video is recorded into VOD, you can trigger transcoding manually.

### Adaptive Bitrate Streaming

You can simultaneously output multiple transcoded streams and select the optimal one for playback based on the quality of the network connection.
