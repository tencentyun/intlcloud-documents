## Overview
VOD’s [Top Speed Codec (TSC)](https://www.tencentcloud.com/document/product/266/49255) feature can achieve **high video quality at lower bitrates** and help you reduce your traffic and storage costs. However, TSC transcoding fees are higher than general transcoding fees. This raises the question of how the TSC technology can be used to maximize your **net cost savings** (**the reduction in traffic and storage costs minus the increase in transcoding costs**).

<img src="https://qcloudimg.tencent-cloud.cn/raw/eb6398ca9b2c0ffe556b0787ebb24158.jpg" width="600" />

With VOD’s smart bitrate reduction feature, you can configure policies to automatically perform TSC transcoding on files whose playback count is high and replace the original transcoding outputs of the files with the low-bitrate files that are generated. This can increase your **net cost savings**. The whole process can be executed automatically.

## Use Cases
<table>
    <tr>
        <th>
            Target customer              
        </th>
				<th>
           Description
        </th>
    </tr>
		<tr>
        <td>
            UGSV platforms
        </td>
				<td>
				UGSV platforms manage a huge number of videos which differ greatly in terms of popularity. VOD’s bitrate reduction feature can automatically reduce the bitrate of popular videos without compromising their quality, helping you save traffic and storage costs.
        </td>
		</tr>
		<tr>
        <td>
            Live streaming platforms
        </td>
				<td>
				Live streaming platforms record a large number of streaming sessions, often at high resolutions, and replaying them may consume a lot of traffic. VOD’s smart bitrate reduction feature can automatically lower the bitrate of popular hosts’ videos and save your traffic and storage costs.
        </td>
		</tr>
		<tr>
        <td>
            Online education platforms
        </td>
				<td>
				The teaching courses provided by online education platforms vary in popularity. To save traffic and storage costs, you can use VOD’s smart bitrate reduction feature to reduce the bitrate of popular courses without compromising their video quality.
        </td>
		</tr>
</table>

## Directions
For detailed directions on how to use this feature, see the following document:
- [Smart Bitrate Reduction](https://www.tencentcloud.com/document/product/266/50451)
