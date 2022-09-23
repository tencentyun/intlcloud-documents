## Scenario


Image lifecycle management supports global configuration and independent configuration for a specified image registry. If global image lifecycle management is enabled, the configured global rules are applied to all images of the root account. You can also configure an image tag automatic clearing policy for a specified image registry, and this policy has higher priority than the global configuration.

This document describes how to implement image lifecycle management in the TKE console.



## Notes
- For an image registry, the image tag automatic clearing policy configured specifically for this image registry has **higher priority than** a global image lifecycle management policy.
- After a global image lifecycle management policy is enabled, image tags are automatically cleared only after the number of image tags of the root account reaches the default quota.


## Directions

### Configuring global image lifecycle management

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and choose **Image Registry** > **My Images** in the left sidebar.
2. On the **My Images** page, click **Image Lifecycle Management**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/ca40ee68178937bbf657877187bde194.png)
3. In the **Image Lifecycle Management** window that appears, configure the related parameters, as shown in the following figure.   
![](https://main.qcloudimg.com/raw/1ea7421903cb114ae0767004dedd433c.png)
    - **Enable Status**: select **Enable image lifecycle management**.
    - **Global Rule**:
       - **Reserve the latest XX image tags**: enter a number based on your actual needs. The number cannot exceed the default quota of image tags under the current root account.
       - **Reserve image tags in the last XX days**: enter a number based on your actual needs.
4. Click **OK**.

### Configuring an image tag automatic clearing policy for a specified image registry

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and choose **Image Registry** > **My Images** in the left sidebar.
2. In the **My Images** list, click the name of the target image to go to the details page of this image.
3. Click **set an automatic clearing policy** in the prompt above the image tag list, as shown in the following figure.
![](https://main.qcloudimg.com/raw/83da83482e8edd1b037d0128b92d9772.png)
4. In the **Setting Automatic Clearing Policy** window that appears, configure the related parameters, as shown in the following figure.
![](https://main.qcloudimg.com/raw/5e98ec835bbc4f69869ee40efb3719a7.png)
   - **Reserve the latest XX image tags**: enter a number based on your actual needs. The number cannot exceed the default quota of image tags under the current root account.
   - **Reserve image tags in the last XX days**: enter a number based on your actual needs.
5. Click **OK**.
