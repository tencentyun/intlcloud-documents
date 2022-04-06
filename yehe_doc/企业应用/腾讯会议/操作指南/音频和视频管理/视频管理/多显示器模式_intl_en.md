## Overview
If your device is connected to multiple monitors, you can enable the **multi-monitor mode** to display VooV Meeting on the extended monitors for a better meeting experience.
## Prerequisites
- **Logged-in user:** Free or Enterprise Edition user
- **Logged-in device:** Windows
- **Version:** v2.2.0 or later

## Notes
VooV Meeting can be displayed on an extended monitor if the following requirements are met:
- Two or more monitors are set for the PC.
- The extended monitors are selected in **Settings** > **System** > **Display** > **Multiple displays** on Windows.
- On the VooV Meeting homepage, go to **Settings** > **General** and enable **Multi-Monitor Mode**.
- If extended monitors are disconnected, the multi-monitor mode will be automatically disabled.

## Extended Display Mode
The secondary window does not have the toolbar and therefore has no meeting control features. It varies a lot in two screen sharing scenarios as detailed:
- **If screen sharing is enabled:**
 - You can switch to speaker view/full screen in the secondary window, and speaker spotlight is supported.
 - If the secondary window is on the monitor of the screen for sharing, after desktop/window sharing starts, the secondary window will be moved to monitor 1. If monitor 1 is shared, the window will be moved to monitor 2 by default (this rule also applies if two or more monitors are connected).
	 - Suppose the secondary window is on monitor 1: if you select monitor 1 or a window on monitor 1 for sharing, the secondary window will be automatically moved to monitor 2. After sharing ends, the secondary window will be automatically restored to the original monitor no matter whether it is moved during sharing.
	 - Suppose the secondary window is on monitor 1: if you select monitor 2 or a window on monitor 2 for sharing, the position of the secondary window will not change. After sharing ends, the secondary window will be automatically restored to the original monitor no matter whether it is moved during sharing.
	 - Suppose over two monitors are connected and the secondary window is not on monitor 1: if you select the monitor where the secondary window is for sharing, the secondary window will be automatically moved to monitor 1 to adapt to the multi-monitor mode.
 - Suppose the whiteboard is being shared: the monitor displayed on the whiteboard will be the one where the screen sharing selection pop-up window is.
 - If the whiteboard and the secondary window are on the same monitor:
    - If two monitors are connected, the secondary window will be automatically moved to the other monitor.
    - If over two monitors are connected: if the whiteboard is on monitor 1, the secondary window will be moved to monitor 2, otherwise, the secondary window will be moved to monitor 1.
- **If screen sharing is not enabled:**
 - Only you yourself are in the meeting: your video image/profile photo will be displayed in the secondary window.
 - The meeting has two people: your video image/profile photo will be displayed in the secondary window, and the video image/profile photo of the other people will be displayed in the main window (speaker spotlight does not take effect). If the other people starts screen sharing, the secondary window will enter the speaker mode by default, and the layout can be switched.
 - The meeting has over two people: the secondary window will display only the video image/profile photo of the single speaker. If the attendees start screen sharing, the secondary window will enter the speaker mode by default, and the layout can be switched.
 - You cannot switch to speaker view/full screen in the secondary window.
 - If an attendee is watching the shared screen, the screen sharing content will be displayed in the secondary window by default. 

## Using Extended Monitor for Display

1. Make sure that your device has been connected to multiple monitors successfully.
2. Select the extended monitors in **Settings** > **System** > **Display** > **Multiple displays** on Windows.
3. On the VooV Meeting homepage, go to **Settings** > **General** and select **Multi-Monitor Mode**, and the settings will take effect immediately and saved under the current account locally.
4. After configuring the above settings, you can view the corresponding video image in the secondary window.

## Locking Video Image
### Prerequisites for locking
- The multi-monitor mode is enabled.
- The meeting has at least 2 people.
- If an attendee enables the camera during the meeting, the attendee will be locked on the screen.

### Notes
- If an attendee (including yourself) enables screen sharing during the meeting, the locking feature will be unavailable.
- An attendee can be locked on multiple screens, but multiple attendees cannot be locked on the same screen.

### Locking operation
**In grid view**
1. In grid view, click **...** in the top-right corner or right-click the image, and options **Lock video to screen 1** and **Lock video to screen 2** will be displayed.
2. Click the target option to lock the video image on the corresponding screen.
3. Right click the image in the grid view again or click **...** and select **Unlock video from screen N** to unlock.

**In speaker view**
1. In speaker view, click **...** in the top-right corner of a thumbnail or right-click the image, and options **Lock video to screen 1** and **Lock video to screen 2** will be displayed.
2. Click the target option to lock the video image on the corresponding screen.
3. Right click the image in the speaker view again or click **...** and select **Unlock video from screen N** to unlock.
