## Overview

The smart toolbox provides capabilities for processing almost all types of visualized multimedia files, such as image watermark, image compression, and audio/video/file format conversion. It presents various capabilities of COS in the form of convenient and quick tools in the console for you to use with speed and easy.

## Note

All the capabilities in the smart toolbox are implemented based on the data processing APIs of COS. Using them is equivalent to calling such APIs. You need to keep the following in mind during use:
- When you use the smart toolbox for the first time, the **CI** service will be activated for you free of charge.
- Whenever a processing operation is completed through the toolbox, it is equivalent to calling a data processing API once and incurs processing fees as detailed below:
<table>
<thead>
<tr>
<th width="70%">Tool</th>
<th>Fees</th>
</tr>
</thead>
<tbody><tr>
<td>Image compression (WebP or JPEG format), image editing, image watermark, and image information</td>
<td>Basic image processing</td>
</tr>
<tr>
<td>Image compression (AVIF or HEIF format)</td>
<td>Advanced image compression</td>
</tr>
<tr>
<td>Audio/Video processing</td>
<td>Media processing</td>
</tr>
<tr>
<td>AI processing</td>
<td>Content recognition</td>
</tr>
<tr>
<td>Online file preview</td>
<td>File preview</td>
</tr>
</tbody></table>

## Tools

The smart toolbox currently contains the following tools:

<table>
   <tr>
      <th>Category</td>
      <th>Tool</td>
   </tr>
   <tr>
      <td rowspan=4>Image processing</td>
			<td><a href="#pictureCompression">Image compression</a></td>
   </tr>
   <tr>
      <td><a href="#pictureEditing">Image editing</a></td>
   </tr>
   <tr>
      <td><a href="#imageWatermark">Image watermark</a></td>
   </tr>
   <tr>
      <td><a href="#imageInformation">Image information</a></td>
   </tr>
   <tr>
      <td rowspan=8>Audio/Video processing</td>
      <td><a href="#formatConversion">Audio/Video format conversion</a></td>
   </tr>
   <tr>
      <td><a href="#extremeHD">Top speed codec transcoding</a></td>
   </tr>
   <tr>
      <td><a href="#videoFrame">Video frame capturing</a></td>
   </tr>
   <tr>
      <td><a href="#videoTurnChart">Video-to-animated image conversion</a></td>
   </tr>
   <tr>
      <td><a href="#smartCover">Intelligent thumbnail</a></td>
   </tr>
   <tr>
      <td><a href="#superresolution">Digital remastering</a></td>
   </tr>
   <tr>
      <td><a href="#videocut">Video montage</a></td>
   </tr>
   <tr>
      <td><a href="#voiceseparate">Voice/Sound separation</a></td>
   </tr>
   <tr>
      <td rowspan=2>AI processing</td>
      <td><a href="#imageTags">Image tagging</a></td>
   </tr>
   <tr>
      <td><a href="#licenseDetection">Vehicle and license plate detection</a></td>
   </tr>
   <tr>
      <td>File processing</td>
      <td><a href="#documentOnline">Online file preview</a></td>
   </tr>
</table>


### Image processing

<dx-tabs>
::: Image compression[](id:pictureCompression)
The image compression tool can downsize an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). On the left sidebar, click **Smart Toolbox**.
2. On the **Smart Toolbox** page, select **Image Processing** > **Image Compression**.
3. In the image upload area, select an existing image in the bucket and add it to the tool.

4. After the image is added, the tool will automatically process it, and you can see the size of the compressed image on the left. You can also download the compressed image.

:::
::: Image editing[](id:pictureEditing)
The image editing tool offers capabilities of image cropping, rotation, scaling, sharpening, brightness adjustment, and contrast adjustment.

#### Directions

After adding an image as instructed in steps 1–3 in the [Image compression](#pictureCompression) section, use tools on the left to make corresponding adjustments.

:::
::: Image watermark[](id:imageWatermark)
The image watermark tool allows you to add an image or text to another image in the form of watermark.

#### Directions

- Image watermark: After adding an image as instructed in steps 1–3 in the [Image compression](#pictureCompression) section, click **Image Watermark** on the left, select an existing image in the bucket, adjust the margins, and click **Generate Watermark**.

- Text Watermark: Click **Text Watermark** on the left, enter the watermark text, adjust the margins, font, and font size, and click **Generate Watermark**.

:::
::: Image information[](id:imageInformation)
The image information tool lists the format, size, and MD5 information of an image.

#### Directions

After adding an image, click **Information** on the left to view the information of the image.
:::
</dx-tabs>


### Audio/Video processing

<dx-tabs>
::: Audio/Video format conversion[](id:formatConversion)
The audio/video format conversion tool can convert your audio/video files into MP4, MP3, MOV, AVI, MKV, and other formats. It allows you to set different parameters such as video resolution and audio bitrate during conversion to adapt to different terminals and network environments.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). On the left sidebar, click **Smart Toolbox**.
2. On the **Smart Toolbox** page, select **Audio/Video Processing** > **Audio/Video Format Conversion**.
3. Select an audio/video file and add it to the tool. You can select existing files in the bucket or local files, but if you select local files, you need to upload them to the bucket, as the tool can convert files in the bucket only.

4. After selecting an audio/video file, you need to select the conversion parameters as detailed below:
The following is an example of converting a video with parameters of **MP4 format, H.264 codec, 720 \* proportional height resolution, and 1024 Kbps bitrate**:
 - Video format: MP4
 - Video codec: H.264
 - Video resolution: 720 (width) \* proportional height of the input video
 - Video bitrate: 1024 Kbps

5. After selecting parameters, select the name and location of the output video in the bucket and click **Finish**.

6. Click **Start Transcoding** and wait for the transcoding to complete.

7. After transcoding is completed, the input and output videos are displayed in the left and right of the video display area respectively for you to directly compare and check the transcoding effect. You can copy the output video link or directly download the output video by clicking buttons in the bottom-right corner.

:::
::: Top speed codec transcoding[](id:extremeHD)
Top speed codec transcoding leverages deep learning algorithms to convert an input video to an output video with higher definition, lower noise, and higher frame rate by reducing the compression and texture distortion of the input video.

#### Directions

The steps of top speed codec transcoding are similar to those of audio/video file conversion, except that the output video transcoded by top speed codec is smaller and clearer.

:::
::: Video frame capturing[](id:videoFrame)
With the video frame capturing tool, you can capture any frame in a video and save it as an image.

#### Directions

1. Add a video to the tool as instructed in steps 1–3 in the [Audio/Video format conversion](#formatConversion) section and select frame capturing parameters.

2. After the video is added, the tool will automatically start capturing frames and display the captured frames on the right.


:::
::: Video-to-animated image conversion[](id:videoTurnChart)
The video-to-animated image conversion tool can convert your video into a GIF or WebP animated image.

#### Directions

1. Add a video to the tool as instructed in steps 1–3 in the [Audio/Video format conversion](#formatConversion) section and select video-to-animated image conversion parameters.
2. After the video is added, the tool will automatically start converting and display the output animated image on the right.

:::
::: Intelligent thumbnail[](id:smartCover)
By intelligently recognizing and analyzing the characteristics of motions, events, and faces in the video, the intelligent thumbnail tool can automatically identify, capture, and save highlight frames as video thumbnails.

#### Directions

1. Add a video to the tool as instructed in steps 1–3 in the [Audio/Video format conversion](#formatConversion) section.
2. After the video is added, the tool will automatically start analyzing the video and capturing highlight frames and display the captured frames on the right.
:::
::: Digital remastering[](id:superresolution)
The digital remastering tool has video noise cancellation, super resolution, SDR to HDR, sharpening, and other capabilities. Through the combination of different capabilities, it can meet your needs for remastering old and low-quality videos.

#### Directions

1. Add a video to the tool as instructed in steps 1–3 in the [Audio/Video format conversion](#formatConversion) section.
2. After adding the video, select the target resolution and click **Start Remastering**.
:::
::: Video montage[](id:videocut)
Video montage generates highlights in a video, which are convenient for secondary creation.

#### Directions

1. Add a video to the tool as instructed in steps 1–3 in the [Audio/Video format conversion](#formatConversion) section.
2. After adding the video, select the target resolution and click **Start Processing**.
:::
::: Voice/Sound separation[](id:voiceseparate)
The voice/sound separation feature separates the voice from the background sound in a video material to generate a new independent audio file. Then, you can apply artistic processing of other styles to the material without accompaniment and noise.

#### Directions

1. Add a video or an audio to the tool as instructed in steps 1–3 in the [Audio/Video format conversion](#formatConversion) section.
2. After adding the video or audio, select the output type and click **Start Processing**.

:::
</dx-tabs>


### AI processing

<dx-tabs>
::: Image tagging[](id:imageTags)
The image tagging tool can identify scenes, objects, people, and other information in images. It contains thousands of tags in over 60 subcategories in 8 categories, such as natural scenery (mountain, sea, sky, sunset, etc.), man-made environment (building, playground, meeting room, etc.), people (male, female, selfie, group photo, etc.), object (food, clothing, daily necessities, etc.), and pet/wild animal (cat, dog, bird, mammal, marine animal, etc.).

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). On the left sidebar, click **Smart Toolbox**.
2. On the **Smart Toolbox** page, select **AI Processing** > **Image Tagging**.
3. Add an image to the tool.
4. After the image is added, the tool will automatically start analyzing the image and display image tag information on the right.

:::
::: Vehicle and license plate detection[](id:licenseDetection)
The vehicle and license plate detection tool can accurately identify the coordinates, brands, models, model years, and colors of almost all passenger cars on the market.

#### Directions

1. Add an image to the tool as instructed in steps 1–3 in the [Image tagging](#imageTags) section.
2. After the image is added, the tool will automatically start analyzing the image and display the vehicle and license plate information on the right.

:::
</dx-tabs>

### File processing

[](id:documentOnline)
#### Online file preview

The file preview tool can convert any Office documents into a webpage format that can be previewed online. After conversion, you can copy the file link to view the file in a browser.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). On the left sidebar, click **Smart Toolbox**.
2. On the **Smart Toolbox** page, select **File Preview** > **Online File Preview**.
3. Add a file (e.g., a PPT file) to the tool.
4. After the PPT file is added, the tool will automatically start processing it to generate the HTML webpage for online preview. You can preview it directly or copy the link to preview it in a browser.

