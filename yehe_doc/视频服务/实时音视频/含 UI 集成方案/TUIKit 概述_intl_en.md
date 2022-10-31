TUIKit is an open-source solution developed by Tencent Cloud’s Audio/Video Team based on its experience serving over 5,000 customers in major audio/video scenarios. It comes with multiple client components for applications such as video call, live streaming, and video room to help you quickly build services for call, customer service, live streaming, audio chat, and education scenarios.

>? All components of TUIKit use two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, IM and the trial edition of the IM SDK (which supports up to 100 DAUs) will be activated automatically. For the billing details of IM, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

## TUIKit Panorama
![](https://qcloudimg.tencent-cloud.cn/raw/22b2ed779af3b76550ae5eefc8704e4c.png)

TUIKit is classified as `TUICompenont` and `TUIWidget` components. It also offers basic backend services which you can choose from.
```java
├── TUIComponent
│   ├── TUICalling     // Call component, which is similar to the call feature of WeChat and can be used in audio/video scenarios such as video call, customer service, and finance review
│   ├── TUIRoom        // Group video room component, which can be used in audio/video scenarios such as education, meeting, and interview and supports features such as muting and freezing
│   ├── TUILiveVoice   // Live audio chat component, which can be used in audio scenarios such as audio chat rooms and music rooms 
│   ├── TUILiveVideo   // Video interactive live streaming component, which has features such as co-anchoring, cross-room communication, and sound effects
│   ├── TUIChatSolon   // Chat salon component, which can be used in audio/video scenarios such as commercial roundtable and forums
│   ├── TUIPusher      // Push component (UI included), which supports push over various protocols, cross-room communication, as well as sound effects and on-screen comments
│   ├── TUIPlayer      // Pull component (UI included), which supports playback over multiple protocols, co-anchoring, as well as on-screen comments and gifts
│   ├── TUIChorus       // Duet component, an innovative component which you can use together with Tencent Cloud’s copyrighted music library to implement more audio/video features.
│   ├── TUIKaroke      // Karaoke component, an innovative component which you can use together with Tencent Cloud’s copyrighted music library to implement more audio/video features.
├── TUWidget
│   ├── TUIBeauty      // Beauty filter widget
│   ├── TUIAudioEffect // Sound effect widget
│   ├── TUIBarrage     // On-screen commenting widget
│   ├── TUIGift        // Gift widget
├── aPass (optional)
│   ├── Room Service   // Provides features such as room list, room user count, and anchor list
```

## Questions & Feedback
It’s normal to run into errors even if you use the exact environment and steps mentioned in our documents to build your project. If you have any needs or feedback, please contact colleenyu@tencent.com.