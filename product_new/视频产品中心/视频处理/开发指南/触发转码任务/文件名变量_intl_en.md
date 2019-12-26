In MPS, you can not only set the output path and bucket for transcoded files, but also set the output files with a wide variety of variables. Filename variables supported by MPS and their definitions are as shown below:

| Variable | Definition | Example | Output Example <br>(Taking Source Filename `video.mp4` as an Example) |
| :--: | :--: | :--: | :--- |
| {inputName} | Source filename <br>(excluding the directory and file extension) |  `{inputName}_transcode`  | Transcoded to MP4: <br>`video_transcode.mp4` <br> Transcoded to FLV: <br>`video_transcode.flv` |
| {number} | Output file number | `{inputName}_snapshot_{number}` | Sampled screenshot in JPG format: <br>`video_snapshot_0.jpg` <br>**...** <br>`video_snapshot_20.jpg` |
| {format}  | File output format  | `{inputName}_transcode.{format}`| Transcoded to HLS: <br>`video_transcode.m3u8` <br> Transcoded to MP4: <br>`video_transcode.mp4`  |
| {definition} | Parameter template ID | `{inputName}_transcode_{definition}` | Transcoded to HD MP4: <br>`video_transcode_30.mp4` <br> Transcoded to LD MP4: <br>`video_transcode_10.mp4`  |

A filename variable is generally used to mark and identify output files to avoid file overwriting due to duplicate names. You can use one or more variables as needed. You can also add any constant strings to mark filenames such as "transcode" and "snapshot" in the above table.
