HLS private encryption is VOD’s proprietary video encryption solution. It uses a private protocol to prevent key leakage and provides better protection against cracking by browser extensions and other tools.

## Workflow

The figure below shows the workflow of HLS private encryption.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9b9c03936ca3730d33da09243728b1cf.png" width="700" />

1. <b>Upload from server</b>: Videos are uploaded to VOD via the console or using server-side APIs.
2. <b>Start video processing</b>: After upload, video encryption starts (videos are encrypted according to the adaptive bitrate streaming parameters specified).
3. <b>Get the key</b>: VOD gets the encryption key from the KMS module.
4. <b>Encrypt and save the videos</b>: VOD encodes and encrypts the videos and saves the outputs.
5. <b>Update the information</b>: The information of the encrypted videos is updated to the media asset management module.
6. <b>Get player signatures</b>: The VOD superplayer, which is integrated into your project, requests player signatures from your server.
7. <b>Get the download URLs</b>: The superplayer gets the download URLs of the videos from VOD.
8. <b>Download</b>: The superplayer downloads the encrypted content via the URLs from the CDN of VOD.
9. <b>Get the key</b>: The superplayer sends a request that carries the signature for the key, which is protected by VOD’s private protocol against leakage.
10. <b>Decrypt and play the content</b>: The superplayer uses the private protocol to get the key and decrypt and play the content.



## Directions

For detailed directions on how to use VOD’s encryption feature, see [Stage 4. Play back an encrypted video](https://intl.cloud.tencent.com/document/product/266/38294).

## FAQs

1. How do I encrypt uploaded videos using HLS private encryption?
VOD’s [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942) feature allows you to convert a video into multiple resolutions and encrypt the content. For detailed directions, see [Stage 4. Play back an encrypted video](https://intl.cloud.tencent.com/document/product/266/38294).
2. How to play encrypted videos?
A client must be integrated with the superplayer SDK in order to play encrypted videos. You also need to build a signature generation tool. For detailed directions, see [Stage 4. Play back an encrypted video](https://intl.cloud.tencent.com/document/product/266/38294).
