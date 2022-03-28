

## Overview
After quick iterations, VooV Meeting currently supports recording video image in multiple layouts.


## Local Recording Layout and Content

### Recording content in different meeting status
- **Pure audio:** attendees only turn on their audio. If no users are speaking, the black background image will be recorded. If a user is speaking, the black background image, speaker name, and speaker audio will be recorded.
- **Video:** when all attendees turn on their video, their video images and audio will be recorded.
- **Video + audio:** when some users turn on their video while others don't, the video images and audio will be recorded for the former, while the black background image, username, and audio will be recorded for the latter.
- **Screen sharing:** if **Record the speaker thumbnail during screen sharing** is not selected in the settings, only the shared screen and audio will be recorded; otherwise, the shared screen, speaker thumbnail, and audio will be recorded.
- **Screen sharing paused:**
 - Sharer: the last frame before the pause and audio will be recorded during the pause.
 - Viewer: the black screen and audio will be recorded during the pause.
 - When an application is being shared, screen sharing will be paused if you drag the application window, and the recording content will be the same as that during screen sharing pause.

### Recording content in different layouts
- In a custom layout, content will be recorded in the grid mode.
- In grid view, the grid image will be recorded.
- In speaker view, the large image of the speaker will be recorded, and image can be switched by speaker spotlight. If the image is locked, only the locked image will be recorded.
- The recording content will be directly switched upon layout, grid, or video attendee switch.
