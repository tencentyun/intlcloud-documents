VOD provides different content security solutions to help you prevent video hotlinking and unauthorized download/distribution, and protect your copyright.

<table class="table auto-table">
  <tr>
	  <td>Solution</td>
	  <th>Feature</td>
		<td>Description</td>
		<td>Security Level</td>
	</tr>
	<tr>
	  <td rowspan="2">Hotlink protection</td>
	  <td>Referer hotlink protection</td>
		<td>Configure an allowlist/blocklist and use the "Referer" field in the header of a playback request to determine whether to allow or block the request</td>
		<td>Low</td>
	</tr>
	<tr>
	  <td>Key hotlink protection</td>
		<td>Use a key to generate a signature and add parameters for validity period, preview time, and max IP count to playback request URLs</td>
		<td>Medium</td>
	</tr>
	<tr>
	  <td rowspan="2">Video encryption</td>
	  <td>HLS AES encryption</td>
		<td><li>Based on <a href=https://tools.ietf.org/html/draft-pantos-http-live-streaming-23?spm=a2c4g.11186623.2.31.409c6a6aYf9Rn8>AES encryption</a></li><li>However, some browser extensions and tools can break the encryption.</li></td>
		<td>Moderately high</td>
	</tr>
	<tr>
	  <td>HLS private encryption</td>
		<td>VOD’s proprietary encryption solution, which provides better protection against cracking than AES encryption</td>
		<td>High</td>
	</tr>
</table>
<dx-alert infotype="notice" title="">
**We do not recommend AES encryption due to its relatively low security level.**
</dx-alert>

* [Hotlink protection](https://intl.cloud.tencent.com/document/product/266/33984) protects your content by blocking or allowing only specified sources of playback requests. However, because the videos are not encrypted, others can still distribute them after they are downloaded, so the security level is not very high.
* With video encryption, your content is encrypted with a key. Even if others have your videos, they cannot play them unless they are authenticated by your backend and issued the decryption key. We recommend [HLS private encryption](https://intl.cloud.tencent.com/document/product/266/46780), which offers a higher security level.
