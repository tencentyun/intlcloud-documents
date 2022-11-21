## TUICallEngine (No UI)

`TUICallEngine` is an audio/video call component that **does not include UI elements**. You can use its APIs to customize your project.

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [createInstance](#createinstance)                            | Creates a `TUICallEngine` instance (singleton mode). |
| [destroyInstance](#destroyinstance)                          | Terminates a `TUICallEngine` instance (singleton mode). |
| [on](#on) | Listens for events.                            |
| [off](#off) | Stops listening for events.                        |
| [login](#login) | Logs in.                            |
| [logout](#logout) | Logs out.                   |
| [setSelfInfo](#setselfinfo) | Sets the alias and profile photo.                  |
| [call](#call) | Makes a one-to-one call.                         |
| [groupCall](#groupcall) | Makes a group call.                        |
| [accept](#accept) | Accepts a call. |
| [reject](#reject) | Rejects a call. |
| [hangup](#hangup) | Ends a call.                            |
| [switchCallingType](#switchcallingtype) | Changes the call type.                      |
| [startRemoteView](#startremoteview) | Starts rendering a remote video.                    |
| [stopRemoteView](#stopremoteview) | Stops rendering a remote video.                    |
| [startLocalView](#startlocalview) | Starts rendering the local video.                    |
| [stopLocalView](#stoplocalview) | Stops rendering the local video.                    |
| [openCamera](#opencamera) | Turns the camera on.                          |
| [closeCamara](#closecamara) | Turns the camera off.                          |
| [openMicrophone](#openmicrophone) | Turns the mic on.                          |
| [closeMicrophone](#closemicrophone) | Turns the mic off.                          |
| [setMicMute(isMute)](#setMicMute)     | Sets whether to mute the mic. |
| [setVideoQuality](#setvideoquality) | Sets the video quality.                        |
| [getDeviceList](#getdevicelist) | Gets the device list.                        |
| [switchDevice](#switchdevice) | Changes to a different camera/mic.              |

## Event Types

`TUICallEvent` is the callback class of `TUICallEngine`. You can use it to listen for events.

| Event                                                        | Description                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [TUICallEvent.ERROR](#error) | An internal error occurred.                                   |
| [TUICallEvent.SDK_READY](#sdk_ready) | The SDK is ready.                      |
| [TUICallEvent.KICKED_OUT](#kicked_out) | The current user was removed from the room due to repeated login.                   |
| [TUICallEvent.USER_ACCEPT](#user_accept) | A user accepted the call.                     |
| [TUICallEvent.USER_ENTER](#user_enter) | A user agreed to join the call.             |
| [TUICallEvent.USER_LEAVE](#user_leave) | A user agreed to leave the call.             |
| [TUICallEvent.REJECT](#reject) | A user rejected the call.                                         |
| [TUICallEvent.NO_RESP](#no_resp) | The invited user did not answer.                                       |
| [TUICallEvent.LINE_BUSY](#line_busy) | The line is busy.                                           |
| [TUICallEvent.CALLING_TIMEOUT](#calling_timeout) | The call timed out (received by an invitee). |
| [TUICallEvent.USER_VIDEO_AVAILABLE](#user_video_available) | A remote user turned on/off their camera.              |
| [TUICallEvent.USER_AUDIO_AVAILABLE](#user_audio_available) | A remote user turned on/off their mic.              |
| [TUICallEvent.USER_VOICE_VOLUME](#user_voice_volume) | A remote user adjusted their call volume.                   |
| [TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE](#group_call_invitee_list_update) | The invitation list for a group call was updated.                           |
| [TUICallEvent.INVITED](#invited) | You were invited to a call.                                       |
| [TUICallEvent.CALLING_CANCEL](#calling_cancel) | The call was canceled (received by an invitee).   |
| [TUICallEvent.CALLING_END](#calling_end) | The call ended.                         |
| [TUICallEvent.DEVICED_UPDATED](#deviced_updated) | The device list was updated.                               |
| [TUICallEvent.CALL_TYPE_CHANGED](#call_type_changed) | The call type changed.                               |
