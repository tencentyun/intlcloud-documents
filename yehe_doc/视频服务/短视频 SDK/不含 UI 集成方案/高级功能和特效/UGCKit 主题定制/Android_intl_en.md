`UGCKit` is a set of encapsulated interactive UIs, which is the UGSV demo app's theme by default. With simple modifications, you can customize your own theme and replace the icons, text, and colors.

## Customizing the recording theme
The recording UI contains the right icon toolbar, the bottom toolbar, music panel, beauty filter panel, and sound effect panel.

![Image description](https://main.qcloudimg.com/raw/7aadc42dc6bb53a4113afdf2dc5bc135.png)

1. Declare a `<style>` in `app/res/values/style.xml`, specify its parent theme as `RecordStyle`, and change the theme to the target theme. You can find all available themes in `app/ugckit/res/values.theme_style.xml`.
Below is the sample code for replacing the music and beauty filter icons on the recording UI:
```java
<style name="RecordActivityTheme" parent="RecordStyle">
	<item name="recordMusicIcon">@drawable/ic_music</item>
	<item name="recordBeautyIcon">@drawable/ic_beauty</item>
</style>
```
2. Declare the custom theme in `AndroidManifest.xml`:
```java
<activity
    android:name="com.tencent.qcloud.xiaoshipin.videorecord.TCVideoRecordActivity"
    android:launchMode="singleTop"
    android:screenOrientation="portrait"
    android:theme="@style/RecordActivityTheme"
    android:windowSoftInputMode="adjustNothing" />
```

## Customizing the editing theme
The editing UI contains the editing and clipping UI, animated effect, beauty filter, and special effect panel, and speed, filter, sticker, and bubble subtitles panels.

![Image description](https://main.qcloudimg.com/raw/4f2b40482068a2d749ac0bc15922606a.png)
1. Declare a `<style>` in `app/res/values/style.xml`, specify its parent theme as `EditerStyle`, and change the theme to the target theme. You can find all available themes in `app/ugckit/res/values.theme_style.xml`.
Below is the sample code for replacing the playback and pause icons on the editing UI:
```java
<style name="EditerActivityTheme" parent="EditerStyle">
	<item name="editorPlayIcon">@drawable/ic_play</item>
	<item name="editorPauseIcon">@drawable/ic_pause</item>
</style>
```
2. Declare the custom theme in `AndroidManifest.xml`:
```java
<activity
    android:name=".videoeditor.TCVideoEffectActivity"
    android:screenOrientation="portrait"
    android:theme="@style/EditerActivityTheme" />
```
