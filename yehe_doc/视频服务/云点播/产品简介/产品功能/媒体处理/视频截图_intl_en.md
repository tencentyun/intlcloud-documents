## Overview

The video screencapturing feature is to take a screenshot of a video at the specified time to generate an image. VOD supports the following screencapturing methods:

| Feature | Description |
| -- | -- |
| Point-in-time screenshot | VOD can capture screenshots of a video at the specified set of time points. |
| Sampled screenshot | VOD can capture a set of screenshots of a video at the specified time interval. |
| Thumbnail screenshot | VOD can capture a screenshot of a video at the specified time point to use it as the video thumbnail. |
| Image sprite | VOD can capture a set of screenshots (subimages) of a video at the specified time interval and splice them together to generate a large image (i.e., an image sprite) and a VTT file for displaying thumbnails on the progress bar. |

## Use Cases

The screencapturing feature can meet your needs in the following scenarios:

| Use Case | Description |
| -- | -- |
| Thumbnail generation | The screenshot taken at the specified time point of a video can be used as the video thumbnail. |
| Highlight collection | Some highlights in the video can be screencaptured to attract more viewers. |
| Manual moderation | To moderate uploaded videos, sampled screenshots can be taken from the videos, and moderators can quickly determine whether the videos are compliant based on the screenshots. |
| Video synopsis | An image sprite is a large image composed of multiple subimages. It shows several images from the video to give viewers a quick overview of the video content. |
| Preview on the progress bar | Together with a VTT file, an image sprite can be used to preview the video content at a time point on the player progress bar. |

## Directions

For detailed directions, see [Screencapturing](https://intl.cloud.tencent.com/document/product/266/33940).
