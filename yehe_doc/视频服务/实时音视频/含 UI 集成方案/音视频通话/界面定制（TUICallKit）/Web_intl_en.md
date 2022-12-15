# TUICallKit UI Customization Guide

This document describes how to customize the UI of `TUICallKit`. We provide two schemes. You can either make minor modifications to the UI source code we provide or implement your own UI.

## Scheme 1: Using our UI source code

You can modify the UI source code to make minor changes to the ready-made UI we provide. The UI source code is in the `Web/` directory of the [TUICallKit project](https://github.com/tencentyun/TUICallKit).

### Replacing icons

You can replace the icons in the `src/icons` folder to customize the color tone and style of the icons in your application. Make sure you do not change the filenames. To preview icons, go to `src/assets`.

<!-- <img style="width:600px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/a8bd4a66f3a8071ea94eb5b270387386.png"/> -->

<img style="width:600px; max-width: inherit;" src="https://user-images.githubusercontent.com/57169560/194735399-64e56ca4-b25b-4eba-8470-92bb55013acc.png"/>

### Changing the layout

You can modify the views in the `src/components/` folder to change the call UI.

```
- components/
    - Calling-C2CVideo.vue          One-to-one video call
    - Calling-Group.Vue             Group audio/video call
    - ControlPanel.vue              The control panel
    - ControlPanelItem.vue          Control panel items
    - Dialing.vue                   The call making UI, incoming call UI, and one-to-one audio call UI
    - MicrophoneIcon.vue            The mic icon that can display changes in the volume level
    - TUICallKit.vue                The overall `TUICallKit` component
```

### Changing the style

The style file is `src/style.css`. You can adjust it to implement your desired UI style.

## Scheme 2: Implementing your own UI

The features of `TUICallKit` are implemented based on the `TUICallEngine` SDK, which does not include UI elements. You can use `TUICallEngine` to implement your own UI. For detailed directions, refer to the documents below:

- [TUICallEngine integration guide](https://www.npmjs.com/package/tuicall-engine-webrtc)
- [TUICallEngine APIs](https://www.tencentcloud.com/document/product/647/51016)