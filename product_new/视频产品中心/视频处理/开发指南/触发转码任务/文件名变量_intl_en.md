In addition to setting the output path and bucket for transcoded files, you can also customize output filenames with variables. Filename variables supported by MPS and their definitions are as shown below:

| Variable | Definition | Example | Output Example <br>(Taking Source Filename `video.mp4` as an Example) |
| :--: | :--: | :--: | :--- |
| {inputName} | Source filename <br>(excluding the directory and file extension) |  `{inputName}_transcode`  | Transcoded to MP4: <br>`video_transcode.mp4` <br> Transcoded to FLV: <br>`video_transcode.flv` |
| {number} | Output file number | `{inputName}_snapshot_{number}` | Sampled screenshot in JPG format: <br>`video_snapshot_0.jpg` <br>**...** <br>`video_snapshot_20.jpg` |
| {format}  | Output file format  | `{inputName}_transcode.{format}`| Transcoded to HLS: <br>`video_transcode.m3u8` <br> Transcoded to MP4: <br>`video_transcode.mp4`  |
| {definition} | Parameter template ID | `{inputName}_transcode_{definition}` | Transcoded to HD MP4: <br>`video_transcode_30.mp4` <br> Transcoded to LD MP4: <br>`video_transcode_10.mp4`  |
| {inputDir} | Source file path (begins and ends with `/`) | `/copy{inputDir}{inputName}_transcode` | Input path:`/`：<br>`/copy/video_transcode.mp4`<br>Input path:`/input/`：<br>`/copy/input/video_transcode.mp4`  |


A filename variable is generally used to label and identify output files. This helps you create unique names to avoid file overwriting. You can use one or more variables as needed. You can also add any constant strings to label filenames such as "transcode" and "snapshot" in the above table.
