### Overall Architecture
This section describes the design and implementation of the TKE system. Its product architecture is as shown below:
![](https://main.qcloudimg.com/raw/8ecde8fe39d8f4cc65b9622823ab1058.png)

### Architecture
1. TKE is adapted and expanded based on Kubernetes, so it supports native Kubernetes capabilities.
2. Tencent Cloud's Kubernetes plugins are available to help you quickly build Kubernetes clusters in Tencent Cloud.
3. TKE provides cluster management, application management, CI/CD, and other advanced capabilities on the upper layer of Kubernetes.

### Module Description
1. **TKE Console and TencentCloud API**: You can manipulate clusters and services using the console, kubectl, or APIs.
2. **Image service modules:** You can upload and download images through the image service modules provided by Tencent Cloud.
3. **TKE modules**: These are the core modules of TKE, and include clusters and services CRUD operations.

