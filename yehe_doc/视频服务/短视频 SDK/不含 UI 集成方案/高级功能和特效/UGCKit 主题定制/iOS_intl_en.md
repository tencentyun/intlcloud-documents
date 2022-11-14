`UGCKit` allows you to freely modify the preset text, colors, and icons.

[](id:write)
## Text
`UGCKit` offers two language packages by default: Simplified Chinese and American English. All their localized strings are stored in the default standard localized string format in `UGCKit/UGCKitResources/Localizable.strings`. You can replace the text to change the default strings or add new languages.

Below is an example of changing the Simplified Chinese animated effect names, which are in `UGCKit/UGCKitResources/zh-Hans.lproj/Localizable.strings`.
```swift
"UGCKit.Edit.VideoEffect.DynamicLightWave" = "动感光波";
"UGCKit.Edit.VideoEffect.DarkFantasy" = "暗黑幻境";
"UGCKit.Edit.VideoEffect.SoulOut" = "灵魂出窍";
"UGCKit.Edit.VideoEffect.ScreenSplit" = "画面分裂";
"UGCKit.Edit.VideoEffect.Shutter" = "百叶窗";
"UGCKit.Edit.VideoEffect.GhostShadow" = "鬼影";
"UGCKit.Edit.VideoEffect.Phantom" = "幻影";
"UGCKit.Edit.VideoEffect.Ghost" = "幽灵";
"UGCKit.Edit.VideoEffect.Lightning" = "闪电";
"UGCKit.Edit.VideoEffect.Mirror" = "镜像";
"UGCKit.Edit.VideoEffect.Illusion" = "幻觉";
```
To change "幻觉" to "幻像", you only need to modify the last line as follows:
```swift
"UGCKit.Edit.VideoEffect.Illusion" = "幻像";
```

[](id:color)
## Color
The methods of getting the colors on all UIs of `UGCKit` are defined in the `UGCKitTheme` class. You can modify the attribute values to change colors. For the specific resource names, see the comments in `UGCKitTheme.h`.
Below is an example of changing the background color of the application UI:
```swift
UGCKitTheme *theme = [[UGCKitTheme alloc] init];
theme.backgroundColor = [UIColor whiteColor]; // Change the background color to white
UGCKitEditViewController *editViewController = [[UKEditViewController alloc] initWithMedia:media config:nil theme:theme]; // Use the custom theme to create a controller
```

[](id:icon)
## Icons
The icons on all UIs of `UGCKit` are in the `UGCKit.xcassets` resource file and can be replaced as needed. The specific icon filenames can be viewed in `UGCKitTheme.h`. An icon's resource name is the same as its attribute/method name, and all icons are defined in `UGCKitTheme.h`. Taking the recording UI as an example, the following names are the icons' attribute names in `UGCKitTheme` as well as the resource names in `UGCKit.xcassets`.
![](https://main.qcloudimg.com/raw/6c44a90aa35af122fdc013c1354a4b9d.jpg)
You can replace icons in `UGCKit` in two ways:
- Directly replace icons in `UGCKitTheme.xcassets`.
- Write code to assign values to objects in `UGCKitTheme` to change icons.

Below is the sample code for changing icons on the recording UI:
```swift
UGCKitTheme *theme = [[UGCKitTheme alloc] init];
theme.nextIcon = [UIImage imageName:@"myConfirmIcon"]; // Set the icon used to complete recording
theme.recordMusicIcon = [UIImage imageName:@"myMusicIcon"]; // Set the icon of the music feature
theme.beautyPanelWhitnessIcon = [UIImage imageNamed:@"beauty_whitness"]; // Set the icon of the brightening filter
UGCKitRecordViewController *viewController = [[UGCKitRecordViewController alloc] initWithConfig:nil theme:theme]; // Use the custom theme to create a controller
```