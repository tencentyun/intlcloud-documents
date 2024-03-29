## 功能简介
对视频或音频执行转码，可指定输出媒体的编码格式、帧率、码率、分辨率等参数，以适应终端对不同清晰度和格式的播放需要。
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="155px"><col  width="132px"><col  width="260px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>类别</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>功能</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>说明</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="3" align="" valign=""><p>输入格式</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>封装格式</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>支持所有常见的音视频封装格式，包括：WMV、RM、MOV、MPEG、MP4、3GP、FLV、AVI、RMVB、TS、ASF、MPG、WEBM、MKV、M3U8、WM、ASX、RAM、MPE、VOB、DAT、MP4V、M4V、F4V、MXF、QT、OGG</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>视频编码格式</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>支持所有常见的音视频编码格式，包括：AV1、AVS2、H.263、H.263+、H.264/AVC、H.265/HEVC、H.266/VVC、MPEG-1、MPEG-2、MPEG-4、MJPEG、VP8、VP9、Quicktime、RealVideo、Windows Media Video</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>音频编码格式</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>AAC、ADPCM、AMR、DSD、MP1、MP2、MP3、PCM、RealAudio、Windows Media Audio、VORBIS</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="7" align="" valign=""><p>输出格式</p></td>
 <td   colspan="1" rowspan="3" align="" valign=""><p>封装格式</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>视频：FLV、MP4、HLS（m3u8+ts）、DASH</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>音频：MP3、MP4、OGG、FLAC、M4A</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>图片：GIF、WEBP</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>视频编码格式</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>H.264/AVC、H.265/HEVC、H.266/VVC、AV1</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>视频高清画质</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>支持 8K UHD 分辨率，支持转码 HDR 输出</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>音频编码格式</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>MP3、AAC、FLAC、MP2</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>音频声道</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>单声道、双声道、立体环绕声</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="3" align="" valign=""><p>其他功能</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>打水印</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>图片水印、文字水印、图文混编水印</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>拼接片头片尾</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>为媒体拼上片头或片尾</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>剪辑</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>仅转码出指定时间段的视频，实现剪辑的效果</p></td>
 </tr>
</tbody>
</table>

## 适用场景
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="301px"><col  width="301px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>场景</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>说明</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>适配更多终端</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>将原始媒体转码成拥有更强终端适配能力的格式（如 MP4 和 HLS），使媒体资源能够在更多设备上播放。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>适配不同带宽</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>将视频转换成流畅、标清、高清以及超清等输出，用户可以根据当前网络环境选择合适码率的视频播放。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>改善播放效率</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>转码可以将 MP4 位于尾部的元信息 MOOV 提前到头部，播放器无需下载完整视频即可立即播放。 </p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>为视频加水印</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>为视频加上水印标识视频的归属或版权。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>拼接片头片尾与剪辑</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>在视频的片头或片尾拼接广告、宣传介绍内容等</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>节省带宽</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>采用更先进的编码方式（如 H.266、AV1）转码或转码模式（极速高清），在不损失原始画质的情况下显著降低码率，节省播放带宽。</p></td>
</tr>
</tbody>
</table>

## 使用方式
请查看 [音视频转码](https://intl.cloud.tencent.com/document/product/266/33938)。



