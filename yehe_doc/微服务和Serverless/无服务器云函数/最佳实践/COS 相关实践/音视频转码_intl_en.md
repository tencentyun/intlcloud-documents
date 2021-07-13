## Overview
In use cases such as video and social networking, users upload high numbers of images and audio/video files frequently, which has high requirements for the real-timeness and concurrency capabilities of the processing system. Multiple functions can be used to process uploaded videos with different definitions in order to meet the needs of users in diversified scenarios and adapt to small-bandwidth and unstable mobile networks.



## How It Works
SCF, FFmpeg, and COS can be used in combination as shown below to transcode audio and video files:
![](https://main.qcloudimg.com/raw/f78b7553884ea86ceef81ef21cd70d3e.png)
In SCF, you can write custom business logic in different programming languages (Python, Node, PHP, Java, and Go). Taking transcoding as an example, the steps are as follows:

1. Create a function and deploy the FFmpeg resource package and transcoding logic in it.
2. Configure a COS bucket trigger to process the source video in real time and generate logs, monitoring data, and alarms in a relayed manner.
3. Return the transcoded video to COS and trigger automatic prefetch.


## Comparison with TKE
Compared with TKE, the combination of SCF and FFmpeg has the following advantages and disadvantages in audio/video transcoding:
<table>
<tr>
<th style="
    width: 11%;
">Item</th><th style="
    width: 36%;
">TKE-based Implementation</th><th style="
    width: 36%;
">SCF-based Implementation</th><th style="
    width: 17%;
">Analysis</th>
</tr>
<tr>
<th>Implementation method</th>
<td><ul class="params">
<li>FFmpeg is run in a Docker container.</li>
<li>FFmpeg is customized, and different versions have different binary dependencies, all of which are packaged as images.</li>
<li>Docker image tags can be autonomously controlled. Different services load different Docker images, which contain different FFmpeg versions.</li>
</ul></td>
<td><ul class="params">
<li>Different FFmpeg versions can be compiled into different executable files, deployed to "layers" of SCF functions, and decoupled from the business logic.</li>
<li>Different functions can be written and bound to different FFmpeg versions at the "layers" to provide different transcoding features.</li>
<li>A scheduling function can be written to segment videos and schedule different transcoding services.</li>
</ul></td>
<td>The implementation methods do not differ greatly.</td>
</tr>
<tr>
<th>Development/Testing/Deployment experience</th>
<td><ul class="params">
<li>After local development and testing, the CI/CD process will be triggered, and an image will be burnt to complete the deployment.</li>
<li>The grayscale release system needs to be maintained, and TKE cluster updates are slow.</li>
</ul></td>
<td><ul class="params">
<li>After local development and testing, the CI/CD process will be triggered to complete the deployment.
</li>
<li>SCF offers beta test/release/rollback features, which allow you to integrate APIs directly to fully automate the deployment process.
</li>
<li>Sub-accounts can use the CLI tool to perform development and debugging in real time in the test environment, thus improving the efficiency.
</li>
</ul></td>
<td>SCF makes the development process easier and more efficient.</td>
</tr>
<tr>
<th>Logging/Monitoring/Alarming
</th>
<td>It is necessary to launch the agent in the TKE cluster and connect it to the logging platform, monitoring center, and alarming platform.
</td>
<td>SCF offers logging/monitoring/alarming capabilities and APIs for connection to third-party logging/monitoring platforms. It supports launching the agent process in the runtime and reporting data synchronously.
</td>
<td>SCF offers a wider range of capabilities, but for connection to self-created platforms, it is more complex to launch the agent in SCF than in TKE.</td>
</tr>
<tr>
<th>OPS</th>
<td>TKE clusters need to be maintained on your own and have low auto-scaling efficiency.</td>
<td>Maintenance is not required, as SCF guarantees cluster availability, load balancing, and auto scaling.</td>
<td>SCF is easier to use.</td>
</tr>
<tr>
<th>Fees</th>
<td>It is necessary to reserve container resources based on the peak values, which may cause a waste of resources.</td>
<td>Resources are auto-scalable and pay-as-you-go, saving more than 30% of costs.</td>
<td>SCF has obvious advantages.</td>
</tr>
</table>

Through comparison with TKE in multiple dimensions above, the following conclusions can be drawn:
**Advantages**:
- SCF provides a standard runtime environment, ensures the high availability and auto scalability of resources, and requires no dedicated maintenance.
- SCF is billed by actual usage, eliminating the waste of resources.
- Development and debugging in SCF are more efficient, and dependencies are decoupled from the business and can be hot updated separately in real time.
- Runtime environments are isolated, so the failure of one single request will not affect the normal execution of other requests.

**Disadvantages**:
- The introduction of SCF needs to be integrated with the existing CI/CD process, so there may be some changes in the development method.
- The existing business code requires modifications mainly in terms of FFmpeg encoding/decoding. SCF can provide encoding/decoding tools and development assistance to facilitate the modifications.





<span id="Precondition"></span>
## Prerequisites
This document uses the Guangzhou region as an example:
- Go to the [COS console](https://console.cloud.tencent.com/cos5/bucket), create a bucket, and set the access permission of the bucket to **public read/private write**.
- (Optional) If the video file is above 500 MB in size, you need to go to the CFS console to activate the CFS service so as to expand the local storage space of SCF. For more information, please see [Mounting CFS File System](https://intl.cloud.tencent.com/document/product/583/37497).
- Go to the CAM console, create an execution role for SCF, and grant the role COS and CFS read/write permissions to authorize SCF to access the corresponding services. For more information, please see [Role and Authorization](https://intl.cloud.tencent.com/document/product/583/38176).


## Directions
### Creating function
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) and click **Function Service** on the left sidebar.
2. Select the region where to create a function at the top of the **Function Service** page and click **Create** to enter the function creation process.
3. Select a function template as follows on the **Create Function** page as shown below:
![](https://main.qcloudimg.com/raw/362904e7e8f06b386774aa83020a9a44.png)
 - **Creation method**: select **Template**.
 - **Fuzzy search**: enter **VideoTranscode** and search. This document uses the Python 3.6 runtime environment as an example.
 Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.
4. Click **Next**. The function name is automatically generated by default and can be modified as needed. Follow the prompts to configure the environment variables and execution role as shown below:
![](https://main.qcloudimg.com/raw/d868aa48a842794c3490db8e0b4f6369.png)
 - **Environment Variable**: enter as shown below:
![](https://main.qcloudimg.com/raw/d3073bbe145a6b19f145ed5ed4fd75da.png)
<table>
<tr>
<th>key</th><th>value</th>
</tr>
<tr>
<td>region</td><td>COS bucket region.</td>
</tr>
<tr>
<td>target_bucket</td><td>The created COS bucket to which the output video will be uploaded after being transcoded.</td>
</tr>
<tr>
<td>target_path</td><td>The specified directory of the bucket to which the output video will be uploaded after being transcoded.</td>
</tr>
</table>
 - **Execution Role**: check **Enable**, select **Configure and use SCF template role**, and the system will automatically create and select an SCF template execution role associated with full access permissions of COS and CFS. You can also check **Use the existing role** and select the existing role created in [Prerequisites](#Precondition) in the drop-down list. This document takes **Configure and use SCF template role** as an example.
 During execution, the function will use the execution role to get a temporary key to read and write resources in the COS bucket.
5. In the **Trigger Configurations** section, configure the COS trigger as shown below:
![](https://main.qcloudimg.com/raw/d655b8da82572422b4a4c4eef59ded21.png)
The main parameter information is as follows. Keep the remaining options as default:
 - **Trigger Method**: select **COS trigger**.
 - **COS Bucket**: select a bucket. <b>If you want to store the source video and the output video in the same bucket, you need to configure the trigger with a prefix filtering rule `/`, such as `demo/`.</b>
6. Click **Complete**.


### (Optional) Configuring CFS mounting
>? If you have activated the CFS service, please enable both the VPC and file system mounting capabilities in the function by following the steps below.
>
1. On the **Function configuration** page of the function, click **Edit** in the top-right corner and configure the function.
 - **VPC**: check **Enable** and select a VPC and subnet.
 - **File System**: check **Enable** and select the file system created in [Prerequisites](#Precondition).
2. Click the **Function code** tab to enter the function code editing page and modify the file upload path as shown below:
![](https://main.qcloudimg.com/raw/6a07faf2807ce47bb7d435fb1dc8a922.png)
Comment on line 76 of the code and add the following code to line 77.
```
upload_path = '/mnt/new-'+ key.split('/')[-1]
```


## Testing Features
Log in to the [COS console](https://console.cloud.tencent.com/cos5/bucket), enter the corresponding bucket directory, upload a video file, and check whether a compressed video file is generated in the corresponding transcoding directory as shown below:
>? The time it takes to compress a video varies by video size. If a video is large, it will take longer to compress the video and display the output video.
>



## Scalability
You can add automated CDN purge/prefetch capabilities to the demo in this document. For example, when the output video is returned to the COS bucket, a new function can be triggered to execute the CDN purge/prefetch features. For more information, please see [CDN Cache Purging](https://intl.cloud.tencent.com/document/product/436/37273).

You can also leverage the high concurrence of SCF to implement fast transcoding or segmenting. For example, function A can schedule tasks while function B can perform actual transcoding/segmenting tasks. With the aid of the CFS mounting capabilities, you can also implement cross-function file sharing with ease.

