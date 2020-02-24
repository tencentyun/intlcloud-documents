## Container Format

A container format is a file format used to store digital video data in a computer system. Here is a list of popular container formats used in internet services:

- **MP4**: MP4 is short for MPEG-4 Part 14. MP4 is the most commonly used digital multimedia container format for storing audio/video data. The typical file extension is ".mp4". It supports data streaming to deliver a smooth viewing experience on iOS/Android devices and on the PC. The header of an MP4 file stores all index information of the file. If a video is lengthy (e.g., several hours), a large file header will extend the loading time.
- **HLS**: HLS is short for HTTP Live Streaming. This is an HTTP-based adaptive bitrate streaming communications protocol developed by Apple. It is widely used on streaming media servers and well supported by iOS/Android devices and PC websites. However, Internet Explorer's support for HLS depends on secondary development of Flash Player (Tencent Cloud's Flash Player control is recommended). Based on the standard HTTP protocol, HLS can pass through any firewall or proxy server that lets through standard HTTP streams. It also includes a standard encryption mechanism and HTTPS-based security key distribution, which can implement a simple digital rights management (DRM) system.
- **FLV**: FLV is a Flash video standard developed by Adobe and can be played back through Adobe Flash Player or web browser plugins. As most mobile operating systems do not support Flash Player plugins, a separate application will be needed to play back FLV videos (Tencent Cloud's Flash Player control is recommended.)

## Video Encoding Terms

### Codec
Codec is short for coder-decoder and refers to a program or device that can encode and decode digital videos. Below are common codecs:

- H.26x series: These codec standards are developed by International Telecommunication Union (ITU), among which the most popular one is H.264. H.265 is the successor of H.264 and offers a doubled compression rate compared to H.264; however, it is not widely used for reasons such as patent limitations.
- MPEG series: These codec standards are developed by Moving Picture Experts Group (MPEG) under International Organization for Standardization (ISO).
- Other series such as VP8 and VP9 developed by Google and RealVideo developed by RealNetworks.

### Bitrate
Bitrate refers to the number of bits that are required in playback of continuous media (e.g., compressed audio or video) per unit time. It is measured in bit/s or bps.

### Frame rate
Frame rate refers to the number of frames in a video per unit time. It is measured in FPS (frame per second) or Hz.

### Resolution
Resolution determines a video's capability to define details and is represented in the number of pixels in each direction, e.g., 640 * 480.

### GOP
A GOP (group of pictures) refers to a set of continuous pictures within an encoded video stream and specifies the order in which the contained frames are arranged. When a new GOP appears, the decoder does not need any previous frames in order to decode the next frame. A GOP can contain the following types of pictures:

- I picture (intra coded picture): a picture coded independently without reference to any other pictures. Each GOP begins (in decoding order) with this type of picture.
- P picture (predictive coded picture): this picture contains motion-compensated difference information relative to one or more previously decoded pictures in display order. In older designs such as MPEG-1, H.262/MPEG-2, and H.263, each P picture can only reference one I or P picture, and that picture must precede the P picture in both display and decoding order. These constraints do not apply in newer standards such as H.264/MPEG-4 AVC and HEVC.
- B picture (bidirectionally predictive coded picture): this picture contains motion-compensated difference information relative to one or more previously decoded pictures in display order. In older designs such as MPEG-1 and H.262/MPEG-2, each B picture can reference only two I or P pictures, the one which precedes the B picture in display order and the one which follows. These constraints do not apply in newer standards such as H.264/MPEG-4 AVC and HEVC.

The number of pictures within a GOP is called GOP length.

### IDR frame alignment
An IDR (instantaneous decoding refresh) picture is a type of I picture. It differs from a common I picture in that an IDR frame specifies that no frame after the IDR frame can reference any frame before it. 

If IDR frame alignment is specified when multi-bitrate transcoding is performed on a video, IDR pictures of all the output videos will be precisely aligned by time point and picture content, so that video players can smoothly switch among videos at different bitrates without obvious lagging.

If you enable IDR frame alignment on the Tencent Cloud transcoding platform, the [frame rate](#帧率), [GOP](#gop) length, [codec](#编解码器), and [container format](#封装格式) of multiple output formats must be identical.

### Profile
A profile is a collection of specific encoding parameters. You need to make tremendous endeavors in hardware and software to support a complete codec standard due to its large number of features. Therefore, to facilitate use of a codec standard, some common parameters are selected and combined to form different profiles. H.264 specifies three profiles as shown below:

- **Baseline:** this is used for low-cost applications that require extra tolerance for data losses, e.g., videoconferencing and video playback on mobile devices.
- **Main:** this is used for mainstream consumer-grade SD digital television broadcasting.
- **High:** this is the main profile for broadcasting and disk storage, especially for HD television applications, e.g., Blu-ray formats and Digital Video Broadcasting (DVB) HD television broadcasting services.

### Color space
A color space is an organization of colors. By combining color spaces such as RGB and HSB and physical device profiling, fixed analog and digital representations of colors can be obtained. A color model is a mathematical model describing the way colors in a color space can be represented as tuples of numbers (e.g., triples in RGB or quadruples in CMYK).

## Video Processing Terms

### Video noise reduction
Video noise is random variation of brightness or colors in an image produced by a sensor, scanner circuit, or digital camera. It can also originate in film grain and fixed shot noise of a photon detector. It is generally viewed as an undesirable by-product of image capturing. Video noise reduction is to remove unwanted noise from a video while retaining useful information such as important details in the video.

### Deinterlacing
In the era of analog television, the processing speed and network bandwidth of playback devices were limited. In this context, interlacing was developed to deliver videos at lower bitrates without reducing the source frame rates. It can reduce the video transmission bandwidth by 50% while basically retaining source image quality. However, it has noticeable negative affects such as low definition, flickering, and jaggies along image edges.
Nowadays, video playback devices and network bandwidth have been improved greatly, and interlacing gradually becomes obsolete and is not supported by some new device models. Therefore, old videos that were processed with interlacing need to be "deinterlaced".

## Audio Encoding Parameters
### Codec
A codec is a method of converting analog audio signals to digital signals (or vice versa) and mainly includes lossless and lossy encoding. According to sampling principles, encoded audio signals can only get "infinitely similar to" natural signals; therefore, all audio codecs are lossy in essence. In computer fields, pulse code modulation (PCM) that achieves the highest fidelity is generally agreed as lossless encoding. All the popular audio codecs in internet services are lossy, such as MP3 and AAC.

### Sample rate
Sample rate refers to the number of discrete signals extracted from continuous signals per second. It is measured in Hz.

### Bitrate
Please see the description of bitrate in the Video Encoding Terms section.

### Sound channel
A sound channel refers to an independent audio signal collected from different spatial positions when sound is recorded or played back. The number of sound channels is the number of sound sources during recording or number of speakers during playback.

## Other general terms

### ISO date format
ISO date format is a time format as specified in ISO 8601. In Tencent Cloud MPS, unless otherwise specified, all time-related parameters use UTC time in ISO 8601 standard (in the format of YYYY-MM-DDThh:mm:ssZ). For example, 2018-10-01T10:00:00Z represents 18:00:00 on October 1, 2018 Beijing Time (UTC+8).
