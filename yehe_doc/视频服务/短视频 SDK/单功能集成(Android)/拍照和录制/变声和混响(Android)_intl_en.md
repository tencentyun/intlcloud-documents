**Voice changing and reverb for video shooting:**

```
// Set reverb
// TXRecordCommon.VIDOE_REVERB_TYPE_0   Disable reverb
// TXRecordCommon.VIDOE_REVERB_TYPE_1   Karaoke room
// TXRecordCommon.VIDOE_REVERB_TYPE_2   Small room
// TXRecordCommon.VIDOE_REVERB_TYPE_3   Big hall
// TXRecordCommon.VIDOE_REVERB_TYPE_4   Deep
// TXRecordCommon.VIDOE_REVERB_TYPE_5   Resonant
// TXRecordCommon.VIDOE_REVERB_TYPE_6   Metallic
// TXRecordCommon.VIDOE_REVERB_TYPE_7   Husky
mTXCameraRecord.setReverb(TXRecordCommon.VIDOE_REVERB_TYPE_1);

// Set voice changing
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_0   Disable voice changing
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_1   Naughty boy
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_2   Little girl
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_3   Middle-aged man
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_4   Heavy metal
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_6   Non-native speaker
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_7   Furious animal
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_8   Chubby
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_9   Strong electric current
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_10   Robot
// TXRecordCommon.VIDOE_VOICECHANGER_TYPE_11   Ethereal voice
mTXCameraRecord.setVoiceChangerType(TXRecordCommon.VIDOE_VOICECHANGER_TYPE_1);
```

>?Voice changing and reverb take effect only for recorded human voice but not for background music.
