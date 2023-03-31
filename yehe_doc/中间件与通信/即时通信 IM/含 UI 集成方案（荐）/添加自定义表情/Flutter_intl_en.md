This document describes how to introduce emoji capabilities to Tencent Cloud Chat Flutter TUIKit.

The `TIMUIKitChat` component supports sending and receiving emojis of the following three types:

| Emoji Type                                                   | Sending Mode | Mix-Up with Text | Sending Content                                              | Parsing Mode                                                 | Introduction Method                                          | Embedded in TUIKit                                           |
| ------------------------------------------------------------ | ------------ | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Unicode](https://unicode.org/emoji/charts/full-emoji-list.html) emoji | Text message | Yes              | [Unicode](https://unicode.org/emoji/charts/full-emoji-list.html) | The device automatically parses [Unicode](https://unicode.org/emoji/charts/full-emoji-list.html) characters into emojis. The parsing result of the same [Unicode](https://unicode.org/emoji/charts/full-emoji-list.html) characters may vary with devices. | [Unicode](https://unicode.org/emoji/charts/full-emoji-list.html) List | A set of [default Unicode emoji list](#unicode) is provided. |
| Small image                                                  | Text message | Yes              | Image name                                                   | The image is automatically matched against the local image assets by name. | Images are stored as assets, and are defined in `List`.      | A QQ small emoji gallery is provided, which can be used directly. |
| Large image                                                  | Text message | No               | `baseURL` plus the image file name, which form the path of the emoji image asset | The asset resources are parsed based on the path.            | Images are stored as assets, and are defined in `List`.      | -                                                            |

![](https://qcloudimg.tencent-cloud.cn/raw/023c3c716b481401c8da763e66ba08d1.png)

Take the following steps to manually introduce emoji capabilities to TUIKit.

>? The emoji capabilities have been changed greatly since [TUIKit](https://pub.dev/packages/tencent_cloud_chat_uikit) V1.1.0. After you upgrade TUIKit to the latest version, re-introduce emoji capabilities as instructed in this document.

## Step 1. Customize Emoji Image Resources

>? **This step is optional.**
>You need to perform this step only when you need to use emojis other than the QQ emojis provided by default, for example, to use custom small and large image emojis.
>The QQ emojis are embedded in TUIKit and are provided by default. Therefore, you do not need to import them in this step.

### Importing resource files to a project

Import the resource files of both small and large image emojis to the `assets/custom_face_resource/` directory of the project.

In this directory, create respective folders for the tabs in the emoji panel. Each tab contains emojis of the same type, for example, small image emojis or large image emojis.

Use the value of the `name` field of a tab to name the corresponding folder. The name is invisible to users. You can name the folders as required.

The names of all emoji resource files must be unique.

For more information about how to import emoji images, see [Demo](https://github.com/TencentCloud/chat-demo-flutter/tree/main/assets/custom_face_resource).

![](https://qcloudimg.tencent-cloud.cn/raw/060d5846a3ad0f5078f40eb05686f9ec.png)

### Declare emoji files

Open the `pubspec.yaml` file. In `flutter` => `assets`, declare the emoji resource files that are imported in the previous step.

```yaml
flutter:
  assets:
    - assets/custom_face_resource/
```

### Configuring the image resource list in the code

>? For the sample code, click [here](https://github.com/TencentCloud/chat-demo-flutter/blob/main/lib/utils/constant.dart) and see the `emojiList` section.

In the code that defines the static parameters or configuration, define a `static List<CustomEmojiFaceData>` line to convert the local image resources into a format that TUIKit accepts, for pass-through in the `List` form.

In the `List` section, each item is a `CustomEmojiFaceData` entry. Each `CustomEmojiFaceData` entry constitutes a tab on the emoji panel. The parameters are described as follows:

```dart
CustomEmojiFaceData(
    {
        String name, // The directory name of the folder.
        String icon, // The name of the icon resource file for the tab.
        List<String> list, // The list of the file names of images.
        bool isEmoji // Specifies whether the image is a small image emoji. The default value is `false`, indicating a large image emoji.
    }
);
```

Sample code:

```dart
static final List<CustomEmojiFaceData> emojiList = [
  // A small image emoji is used, which supports mix-up with text and is sent in the form of a text message.
  CustomEmojiFaceData(
      name: '4349',
      icon: "aircraft.png",
      isEmoji: true,
      list: [
        "aircraft.png",
        "alarmClock.png",
        "anger.png",
        // ...
      ]),

  // A large image emoji is used, which does not support mix-up with text and is sent in the form of an emoji message.
  CustomEmojiFaceData(
    name: '4350',
    icon: "menu@2x.png",
    list: [
    "yz00@2x.png",
    // ...
  ]),
]
```

## Step 2. Customize the Emoji Unicode Character String List

>? **This step is optional.**
>You need to perform this step only when you need to use [Unicode](https://unicode.org/emoji/charts/full-emoji-list.html) emojis.

In the code that defines the static parameters or configuration, define a `List<Map<String, Object>>` Unicode list for pass-through.

See [Appendix](#unicode) for the sample list.

You can copy the sample code to introduce the list or modify the code to introduce a customized list.

## Step 3. Save Emoji Resources to the Memory

>?
>For the sample code, click [here](https://github.com/TencentCloud/chat-demo-flutter/blob/main/lib/src/pages/app.dart), and see the `setCustomSticker` section.
>The QQ emojis are embedded in TUIKit and are provided by default. Therefore, you do not need to import them in this step.

After your project starts and before the first `TIMUIKitChat` component is rendered, convert the emoji resource list defined the previous step into TUIKit emoji instances, and place the instances in the global provider so that the instances are saved in the memory.

**This step needs to be performed only once. All resources in the list will then be saved in the memory.** Displaying and rendering emoji resources are high-frequency operations. If the resources are read to the memory each time before being displayed, resource consumption will be high, compromising the performance.

The memory instance of each emoji is generated by using the `CustomSticker` class. If `unicode` is passed in, the emoji is a Unicode emoji. Otherwise, it is an image emoji.

```dart
class CustomSticker {
  int? unicode; // The Unicode int value. If `unicode` is passed in, the emoji is a Unicode emoji. Otherwise, it is an image emoji.
  String name; // The name of the emoji.
  int index; //The sequence number of the emoji.
  bool isEmoji; // Whether the image is a small image emoji. The default value is `false`, indicating a big image emoji.
}
```

The memory instance of each tab is generated by using the `CustomStickerPackage` class.

```dart
class CustomStickerPackage { // A series of emojis are defined as a package and occupy one tab on the emoji panel.
  String name; // The emoji package name, which is the name of the tab folder.
  String? baseUrl; // The emoji package baseUrl. We recommend that you set it to "assets/custom_face_resource/${Emoji package name}"
  List<CustomSticker> stickerList; // The emoji resource list.
  CustomSticker menuItem; // The tab icon on the emoji panel.
  bool isEmoji; // Whether the image is a small image emoji. The default value is `false`, indicating a big image emoji.
}
```

The sample code is provided in accordance with the preceding description.

Emoji item 1 shows how to use a Unicode emoji package, and emoji item 2 shows how to use an image emoji package (including large and small image emojis). You can use some or all the code as needed.

```dart
setCustomSticker() async {
  // Define a large list that accommodates the emoji package tabs.
  List<CustomStickerPackage> customStickerPackageList = [];

  // Emoji item 1: Use a Unicode emoji list, which can be embedded in text.
  // `emojiData` is configured in Step 2.
  final defEmojiList = emojiData.asMap().keys.map((emojiIndex) {
    final emoji = Emoji.fromJson(emojiData[emojiIndex]);
    return CustomSticker(
        index: emojiIndex, name: emoji.name, unicode: emoji.unicode);
  }).toList();
  customStickerPackageList.add(CustomStickerPackage(
      name: "defaultEmoji",
      stickerList: defEmojiList,
      menuItem: defEmojiList[0]));

  // Emoji item 2: Use an image emoji package of your own.
  // Make sure that the value of `customEmojiPackage.name` is the name of the tab folder.
  // `Const.emojiList` is configured in Step 1.
  customStickerPackageList.addAll(Const.emojiList.map((customEmojiPackage) {
    return CustomStickerPackage(
        name: customEmojiPackage.name,
        baseUrl: "assets/custom_face_resource/${customEmojiPackage.name}",
        stickerList: customEmojiPackage.list
            .asMap()
            .keys
            .map((idx) =>
            CustomSticker(index: idx, name: customEmojiPackage.list[idx]))
            .toList(),
        menuItem: CustomSticker(
          index: 0,
          name: customEmojiPackage.icon,
        ));
  }).toList());

  Provider.of<CustomStickerPackageData>(context, listen: false)
      .customStickerPackageList = customStickerPackageList;
}
```

## Step 4. Add Emoji Parsing Capabilities to the TIMUIKitChat Component

>?
>For the sample code in this step, click [here](https://github.com/TencentCloud/chat-demo-flutter/blob/main/lib/src/chat.dart) and see the `renderCustomStickerPanel`, `customStickerPanel`, and `customEmojiList` sections.

Copy the following code to the class that hosts the `TIMUIKitChat` component.

```dart
Widget renderCustomStickerPanel({
  sendTextMessage,
  sendFaceMessage,
  deleteText,
  addCustomEmojiText,
  addText,
  List<CustomEmojiFaceData> defaultCustomEmojiStickerList = const [],
}) {
  final theme = Provider.of<DefaultThemeData>(context).theme;
  final customStickerPackageList =
      Provider.of<CustomStickerPackageData>(context).customStickerPackageList;
  final defaultEmojiList =
      defaultCustomEmojiStickerList.map((customEmojiPackage) {
    return CustomStickerPackage(
        name: customEmojiPackage.name,
        baseUrl: "assets/custom_face_resource/${customEmojiPackage.name}",
        isEmoji: customEmojiPackage.isEmoji,
        isDefaultEmoji: true,
        stickerList: customEmojiPackage.list
            .asMap()
            .keys
            .map((idx) =>
                CustomSticker(index: idx, name: customEmojiPackage.list[idx]))
            .toList(),
        menuItem: CustomSticker(
          index: 0,
          name: customEmojiPackage.icon,
        ));
  }).toList();
  return StickerPanel(
      sendTextMsg: sendTextMessage,
      sendFaceMsg: (index, data) =>
          sendFaceMessage(index + 1, (data.split("/")[3]).split("@")[0]),
      deleteText: deleteText,
      addText: addText,
      addCustomEmojiText: addCustomEmojiText,
      customStickerPackageList: [
        ...defaultEmojiList,
        ...customStickerPackageList
      ],
      backgroundColor: theme.weakBackgroundColor,
      lightPrimaryColor: theme.lightPrimaryColor);
}
```

### Step 4.1. Render small image emojis

>? **This step is optional.**
>- You need to perform this step only when you need to use small image emojis, including custom small image emojis and QQ small emojis that are provided by default.
>- The display form of small image emojis is similar to that of Unicode emojis. We recommend that you use either Unicode emojis or small image emojis. Therefore, if you have chosen Unicode emojis, you can skip this step.

- Perform Step 4.1 (a) to enable custom small image emojis.
- Perform Step 4.1 (b) to enable QQ small emojis that are provided by default.

Perform either Step 4.1 (a) or Step 4.1 (b).

If you want to use both custom small image emojis and QQ small emojis that are provided by default, make sure that the custom small image emojis do not duplicate with the QQ small emojis.

#### Step 4.1 (a). Enable rendering and parsing of  custom small image emojis

In the `build` method that hosts the `TIMUIKitChat` component, define a `List customEmojiList` variable to store the list of small image emojis.

```dart
List customEmojiList =
    Const.emojiList.where((element) => element.isEmoji == true).toList();
```

Pass the list to the `customEmojiStickerList` parameter of the `TIMUIKitChat` component.

```dart
return TIMUIKitChat(
    customEmojiStickerList: customEmojiList,
    // ......
);
```

>? If the class that hosts the `TIMUIKitChat` component is `StatefulWidget`, you can place the `customEmojiList` variable in the State, and execute the `where` command only in the first build for better performance.

#### Step 4.1 (b). Enable the QQ emoji package

Set the `isUseDefaultEmoji` parameter of  `TIMUIKitChatConfig` to `true` for the `TIMUIKitChat`  component. Then, a tab that contains the QQ emojis is automatically generated in the leftmost side of the emoji panel.

```dart
return TIMUIKitChat(
    config: TIMUIKitChatConfig(
        isUseDefaultEmoji: true,
        // ......
    ),
    // ......
);
```

![](https://qcloudimg.tencent-cloud.cn/raw/ed14b886c08cb1c0e8371ba54925bd71.png)

### Step 4.2. Introduce the emoji capabilities to TIMUIKitChat

Pass the code copied in the beginning of Step 4 to the `customStickerPanel` parameter of the `TIMUIKitChat` component.

```dart
return TIMUIKitChat(
    customStickerPanel: renderCustomStickerPanel,
    // ......
);
```

Until now, the emoji capabilities have been introduced to TUIKit. You can test emoji sending and receiving. If you encounter any problems when you introduce the emoji capabilities, [contact us](#contact).

[](id:unicode)

## Appendix: Sample emoji unicode list

This list is merely intended for demo purposes. You can modify the list as needed.

```dart
List<Map<String, Object>> emojiData = [
  {"name": "GRINNING FACE WITH SMILING EYES", "unicode": 128513},
  {"name": "FACE WITH TEARS OF JOY", "unicode": 128514},
  {"name": "SMILING FACE WITH OPEN MOUTH", "unicode": 128515},
  {"name": "SMILING FACE WITH OPEN MOUTH AND SMILING EYES", "unicode": 128516},
  {"name": "SMILING FACE WITH OPEN MOUTH AND COLD SWEAT", "unicode": 128517},
  {
    "name": "SMILING FACE WITH OPEN MOUTH AND TIGHTLY-CLOSED EYES",
    "unicode": 128518
  },
  {"name": "WINKING FACE", "unicode": 128521},
  {"name": "SMILING FACE WITH SMILING EYES", "unicode": 128522},
  {"name": "FACE SAVOURING DELICIOUS FOOD", "unicode": 128523},
  {"name": "RELIEVED FACE", "unicode": 128524},
  {"name": "SMILING FACE WITH HEART-SHAPED EYES", "unicode": 128525},
  {"name": "SMIRKING FACE", "unicode": 128527},
  {"name": "UNAMUSED FACE", "unicode": 128530},
  {"name": "FACE WITH COLD SWEAT", "unicode": 128531},
  {"name": "PENSIVE FACE", "unicode": 128532},
  {"name": "CONFOUNDED FACE", "unicode": 128534},
  {"name": "FACE THROWING A KISS", "unicode": 128536},
  {"name": "KISSING FACE WITH CLOSED EYES", "unicode": 128538},
  {"name": "FACE WITH STUCK-OUT TONGUE AND WINKING EYE", "unicode": 128540},
  {
    "name": "FACE WITH STUCK-OUT TONGUE AND TIGHTLY-CLOSED EYES",
    "unicode": 128541
  },
  {"name": "DISAPPOINTED FACE", "unicode": 128542},
  {"name": "ANGRY FACE", "unicode": 128544},
  {"name": "POUTING FACE", "unicode": 128545},
  {"name": "CRYING FACE", "unicode": 128546},
  {"name": "PERSEVERING FACE", "unicode": 128547},
  {"name": "FACE WITH LOOK OF TRIUMPH", "unicode": 128548},
  {"name": "DISAPPOINTED BUT RELIEVED FACE", "unicode": 128549},
  {"name": "FEARFUL FACE", "unicode": 128552},
  {"name": "WEARY FACE", "unicode": 128553},
  {"name": "SLEEPY FACE", "unicode": 128554},
  {"name": "TIRED FACE", "unicode": 128555},
  {"name": "LOUDLY CRYING FACE", "unicode": 128557},
  {"name": "FACE WITH OPEN MOUTH AND COLD SWEAT", "unicode": 128560},
  {"name": "FACE SCREAMING IN FEAR", "unicode": 128561},
  {"name": "ASTONISHED FACE", "unicode": 128562},
  {"name": "FLUSHED FACE", "unicode": 128563},
  {"name": "DIZZY FACE", "unicode": 128565},
  {"name": "FACE WITH MEDICAL MASK", "unicode": 128567},
  {"name": "GRINNING CAT FACE WITH SMILING EYES", "unicode": 128568},
  {"name": "CAT FACE WITH TEARS OF JOY", "unicode": 128569},
  {"name": "SMILING CAT FACE WITH OPEN MOUTH", "unicode": 128570},
  {"name": "SMILING CAT FACE WITH HEART-SHAPED EYES", "unicode": 128571},
  {"name": "CAT FACE WITH WRY SMILE", "unicode": 128572},
  {"name": "KISSING CAT FACE WITH CLOSED EYES", "unicode": 128573},
  {"name": "POUTING CAT FACE", "unicode": 128574},
  {"name": "CRYING CAT FACE", "unicode": 128575},
  {"name": "WEARY CAT FACE", "unicode": 128576},
  {"name": "FACE WITH NO GOOD GESTURE", "unicode": 128581},
  {"name": "FACE WITH OK GESTURE", "unicode": 128582},
  {"name": "PERSON BOWING DEEPLY", "unicode": 128583},
  {"name": "SEE-NO-EVIL MONKEY", "unicode": 128584},
  {"name": "HEAR-NO-EVIL MONKEY", "unicode": 128585},
  {"name": "SPEAK-NO-EVIL MONKEY", "unicode": 128586},
  {"name": "HAPPY PERSON RAISING ONE HAND", "unicode": 128587},
  {"name": "PERSON RAISING BOTH HANDS IN CELEBRATION", "unicode": 128588},
  {"name": "PERSON FROWNING", "unicode": 128589},
  {"name": "PERSON WITH POUTING FACE", "unicode": 128590},
  {"name": "PERSON WITH FOLDED HANDS", "unicode": 128591},
  {"name": "BLACK SCISSORS", "unicode": 9986},
  {"name": "WHITE HEAVY CHECK MARK", "unicode": 9989},
  {"name": "AIRPLANE", "unicode": 9992},
  {"name": "ENVELOPE", "unicode": 9993},
  {"name": "RAISED FIST", "unicode": 9994},
  {"name": "RAISED HAND", "unicode": 9995},
  {"name": "VICTORY HAND", "unicode": 9996},
  {"name": "PENCIL", "unicode": 9999},
  {"name": "BLACK NIB", "unicode": 10002},
  {"name": "HEAVY CHECK MARK", "unicode": 10004},
  {"name": "HEAVY MULTIPLICATION X", "unicode": 10006},
  {"name": "SPARKLES", "unicode": 10024},
  {"name": "EIGHT SPOKED ASTERISK", "unicode": 10035},
  {"name": "EIGHT POINTED BLACK STAR", "unicode": 10036},
  {"name": "SNOWFLAKE", "unicode": 10052},
  {"name": "SPARKLE", "unicode": 10055},
  {"name": "CROSS MARK", "unicode": 10060},
  {"name": "NEGATIVE SQUARED CROSS MARK", "unicode": 10062},
  {"name": "BLACK QUESTION MARK ORNAMENT", "unicode": 10067},
  {"name": "WHITE QUESTION MARK ORNAMENT", "unicode": 10068},
  {"name": "WHITE EXCLAMATION MARK ORNAMENT", "unicode": 10069},
  {"name": "HEAVY EXCLAMATION MARK SYMBOL", "unicode": 10071},
  {"name": "HEAVY BLACK HEART", "unicode": 10084},
  {"name": "HEAVY PLUS SIGN", "unicode": 10133},
  {"name": "HEAVY MINUS SIGN", "unicode": 10134},
  {"name": "HEAVY DIVISION SIGN", "unicode": 10135},
  {"name": "BLACK RIGHTWARDS ARROW", "unicode": 10145},
  {"name": "CURLY LOOP", "unicode": 10160},
  {"name": "ROCKET", "unicode": 128640},
  {"name": "RAILWAY CAR", "unicode": 128643},
  {"name": "HIGH-SPEED TRAIN", "unicode": 128644},
  {"name": "HIGH-SPEED TRAIN WITH BULLET NOSE", "unicode": 128645},
  {"name": "METRO", "unicode": 128647},
  {"name": "STATION", "unicode": 128649},
  {"name": "BUS", "unicode": 128652},
  {"name": "BUS STOP", "unicode": 128655},
  {"name": "AMBULANCE", "unicode": 128657},
  {"name": "FIRE ENGINE", "unicode": 128658},
  {"name": "POLICE CAR", "unicode": 128659},
  {"name": "TAXI", "unicode": 128661},
  {"name": "AUTOMOBILE", "unicode": 128663},
  {"name": "RECREATIONAL VEHICLE", "unicode": 128665},
  {"name": "DELIVERY TRUCK", "unicode": 128666},
  {"name": "SHIP", "unicode": 128674},
  {"name": "SPEEDBOAT", "unicode": 128676},
  {"name": "HORIZONTAL TRAFFIC LIGHT", "unicode": 128677},
  {"name": "CONSTRUCTION SIGN", "unicode": 128679},
  {"name": "POLICE CARS REVOLVING LIGHT", "unicode": 128680},
  {"name": "TRIANGULAR FLAG ON POST", "unicode": 128681},
  {"name": "DOOR", "unicode": 128682},
  {"name": "NO ENTRY SIGN", "unicode": 128683},
  {"name": "SMOKING SYMBOL", "unicode": 128684},
  {"name": "NO SMOKING SYMBOL", "unicode": 128685},
  {"name": "BICYCLE", "unicode": 128690},
  {"name": "PEDESTRIAN", "unicode": 128694},
  {"name": "MENS SYMBOL", "unicode": 128697},
  {"name": "WOMENS SYMBOL", "unicode": 128698},
  {"name": "RESTROOM", "unicode": 128699},
  {"name": "BABY SYMBOL", "unicode": 128700},
  {"name": "TOILET", "unicode": 128701},
  {"name": "WATER CLOSET", "unicode": 128702},
  {"name": "BATH", "unicode": 128704},
  {"name": "CIRCLED LATIN CAPITAL LETTER M", "unicode": 9410},
  {"name": "NEGATIVE SQUARED LATIN CAPITAL LETTER A", "unicode": 127344},
  {"name": "NEGATIVE SQUARED LATIN CAPITAL LETTER B", "unicode": 127345},
  {"name": "NEGATIVE SQUARED LATIN CAPITAL LETTER O", "unicode": 127358},
  {"name": "NEGATIVE SQUARED LATIN CAPITAL LETTER P", "unicode": 127359},
  {"name": "NEGATIVE SQUARED AB", "unicode": 127374},
  {"name": "SQUARED CL", "unicode": 127377},
  {"name": "SQUARED COOL", "unicode": 127378},
  {"name": "SQUARED FREE", "unicode": 127379},
  {"name": "SQUARED ID", "unicode": 127380},
  {"name": "SQUARED NEW", "unicode": 127381},
];
```

[](id:contact)
