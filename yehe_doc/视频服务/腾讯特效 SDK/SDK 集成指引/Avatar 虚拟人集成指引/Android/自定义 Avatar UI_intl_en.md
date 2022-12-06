## Demo UI
<img src="https://qcloudimg.tencent-cloud.cn/raw/1b25592a83e2e7f38ded001ca8c0b93b.png" style="zoom: 67%;" />

## Implementation
The panel configuration data can be stored anywhere. In the demo, it is in `assets`. When the panel file is used for the first time, it will be copied to the installation directory.
![](https://qcloudimg.tencent-cloud.cn/raw/b178070d012fca8cbbf275c0b1e84f44.png)

**Mappings between the JSON structures and panel elements**:

- The items in the JSON file on the left correspond to the top-level menu on the right. `head` corresponds to the first item of the menu.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6547824e221494545e5353e8dce5e1cc.png" style="zoom:67%;" />
- `subTabs` on the left corresponds to the second-level menu:
<img src="https://qcloudimg.tencent-cloud.cn/raw/0cb8236d813fc9ec278b7026063a7b88.png" style="zoom:67%;" />
- The icons on the left are configured in the `resources` folder. The file on the right is the panel data. You can **associate them using the `category` field**. The SDK parses data in the `resources` folder and outputs the parsed data in a map. The key in the map corresponds to the value of `category`. After the `panel.json` file is parsed, you can use an API of the SDK to get the data and associate it.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2ad79a0d0efcb34cc5c1816975badfd8.png" style="zoom:67%;" />

## Key Classes of the Demo
Path: `com.tencent.demo.avater.AvatarResManager.java`

### 1. Load the avatar resources
```java
/**
     * Used to load the avatar resources
     *
     * @param xmagicApi: The `XmagicApi` object.
     * @param avatarResName: The name.
     * @param avatarSaveData: The default configuration of the loading model. If there isn’t a default configuration, pass null.
     */
    public void loadAvatarRes(XmagicApi xmagicApi, String avatarResName, String avatarSaveData)
```

### 2. Get the panel data
```java
 /**
     * Get the avatar panel data
     *
     * @param avatarResName: The avatar material name.
     * @param avatarDataCallBack: This API accesses files. The operation is performed in a child thread, and the data obtained is returned in a callback in the main thread.
     *                           The returned data already contains the data in the `resources` directory.
     */
    public void getAvatarData(String avatarResName, String avatarSaveData, LoadAvatarDataCallBack avatarDataCallBack)
```

### 3 Get the user’s settings or default settings from the panel data
```java
// Get the user’s settings or the default settings from the panel file
public static List<AvatarData> getUsedAvatarData(List<MainTab> mainTabList) 
```

### 4. Get the background data of the model
```java
 /**
     * Get the `plane Config` data.
     *
     * @param avatarResName: The resource name.
     * @param avatarType: The background type.
     * @return
     */
    public AvatarData getAvatarPlaneTypeConfig(String avatarResName, AvatarBgType avatarBgType) 
```

## Appendix

This section provides descriptions of fields in [MainTab.java](#maintab) and [SubTab.java](#subtab).

### MainTab

| Field | Type | Required | Description  |
| ----------- | ----------- | ----------- | ----------- |
| id   | String | Yes | The globally unique identifier of a main menu option. |
| label| String| No | The name of a main menu option (this is not displayed in the demo).        |
| iconUrl        | String| Yes | The URL of the icon when not selected. |
| checkedIconUrl | String| Yes | The URL of the icon when selected. |
| subTabs | A list of [SubTab](#subtab) | Yes       | The options of the second-level menu. |

### SubTab

| Field | Type | Required | Description  |
| --------------- | -------- | -------- | ----------- |
| label | String   | Yes       | The name of a second-level menu option. |
| category        | String   | Yes       | The category of a second-level menu option, which is defined in the `com.tencent.xmagic.avatar.AvatarCategory` class of the SDK. |
| relatedCategory | String   | No       | The related category. For example, hair color is a related category of the hairstyle category. When the user changes the hairstyle, you need to set this field of the hairstyle option to the currently used hair color (the value of `category` of the hair color option). Currently, this field is only applicable when `type` is `TYPE_SELECTOR`. |
| avatarDataList  | List | Yes | A list of [AvatarIcon].                                       |

### AvatarIcon

| Field | Type | Required | Description  |
| ----------- | ----------- | ----------- | ----------- |
|id| String| Yes |The property ID, which corresponds to the ID in `AvatarData` returned by the SDK. |
| icon | String| Yes       | The URL of the icon or the color in ARGB format (“#FF0085CF”).     |
| type | Int   | Yes       | The display type. Valid values: `AvatarData.TYPE_SLIDER` (Slider), `AvatarData.TYPE_SELECTOR` (Icon). |
| selected    | boolean             | Yes       | If `type` is `AvatarData.TYPE_SELECTOR`, this field indicates whether the item is selected. |
| downloadUrl | String | No | The dynamic download address of the configuration file. |
| category    | String | Yes | Same as `category` in `SubTab`.                                     |
| labels | Map&lt;String, String&gt; | No       | The labels on the left of the panel. This field is not empty if `type` is `AvatarData.TYPE_SLIDER`. |
| avatarData  | AvatarData          | Yes       | The property operation class defined in the SDK.                                      |