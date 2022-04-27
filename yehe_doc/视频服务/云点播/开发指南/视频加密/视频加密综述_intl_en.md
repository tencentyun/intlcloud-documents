To protect the security of your videos and prevent them from hotlinking and unauthorized download and distribution, VOD provides multiple protection mechanisms for video content security to defend your video copyright against infringements in many dimensions.

<table class="table auto-table">
  <tr>
	  <td>Category</td>
	  <td>Feature</td>
		<td>Advantage</td>
		<td>Security Level</td>
	</tr>
	<tr>
	  <td rowspan="2">Hotlink protection</td>
	  <td>Referer hotlink protection</td>
		<td>It identifies the request source through the `Referer` field in the playback request header and controls the request sources through a blocklist or allowlist</td>
		<td>Low</td>
	</tr>
	<tr>
	  <td>Key hotlink protection</td>
		<td>It adds control parameters in the playback URL and uses `Key` as a signature to control the URL validity period, preview duration, number of IPs allowed for playback, etc.</td>
		<td>Medium</td>
	</tr>
	<tr>
	  <td rowspan="1">Video encryption</td>
	  <td>HLS common encryption</td>
		<td>It is an HLS-based <a href=https://tools.ietf.org/html/draft-pantos-http-live-streaming-23?spm=a2c4g.11186623.2.31.409c6a6aYf9Rn8>AES encryption</a> scheme and uses keys to encrypt video data</td>
		<td>High</td>
	</tr>
</table>

* [Hotlink protection](https://intl.cloud.tencent.com/document/product/266/33984) is mainly used to control the validity of the sources of video playback requests, but does not encrypt video content, which means that users can download videos for secondary distribution; therefore, the security level of copyright protection is low.
* Video encryption is a means to encrypt the video content itself with a key, which cannot be played back directly after being obtained by others. Only when a terminal device passes the authentication by the business backend and the decryption key is obtained can the content by played back.

VOD's video encryption feature provides the HLS common encryption capability, which has a higher security level than hotlink protection.

## How It Works

The overall architecture of VOD video encryption, decryption, and playback is as follows:

1. <b>Upload from server</b>: the business backend uploads a video to VOD through the console, server API, or other means.
2. <b>Trigger video processing</b>: when the video is uploaded, adaptive bitrate streaming with encryption is specified. After the video is uploaded, the encryption process begins.
3. <b>Get the key</b>: the video is transcoded to adaptive bitstream and encrypted. VOD gets the key used during video encryption from the KMS module.
4. <b>Encrypt and write to storage</b>: after the video is transcoded to adaptive bitstream and encrypted, the output video content is written to the VOD storage.
5. <b>Update the media asset</b>: the encrypted video information is written into the media asset management module.
6. <b>Get the player signature</b>: the business terminal integrates with VOD superplayer, and the player requests the player signature from the business server.
7. <b>Request the download address</b>: superplayer gets the download address of the video from VOD's playback service.
8. <b>Download the content</b>: superplayer downloads the content from VOD CDN at the download address.
9. <b>Get the key</b>: superplayer requests the decryption key with the player signature.
10. <b>Decrypt and play back</b>: superplayer uses the decryption key to decrypt the video for playback.

<img src="https://main.qcloudimg.com/raw/35a43c169f71ffd56142188784f2a915.png" width="700" />

## Integration Guide

To help you quickly integrate the encryption capabilities of VOD, we provide a video encryption [integration guide] to describe the integration steps by way of demos.

## FAQs

1. How do I encrypt uploaded videos?
VOD's [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942) feature can transcode videos into multiple resolutions and encrypt them.For specific steps, please see the [operation guide](https://intl.cloud.tencent.com/document/product/266/38294).
2. How do I play back encrypted videos on terminal devices?
To play back videos encrypted in VOD, you need to integrate the superplayer SDK on the terminal devices and build a signature distribution service.For specific steps, please see the [operation guide](https://intl.cloud.tencent.com/document/product/266/38294).
