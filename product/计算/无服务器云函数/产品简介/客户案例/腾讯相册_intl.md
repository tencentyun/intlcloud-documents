## Customer Profile

The Tencent Photos Mini Program is Tencent's official photos applet in WeChat, which saves original photos and videos for users free of charge, supports posting long video clips to WeChat Moments, and allows users to generate more elegant music-enabled albums or themed albums with one tap.
![](https://main.qcloudimg.com/raw/de1f73155e8fa76a9011c4b7dd02babd.jpg)

## Solution for the Customer

Tencent Photos is connected with Qzone Photos through the Mini Program, enabling features such as uploading, downloading, sharing, liking, commenting, and generating Mini Program QR code in the Mini Program. This document uses the liking and commenting features and the optimization of Mini Program sharing QR code as examples.

### Liking and Commenting Features Based on Mini Program Cloud Development

![](https://main.qcloudimg.com/raw/de72f1c5064fe665866476d2772955dd.png)
The operation logic for the liking and commenting features based on the Mini Program cloud development is as shown in the figure below:
![](https://main.qcloudimg.com/raw/844a889525ca2c1be52f4918a99558a6.png)
In SCF, the following features are implemented:
- Pull and store data such as comments and likes in the Mini Program.
- When an liking or commenting action is performed in the Mini Program, the routing feature of SCF obtains the authentication information of the user from the original photos server.

### Optimization of Mini Program Sharing QR Code

![](https://main.qcloudimg.com/raw/421ece0c70a7ff0285fb135fdf8c9d4e.png)
The SCF handling logic for the optimization of Mini Program sharing QR code is as shown in the figure below:
![](https://main.qcloudimg.com/raw/3bc4e810e89c95dd494bae4505d1b26a.png)
In SCF, the following features are implemented:
- Call WeChat's API for generating Mini Program code
- Store the image or video for which the QR code needs to be generated to the file storage of Tencent Cloud Base (TCB)
- Get the temporary URL of the image and return to the frontend

## Benefits to the Customer

- The newly developed Mini Program backend does not conflict with the original backend service.
- The original backend service architecture is complex and it is difficult to add new features.
- Use of Mini Program TCB can reduce the time required for scheduling and debugging and improve development efficiency.
- Authentication is completed in SCF, making it easy to connect with existing data resources.
