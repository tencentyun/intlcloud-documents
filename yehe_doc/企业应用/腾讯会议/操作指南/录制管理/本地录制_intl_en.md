## Overview
Local recording helps you record meetings quickly and conveniently. It can save the meeting video and shared content in your local folder.

## Prerequisites
- **Logged-in user:** Free or Enterprise edition user
- **Logged-in device:** Windows or macOS
- **Version:** v2.3.0 or later

## Notes
### Notes on recording process
- During recording, you cannot change the recording file storage path.
- If a meeting ends during recording or you are kicked out, recording will stop and the recording file will be converted automatically.
- The host and co-hosts are mutually exclusive in local and cloud recording, who share the same start/pause/resume/end operations.

### Notes on recording permission
- Currently, the VooV Meeting app does not support local recording but can control the recording permission.
- In the permission status of **Allow selected attendees to record**, **Allow Recording/Forbid Recording** are displayed in **Attendees** > **More**.
- If the permission status is changed from **Allow all attendees to record** to **Allow selected attendees to record**, all attendees can still keep their recording permission, the **Attendees** > **More** > **Forbid Recording** option will be displayed for the host to disable recording for a specified attendee, and new attendees after the change cannot record the meeting.
- When the recording permission status is **Allow selected attendees to record**, if you revoke the co-host role from an attendee, the **Allow Recording** permission will be kept by default. When the recording permission status is changed from **Allow selected attendees to record** to **Only the host can record**, the attendees allowed to record will become unable to record.
- Before using the recording feature, you can click **Record** to check whether you have the recording permission, and if not, apply to the host for it promptly.

### Notes on recording file
- If a meeting has multiple recording segments, multiple recording files will be generated in chronological order. After recording is resumed, the recording content before pause will be merged with the content after resumption into one recording file.
- If recording is interrupted due to any exception, you can find the recording file in **Past Meetings** and convert it to watch the content before interruption.


## Enabling Local Recording
### Windows/macOS
1. Click **Recording** and select **Local Recording** during a meeting.
 - If you are muted, you can select **Unmute** or **Record without audio** when enabling recording.
 - If you are not muted, recording will be enabled normally.
2. After recording is enabled:
 - **Record** at the bottom will become **End*.
 - The recording status will be displayed in the top-left corner of the main window, and the **Pause Recording** and **End Recording** buttons will be displayed.
 - **Pause Recording** and **End Recording** options will be added to the menu expanded after you click the arrow button on the right of **End** on the bottom bar.
 - Pause Recording: you can click this button to pause the current recording, and it will become **Resume Recording**.
 - Resume Recording: you can click it to resume recording.
 - End Recording: you can click it to end and exit recording, and **After the meeting ends, the recording file will be automatically converted to MP4 format.** will be prompted.
 - The recording status will be displayed in the attendee list.
3. After a meeting ends, the system will automatically convert the recording file and then open its folder, so that you can quickly view the recording file.

## Local Recording Permissions (only for Host/Co-hosts)

### Windows/macOS
During a meeting, click the arrow icon on the right of **Recording** at the bottom, and three recording permissions will be displayed: **Only the host can record**, **Allow all attendees to record**, and **Allow selected attendees to record**.
- Only the host can record: it is the default option. If it is selected, only the host/co-hosts can enable recording.
- Allow all attendees to record: all attendees can enable recording.
- Allow selected attendees to record: after it is enabled, the host/co-hosts can enable recording and allow specified attendees to enable recording in **Attendees**.
 - **Forbid Recording**: when **Allow selected attendees to record** is selected, the cost/co-hosts can select an attendee allowed to enable recording in **Attendees** and click **Forbid Recording** to revoke the recording permission.

### Android/iOS
During a meeting, tap **More** > **Settings**, and find Recording Settings, three recording permissions will be displayed: **Only the host can record**, **Allow all attendees to record**, and **Allow selected attendees to record**.
- Only the host can record: it is the default option. If it is selected, only the host/co-hosts can enable recording.
- Allow all attendees to record: all attendees can enable recording.
- Allow selected attendees to record: after it is enabled, the host/co-hosts can enable recording and allow specified attendees to enable recording in **Attendees**.
 - **Forbid Recording**: when **Allow selected attendees to record** is selected, the cost/co-hosts can select an attendee allowed to enable recording in **Attendees** and click **Forbid Recording** to revoke the recording permission.

