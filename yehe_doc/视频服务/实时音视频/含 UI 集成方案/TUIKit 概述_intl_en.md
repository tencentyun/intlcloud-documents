`TUIKit` is an open-source solution developed by the Tencent Cloud audio/video team based on its experience in serving over 5,000 customers in major audio/video scenarios. It contains multiple client audio/video components for video call, live streaming, video room, etc. to help you quickly set up solutions for call, customer service, live streaming, audio chat, and education scenarios.

## `TUIKit` Panorama
![](https://qcloudimg.tencent-cloud.cn/raw/86cf5a688af5cee4d0b5f3a223348bde.png)

As shown above, TUIKit can be divided into `TUICompenont` and `TUIWidget` categories and supports optional basic backend services.
```java
├── TUIComponent
│   ├── TUICalling     // Call component, which is similar to the call feature of WeChat and can be used in audio/video scenarios such as video call, customer service, and finance review
│   ├── TUIRoom        // Group video room component, which can be used in audio/video scenarios such as education, meeting, and interview and supports features such as muting and freezing
│   ├── TUILiveVoice   // Audio chat live streaming component, which can be used in audio scenarios such as audio chat rooms and music rooms 
│   ├── TUILiveVideo   // Video interactive live streaming component, which has features such as co-anchoring, anchor competition, and sound effects
│   ├── TUIChatSolon   // Chat salon component, which can be used in audio/video scenarios such as commercial roundtable and forums
│   ├── TUIPusher      // Push component with complete UIs, which supports features such as push over various protocols and anchor competition as well as widgets such as sound effect and on-screen commenting
│   ├── TUIPusher      // Playback component with complete UIs, which supports features such as playback over various protocols and co-anchoring as well as widgets such as gift and on-screen commenting
│   ├── TUIPlayer      // Innovative audio/video component for new features such as online karaoke, which can be used with Tencent Cloud's copyrighted music library to support more features
│   ├── TUIChous       // Innovative audio/video component for chorus, which can be used with Tencent Cloud's copyrighted music library for more features
│   ├── TUIKaroke      // Innovative audio/video component for new features such as online karaoke, which can be used with Tencent Cloud's copyrighted music library for more features
├── TUWidget
│   ├── TUIBeauty      // Beauty filter widget
│   ├── TUIAudioEffect // Sound effect widget
│   ├── TUIBarrage     // On-screen commenting widget
│   ├── TUIGift        // Gift widget
├── aPass (optional)
│   ├── Room Service   // It provides features such as room list, room popularity, and anchor list
```

## Technical Exchange and Feedback
Even when using the same environment and process, it is still normal that different developers may encounter different kinds of errors. If you have any requirements or feedback, contact colleenyu@tencent.com.