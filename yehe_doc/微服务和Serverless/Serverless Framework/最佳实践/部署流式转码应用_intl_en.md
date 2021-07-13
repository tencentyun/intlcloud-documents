## Application Overview
By using COS + SCF + CLS + FFmpeg, you can quickly build a highly available and customizable video transcoding service that features concurrent processing and real-time logging.

### Architecture
Create an FFmpeg task process through SCF. The SCF process and FFmpeg task process carry out data transfer through pipe and FIFO. The two task threads in the SCF process respectively receive the FFmpeg log stream output by the FFmpeg task process to the SCF process and the transcoded file stream. The real-time logging thread outputs the log stream, and the upload task is responsible for caching the file stream and uploading it to the user-defined destination COS bucket. 

![1608278445413](https://main.qcloudimg.com/raw/4e008b577fe7cc8dc2a7ebdb23fdc1ab.svg)

### Application advantages
- **Streaming transcoding**
The source video file is pulled and the transcoded file is uploaded in a streaming manner, which breaks through the limitation of local storage and eliminates the need for additional deployment of CFS and other services.
- **Real-time logging**
During video transcoding, you can view the transcoding progress in real time through CLS logs. In addition, this scheme supports outputting the complete logs of the FFmpeg application.
- **Prolonged execution**
By leveraging the [prolonged execution mechanism](https://intl.cloud.tencent.com/document/product/583/39466) of SCF, this scheme can be run for 12 to 24 hours, making it suitable for transcoding large files that take a long time.
- **Custom parameters**
You can customize the FFmpeg command parameters.

### Application resources
After the transcoding application is deployed, the following resources will be created:
- **SCF function**: it reads COS files, outputs files transcoded with FFmpeg to COS, and outputs the real-time log of the transcoding process to CLS in a streaming manner.
- **CLS log**: it stores the real-time log of the transcoding process. CLS logs may incur fees. For more information, please see [CLS Billing Rules](https://intl.cloud.tencent.com/document/product/614/37889).

### Notes
- The transcoding application relies on the prolonged function execution capability. For more information, please see [Async Execution](https://intl.cloud.tencent.com/document/product/583/39466).
- We recommend you configure the transcoding output bucket and the function in the same region, because cross-region configuration will reduce the stability and efficiency of the transcoding application and incur traffic fees.
- You need to create an execution role for the function of the transcoding application and grant it the read/write permissions of COS. For detailed configuration, please see [Execution Role](#role).
- FFmpeg command parameter configuration varies by transcoding scenario; therefore, you should have basic knowledge of FFmpeg. This document only provides a few samples for your reference. For more FFmpeg commands, please visit [FFmpeg official website](https://ffmpeg.org/documentation.html).


## Prerequisites

1. Install [Serverlesss Framework](https://intl.cloud.tencent.com/document/product/1040/37034).
3. Configure and deploy account permissions as detailed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793). 
4. Configure [execution role](#role) permissions.

## Directions
#### 1. Download the transcoding application
```
sls init transcode-app
```

Enter the project directory `transcode-app`, and you will see the directory structure as follows:
```
transcode-app
|- .env  # Environment configuration
|- serverless.yml # Application configuration
|- log/ # Log configuration
|  └── serverless.yml
└──transcode/  # Transcoding function configuration
       |- src/
       |   |- ffmpeg   # FFmpeg transcoding tool
       |   └── index.py
       └── serverless.yml
```
 - `log/serverless.yml` defines a CLS logset and topic, which are used to store the logs output during the transcoding process. Currently, CLS is used for log storage. Each transcoding application will create related resources based on the configured CLS logset and topic. Using CLS will incur fees. For more information, please see [CLS Billing Rules](https://intl.cloud.tencent.com/document/product/614/37889).
 - `transcode/serverless.yml` defines the basic function configuration and transcoding parameter configuration.
 - `transcode/src/index.py` implements the transcoding feature.
 - `transcode/src/ffmpeg` is the Ffmpeg transcoding tool.

#### 2. Configure environment variables and application parameters
- Application parameters are in the `transcode-app/serverless.yml` file.
```
# Application information
app: transcodeApp # You need to configure it as your application name
stage: dev # Environment name. Default value: dev
```

- Environment variables are in the `transcode-app/.env` file.
```
REGION=ap-shanghai  # Application region
TENCENT_SECRET_ID=xxxxxxxxxxxx # Your Tencent Cloud `sercretId`
TENCENT_SECRET_KEY=xxxxxxxxxxxx # Your Tencent Cloud `sercretKey`
```
>?
>- You can log in to the Tencent Cloud console and get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
>- If your account is the root account or a sub-account that has the permission to scan QR codes, you can also directly scan the QR code to deploy the application without configuring `SercretId` and `SercretKey`. For more information, please see [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

#### 3. Configure the parameters needed for transcoding
- CLS log definition is in the `transcode-app/log/serverless.yml` file:
```
	# Component information. For all configuration items, please visit https://github.com/serverless-components/tencent-cls/blob/master/docs/configure.md
	component: cls # Name of the imported component
	name: cls-video # Name of the created instance. Replace it with the name of your instance
   
		 # Component parameters
	inputs:
			 name: cls-log  # You need to configure a name as the name of your CLS logset
			 topic: video-log # You need to configure a topic as the name of your CLS log topic
			 region: ${env:REGION} # Region, which is uniformly defined in environment variables
			 period: 7 # Log retention period in days
```

 - SCF function and transcoding configurations are in the `transcode-app/transcode/serverless.yml` file:

```
		 # Component information. For all configuration items, please visit https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md.
		 component: scf # Name of the imported component
		 name: transcode-video # Name of the created instance. Replace it with the name of your instance


			# Component parameters
			 inputs:
			 name: transcode-video-${app}-${stage}
			 src: ./src
			 handler: index.main_handler 
			 role: transcodeRole # Function execution role which has been granted full access to the corresponding COS bucket
			 runtime: Python3.6 
			 memorySize: 3072 # Memory size in MB
			 timeout: 43200 # Function execution timeout period in seconds. This example indicates that the demo can be run for up to 12 hours
			 region: ${env:REGION} # Function region, which is uniformly defined in environment variables
			 asyncRunEnable: true # Enable prolonged execution
			 cls: # Function log
				 logsetId: ${output:${stage}:${app}:cls-video.logsetId}  # CLS logset. `cls-video` is the instance name of the CLS component
				 topicId: ${output:${stage}:${app}:cls-video.topicId}  # CLS log topic
			 environment: 
				 variables:  # Transcoding parameters
					 REGION: ${env:REGION} # Output bucket region
					 DST_BUCKET: test-123456789 # Output bucket name
					 DST_PATH: video/outputs/ # Output bucket path
					 DST_FORMAT: avi # Transcoding format
					 FFMPEG_CMD: ffmpeg -i {input} -y -f {dst_format} {output}  # Basic transcoding command. You can customize the configuration, but it must include the FFmpeg configuration parameters and formatted part; otherwise, the transcoding task will fail
					 FFMPEG_DEBUG: 1 # Whether to output FFmpeg log. 0: no; 1: yes
					 TZ: Asia/Shanghai # CLS log output time zone
			 events:
				 - cos: # COS trigger    	
					 parameters:          
					   bucket: test-123456789.cos.ap-shanghai.myqcloud.com  # Input bucket
					   filter:
					     prefix: video/inputs/  # Bucket path
					   events: 'cos:ObjectCreated:*'  # Triggering event
	             enable: true
```

>?
>- We recommend you configure the output bucket and the function in the same region, because cross-region configuration will reduce the stability and efficiency of the application and incur traffic fees.
>- The upper limit of memory size is 3,072 MB, and the upper limit of execution time is 43,200s. If you need to adjust them, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) for application.
>- The prolonged execution feature of SCF must be enabled for the transcoding application with `asyncRunEnable: true`.
>- Please create and authorize the execution role according to [Execution Role](#role).
>- The FFmpeg command configured in the example is only applicable to AVI transcoding. For more information, please see [FFmpeg commands](#FFmpeg).

#### 4. Deploy the project
In the `transcode-app` project directory, run `sls deploy` to deploy the project.
```
cd transcode-app && sls deploy
```

#### 5. Upload the video file
Upload the video file to the specified path of the configured COS bucket, and it will be automatically transcoded, which is `/video/inputs/` in the COS bucket `test-123456789.cos.ap-shanghai.myqcloud.com` in this example.

After successful transcoding, the file will be saved in the output bucket path you configured, which is `/video/outputs/` in the COS bucket `test-123456789.cos.ap-shanghai.myqcloud.com` in this example.

#### 6. Redeploy
If you need to adjust the transcoding configuration, you can modify the `transcode/serverless.yml` file and redeploy the function:
```
cd transcode && sls deploy
```




## Monitoring and Logging
Batch uploading files to COS will trigger concurrent transcoding executions.

1. Go to the **Function Service** page in the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click the function name to enter the function management page.
2. Click **Log Query** to view the log monitoring data.
3. Select **Function Management** > **Function configuration** and click the link of the log topic to redirect to the CLS console.
4. On the **Search and Analysis** page in the CLS console, select the logset and log topic to search for and analyze logs.




## FFmpeg Tool
<span id="FFmpeg"></span>

### FFmpeg commands

`DST_FORMAT` and `FFMPEG_CMD` in the `transcode-app/transcode/serverless.yml` file specify the transcoding commands of the transcoding application. You can customize the configuration according to your actual use case.

For example, to transcode videos to MP4 format, you can configure `FFMPEG_CMD` as follows:
```
DST_FORMAT: mp4
FFMPEG_CMD: ffmpeg -i {input} -vcodec copy -y -f {dst_format} -movflags frag_keyframe+empty_moov {output}
```

>?
> - `FFMPEG_CMD` must include the FFmpeg configuration parameters and formatted part; otherwise, the transcoding task will fail.
> - FFmpeg command parameter configuration varies by transcoding scenario; therefore, you should have basic knowledge of FFmpeg. The above commands are only for the described use cases. For more FFmpeg commands, please visit [FFmpeg official website](https://ffmpeg.org/documentation.html).

### Customizing FFmpeg

The default FFmpeg tool is provided in the sample transcoding application. If you want to customize FFmpeg, you can do the following:

1. Replace the FFmpeg in the sample with your customized FFmpeg.
2. Run `sls deploy` in the `transcode-app/transcode` directory again to deploy the update.
```
 cd transcode && sls deploy
```

 >? If your FFmpeg compilation environment is different from the SCF runtime environment, FFmpeg permission issues may occur. We provide an [official image](https://intl.cloud.tencent.com/document/product/583/39009) of the SCF runtime environment, which can be used to compile your FFmpeg.



<span id="role"></span>

## Execution Role

When the transcoding function is running, it needs to read resources in COS for transcoding and write the transcoded resources back to COS; therefore, the function should be configured with an execution role that has read/write permissions of COS. For more information, please see [Role and Authorization](https://intl.cloud.tencent.com/document/product/583/38176).

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) and create a role with **Tencent Cloud Product Service** as the role entity. 
 
2. In the **Enter role entity info** step, select **Serverless Cloud Function (scf)** and click **Next**.

3. In the "Configure role policy" step, select the policies required by the function and click **Next**.

 >?You can directly select `QcloudCOSFullAccess` (full access to COS). If you need more fine-grained permission control, please configure and select according to the actual situation.

4. Enter the role name to complete the role creation and authorization. This role will be used as the execution role of the function and configured in the `transcode-app/transcode/serverless.yml` file.

 >? As the maximum validity period of an execution role key is 12 hours, the timeout period configured for the function should not be greater than 12 hours. If you need a longer function execution time, you can change the COS access method in `transcode-app/transcode/src/index.py` to configure a permanent key for full access to COS. However, this will expose your key in the code and should be used with caution.

