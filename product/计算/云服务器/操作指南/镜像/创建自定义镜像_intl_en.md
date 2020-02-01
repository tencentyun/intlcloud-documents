## Scenario
You can launch an instance with a public image or a service marketplace image, and then connect to the instance and deploy your software environment. If the instance runs normally, you can create a new custom image based on this instance as needed, so that you can use this image to launch more new instances that have the same custom configurations with the original one.

>- Shut down the instance before you can create a custom image to ensure that the image has exactly the same deployment environment as that of the current instance.
>- To keep the data in the original instance data disk when you lunch a new instance, you can first take a Snapshot of the data disk, and then create a new CBS data disk with this snapshot when launching the new instance.

## Notes
- Each region supports a maximum of 10 custom images.
- The following directory and files will be removed.
 > /var/log/  
 > /root/.bash_history, /home/ubuntu/.bash_history (Ubuntu system)
- When create image for Linux instance, make sure that /etc/fstab does not include data disk configuration. Otherwise, launching the instance created by the image might fail.

## Directions
### Create an image from an instance via the console

 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. Shut down the instance. Select the instance to be shut down, and then click **More** > **Instance Status** > **Shutdown**.
 3. Click **More** on the right side of the instance used to create an image, and click **Create Image**.
 4. Enter **Image Name** and **Image Description** in the pop-up box, and click **Create Image** to submit the creation application.
 5. To purchase a server with the same image as the previous one, click **Create Instance** on the right side of the image in the image list.

### Create an image using API
You can use the API [CreateImage](https://intl.cloud.tencent.com/document/api/213/33276) to create a custom image.
