This document describes how to customize the UI of `TUICallKit` and provides two schemes for customization: slight UI adjustment and custom UI implementation.

## Scheme 1. Slight UI Adjustment

You can adjust the UI of `TUICallKit` by directly modifying the UI source code in the `Web/` folder in [tencentyun/TUICallKit](https://github.com/tencentyun/TUICallKit).

### Replacing icons

You can directly replace the icons in the `src/icons` folder to customize the color tone and style of all the icons in your application. When you replace an icon, make sure the filename is the same as the original icon. To preview icons, go to `src/assets`.
![img](https://qcloudimg.tencent-cloud.cn/image/document/63512402ae3cee72786afcc919a988ce.png)

### Adjusting the UI layout

You can modify UIs in the `src/components/` folder to modify the audio/video call UI.

```bash
- components/
    - Calling-C2CVideo.vue          One-to-one video call
    - Calling-Group.Vue             Group audio/video call
    - ControlPanel.vue              The control panel
    - ControlPanelItem.vue          Control panel items
    - Dialing.vue                   The call making UI, incoming call UI, and one-to-one audio call UI
    - MicrophoneIcon.vue            The mic icon that can display changes in the volume level
    - TUICallKit.vue                The overall `TUICallKit` component
```

### Modifying the style

The style file is `src/style.css`. You can adjust it to implement your desired UI style.

## Scheme 2. Custom UI Implementation

The entire call feature of `TUICallKit` is implemented based on the UI-less SDK `TUICallEngine`. You can implement your own UIs based entirely on `TUICallEngine`. For more information, see [TUICallEngine](https://www.tencentcloud.com/document/product/647/51016).