## Overview
This document describes how to perform video encoding and decoding as well as AI image quality enhancement on GN7vi instances, which are fully compatible with the open-source FFmpeg.


## Directions

### Preparing the instance environment
Create an instance:
 - **Instance**: Select an instance based on the requirements for GPU and the number of cores as instructed in [Computing Instance](https://intl.cloud.tencent.com/document/product/560/19701).
 - **Image**: Select an image from the [available images](https://intl.cloud.tencent.com/document/product/560/19701) in the table.
 - **Driver**: The automatic installation of CUDA and cuDNN is optional. You can also install them manually after creating the instance as needed:
    - Log in to the created GPU instance as instructed in [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
    - Run the following command to have the GPU driver, CUDA, and cuDNN installed automatically.
   <dx-alert infotype="explain" title="">
   Configure the environment with GPU driver 460.106.00, CUDA 11.2.2, and cuDNN 8.2.1.
   </dx-alert> ```shell
   wget https://gpu-related-scripts-1251783334.cos.ap-guangzhou.myqcloud.com/gpu-auto-install/gpu_auto_install_220823.sh && wget https://gpu-related-scripts-1251783334.cos.ap-guangzhou.myqcloud.com/gpu-auto-install/driver460_cuda11.2.2.txt && sudo bash ./gpu_auto_install_220823.sh install --config_file=./driver460_cuda11.2.2.txt && source /etc/bash.bashrc && source ${HOME}/.bashrc
```


### File overview
Run the following commands in sequence to view all files under `tscsdk-center`.
```shell
cd /usr/local/qcloud/tscsdk-center
```
```shell
ls -l
```
The following information appears:
![](https://qcloudimg.tencent-cloud.cn/raw/b95500646122d69983e86bcce2563ffb.png)
The description is as follows:
<table>
<tr>
<th>File Name</th>
<th>Description</th>
</tr>
<tr>
<td>fflib_gpu</td>
<td>Dependency library for image quality processing.</td>
</tr>
<tr>
<td>ffmpeg</td>
<td>FFmpeg program embedded with the image quality processing feature.</td>
</tr>
<tr>
<td>tenmodel</td>
<td>AI model used in image quality processing.</td>
</tr>
<tr>
<td>videos</td>
<td>Built-in sample videos.</td>
</tr>
</table>


### Getting started
1. Run the following commands in sequence to set environment variables.
```shell
cd /usr/local/qcloud/tscsdk-center
```
```shell
export LD_LIBRARY_PATH=./fflib_gpu:$LD_LIBRARY_PATH
```
2. Under the `tscsdk-center` directory, run the following commands in sequence to generate the sample output video after image quality processing.
 - LD video processing: LD videos usually have a resolution of up to 720p. The command uses the standard super resolution model in the balance mode of tenfilter and unsharp sharpening.
```shell
./ffmpeg -i ./videos/input1.mp4 -vf tenfilter=mag_filter=1:mag_sr=2:mag_sr_stre=balance,unsharp -c:v libten264 -ten264opts crf=26:vbv-maxrate=2000 -y output1.mp4
```
 - HD video processing: HD videos usually have a resolution of above 720p. The command uses the high-quality super resolution model in tenfilter.
```shell
./ffmpeg -i ./videos/input2.mp4 -vf tenfilter=mag_srgan=1 -c:v libten264 -ten264opts crf=26:vbv-maxrate=2000 -y output2.mp4
```
 - Fast processing model: The following commands use compression artifact removal in tenfilter, standard super resolution model in general mode, and unsharp sharpening.
```shell
./ffmpeg -i ./videos/input1.mp4 -vf tenfilter=af=auto,tenfilter=mag_filter=1:mag_sr=2:mag_sr_stre=normal,unsharp -c:v libten264 -ten264-params crf=26:vbv-maxrate=2000 -y fast_output1.mp4
```
```shell
./ffmpeg -i ./videos/input2.mp4 -vf tenfilter=af=auto,tenfilter=mag_filter=1:mag_sr=2:mag_sr_stre=normal,unsharp -c:v libten264 -ten264-params crf=26:vbv-maxrate=2000 -y fast_output2.mp4
```
<dx-alert infotype="explain" title="">
The running speed of a model is affected by the input resolution. The higher the resolution, the slower the running. When a specific AI model is run for the first time, the initialization will take a long time. During subsequent command execution, the speed will be improved significantly. You can evaluate the running speed by comparing subsequent execution results.
</dx-alert>
Some parameters in the `ffmpeg` command are as described below:
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td><code>-i videos/input1.mp4</code></td>
<td>Specifies the input video file.</td>
</tr>
<tr>
<td><code>-vf tenfilter=mag_srgan=1</code></td>
<td>Specifies the video processing filter graph. For more information on parameter descriptions, see <a href="#ai">List of features of the AI model for video processing</a>.</td>
</tr>
<tr>
<td><code>-c:v libten264</code></td>
<td>Specifies Tencent's proprietary Ten264 or Ten265 as the video encoder.</td>
</tr>
<tr>
<td><code>-ten264opts crf=26:vbv-maxrate=2000</code></td>
<td>Sets video encoder parameters. For more information on parameter descriptions, see <a href="#videoEncoder">List of features of the video encoder</a>.</td>
</tr>
<tr>
<td><code>-y output.mp4</code></td>
<td>Specifies the output video file to automatically overwrite the existing file.</td>
</tr>
</table>
3. Wait for the program to end and download the output video file. We recommend you use Xshell or MobaXterm. The following are screenshots of the four video files output by the commands.
<dx-tabs>
::: output1.mp4
Screenshot taken at 01:15 (minute)
![](https://qcloudimg.tencent-cloud.cn/raw/9773d6f0790e5e1ceedf3a2bf5c958ee.png)
:::
::: fast_output1.mp4
Screenshot taken at 01:15 (minute)
![](https://qcloudimg.tencent-cloud.cn/raw/12da44d281de1acf74cd823acbcc0f44.png)
:::
::: output2.mp4
Screenshot taken at 00:10 (minute)
![](https://qcloudimg.tencent-cloud.cn/raw/891787f7ed4754ee10a97ac74e2d7eba.png)
:::
::: fast_output2.mp4
Screenshot taken at 00:10 (minute)
![](https://qcloudimg.tencent-cloud.cn/raw/108db7750a9ee26e7661ff621af2b1c5.png)
:::
</dx-tabs>


## Feature List

The tscsdk-center consists of two parts: [AI model for video processing](#ai) and [Tencent's proprietary video encoder](#videoEncoder).
The AI model for video processing is integrated by using the FFmpeg filter mechanism, so that filters can embed AI inference capabilities into video encoding/decoding and processing processes. This improves hardware utilization efficiency and throughput. With Tencent's proprietary video encoder, a higher video encoding compression rate is delivered in addition to image quality enhancement.


### List of features of the AI model for video processing[](id:ai)
The AI model for video processing is integrated in a filter named "tenfilter" and is called and configured through `"-vf tenfilter=name1=value1:name2=value2"`. One AI model can be enabled in one tenfilter, and free combinations are available when there are multiple tenfilters.
All AI models are as described below:

<table>
<tr>
<th>Model or Feature Name</th>
<th>Parameter</th>
<th>Sample</th>
</tr>
<tr>
<td>General parameters</td>
<td>
<ul class="params">
<li>mdir: It is the configuration file path of the model, which defaults to `./tenmodel/tve-conf.json`.</li>
<li>gpu: It is the GPU No. of the tenfilter.</li>
</ul>
</td>
<td>tenfilter=mdir=./tenmodel/tve-conf.json:gpu=1</td>
</tr>
<tr>
<td>Compression artifact removal</td>
<td>af: It is the strength of compression artifact removal, which can be only `auto` currently.</td>
<td>tenfilter=af=auto</td>
</tr>
<tr>
<td>Face protection</td>
<td>
<ul class="params">
<li>face_protect_enable: The face protection logic is enabled when it is `1`.</li>
<li>face_af_ratio: It is the face area denoising weakening coefficient.</li>
<li>face_sp_ratio: It is the face area sharpening coefficient.</li>
</ul>
</td>
<td>tenfilter=face_protect_enable=1:face_af_ratio=0.5:face_sp_ratio=0.5</td>
</tr>
<tr>
<td>Video frame interpolation</td>
<td>
<ul class="params">
<li>mag_fps: Video frame interpolation is enabled when it is `1`.</li>
<li>fps: It is the target frame rate.</li>
</ul>
</td>
<td>tenfilter=mag_fps=1:fps=60</td>
</tr>
<tr>
<td>Color enhancement</td>
<td>
<ul class="params">
<li>mag_filter: It needs to be set to `1`.</li>
<li>cebb: Color enhancement is enabled when it is `1`.</li>
</ul>
</td>
<td>tenfilter=mag_filter=1:cebb=1</td>
</tr>
<tr>
<td>Standard super resolution</td>
<td>
<ul class="params">
<li>mag_filter: It needs to be set to `1`.</li>
<li>mag_sr: It is the super resolution rate. Currently, only the twice super resolution is supported.</li>
<li>mag_sr_stre: It is the super resolution mode, which can be set to `normal` or `balance`.</li>
</ul>
</td>
<td>tenfilter=mag_filter=1:mag_sr=2:mag_sr_stre=normal</td>
</tr>
<tr>
<td>High-quality super resolution</td>
<td>mag_srgan: High-quality super resolution is enabled when it is `1`.</td>
<td>tenfilter=mag_srgan=1</td>
</tr>
<tr>
<td>Video noise removal</td>
<td>
<ul class="params">
<li>mag_filter: It needs to be set to `1`.</li>
<li>dn: It is the noise removal strength, which can be only `3` currently.</li>
</ul>
</td>
<td>tenfilter=mag_filter=1:dn=3</td>
</tr>
<tr>
<td>Video image quality enhancement<br>
Face enhancement<br>
Font enhancement<br>
(Support for multiple models)</td>
<td>
<ul class="params">
<li>mag_filter: It needs to be set to `1`.</li>
<li>eh: Image quality enhancement is enabled when it is `1`.</li>
<li>faceeh: Face enhancement is enabled when it is `1`.</li>
<li>fonteh: Font enhancement is enabled when it is `1`.</li>
<li>prior: It is the priority for executing AI models, for example, "faceeh-eh-fonteh". Corresponding models need to be enabled. When `-parally` is added, parallel optimization is enabled.</li>
</ul>
</td>
<td>
<ul class="params">
<li>Single model:
tenfilter=mag_filter=1:eh=1</li>
<li>Multiple models:
tenfilter=mag_filter=1:eh=1:faceeh=1:prior=faceeh-eh-parally</li>
</ul>
</td>
</tr>
</table>




### Tencent's proprietary video encoder[](id:videoEncoder)

tscsdk-center contains Ten264 and Ten265 video encoders independently developed by Tencent. Encoder types and parameters can be set through command parameters during video processing.
Each encoder can be specified and set in the following ways:

<table>
<thead>
<tr>
<th>Encoder Name</th>
<th>Method to Specify</th>
<th>Method to Set</th>
</tr>
</thead>
<tbody><tr>
<td>Ten264</td>
<td>-vcodec libten264-c:v libten264</td>
<td>-ten264opts name1=value1:name2=value2</td>
</tr>
<tr>
<td>Ten265</td>
<td>-vcodec libten265-c:v libten265</td>
<td>-ten265-params name1=value1:name2=value2</td>
</tr>
</tbody></table>

The parameters of each encoder are as detailed below:

<dx-tabs>
::: Ten264 encoder


<table>
<thead>
<tr>
<th width="15%">Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>preset</td>
<td>Specifies the configuration of the encoder's encoding parameter set.<br>0: Ultrafast; 1: Superfast; 2: Very fast; 3: Faster; 4: Fast; 5: Medium; 6: Slow; 7: Slower; 8: Very slow; 9: Placebo.</td>
</tr>
<tr>
<td>bitrate</td>
<td>Bitrate of the output video in ABR mode.</td>
</tr>
<tr>
<td>crf</td>
<td>CRF value in CRF mode.</td>
</tr>
<tr>
<td>aq-mode</td>
<td>0: Disable aqmode; 1: Enable aqmode; 2: Variance-based aqmode; 3: Variance-based aqmode towards dark scenes.<br>2 is the default value and produces better SSIM results.</td>
</tr>
<tr>
<td>vbv-maxrate</td>
<td>Maximum VBV bitrate. This value is the same as the configured bitrate by default.</td>
</tr>
<tr>
<td>vbv-bufsize</td>
<td>VBV buffer size. This value is four times the configured bitrate by default.</td>
</tr>
<tr>
<td>rc-lookahead</td>
<td>Length of the lookahead.</td>
</tr>
<tr>
<td>scenecut</td>
<td>Whether to enable scene switch. It is enabled by default and we generally recommend you keep it enabled.</td>
</tr>
<tr>
<td>keyint</td>
<td>Maximum keyframe interval. It is 256 by default and can be configured as needed; generally, you should configure it as the number of frames with a time interval of 2–5s.</td>
</tr>
<tr>
<td>threads</td>
<td>Number of threads in the used thread pool.</td>
</tr>
<tr>
<td>lookahead-threads</td>
<td>Number of threads used for lookahead.</td>
</tr>
<tr>
<td>profile</td>
<td>"baseline", "main", "high", "high422", and "high444".</td>
</tr>
</tbody></table>


:::
::: Ten265 encoder


<table>
<thead>
<tr>
<th width="15%">Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>preset</td>
<td>Specifies the configuration of the encoder's encoding parameter set.<br>-1: Ripping; 0: Placebo; 1: Very slow; 2: Slower; 3: Slow; 4: Universal; 5: Medium; 6: Fast; 7: Faster; 8: Very fast; 9: Superfast.</td>
</tr>
<tr>
<td>rc</td>
<td>Bitrate control method.<br>0: CQP; 1: ABR_VBV; 2: ABR; 3: CRF_VBV; 4: CRF.</td>
</tr>
<tr>
<td>bitrate</td>
<td>Bitrate of the output video in ABR mode.</td>
</tr>
<tr>
<td>crf</td>
<td>CRF value in CRF mode. Value range: [1,51].</td>
</tr>
<tr>
<td>aq-mode</td>
<td>0: Disable aqmode; 1: Enable aqmode; 2: Variance-based aqmode; 3: Variance-based aqmode towards dark scenes.<br>2 is the default value and produces better SSIM results.</td>
</tr>
<tr>
<td>vbv-maxrate</td>
<td>Maximum VBV bitrate. This value is the same as the configured bitrate by default.</td>
</tr>
<tr>
<td>vbv-bufsize</td>
<td>VBV buffer size. This value is four times the configured bitrate by default.</td>
</tr>
<tr>
<td>rc-lookahead</td>
<td>Length of the lookahead.</td>
</tr>
<tr>
<td>scenecut</td>
<td>Scene switch threshold. Value range: [0,100]. 0 indicates disabled. It is enabled by default and we generally recommend you keep it enabled.</td>
</tr>
<tr>
<td>open-gop</td>
<td>Whether to enable open GOP.<br>0: Disabled; 1: Enabled. It is enabled by default; in order to support random access in the live streaming scenario, we recommend you disable it.</td>
</tr>
<tr>
<td>keyint</td>
<td>Maximum keyframe interval. It is 256 by default and can be configured as needed; it needs to be a multiple of 8 greater than 50.</td>
</tr>
<tr>
<td>ltr</td>
<td>Whether to support long-term reference frames. 0: Disabled; 1: Enabled. It is enabled by default; if the hardware device that plays back HEVC videos is poor, we recommend you disable it.</td>
</tr>
<tr>
<td>pool-threads</td>
<td>Number of threads in the thread pool used by WPP. It is the same as the number of CPU cores by default; if you want to reduce CPU usage, lower this number.</td>
</tr>
</tbody></table>

:::
</dx-tabs>


## Usage Recommendations
- tscsdk-center allows for the flexible control of each AI model. If you have special requirements or scenarios, you can set the switch for each model and combine different models to deliver better video processing effects.
- tscsdk-center provides two super resolution models. The standard model is suitable for earlier sources at a low resolution, while the high-quality model is more suitable for HD sources. We recommend you evaluate the effects of the two models while considering the video source type.
- In tscsdk-center, AI models need to run on GPU, while video encoders run only on CPU. In most cases, when the GPU computing power is fully used, there will be some idle CPU space. Therefore, some video processing tasks running only on CPU can be assigned, such as video transcoding, to fully utilize hardware resources.


<style>
 .params{margin-bottom:0px !important}
</style>
