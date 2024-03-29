媒体处理将音视频文件转码为不同码率和分辨率的格式，以满足不同网络带宽和终端设备的用户需求。支持以下功能：

## 音视频转码[](id:video_trans)
转码是将原始音视频码流转换成另一个音视频码流的过程，是一种离线任务。通过转码，可以改变原始码流的编码格式、分辨率和码率等参数，从而适应不同终端和网络环境的播放。通过转码功能可以实现：

| 可实现功能   | 说明                                                         |
| ----------- | ----------------------------------------------------------- |
| 适配更多终端 | 将原始视频转码成拥有更强的终端适配能力的格式（如 MP4），使视频资源能够在更多设备上播放 |
| 适配不同带宽 | 将视频转换成流畅、标清、高清及超清等输出，用户可以根据当前网络环境选择合适码率的视频播放 |
| 改善播放效率 | 转码可以将 MP4 位于尾部的元信息 MOOV 提前到头部，播放器无需下载完整视频即可立即播放 |
| 节省带宽     | 采用更先进的编码方式（如 H.265）转码，在不损失原始画质的情况下显著降低码率，节省播放带宽 |

转码的目标规格包含编码格式、分辨率和码率等参数。您可自定义以下转码相关参数。
<table>
<thead>
   <tr>
      <th width="15%" style="text-align:center">参数</td>
      <th width="17%" style="text-align:center">类型</td>
      <th  style="text-align:center">详细说明</td>
   </tr>
</thead>
   <tr>
      <td rowspan='3' style="text-align:center">输入格式</td>
      <td style="text-align:center">封装格式</td>
      <td>3GP、AVI、FLV、MP4、M3U8、MPG、ASF、WMV、MKV、MOV、TS、WebM、MXF</td>
   </tr>
   <tr>
      <td style="text-align:center">视频编码格式</td>
      <td>AV1、AVS2、H.264/AVC、H.263、 H.263+、H.265、MPEG-1、MPEG-2、MPEG-4、MJPEG、VP8、VP9、RealVideo、Windows Media Video、Quicktime</td>
   </tr><tr>
      <td style="text-align:center">音频编码格式</td>
      <td>AAC、ADPCM、AMR、DSD、MP1、MP2、MP3、PCM、RealAudio、Windows Media Audio、VORBIS、AC-3</td>
   </tr>
   <tr>
      <td rowspan='5' style="text-align:center">输出格式</td>
      <td rowspan='3' style="text-align:center">封装格式</td>
      <td>视频：FLV、MP4、HLS（m3u8+ts）、MXF</td>
   </tr><tr>
      <td>音频：MP3、MP4、OGG、FLAC、m4a</td>
   </tr><tr>
      <td>图片：GIF、WEBP</td>
   </tr>
   <tr>
      <td style="text-align:center">视频编码格式</td>
      <td>H.264/AVC、 H.265/HEVC、AV1</td>
   </tr><tr>
      <td style="text-align:center">音频编码格式</td>
      <td>MP3、AAC、FLAC、MP2、VORBIS</td>
   </tr><tr>
			 <td rowspan='2'  style="text-align:center">封装</td>
      <td style="text-align:center">删除视频流</td>
      <td>如果开启“删除视频流”，转码出来的视频将不包含视频流（仅保留音频流）</td>
   </tr>
	 	 	   <tr>
      <td style="text-align:center">删除音频流</td>
      <td>如果开启“删除音频流”，转码出来的视频将不包含音频流（仅保留视频流）</td>
</table>


## 音视频增强[](id:video_enhance)

通过画质修复和画质增强两大模块结合 AI 算法，提升分辨率的同时，能够提供视频去噪、轮廓修复、超分辨重建等功能，适用于 UGC/PGC 视频质量提升, 老片翻新，4K 生产等业务场景。

| 能力           | 说明                                                         |
| :------------- | :----------------------------------------------------------- |
| 视频降噪       | 由于影片拍摄中会因为相机和环境引入随机噪点，这里提供降噪服务，在保持细节不损失的情况下，消除画面中的随机噪声。 |
| 去伪影（毛刺） | 由于影片在转码或多次转码过程中对视频进行了多次压缩，会引入块效应、振铃效应、色度渗透和蚊噪等，使得视频画面出现一些影响视觉效果的失真，去压缩失真能有效修复编码引入的失真。 |
| 去划痕         | 由于影片在拍摄、保存和转存过程中一些未知因素导致胶片产生划痕和雪花点等破坏，去划痕可以修复视频中的划痕和雪花点等破坏的内容。 |
| 细节增强       | 由于拍摄相机质量、后期保存和转码过程中导致视频细节不够清晰，细节增强对视频中需要关注的细节进行增强，使画面内容更清晰，内容更丰富。 |
| 综合增强       | 通过 AI 的综合分析能力，自动平衡画面中的纹理内容，在去除压缩伪影和毛刺的同时增强关键细节，从而提高整个画面的总体主观感受。 |
| 超分           | 针对一些影片分辨率较低，不适应如今对高分辨率影片的要求，提供超分辨率能力对影片细节进行增强修复，利用AI模型达到高分辨率输出的同时有效细节更清晰。 |
| 人脸增强       | 通过人脸检测针对视频中人眼视觉特别关注的人脸部分进行增强，使该区域的细节更加清晰，提高主观感受。 |
| 色彩增强       | 因拍摄设备的色彩问题或影片的保存问题，导致影片的色彩存在一定的失真或可增强的情况，色彩增强使画面更接近真实色彩，并在一定程度上进行增强满足人眼的喜好。 |
| 低光照增强     | 因环境状况及拍摄摄像头的硬件限制，在某些场景下拍摄的画面亮度和对比度缺失，导致画面较暗或画面较暗区域细节看不到，因此暗场景增强能够自动识别场景对画面进行自适应增强，特别在暗场景下能大幅提升暗区的细节和对比度，提升人眼主观质量。 |
| HDR            | SDR 转 HDR 能力可将普通 SDR 视频转化为 HDR 视频，色深提升至10bit，获得更宽的色域，展现更多色彩细节，以提供更高品质的视频内容。 |
| 插帧           | 通过对原始视频帧间补充新的视频帧，给用户提供更加流畅丝滑的视觉效果。另外，也能够帮助解决低帧率老视频中卡顿、抖动等画质问题。 |


## 水印[](id:watermark)
添加水印是在视频转码或截图时，将特定的图片附加在画面指定位置的过程，是一种离线任务。媒体处理支持以下类型的水印：
- **静态图片水印**：PNG 格式的图片水印，可以是版权方的 LOGO、台标等，常用于表明视频的版权归属。
- **动态图片水印**：APNG 格式的动态图片水印，可以实现水印图片动态变化的效果。

媒体处理支持为视频或截图添加多个水印，并可以指定各个水印在画面中的大小和位置。
水印的目标规格包含水印类型、宽高和位置等参数。您可自定义以下水印相关参数。

| 参数                     | 说明                           |
| ------------------------ | ------------------------------ |
| 水印类型（Type）         | 支持静态图片水印和动态图片水印 |
| 水印位置（Position）     | 水印在视频画面中的相对位置     |
| 图片大小（ImageSize）    | 图片水印占视频画面的大小       |
| 图片内容（ImageContent） | 图片水印中图片的二进制内容     |


## 视频截图[](id:screenshot)
截图是截取视频特定位置的图像并生成图片的过程，是一种离线任务。媒体处理提供以下类型的截图：
- **指定时间点截图**：指定一组时间点，截取视频在这些时间点的图像。
- **采样截图**：按相同的时间间隔对视频截取多张图。
- **雪碧图**：按相同的时间间隔对视频截取多张小图，然后组装成若干大图（即 [雪碧图](https://intl.cloud.tencent.com/document/product/1041/33504#1666)）。

截图的目标规格，包含了截图文件格式、截图宽高等参数。您可自定义以下截图相关参数。

### 时间点截图[](id:time)

| 参数                 | 说明                                                         |
| -------------------- | ------------------------------------------------------------ |
| 格式（Format）       | 截图文件的输出格式，目前仅支持 JPG                           |
| 宽度（Width）        | 截图宽度，范围是128px - 4096px                               |
| 高度（Height）       | 截图高度，范围是128px - 4096px                               |
| 填充方式（FillType） | 当截图的宽高比与原始视频的宽高比不一致时，对截图的处理方式，即为“填充”。一般有以下几种填充方式：<li>拉伸：对图片进行拉伸，填满整个图片，可能导致图片被“压扁”或者“拉长”</li><li>留黑：保持图片宽高比不变，边缘剩余部分使用黑色填充</li><li>留白：保持图片宽高比不变，边缘剩余部分使用白色填充</li><li>高斯模糊：保持图片宽高比不变，边缘剩余部分使用高斯模糊化后填充</li> |


### 采样截图[](id:sampling)

| 参数                   | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 格式（Format）         | 截图文件的输出格式，目前仅支持 JPG                           |
| 宽度（Width）          | 截图宽度，范围是128px - 4096px                               |
| 高度（Height）         | 截图高度，范围是128px - 4096px                               |
| 采样方式（SampleType） | 采样方式分为两种：<li>按百分比采样：例如按照5%为间隔采样，生成截图张数将为20张</li><li>按时间间隔采样：例如按照10s为间隔采样，截图张数取决于视频的时长</li> |
| 采样间隔（Interval）   | 采样的间隔长度：<li>如果按百分比采样，间隔是百分比</li><li>如果按时间间隔采样，间隔是多少秒</li> |
| 填充方式（FillType）   | 当截图的宽高比与原始视频的宽高比不一致时，对截图的处理方式，即为“填充”。一般有以下几种填充方式：<li>拉伸：对图片进行拉伸，填满整个图片，可能导致图片被“压扁”或者“拉长”</li><li>留黑：保持图片宽高比不变，边缘剩余部分使用黑色填充</li><li>留白：保持图片宽高比不变，边缘剩余部分使用白色填充</li><li>高斯模糊：保持图片宽高比不变，边缘剩余部分使用高斯模糊化后填充</li> |


### 雪碧图[](id:sprite)

| 参数                   | 说明                                     |
| ---------------------- | ---------------------------------------- |
| 格式（Format）         | 雪碧图文件的输出格式，目前仅支持 JPG     |
| 小图宽度（Width）      | 雪碧图中小图的宽度                       |
| 小图高度（Height）     | 雪碧图中小图的高度                       |
| 小图行数（Rows）       | 一张大图中有多少行小图                   |
| 小图列数（Columns）    | 一张大图中有多少列小图                   |
| 采样方式（SampleType） | 小图采样方式，目前仅支持按照时间间隔采样 |
| 采样间隔（Interval）   | 小图采样的间隔，即隔多久采样一张小图     |

>!
>- Width × Columns 需要在128px - 4096px之间（即大图宽度在128px - 4096px之间）。
>- Height × Rows 需要在128px - 4096px之间（即大图高度在128px - 4096px之间）。

### 视频转动图[](id:gif)
转动图是选取视频片段生成动图（GIF 和 WEBP 等）的过程，是一种离线任务。动图是一组连续帧的无缝循环，以较小的体积实现动画效果。
转动图的目标规格，包含了动图格式、宽高和帧率等参数。您可自定义以下动图相关参数。

| 参数           | 说明                                       |
| -------------- | ------------------------------------------ |
| 格式（Format） | 动图文件的输出格式，目前仅支持 GIF 和 WEBP |
| 宽度（Width）  | 动图宽度，范围是128px - 4096px             |
| 高度（Height） | 动图高度，范围是128px - 4096px             |
| 帧率（FPS）    | 支持的帧率范围是1fps - 60fps               |


## 内容理解
### 内容识别[](id:identification)
内容识别基于腾讯实验室的最新研究成果，为您提供视频内容的全方位识别，支持识别视频内的人物、语音、文字以及帧标签，对视频进行多维度结构化分析。
<table>
<thead>
<tr>
<th width=15%>识别类型</th>
<th>功能说明</th>
</tr>
</thead>
<tbody><tr>
<td>人脸识别</td>
<td>基于深度学习方案，帮助客户快速识别视频中的人脸信息并快速定位出视频中的人物所在帧画面，以及人脸所在区域。客户可自定义人物库或调用视频 AI 公共人物库进行人脸识别。</td>
</tr>
<tr>
<td>语音识别</td>
<td>基于深度学习方案，帮助客户快速识别视频中的声音并转化成文字，支持客户自定义关键词且定位出关键词所在视频的时间点。</td>
</tr>
<tr>
<td>文字识别</td>
<td>帮助客户识别视频中出现的文字信息，可用于视频内自定义关键词的提取，也支持竖版文字的识别。</td>
</tr>
<tr>
<td>帧标签识别</td>
<td>基于深度学习方案，支持根据客户自定义视频截帧间隔，自动识别截帧画面内的标签，并定位标签所在的视频位置，帧标签涵盖人物、风景、人造物、建筑、动植物、食物等9个大类，包含日常生活的各个信息维度，并且支持在标签体系基础上使用自定义标签，具备迁移学习能力，只需提供原始用户数据便可定制分类器，满足不同类型的用户需求，使标签分类更具灵活性。</td>
</tr>
<tr>
<td>片头片尾识别</td>
<td>根据视频画面特征、文字、语音等信息自动识别定位电影/电视剧片头片尾时间点。</td>
</tr>
</tbody></table>

### 内容分析[](id:analyze)
<table>
<thead>
<tr>
<th width=14%>分析类型</th>
<th>能力说明</th>
</tr>
</thead>
<tbody><tr>
<td>分类识别</td>
<td>通过分析视频内容，给视频推荐一个类别。目前支持美食、旅游、动漫、音乐等19大类（支持定制，需支付定制费）。</td>
</tr>
<tr>
<td>视频标签识别</td>
<td>基于腾讯深度学习方案，智能识别出最符合视频内容的前五项标签摘要，用于视频推荐、检索等场景，用户可在接口中自行选择返回的标签个数。</td>
</tr>
<tr>
<td>智能封面</td>
<td>结合视频画面纹理、场景识别等特征信息自动生成文件封面，支持静态封面输出，提升视频封面体验和点击转化率。</td>
</tr>
</tbody></table>

## 智能审核[](id:audit)
智能审核包括安全审核和质量审核两大类。
**安全审核**借助 AI 对视频内容（画面、音频及文字三种维度）进行涉黄、违法违规的检测。
**质量审核**支持检测直播、点播视频中的画面帧以及声音质量，涵盖花屏、黑边、马赛克、噪声等全方位13项检测类型，并提供主播视频整体质量检测评分。

<table>
    <thead><tr>
        <th>审核类型</th>
        <th>检测类型</th>
        <th>检测项说明</th>
    </tr>
		 </thead> <tbody>
    <tr>
        <td rowspan="3">安全审核</td>
        <td>视频画面审核</td>
        <td>
            对视频画面做涉黄、违规检测，具体检测项如下：<ul style="margin:0">
                            <li><strong>涉黄检测</strong><ul>
                                <li>porn：色情</li>
                                <li>vulgar：低俗</li>
                                <li>intimacy：亲密行为</li>
                                <li>sexy：性感</li>
                            </ul>
                            </li>
                            <li><strong>违法违规检测</strong><ul>
                                <li>guns：武器枪支</li>
                                <li>bloody：血腥画面</li>
                                <li>explosion：爆炸火灾</li>
                                <li>violation_photo：违规图标</li>
                            </ul>
                            </li>
                            </ul>
        </td>
    </tr>
    <tr>
        <td>音频审核</td>
        <td>
            对音频中的文字进行检测，具体检测项如下：
                    <ul style="margin:0">
                        <li><strong>涉黄检测</strong>：对音频中的文字做涉黄检查，识别出嫌疑关键词</li>
                        <li><strong>违法违规检测</strong>：对音频中的文字做违法违规检查，识别出嫌疑关键词</li>
                    </ul>
        </td>
    </tr>
    <tr>
        <td>文字审核
        </td>
        <td>
            对画面中的文字进行检测，具体检测项如下：
<ul style="margin:0">
<li><strong>涉黄检测</strong>：对画面中的文字做涉黄检查，识别出嫌疑关键词</li>
<li><strong>违法违规检测</strong>：对画面中的文字做违法违规检查，识别出嫌疑关键词</li>
</ul>
        </td>
    </tr>
    <tr>
        <td rowspan="2">质量审核</td>
        <td>画面质量</td>
        <td>支持对视频的画面质量做出检测，具体检测项如下：
            <li>JitterResults：画面抖动
            </li><li>BlurResults：画面模糊
            </li><li>AbnormalLightingResults：低光、过曝
            </li><li>CrashScreenResults：花屏
            </li><li>BlackWhiteEdgeResults：画面黑边、白边、黑屏、白屏、纯色屏时间段
            </li><li>NoiseResults：画面有噪点
            </li><li>MosaicResults：画面有马赛克
            </li><li>QRCodeResults：画面有二维码
        </li></td>
    </tr>
    <tr>
        <td>声音质量</td>
        <td>
            支持对视频的声音质量做出检测，具体检测项如下：
            <li>VoiceResults：音频异常，包括静音、低音、爆音
        </li></td>
    </tr>
</tbody></table>


## 智能编辑[](id:edit)
智能编辑基于 AI 以及腾讯多年的音视频技术，支持多维度全方位理解视频内容，智能集锦以及智能拆条的能力，辅助视频内容生产。

| 能力类型 | 能力说明                                                     |
| :------- | :----------------------------------------------------------- |
| 拆条     | 对视频内容进行结构化分析，根据视频的场景信息、语音信息及文字信息，对视频生成智能拆条，支持新闻拆条、广告拆条。 |
| 智能集锦 | 基于视频时域/空域特征匹配、场景识别、目标检测等技术，自动生成视频精彩片段，支持足球、篮球、绝地求生、王者荣耀等视频场景（支持定制，需支付定制费）。 |
| 剪辑制作 | 支持视频的裁剪、拼接、图片转视频、贴片、帖字、画中画、音频编辑等操作 |

