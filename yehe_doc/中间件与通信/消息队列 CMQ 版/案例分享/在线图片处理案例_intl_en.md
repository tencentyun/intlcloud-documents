
An image processing company builds an online image processing service in Tencent Cloud which enables users to upload their images and specify operations to be performed on them, such as cropping, red eye removal, teeth whitening, colorization, contrast adjustment, and thumbnail generation. A user can upload an image, submit a task, wait for the image to be processed, and download the output image. The time taken for processing varies by operation, from several seconds to several minutes, and the user may upload several, dozens of, or hundreds of images at a time. Therefore, the total processing time is subject to the number of uploaded images, image size, and selected operations.

![](https://qcloudimg.tencent-cloud.cn/raw/33c8fe37dcb185226967f988b54e18a6.png)

After TDMQ for CMQ is integrated to implement the above-mentioned needs, user images will be stored in Tencent Cloud storage (such as CBS and COS), and each user operation request will be stored in the request queue as a message. The message content is an image index composed of elements such as the image name, operation type in user request, and image storage location index key.

The image processing service running on CVM gets a message (image index) from the request queue. The image processing server downloads the data from the cloud and edits the image. Then, it sends the processing result to the response queue and stores the output image in cloud storage. After this process is completed, the user has stored all the original and output images in cloud storage and can download them for use at any time.

More details about scalability and high reliability:

- Even if the image processing service is temporarily unavailable due to bugs or other problems, as TDMQ for CMQ is used, the crash will be imperceptible to the user. In this case, on one hand, the user can still upload images, and the web server can still send messages to the request queue where the messages will be retained and can be fetched out only after the image processing service is back online; on the other hand, the image processing service does not need to record the messages being processed before the crash when it is implemented, and such messages can be processed again, as the message (including messages received sequentially and concurrently in the queue) receipt feature of TDMQ for CMQ ensures that messages can remain in the queue after being received until they are explicitly deleted by the recipient. This feature ensures decoupling of the image processing service and the image upload service.

- If a single image processing service cannot meet user needs (i.e., users can upload images but cannot get the processing results after waiting for a long time), you can use TDMQ for CMQ to start multiple image processing services to satisfy ever-increasing user access needs based on its following two characteristics:
	- A single TDMQ for CMQ queue can be accessed by multiple servers simultaneously (i.e., message sending, receipt, and deletion can be concurrent).
	- A message will not be received by multiple services, which is implemented by the temporary message lock. The message recipient can specify the time during which the message is locked and needs to proactively delete the message after processing it. If the recipient fails to process the message, another service can get the message again after the lock expires.

These two characteristics ensure that the number of processing servers can be dynamically adjusted according to the load.
