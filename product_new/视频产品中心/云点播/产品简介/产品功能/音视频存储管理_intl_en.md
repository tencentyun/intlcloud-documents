## System Architecture
<img src="https://main.qcloudimg.com/raw/146d801f4900734b8faa0435b34ea6cc.png" width="650">

## Features
### Audio/video upload
VOD offers a wide selection of options for video upload to meet your upload requirements in various scenarios, including local file upload, URL file pull, and upload via API. It supports resumable upload, large file upload, and redundant file backup.
Supported formats for upload include:

* Video: MP4, TS, FLV, WMV, ASF, RM, RMVB, MPG, MPEG, 3GP, MOV, WEBM, AVI.
* Audio: MP3, M4A, FLAC, OGG, and WAV.

### Audio/video storage
VOD features redundant storage of video files across architectures and devices to support remote disaster recovery and isolation of resources. It achieves 99.9% persistence for file objects, which is higher than that on traditional architectures. In addition, it supports cold/hot backup for video file storage, offering more choices to meet your diverse storage needs.

### Media asset management
VOD allows you to manage video files through the console or API by performing such operations as categorization and tagging. All the information can be exported for viewing.

- Video information editing
- Fuzzy search for videos
- Video transcoding, watermarking, and cover setting
- Export of video information in CSV format
- Video sharing via WeChat QR code
- Multi-level categorization and tagging of videos
- List-based video management and online preview
- Cold backup and storage of videos
- Blacklist/whitelist hotlink protection
- Dynamic URL hotlink protection
- APIs for video release via WeChat Official Account

### Origin server sync
With this feature, the video files stored on other origin servers can be seamlessly synced and backed up to Tencent Video Cloud Storage with the original directory structure and playback URLs unchanged.
