### License

Certain VOD packages come with licenses for Tencent Cloud media SDKs, which you can use to activate UGSV features in the SDKs.

>! After you purchase a VOD package, you need to bind the license to your application in the console. Make sure you double-check the [bundle ID and package name](https://intl.cloud.tencent.com/document/product/1069/46320) when binding a license. **The information cannot be modified after submission**.

### Player signature

A player signature is used to authorize a playback device to play videos. If your application playback service issues a valid signature to a device, the device will be able to play the video within the signature’s validity period. A player signature is required for playback in one of the following cases:

- You have enabled [key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986) for your playback domain.
- A non-default [player configuration](https://intl.cloud.tencent.com/document/product/266/38296) is used.
- The video to be played is [encrypted](https://intl.cloud.tencent.com/document/product/266/38294).

>? For more information on player signatures and how to use them, see [Player Signature](https://intl.cloud.tencent.com/document/product/266/38099).

### Frame rate
Frame rate refers to the number of frames in a video per unit time. It is measured in fps (frames per second).

### Bitrate
Bitrate refers to the number of bits required per unit time to play continuous media (such as compressed audio or video). It is measured in bit/s (or bps).

### Transcoding
Transcoding converts a video bitstream into another one. It changes the codec, resolution, bitrate, and other parameters of the bitstream for playback on different devices in various network environments. This feature can achieve the following:
- Increase compatibility: Transcode a source video to formats (MP4 for example) that are compatible with more types of devices for smooth playback.
- Increase bandwidth adaptability: Transcode a source video into different video qualities such as smooth, SD, HD, and FHD. End users can select the bitrate that best suits their network conditions.
- Improve playback efficiency: Move the moov atom from the end of an MP4 file to the beginning, so that a video can be played before it is downloaded completely.
- Watermark: Add a watermark to a video for copyright protection.
- Reduce bandwidth consumption: The use of more advanced codec technology (such as H.265) makes it possible to significantly reduce the bitrate of a video while maintaining its quality, which helps reduce bandwidth consumption.

### Keyframe
Frame is the basic unit of videos. A video consists of multiple continuous frames.

### Timestamp
Timestamp is the current time of data.

### GOP
A GOP (group of pictures) refers to a collection of successive pictures within an MPEG encoded video stream. It starts with an I-frame and ends with the next I-frame. A GOP can contain the following types of pictures:
- I-frame: Intra encoded picture. It is a fixed image independent of other image types. Each GOP begins with this type of image.
- P-frame: Predictive coded picture. It contains difference information relative to the previous I or P frame.
- B-Frame: Bidirectionally predictive coded picture. It contains difference information relative to the previous or ensuing I or P frame.

The number of frames within a GOP is called GOP length.

### Codec
A video codec refers to a program or a device that can compress or decompress (video decoding) digital videos. Common codecs include:
- H.26x series: Standards developed by the International Telecommunication Union (ITU), among which the most popular is H.264. H.265 is the successor of H.264 and offers a doubled compression rate compared to H.264, yet H.265 is not widely used due to patent and other reasons.
- MPEG series: Codec standards developed by Moving Picture Experts Group (MPEG) under International Organization for Standardization (ISO).
- Other series such as VP8 and VP9 developed by Google and RealVideo developed by RealNetworks

### Event notification
Operations in VOD, such as video uploading, deleting, and processing, are referred to as events. It may take some time for an operation to be completed, and once it is completed, VOD will notify your application service of the result. This is an event notification.
