
Tencent Cloud MediaLive (MDL) is a dedicated platform that provides ultra-fast, stable, and high-quality live streaming media processing services for global users. Leveraging the compute resources in Tencent Cloud's abundant AZs deployed around the globe and proprietary well-established audiovisual platforms and world-leading AI technologies in audio and video, MediaLive unveils the core capabilities of Tencent Cloud live streaming to provide developers with professional, stable, and efficient basic services such as live stream transcoding, remuxing, and transfer, as well as value-added services such as DRM and SCTE-35 ad solutions. It uses Tencent Cloud’s unique high-performance video encoding and compression algorithms, and tries to save the transmission traffic while ensuring a better viewing experience. At the same time, it also guarantees 24/7 availability.

## Mapping Relationship of MediaLive Input Streams

![](https://main.qcloudimg.com/raw/62bf460b9d22d6450c828bcc8827d876.jpg)

Each MediaLive channel supports setting two pipelines (e.g. pipeline A and B) when configuring the input. Pipeline A (required) and Pipeline B (optional) run independently. That is, the stream from input A will be output to the destination A of each output group, and the stream from input B will be output to the destination B of each output group. (When the output type is MediaPackage, Pipeline A and Pipeline B will be input to the MediaPackage channel as two streams.)

The relationship diagram between the output group and output is as follows:

![](https://main.qcloudimg.com/raw/6b2dca814f0b08a75ce6623749a00cc3.jpg)

Each output group, which can contain multiple outputs, determines an output protocol or type. Each output can select video streams with different resolutions and bitrates to combine and output a live stream with adaptive bitrates.
