## Container Format

The container format (`Format`) means that the encoded and compressed video stream and audio stream are put into one file according to a certain format specification. For online VOD, a more appropriate term is called "streaming network transport protocol". The most widely used protocols in the internet are as follows:

- **MP4**: it is a classic format well supported by iOS and Android devices and PC websites. However, the header of an MP4 file is often too large and complicated. If a video is lengthy (e.g., several hours), a very large file header will slow down video loading. Therefore, it is more suitable for UGSV scenarios.
- **HLS (HTTP Live Streaming)**: it is a protocol developed by Apple and compatible with iOS and Android, but Internet Explorer's support for HLS depends on secondary development of Flash Player (Tencent Cloud's Flash Player control is recommended). With a streamlined m3u8 index structure, it is free from MP4's drawback of slow indexing, making it a favorable choice for VOD.
- **FLV**: it is a protocol developed by Adobe and well supported by Flash Player on PCs, but requires the implementation of a dedicated player on mobile devices (Tencent Cloud's Flash Player control is recommended). It is not supported by most mobile browsers.

## Video Encoding Terms

### Codec
A codec is a program or device that can compress or decompress (video decoding) digital videos. The common encoding methods include:

- H.26x series: these standards are developed by the International Telecommunication Union (ITU), among which the most popular one is H.264. H.265 is the successor of H.264 and offers a doubled compression rate compared to H.264; however, it is not widely used for reasons such as patent limitations.
- MPEG series: these standards are developed by Moving Picture Experts Group (MPEG) under the International Organization for Standardization (ISO).
- Other series such as VP8 and VP9 developed by Google and RealVideo developed by RealNetworks.

### Bitrate
Bitrate refers to the number of bits that are required in playback of continuous media (e.g., compressed audio or video) per unit time. It is measured in bit/s or bps.

### Frame rate
Frame rate refers to the number of frames in a video per unit time. It is measured in FPS (frame per second) or Hz.

### Resolution
Resolution determines a video's capability to define details and is represented in the number of pixels in each direction, e.g., 640 * 480.

### GOP
A GOP (group of pictures) refers to a set of continuous pictures within an encoded video stream. It lasts from an I-frame till the next I-frame. A GOP can contain the following types of pictures:

- I-Frame (Intra Coded Picture): the node-encoded picture. It is a fixed image independent of other image types. Each GOP begins with a picture of this type.
- P-Frame (Predictive Coded Picture): the predictive coded picture before and after. It contains the difference information from the previous I or P frame.
- B-Frame (Bidirectionally Predictive Coded Picture): the predictive coded picture before and after. It contains the difference information from the previous and/or the next I or P frame.

The number of pictures within a GOP is called GOP length.

### IDR frame alignment
An IDR (instantaneous decoding refresh) picture is a type of I picture. Different from a common I picture where P and B pictures after it can reference other I pictures before it, no pictures after an IDR picture can reference any pictures before it.

In VOD scenarios, a player generally allows dragging on the progress bar to a desired position. The most convenient way for the end is to start playback from the IDR picture in close proximity to that position. This is because the player knows that all pictures after the IDR picture will not reference other I pictures before it, thus avoiding complicated reverse resolution.

If IDR frame alignment is specified when multi-bitrate transcoding is performed on a video, IDR pictures of all the output videos will be precisely aligned by time point and picture content, so that video players can smoothly switch among videos at different bitrates without obvious lagging.

If you enable IDR frame alignment on the VOD platform during transcoding, the settings of [frame rate](#.E5.B8.A7.E7.8E.87), [GOP](#gop) length, [codec](#.E7.BC.96.E7.A0.81.E6.96.B9.E5.BC.8F), and [container format](#.E5.B0.81.E8.A3.85.E6.A0.BC.E5.BC.8F) of multiple output formats must be identical.

### Profile
Profile is a collection of specific encoding features for a specific application scenario. H.264 mainly supports three profiles:

- **Baseline**: it supports I/P pictures, and only supports Progressive and CAVLC. It is generally used in low-end applications or those that need extra fault tolerance, such as video chat, mobile video, and other instant messaging applications.
- **Main**: it provides I/P/B pictures, and supports Progressive and Interlaced as well as CAVLC and CABAC. It is used for mainstream consumer electronics specifications, such as MP4 with low decoding rate (relatively), portable video player, PSP, and iPod.
- **High**: 8x8 intra prediction, custom quantification, lossless video encoding, and more YUV formats (e.g., 4:4:4) are added on the basis of Main for broadcast and video disc storage (Blu-ray movies) and HDTV.

### Color space
A color space is an abstract mathematical model which simply describes the range of colors as tuples of numbers, typically as 3 or 4 values or color components.

## Video Processing Terms

### Video noise reduction
Video noise is random variation of brightness or colors in an image produced by a sensor, scanner circuit, or digital camera. It can also originate in film grain and fixed shot noise of a photon detector. It is generally viewed as an undesirable by-product of image capturing. Video noise reduction is to remove unwanted noise from a video while retaining useful information such as important details in the video.

### Deinterlacing
In the era of analog television, the processing speed and network bandwidth of playback devices were limited. In this context, interlacing was developed to deliver videos at lower bitrates without reducing the source frame rates. It can reduce the video transmission bandwidth by 50% while basically retaining source image quality. However, it has noticeable negative effects such as low definition, flickering, and jaggies along image edges.
Nowadays, video playback devices and network bandwidth have been improved greatly, and interlacing gradually becomes obsolete and is not supported by some new device models. Therefore, old videos that were processed with interlacing need to be "deinterlaced".

## Audio Encoding Parameters
### Codec
A codec is a method of converting analog audio signals to digital signals (or vice versa) and mainly includes lossless and lossy encoding. According to sampling principles, encoded audio signals can only get "infinitely similar to" natural signals; therefore, all audio codecs are lossy in essence. In computer fields, pulse code modulation (PCM) that achieves the highest fidelity is generally agreed as lossless encoding. All the popular audio codecs in internet services are lossy, such as MP3 and AAC.

### Sample rate
Sample rate refers to the number of discrete signals extracted from and comprising continuous signals per second. It is measured in Hz.

### Bitrate
Please see the description of bitrate in the Video Encoding Terms section.

### Sound channel
A sound channel refers to an independent audio signal collected from different spatial positions when sound is recorded or played back. The number of sound channels is the number of sound sources during recording or number of speakers during playback.

## Other General Terms

### ISO date format
ISO date format is a time format as specified in ISO 8601. In VOD, unless otherwise specified, all time-related parameters use UTC time in ISO 8601 standard (in the format of YYYY-MM-DDThh:mm:ssZ). For example, 2018-10-01T10:00:00Z represents 18:00:00 on October 1, 2018 Beijing Time (UTC+8).
