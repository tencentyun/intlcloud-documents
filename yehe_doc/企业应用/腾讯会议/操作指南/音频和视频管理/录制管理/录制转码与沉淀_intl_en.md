
## Overview
Local recording of VooV Meeting supports the MP4 format, and recording files can be saved to a specified folder. After a meeting is recorded, you can directly find the recording in **Past Meetings**, play it back, open its folder, or delete it.

## Prerequisites
- **Logged-in user:** Free or Enterprise Edition user
- **Logged-in device:** Windows or macOS
- **Version:** v2.3.0 or later

## Notes
- During recording, you cannot change the recording file storage path.
- If you **delete** a recording in **Past Meetings**, the original local recording file will **also be deleted**.
- Recording file format:
  - Recorded video file: .mp4
  - Temporary recording file: .wemta, .wemta.idx, .wemtv, and .wemtv.idx
  - Recorded audio file: .m4a
- Resolution and frame rate of recorded video:
  - If **Record the speaker thumbnail during screen sharing** is not enabled in the settings, the resolution will be 1920 x 1080.
  - If **Record the speaker thumbnail during screen sharing** is selected, the resolution will be (1920 + 240) x 1080. Here, the big image resolution is 1920 x 1080, and the thumbnail resolution is 240 x 1080.


## Recording File Conversion and Retention
- After a meeting ends, the system will automatically convert the recording file and then open its folder, so that you can quickly view the recording.
- If recording is interrupted due to an exception, you can find the recording of the meeting in **Past Meetings** and click **Convert** to convert the temporary recording file (.wemta, .wemta.idx, .wemtv, or .wemtv.idx) into a video recording file (.mp4).
- After a meeting is recorded, you can directly find the recording in **Past Meetings**, play it back, open its folder, or delete it.

## Recording Settings
In the Settings page on the meeting homepage, you can specify the following configurations in **Recording**:
- Save the recording file to (the folder can be directly opened): specify the folder for saving recording files.
- Record the speaker thumbnail during screen sharing: after this is selected, if local recording is started during screen sharing, the image of the shared screen and the speaker image will be recorded together.
- Record audio files at the same time: after this is selected, the recorded audio will be output as a separate audio file and saved in the folder.
- Save temporary recording files: after this is selected, recording files before conversion will also be saved.
