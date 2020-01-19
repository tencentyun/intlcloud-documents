## Operation Scenarios

With the web player management feature, you can easily customize the style of the video player provided by Tencent Cloud and then embed the player code in your webpage to display the custom style.

## Directions

1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview), and click **Delivery and Playback Settings** > **Web Player Management** on the left sidebar to enter the "Web Player Management" page.
>This page displays a list of players. You can create and maintain up to 10 custom players.
2. Click **Create Player** in the top-left corner to pop up the "Create Player" dialog box, and set the following options as prompted:
![](https://main.qcloudimg.com/raw/19df12286ce87efb2d01b3c33f86299b.png)
	- Basic Settings: you can configure the player name, description, and default definition.
		- Player Name: you can enter letters, digits, and underscores, with a length of up to 20 chars.
		- Description: up to 50 characters.
		- Default Definition: valid values include LD, SD, HD, and FHD. Default value: LD.
	- Appearance: you can upload your own logo image, customize its position in the player, and set the redirection link upon click.
		- Logo Image: GIF, JPG, PNG, and BMP formats are supported. Dimensions: ≤ 200 * 200p. Size: ≤ 1MB.
		- Redirection Link: this is the URL to redirect to upon clicking the logo image. You need to enter a valid URL and add the HTTP(S) protocol.
		- Logo Position: bottom left, top left, bottom right, or top right.
	- Roll Image: you can customize the pre-, mid-, and post-roll images for the video in the player, and redirection is supported for the images. GIF, JPG, PNG, and BMP formats are supported (for GIF files, only the first frame will be used). Video roll files of less than 1 MB will be supported in the future.
3. After creating the player, you can preview, modify, copy, or delete it or set it as the default player:
	- Preview: open the preview video file and see the effects of the selected player.
	- Modify: modify player settings in the "Modify Player" dialog box.
	- Copy: copy the selected player for further editing.
	- Set as Default Player: set the selected player as the default player.
	- Delete: delete the selected player.
	
>
>- In the player list, only one player can be set as the default player.
>- If the selected player is associated with a video file, it cannot be deleted, and you need to unassociate it first in [Media Assets](https://console.cloud.tencent.com/vod/media) first. For directions, please see [Directions for Generating Web Player Code](https://cloud.tencent.com/document/product/266/36452#web-.E6.92.AD.E6.94.BE.E5.99.A8.E4.BB.A3.E7.A0.81.E7.94.9F.E6.88.90.E6.AD.A5.E9.AA.A4).










