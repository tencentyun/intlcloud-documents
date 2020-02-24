Tencent Cloud Media Processing Service (MPS) is a cloud-based multimedia transcoding and processing service. It can handle vast amounts of multimedia data. MPS performs adaptive transcoding on demand for audio and video files, making them suitable for OTT services or playback on PC and mobile devices. You can easily adjust bitrates and resolutions, add watermarks or perform screen captures with this service.

## Product Architecture
You can upload source video files to a Cloud Object Storage (COS) bucket through the console, SDKs, or APIs. You can set a workflow trigger for MPS to automatically execute video processing and send a notification to Cloud Message Queue (CMQ) at the same time to keep yourself informed of the status of transcoding tasks. The figure below shows the product architecture of MPS: 
![](https://main.qcloudimg.com/raw/97b9e397152a18a921011f7a489c6ce0.png)

