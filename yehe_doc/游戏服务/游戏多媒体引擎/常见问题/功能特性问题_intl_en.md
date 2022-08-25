
### What features does GME have?

GME supports voice chat, offline voice messaging, speech-to-text conversion, and voice analysis.

### What are the gaming application scenarios of GME?

E-sports, commander games, casual games, Werewolf, etc.

### Which games use GME?
For the specific games, see the Customer Success module on the [Game Multimedia Engine (GME)](https://www.tencentcloud.com/products/gme) page.

### Does GME support countries/regions outside the Chinese mainland?

Yes. Based on self-built 10-Gigabit cloud data centers connected over 20 BGP lines, GME accelerates the domain name based on your business conditions to deliver a stable and fast gaming experience to players. In addition, it supports sites deployed in third-party data centers to cover regions that can be hardly covered by traditional cloud vendors, such as Middle East, South America, and Australia, so as to implement global availability.

### Does the voice chat feature of GME support mobile systems?
Yes.

### Does GME support WeChat Mini Game?
Currently, GME doesn't support WeChat Mini Game and only supports WeChat Mini Program.

### What game engines and platforms does GME support?

The following game engines are supported: Unity, Unreal, and Cocos2d-x. The following platforms are supported: Windows, macOS, iOS, Android, and HTML5.

### Does GME support mini programs?

Yes. GME supports mini programs; however, only pull (listening) from mini programs is supported, while push (speaking) is not.

### Does GME provide a demo for a mini program?

No. GME currently does not have a demo for a mini program.

### Can GME on Android and GME on iOS communicate with each other?

Yes. They can be interconnected by entering the same room with the same `SDKAppId`.

### Does GME support Bluetooth switching on mobile phones?

No. The switching of sound playback is at the OS level. GME supports playback by Bluetooth devices.

### Does a GME room support mic sequence-based karaoke?

GME's HD sound quality can meet the needs of karaoke; however, mic sequence is something that should be implemented at your own product's application layer through a delivery protocol, for example.

### What should I do if another player (such as QQ Player) is required to play back accompaniment on the Windows client?

Call the relevant API as instructed in the document of player accompaniment for Windows. As accompaniment with a third-party player uses an advanced API, you need to [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance and provide the `tmg_adv_win.h` header file.


### How do I enable the minor speech recognition feature of GME?
The minor speech recognition feature is currently made available through an **allowlist**.
- To enable the minor speech recognition feature for a created application, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application.
- If you haven't created an application, you need to log in to the console to [create one](https://console.cloud.tencent.com/gamegme/create) first, and then [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application.



### Can GME's voice messaging and speech-to-text conversion services be used together with voice chat?
Yes. The features in the SDK are compatible with each other.


### Which file formats can be recorded by the karaoke feature of GME?
MP3 and OGG formats are supported.

