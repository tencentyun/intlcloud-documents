## Overview
Audio/Video transcoding transcodes audios/videos and allows you to specify the parameters of the output media, such as encoding format, frame rate, bitrate, and resolution for the media to be played back on terminals supporting different definitions and formats.
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="155px"><col  width="132px"><col  width="260px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>Category</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>Feature</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>Description</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="3" align="" valign=""><p>Input format</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Container format</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Common audio/video container formats are supported, including WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WEBM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, and OGG.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Video encoding format</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Common video encoding formats are supported, including AV1, AVS2, H.263, H.263+, H.264/AVC, H.265/HEVC, H.266/VVC, MPEG-1, MPEG-2, MPEG-4, MJPEG, VP8, VP9, QuickTime, RealVideo, and Windows Media Video.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Audio encoding format</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>AAC, ADPCM, AMR, DSD, MP1, MP2, MP3, PCM, RealAudio, Windows Media Audio, and Vorbis.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="7" align="" valign=""><p>Output format</p></td>
 <td   colspan="1" rowspan="3" align="" valign=""><p>Container format</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Video: FLV, MP4, HLS (M3U8 + TS), and DASH.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Audio: MP3, MP4, OGG, FLAC, and M4A.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Image: GIF and WebP.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Video encoding format</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>H.264/AVC, H.265/HEVC, H.266/VVC, and AV1.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>HD video</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>The 8K FHD definition and HDR output are supported.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Audio encoding format</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>MP3, AAC, FLAC, and MP2.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Sound channels</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Mono-channel, dual-channel, and stereo.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="3" align="" valign=""><p>Other features</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Watermarking</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Image, text, and image-text watermarks.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Opening and ending segment splicing</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Adds an opening or ending segment to the media.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Clipping</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Transcodes and outputs the specified portion of a video.</p></td>
 </tr>
</tbody>
</table>

## Use Cases
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="301px"><col  width="301px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>Use Case</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>Description</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Increased compatibility</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>A source media file can be transcoded to formats (such as MP4 and HLS) that are compatible with more types of devices for smooth playback.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Increased bandwidth compatibility</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>A source video can be transcoded for output in multiple definitions such as LD, SD, HD, and FHD. End users can select the most appropriate bitrate depending on their network conditions.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Improved playback efficiency</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>The moov atom can be moved from the end of an MP4 file to the beginning of the file, allowing the video to be played before it is entirely downloaded.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Watermarking</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>A watermark can be added to a video to mark video ownership or copyright.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Opening and ending credits splicing and clipping</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>Content such as ad and promotional material can be added to a video as opening or ending credits.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>Reduced bandwidth usage</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>With a more advanced codec (such as H.266 and AV1) or transcoding mode (Top Speed Codec transcoding), the bitrate of a video can be substantially reduced while retaining the original quality, which helps reduce the bandwidth usage.</p></td>
</tr>
</tbody>
</table>

## Directions
For more information, see [Transcoding](https://intl.cloud.tencent.com/document/product/266/33938).



