 The image editing feature is added starting from SDK 4.9. You can select a desired image to add effects such as transition animation, background music, and stickers.  
The API functions are as follows:

```
/*
 * bitmapList: list of transition images, which must contain at least three images (note: we recommend you compress the images to 720p or lower (as shown in the demo); otherwise, the memory usage may be too high, causing editing exceptions).
 * fps: frame rate of the video generated from the transition images in fps. Value range: 15–30.
 * Returned values:
 *       0: set successfully
 *      -1: failed to set. Please check whether the image list exists
 */
public int setPictureList(List<Bitmap> bitmapList, int fps);

/*
 * type: transition type. For more information, please see `TXVideoEditConstants`
 * Returned values:
 *       duration: transition video duration (note: the duration for the same image list may vary by transition animation. You can get the transition image duration here)
 */
public long setPictureTransition(int type)
```
- Here, the `setPictureList` API is used to set the image list, which must contain at least three images. If too many images are set, the image size should be appropriate to avoid editing exceptions due to high memory usage.
- The `setPictureTransition` API is used to set the transition effect. Currently, six effects are available, and their durations may vary. You can get the transition duration through the returned value here.
- Pay attention to the API call sequence: call `setPictureList` first and then call `setPictureTransition`.
- Image editing currently does not support loop, reverse, and fast/slow motions, but supports other video editing features. The call method is the same as that of video editing.
 
