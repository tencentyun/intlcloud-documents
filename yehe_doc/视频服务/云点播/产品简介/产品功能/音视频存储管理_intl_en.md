## System Architecture
<img src="https://qcloudimg.tencent-cloud.cn/raw/fab36bc70e18363d8b6a611a765ef61d.png" width="650">

## Product Features
### Audio/video upload
You can upload files from your local file system or upload files via URL or using API. VOD supports checkpoint restart, large file upload, and multi-replica backup. For details, see [Media Upload Overview](https://intl.cloud.tencent.com/document/product/266/9760).
Supported file formats for upload include:

* Video: WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WEBM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, and OGG
* Audio: MP3, M4A, FLAC, OGG, WAV, RA, AAC, and AMR
* Thumbnail: JPG, JPEG, PNG, GIF, BMP, TIFF, AI, CDR, EPS, and TIF

### Audio/video storage
VOD supports redundant data storage across architectures and devices. It provides 99.9% durability of objects, outperforming traditional architectures. It also supports multiple storage classes to meet a variety of needs.
* Storage classes: STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE.
* Lower storage costs: Custom rule-based storage policies, auto-deletion of media files, and real-time image processing.

### Media asset management
You can manage your media files by adding categories and labels to them from the VOD console or via API. You can also export all the information of your media files.

- Quickly edit media file information
- Use filters to search for specific types of media files
- Media file processing, transcoding, watermarking, thumbnail generation, and screen capture
- Export media file information in CSV or JSON format
- Set multiple levels of categories and labels for videos
- Manage, preview, and download media files
- Store files with multiple storage classes
- Set hotlink protection with allowlists/blocklists

  


