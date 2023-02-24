## Overview

Custom risk libraries help you manage moderated files in a targeted manner. They allow you to set whether to block or pass files in advance and are suitable for all moderation scenes.

Custom risk libraries are divided into sensitive libraries (non-compliant file libraries) and normal libraries (normal file libraries). When a custom risk library is enabled, moderated files that hit samples in the library will be tagged with the corresponding library tag. The tag of sensitive libraries is **Regulation-violating (Block)**, and that of normal libraries is **Normal (Pass)**.

>?
> - Currently, only preset image risk libraries are available, including normal image libraries and sensitive image libraries for five types of non-compliant scenes.
> - An image library can have up to 10,000 images.
> - Some specific images may fail to be added to the image library. In this case, contact [online customer service](https://intl.cloud.tencent.com/contact-sales) for assistance.
> 

## Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci). On the **Bucket Management** page, select the target bucket to enter the bucket management page.
2. On the left sidebar, select **Sensitive Content Moderation** > **Custom Risk Library**.
3. On the **Preset Image Library** tab, you can see six preset image libraries. Click **Manage** on the right of a library to enter the library management page.
4. On the custom image library management page, you can perform the following operations:

 - View the image library policy: View whether the risky image library policy is "pass" or "block".
 - View the number of samples: View how many samples have been added to the risky image library.
 - Add samples: Add specified images as samples to the risky image library.
 - Remove samples: Remove sample images from the risky image library.
5. After you configure a risk library, if files in the risk library are hit when you use the COS content moderation feature, the system will automatically pass or block the files according to the risk policy.
