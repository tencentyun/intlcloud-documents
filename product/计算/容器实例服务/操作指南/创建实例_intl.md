## Procedure

1. Log in to the [Tencent Cloud CIS console](https://console.cloud.tencent.com/cis).

2. Click **New** on the container instance list page.
![][1]

3. Configure the basic information of the instance.

 **Instance Name**: The name of the service to be created, with a length limited to 63 characters. It is composed of lowercase letters, numbers and "-". It starts with a lowercase letter and ends with a lowercase letter or a number.

 **Region**: Select the region where the container is deployed.

 **Network**: Select the private network in which the container resides and the IP address range.

4. Set up the instance container.

 **Name**: The name of the container to be created, with a length limited to 63 characters.

 **Image**: Click **Select Image**. You can select an image under My Images, My Favorites, TencentHub Image, or DockerHub Image.

 **Tag**: The latest tag is selected by default. To use a different image tag, click tag display window to select one.

 **CPU**: Select the CPU capacity required to run the instance. The value is the upper limit of the CPU available to the container. Please proceed with caution.

 **Memory**: Select the memory capacity required to run the instance. The value is the upper limit of the memory available to the container. Please proceed with caution.
![][3]

5. In the advanced settings, you can set the environment variables, startup commands and parameters for the container. This is optional.
![][4]

6. Click **Add Container** to add multiple related containers in an instance.
![][5]

7. Restart policy.

 **Always**: The container instance always restarts regardless of its exit code. It is the default value.

 **OnFailure**: The container instance restarts when it exits with a non-zero status code.

 **Never**: The container instance will not restart automatically after it exits.

8. Click **Next** to complete the creation of the container instance. Before clicking **Finish**, view and confirm the settings of the instance again.
![][6]


[1]:https://main.qcloudimg.com/raw/216083c129e2c23db289e1b617785f0c.png
[2]:https://main.qcloudimg.com/raw/cd20deb83f7d723e584625906fd09746.png
[3]:https://main.qcloudimg.com/raw/818d55f41653bd5629d044b909b4d189.png
[4]:https://main.qcloudimg.com/raw/c435fad17d846e708ae2f1ebf58e64c1.png
[5]:https://main.qcloudimg.com/raw/735714dd5ccdcc7087313b3139d0ef54.png
[6]:https://main.qcloudimg.com/raw/6df3f5a3a76072a7a623805e2755814e.png
