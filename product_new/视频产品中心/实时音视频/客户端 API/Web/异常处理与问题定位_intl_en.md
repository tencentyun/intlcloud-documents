
In actual product development process, developers not only need to implement business requirements, but also need to implement various troubleshooting and corresponding interactive logics. The workloads of business development and troubleshooting logic implementation can be easily evaluated based on the 80/20 rule (i.e., troubleshooting logic implementation accounts for only 20% of the overall workload but can determine 80% of the effect). Therefore, troubleshooting logics are an important contribution to the user experience and thus of great significance and necessity. It is highly recommended that developers read and understand this document.

## Non-Trust Principle
You shall not completely trust any experience or description summarized by us, as the diversity and complexity of network environments, devices, and operating systems may lead to unsuspected exceptions in every step. Therefore, we provide notifications for captured errors and exceptions throughout the lifecycle of our products. Here, you need to pay attention to the following key exception notifications:

### 1. Detection of WebRTC support by device
> WebRTCAPI.fn.detectRTC (for more information, please see the API)

### 2. Error notification
> onErrorNotify

### 3. Stream status notification
> onStreamNotify


## Exception Categories and Troubleshooting Rules
### 1. Network problems
- How to detect user's network conditions.
- Suggestions from the product aspect.
- In what cases the network connection may fail.
- Blocked ports: what ports are required, how to check whether they are opened, and how to inform user of unstable network connection and solution.

### 2. Client problems
- What data can be showed to user after `WebRTCAPI.fn.detectRTC` completes data check.
	-  H.264 must be supported:
		-  The Chrome version must be above v52.
		-  Windows XP is not supported (as the highest Chrome version on it is v49 only).
		-  Some Chrome browsers on Android phones may be unsupported because they do not support H.264 hardware codec.
	- TBS check failed for Mobile QQ/WeChat: it may be because TBS installation failed. You can guide user to x5debug.qq.com to download and install TBS.
- Exceptions in the connection establishment process.
	- SDP setting failure: check whether the browser environment has full support for WebRTC.
	- ICE connection failure: check whether there is firewall and port blocking in the current network environment.
	- Camera failure: check whether there is a camera in the current environment and whether required permissions are granted.
	- No image from camera: your business page should prominently display a prompt to advise user to check and reinstall drivers. This problem usually occurs on ThinkPad laptops.
- Exceptions during video call.
	- Network problem: first, your business needs to establish a connection again; then, user must be prompted to keep network connection stable after multiple connection retries.


### 3. Exception report
A reliable business not only provides a feedback channel, but also needs to implement monitoring and data report.

We need the following information to help you troubleshoot exceptions:
- `sdkappid`.
- Time point (or a short time period).
- `userId` (username).
- `roomId` (room number).
- Exception description.

The information above will greatly speed up our troubleshooting process.

