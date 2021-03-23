### Profile

Profiles are a “family” of encoding techniques targeted for specific application scenarios. The three most commonly applied H.264 profiles are:

- Baseline: it includes I- and P-frames. This profile is designed for progressive video and supports CAVLC entropy coding. It is used primarily in low-cost applications or those needing extra fault tolerance, for instant messaging scenarios such as video call, and mobile video.
- Main: it includes I-, P-, and B- frames. This profile is for progressive and interlaced videos, and supports CAVLC and CABAC entropy coding. It is used in videos for mainstream consumer electronic devices, such as MP4 with relatively low decoding rate, portable video player, PSP and iPod.
High: it adds 8x8 internal prediction, custom quantification, lossless video encoding and more YUV formats (e.g., 4:4:4) on the basis of main profile. High profile is used for broadcast and video disc storage (Blu-ray movies), and HDTV applications.

### Sampling rate

Sampling rate defines the number of samples per second (in Hz) taken from a continuous signal to make a discrete signal. 

### Superplayer

Supeperplayer is a player SDK that VOD provides for [long video playback](https://intl.cloud.tencent.com/document/product/266/38295) scenarios. VOD offers Android, iOS, and Web-client players. `FileId` parameter is used to uniquely identify videos in VOD for playback.

### Superplayer configuration

When the superplayer plays back a video with a certain `FileId`, the superplayer configuration specifies:

- Adaptive bitrate streaming used for playback.
- Image sprite used for thumbnail preview.
- Substream definition name used for player display.

For the specific features and using methods, see [Superplayer Configuration](https://intl.cloud.tencent.com/document/product/266/38296).

### Superplayer signature

A superplayer signature is used by the application playback service to authorize a client for playback. If the playback service allows the client to play back, it will distribute a valid signature to the client. The client can play back the video within the validity period of the signature. An application terminal needs a superplayer signature before it can play back the video in the following circumstances:

- [Key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986) has been enabled for the domain name.
- Other [superplayer configurations](https://intl.cloud.tencent.com/document/product/266/38296) than the `default` one has been used.
- An [encrypted](https://intl.cloud.tencent.com/document/product/266/38294) video needs to be played back.

For specific features and using methods, see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).

### Sampling interval

Sampling interval refers to extracting video frames at a certain time interval for video AI processing. Generally, the shorter the sampling interval, the finer the results of recognition, and analysis, but the longer the processing time.

### CNAME

An alias record that resolves one domain name to another. You can use CNAME to point multiple host names to one alias so that you can quickly change IP addresses.

### CNAME record

A CNAME (Canonical Name) record refers to the alias record in a domain name resolution.
For example, a server named `host.example.com` provides both WWW and MAIL services. To make it easier for users to access those services, two CNAME records (`www.example.com` and `mail.example.com`) can be added for this server at its DNS service provider, and all requests to access these two CNAME records will be forwarded to `host.example.com`.

### Resolution

Resolution determines a video's capability to resolve details and is represented by the number of pixels in each dimension, such as 640 x 480.

### Container format

The encoded and compressed video stream and audio stream are put into one file according to a certain format specification, which is container format. For on-demand content, a more appropriate term should be "streaming media transport protocol". The most widely used protocols in the Internet are as follows:

- **MP4**: a classic file format well supported by iOS, Android, PC Web clients. However, the header of an MP4 file is often too large and complicated. For a long video (e.g., several hours), a large file header will slow down video loading. Therefore, this protocol is more suitable for short video scenarios.
- **HLS (HTTP Live Streaming)**: a protocol developed by Apple and well compatible with iOS and Android clients.  For Internet Explorer to support HLS, secondary development of Flash player is needed (Tencent Cloud's Flash player control is recommended). With a streamlined M3U8 index structure, HLS does not have MP4's drawback of slow indexing and is a favorable choice for on-demand content.
- **FLV**: a protocol developed by Adobe and well supported by Flash player on PCs, but requires a player on applications if FLV format is to be used on mobile clients (Tencent Cloud's Flash player control is recommended). Most mobile browsers do not support FLV.

### GOP

A GOP (group of pictures) refers to a collection of successive pictures within an MPEG encoded video stream. It starts with an I-frame and ends with the next I-frame. A GOP can contain the following types of pictures:

I-frame: intra encoded picture. It is in block-based frame and is a fixed image independent of other image types. Each GOP begins with this type of image.
- P-frame: predictive coded picture. It contains the information of the difference from the previous I or P frame.
B-Frame: bidirectionally predictive coded picture, which contains the information of difference from the previous and/or the latter I or P frame.

The number of frames within a GOP is called GOP length.

### HTTP method

HTTP defines a set of request methods to indicate the desired action to be performed for a given resource. For commonly used GET, HEAD, POST methods, see [HTTP request methods](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods).

### HTTP protocol identifier

An HTTP protocol identifier refers to a specific protocol used to request media files, namely, HTTP or HTTPS.

### HTTP status code

An HTTP status code (or HTTP response status code) indicates whether an HTTP request has been successfully completed. There are five categories of status codes: information response (100-199), response success (200-299), redirection (300-399), client error (400-499), and server error (500-599). For more information, please see [HTTP Response Codes](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status) and [RFC 2616](https://tools.ietf.org/html/rfc2616#section-10).

### Cache Hit/Miss

Cache hit/miss indicates whether a media access request needs to go back to the origin server. If the request hits any level in the CDN multi-level cache, it is a hit; otherwise, it is a miss.

### Cache purge

Cache purge is to clear the cache of corresponding media files on the CDN nodes. It is usually used to ensure that the latest content can be obtained by clearing the corresponding CDN cache when the media content changes.

### ISO date format

ISO date format is a time format as specified in ISO 8601. In VOD, unless otherwise specified, all time-related parameters use UTC time in ISO 8601 standard (in the format of YYYY-MM-DDThh:mm:ssZ). For example, 2018-10-01T10:00:00Z represents 18:00:00 on October 1, 2018 Beijing Time (UTC+8).

### IDR frame alignment

An IDR (instantaneous decoding refresh) picture is a type of I frame. Different from a common I frame where P and B frames after it can reference other I frames before it, no frames after an IDR frame can reference any frames before it.

In VOD scenarios, a player generally allows dragging on the progress bar to a desired position. The most convenient way is to start playback from the IDR picture in close proximity to that position, because it is clear for the player that all frames after the IDR frame will not reference other I frames before it, thus avoiding complicated reverse resolution.

If IDR frame alignment is specified when multi-bitrate transcoding is performed on a video, IDR frames of all the output videos will be precisely aligned by time point and picture content, so that video players can smoothly switch among videos at different bitrates without obvious lagging.

If you enable IDR frame alignment on the VOD platform during transcoding, the settings of frame rate, GOP length, codec, and container format of multiple output formats must be identical.

### Basic player

VOD provides player SDKs for Android, iOS, and Web clients for [short video playback](https://intl.cloud.tencent.com/document/product/266/38295). The URL contains parameters used for playing back on-demand videos.

### Bitrate

Bitrate refers to the number of bits that are required in playback of continuous media (e.g., compressed audio or video) per unit time. It is measured in bit/s (or bps).

### Content prefetch 

Content prefetch is to prefetch the media content to CDN nodes in advance, which can effectively improve the playback quality when the content is accessed again.

### Deinterlacing

In the era of analog television, the processing speed and network bandwidth of playback devices were limited. Thus, interlacing technology was developed to deliver videos at lower bitrates without reducing the source frame rates. It can reduce the video transmission bandwidth by 50% while basically retaining source image quality. However, it has noticeable negative effects such as low definition, flickering, and jagged image edges.
As video playback devices have been advanced and network bandwidth have been improved, interlacing gradually becomes outdated and is not supported by some new device models. Therefore, old videos that were processed with interlacing need to be "deinterlaced".

### Range parameter

The `Range` parameter is the response content range specified by the `Range` header in an HTTP request. When a modern player plays back a large media file, it usually doesn't download the entire file; instead, it requests the file in segments. A `Range` request allows the server to send only a part of the media file to the client for playback. For more information, please see [HTTP range requests](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Range_requests).

### Sound channel

A sound channel refers to an independent audio signal collected or played back from different spatial positions when the sound is recorded or played back. The number of sound channels is the number of sound sources during recording or number of speakers during playback.

### Video codec

A video codec refers to a program or a device that can compress or decompress (video decoding) digital videos. The common codecs include:

- H.26x series: standards developed by the International Telecommunication Union (ITU), among which the most popular one is H.264. H.265 is the successor of H.264 and offers a doubled compression rate compared to H.264, yet H.265 is not widely used dut to patent and other reasons.
- MPEG series: codec standards developed by Moving Picture Experts Group (MPEG) under International Organization for Standardization (ISO).
- Other series such as VP8 and VP9 developed by Google and RealVideo developed by RealNetworks.

### Event notification

An operation such as uploading, deleting, or video processing initiated on a video in VOD can be referred to as an event. The execution of an event takes a certain amount of time. Upon completion of the event, VOD will immediately notify the application service of the execution result, i.e., sending an event notification.

### Video noise reduction

Video noise is random variation of brightness or colors in an image produced by a sensor, scanner circuit, or digital camera. It can also originate in film grain and fixed shot noise of a photon detector. It is generally viewed as an undesirable by-product of image capturing. Video noise reduction is to remove unwanted noise from a video while retaining important details and other useful information in the video.

### Video pull

The process of pulling videos in the Internet to VOD as media assets. For details, see [PullUpload](https://intl.cloud.tencent.com/document/product/266/34118).

### Digital rights management (DRM)

Digital rights management (DRM) is to technically prevent the unauthorized copy and use of digital content to protect the copyright. It provides the capabilities to securely deliver, control, and operate digital content. Users must be authorized first before they can consume such content within the scope of corresponding permissions and pay corresponding fees.

VOD provides video encryption capabilities to protect copyrights of contents and only offers keys for decryption and playback to authorized users. For specific features and using methods, see [Video Encryption Overview](https://intl.cloud.tencent.com/document/product/266/38131).

### SimpleAES encryption

SimpleAES is an HLS-based AES encryption scheme that uses a key to encrypt video data. In VOD, videos encrypted with SimpleAES can be played back only by VOD superplayer.

### VOD

For details, see [Video on-demand (VOD)](https://intl.cloud.tencent.com/document/product/266/11732).

### Web/mobile player

A web player is a player used on webpages. A mobile player is a player integrated in applications on mobile devices (phones and tablets). VOD currently provides three player SDKs for Android, iOS, and web respectively, among which Android and iOS players are mobile players.

### Image sprite

An image sprite (aka sprite) is a big image formed by combining any number of small images in the format of a two-dimensional matrix. The multiple images that make up the big image are called subimages, which are captured from the original video at a fixed sampling interval. With the aid of an image sprite, viewers can quickly know the general content of the entire video. In VOD, image sprites are also used in the superplayer to implement thumbnail preview on the progress bar.

### Color space

A color space is an abstract mathematical model which simply describes the range of colors as tuples of numbers, typically as 3 or 4 values or color components.

### Audio codec

An audio codec is a method of encoding analog audio as digital signals or decoding digital back into analog. There are mainly two kinds of audio codecs: lossless and lossy. According to sampling principles, encoded audio signals can only get "close to indefinitely" to natural signals; therefore, all audio codecs are lossy. In computer field, pulse code modulation (PCM) that achieves the highest fidelity is regarded as lossless encoding. Commonly used audio codecs in Internet services are all lossy, such as MP3 and AAC.

### Video on-demand (VOD)

Based on Tencent's years of technical expertise and experience in infrastructure construction, Video on-demand (VOD) provides customers with a one-stop solution for audio/video application, covering cloud audio/video storage, transcoding, playback acceleration and communication service.

### Frame rate

Frame rate refers to the number of frames in a video per unit time. It is measured in fps (frame per second).

### Transcoding

Transcoding converts a video bitstream into another one. It changes the codec, resolution, bitrate, and other parameters of the bitstream for playback on different devices in various network environments. This feature can achieve the following:

- Increase compatibility: transcode a source video to formats (MP4 for example) that are compatible with more types of devices for smooth playback.
  - Increase bandwidth adaptability: transcode a source video to outputs in smooth, SD, HD, and UHD. End users can select the bitrates as appropriate for their network conditions.
  - Improved playback efficiency: The moov atom can be moved from the end of an MP4 file to its beginning, so the video can be played before it is entirely downloaded.
  - Watermarking: a watermark can be added to a video to mark video ownership or copyright.
  - Reduce bandwidth usage: use advanced encoding modes (such as H.265) for transcoding to reduce the bitrate of a video substantially with the original quality retained, thus lowering the payback bandwidth usage.

### Substream

An adaptive bitstream is composed of multiple audio/video files with different bitrates, each of which is called a substream.

### Transcoding to adaptive bitrate streaming

Adaptive bitrate streaming involves audio/video files with various bitrates and a descriptive file (manifest). A player can dynamically select the most appropriate bitrate for playback based on the current bandwidth.
HLS [master playlist](https://developer.apple.com/documentation/http_live_streaming/example_playlists_for_http_live_streaming/creating_a_master_playlist) format is the most widely used adaptive bitrate streaming format. Other mainstream adaptive bitrate streaming formats include [MPEG-DASH](https://mpeg.chiariglione.org/standards/mpeg-dash) and [MSS](https://www.microsoft.com/silverlight/smoothstreaming/).