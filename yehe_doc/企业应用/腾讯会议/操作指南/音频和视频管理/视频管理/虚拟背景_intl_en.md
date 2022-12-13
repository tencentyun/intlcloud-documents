

## Overview
Background is an application of the portrait segmentation technology. During a video meeting, VooV Meeting can automatically recognize the attendees and replace their backgrounds with the specified image or video. On one hand, the virtual background can protect the attendees' privacy; on the other hand, it can replace a real exhibition background to facilitate themed promotion of the meeting and reduce the meeting costs. To get a better virtual background experience, we recommend you use this feature in a simple scenario with even lighting. If you have a green screen, you can use the green screen feature to further improve the virtual background effect.

## Prerequisites
- **Logged-in user:** Enterprise Edition user
- **Logged-in device:** Windows, macOS, iOS, or Android
- **Version:** v1.3.0 or later
- **Hardware requirements:**
<table>
<thead>
<tr>
<th>Hardware</th>
<th>Requirements</th>
</tr>
</thead>
<tbody><tr>
<td>Windows/macOS</td>
<td>Models with a CPU that supports AVX2 and has more than two cores (generally, CPUs launched after 2013 meet such requirements).</td>
</tr>
<tr>
<td>iOS</td>
<td>iPhone 6s or later and iPad Pro 1st gen launched in 2015 or later (not on iOS 10.3).</td>
</tr>
<tr>
<td>Android</td>
<td>Models with the following chips:<br>For Snapdragon 600 series, the chip model must be at least 670, such as vivo X23<br>For Snapdragon 700 series, the chip model must be at least 710, such as vivo NEX<br>For Snapdragon 800 series, the chip model must be at least 835, such as Mi MIX 2<br>For Kirin 700 series, the chip model must be at least 710, such as Honor 20i<br>For Kirin 800 series, the chip model must be at least 810, such as Honor 9X<br>For Kirin 900 series, the chip model must be at least 955, such as Huawei P9.</td>
</tr>
</tbody></table>

## Notes
**Requirements for customized image or video:**
- Image: 
	- Format: .jpg, .bmp, .png
	- Resolution: 4096 × 4096
	- Size: within 20 MB
	- Aspect ratio: 0.01–100. We recommend you use 16:9
	- Quantity: 19 images for Android/iOS each and 49 images for macOS/Windows each. The quantity includes the numbers of blurred backgrounds, images in the 	system, and images uploaded by users.
- Video:
	- Format: .mov and .mp4
	- Resolution: 1920 × 1080
	- Size: unlimited

**To have a better virtual background experience, we recommend you use this feature in a simple environment:**
- If the environment has few objects and monotonous background color, we recommend you use green screen.
- A clearer camera is used for the video meeting.
- The lighting in the meeting environment is even.
- Avoid dressing in the same color as the background.

**If video is used as the virtual background, do not block the camera:**
After the camera is blocked, the capture frame rate will become too low and reduce the refresh rate, which will slow down background loading.

## Using Virtual Background
### Windows/macOS
1. Go to the background settings page:
  - Click the **Settings** icon in the top-right corner on the meeting homepage to enter the settings page and click **Background&Beauty**.
  - During the meeting, click **Apps** > **Filters** > **Background&Beauty**.
  - During the meeting, click **Settings** > **Background&Beauty**.
2. You can also select an image or video in the system as the meeting background or select **Blur** and view the background in the preview window.
3. Click **+** to upload an image or video as the meeting background. To delete it, click **X** in the top-right corner of the image or video.
4. If you have installed a physical green screen, select **I Have a Green Screen**, and you can use the color picker to select the background color to be removed in the preview window. If the picked color is not accurate, you can click **Reset** to pick the recommended color.
5. To disable the background, select **None**.

### Android/iOS
1. Go to the background settings page:
 - Tap the profile photo on the homepage to enter the account center page and tap **Settings** > **Background**.
 - During the meeting, tap **More** on the toolbar and tap **Background**.
2. You can select an image as the meeting background or select **Blur** and directly view the effect in the preview window.
3. Tap **+** to upload an image as the meeting background. To delete it, select the image and tap **Delete** in the bottom-left corner of the page.
4. To disable the background, select **None**.
