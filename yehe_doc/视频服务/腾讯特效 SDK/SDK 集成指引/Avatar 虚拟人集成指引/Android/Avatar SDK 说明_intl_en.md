## SDK Integration
For how to download and integrate the SDK, how to set the license, as well as how to run a demo project, see [Integrating Tencent Effect SDK](https://intl.cloud.tencent.com/document/product/1143/45385).

## Copying the Avatar Materials

We offer multiple sets of face customization and dress-up materials, which can be found in the `MotionRes/avatarRes` directory in the SDK package after decompression. Like other animated effect materials, you need to copy them to the `assets` directory of your project.
![](https://qcloudimg.tencent-cloud.cn/raw/f712ea1424c224b5cac36403c4c218bf.png)

## Avatar Customization and SDK APIs
<table>
<tr>
	<th style="text-align:center">Avatar Customization</th>
	<th style="text-align:center">Photo-Based Avatar Customization</th>
</tr>
<tr>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/744618a7c9dfb622b3bd0e19e2d4969f.jpg" width=650></td>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/343aea35f8fd235f15cb029402577373.jpg" width=550></td>
</tr>
</table>


The section below offers descriptions of the APIs of `XMagicApi`, including the APIs for data loading, avatar customization, and photo-based avatar customization.

### 1. Load the avatar materials (`loadAvatar`)
```java
public void loadAvatar(XmagicProperty<?> property, UpdatePropertyListener updatePropertyListener)
```
The avatar materials are loaded in the same way as other animated effect materials. The `loadAvatar` API is equivalent to the [updateProperty](https://intl.cloud.tencent.com/document/product/1143/45399) API.

### 2. Load the avatar source data (`getAvatarConfig`)
```java
public static Map<String,List<AvatarData>> getAvatarConfig(String avatarResPath, String savedAvatarConfigs)
```

- Input parameters:
	- **avatarResPath**: The absolute path of the avatar materials on the user’s mobile device, such as `/data/data/com.tencent.pitumotiondemo.effects/files/xmagic/MotionRes/avatarRes/animoji_0624`.
	- **savedAvatarConfigs**: The avatar configuration data (a JSON string) saved from the last time the user customized an avatar. If an avatar is customized for the first time or no configuration data is saved, pass in `null`.
- Output parameters:
  This API returns a map, in which `key` corresponds to `category` and `value` corresponds to the data of the category. For details, see the `AvatarCategory` class. After the application layer gets the map, display the data on the UI as needed.

### 3. Customize the face and dress up (`updateAvatar`)
```java
public void updateAvatar(List<AvatarData> avatarDataList, UpdateAvatarConfigListener upDataAvatarConfigListener)
```
When this API is called, the avatar preview will be updated in real time. Each `AvatarData` object corresponds to a configuration (such as changing the hairstyle). You can pass multiple `AvatarData` objects to an API call to edit multiple aspects of an avatar, for example, change the hairstyle and hair color. The API will validate the `AvatarData` objects passed in. If an object is valid, it will be passed to the SDK; if not, a callback will be sent.
- For example, if an `AvatarData` object is passed in to change the hairstyle, but the hair model file (specified by `value` in `AvatarData`) cannot be found on the local device, the `AvatarData` object will be considered invalid.
- Also, if an `AvatarData` object is passed in to change the iris image, but the image file (specified by `value` in `AvatarData`) cannot be found on the local device, the `AvatarData` object will be considered invalid.

### 4. Export avatar settings (`exportAvatar`)
```java
public static String exportAvatar(List<AvatarData> avatarDataList)
```
When the user edits their avatar, the value of `selected` or shape change values in `AvatarData` will change. After editing, a new `AvatarData` list will be generated and can be exported as a JSON string. You can save it locally or upload it to the server.
The string is exported for the following purposes:
- The next time you call `loadAvatar` of `XMagicApi` to load the avatar materials, you need to set `customConfigs` of `XMagicProperty` to the JSON string so that the preview will remember the avatar settings from the last time.
- Also, you need to pass in this JSON string when you call `getAllAvatarData` to update `selected` and the shape change values in the avatar source data.

### 5. Customize an avatar based on a photo (`createAvatarByPhoto`)
For this API to work, the SDK must be connected to the internet.
```java
public void createAvatarByPhoto(String photoPath, List<String> avatarResPaths, boolean isMale,
            final FaceAttributeListener faceAttributeListener)
```
- **photoPath**: The photo path. Make sure that the face is in the center of the photo. Ideally, the photo should include only one face. If there are multiple, the SDK will select one randomly. To ensure the recognition results, the short side of the photo should preferably be longer than 500 px.
- **avatarResPaths**: You can pass in multiple sets of avatar materials, and the SDK will select the most suitable set based on the photo analysis result. Note: Currently, only one set of materials is supported. If multiple sets are passed in, the SDK will use the first one.
- **isMale**: Whether the person is male. Currently, this property is not used. However, it may be in the future. We recommend you pass in a correct value.
- **faceAttributeListener**: If customization fails, `void onError(int errCode, String msg)` will be returned; if it succeeds, `void onFinish(String matchedResPath, String srcData)` will be returned, in which the first parameter indicates the path of the matched avatar materials, and the second is the matching result (same as the return value of `exportAvatar`).
- The error codes of `onError` are defined in `FaceAttributeHelper.java`:
```
    public static final int ERROR_NO_AUTH = 1;// Insufficient permission.
    public static final int ERROR_RES_INVALID = 5;// The avatar material path passed in is invalid.
    public static final int ERROR_PHOTO_INVALID = 10;// Failed to read the photo.
    public static final int ERROR_NETWORK_REQUEST_FAILED = 20;// Failed to connect to the internet.
    public static final int ERROR_DATA_PARSE_FAILED = 30;// Failed to parse the data returned from the network.
    public static final int ERROR_ANALYZE_FAILED = 40;// Failed to recognize the face.
    public static final int ERROR_AVATAR_SOURCE_DATA_EMPTY = 50;// Failed to load the avatar source data.
```

### 6. Save the downloaded configuration file (`addAvatarResource`)

```
public static Pair<Integer, List<AvatarData>> addAvatarResource(String resourceRootPath, String category, String zipFilePath)
```

This API is used if avatar materials are downloaded dynamically. For example, suppose you offer 10 hairstyles and one of them is dynamically downloaded to a device. You need to call this API to pass the path of the downloaded ZIP file to the SDK. The SDK will parse the file and save it to the folder of the corresponding category. When you call `getAllAvatarData` the next time, the SDK will return the newly added data.
Parameters:

- **resourceRootPath**: The root directory of the avatar materials, such as `/data/data/com.tencent.pitumotiondemo.effects/files/xmagic/MotionRes/avatarRes/animoji_0624`.
- **category**: The category of the downloaded material.
- `zipFilePath`: The path of the downloaded ZIP file.
The API returns `Pair<Integer, List<AvatarData>>`, where `pair.first` is the error code, and `pair.second` is the newly added data.
The error codes are as follows:
```
    public interface AvatarActionErrorCode {
        int OK = 0;
        int ADD_AVATAR_RES_INVALID_PARAMS = 1000;
        int ADD_AVATAR_RES_ROOT_RESOURCE_NOT_EXIST = 1001;
        int ADD_AVATAR_RES_ZIP_FILE_NOT_EXIST = 1002;
        int ADD_AVATAR_RES_UNZIP_FILE_FAILED = 1003;
        int ADD_AVATAR_RES_COPY_FILE_FAILED = 1004;
    }
```

### 7. Call `AvatarData`
The `AvatarData` class is at the core of the above APIs. `AvatarData` contains the following fields:
```
public class AvatarData {
    /**
     * The selector data. For example, for glasses, different types of glasses are offered, and only one can be selected.
     */
    public static final int TYPE_SELECTOR = 0;

    /**
     * The slider data, such as cheek width.
     */
    public static final int TYPE_SLIDER = 1;

    // The category, such as face shape and eye adjustment. Standard categories are defined in `AvatarCategory.java`. If they cannot meet your requirements, you can customize a category (make sure it’s not the same as an existing one).
    // This field cannot be empty.
    public String category;

    // The ID of an avatar configuration item.
    // For example, each type of glasses has a unique ID. So does each adjustment item.
    // This field cannot be empty.
    public String id;

    // `TYPE_SELECTOR` or `TYPE_SLIDER`
    public int type;

    // If `type` is `TYPE_SELECTOR`, this field indicates whether the item is selected.
    public boolean selected = false;

    // Each icon or adjustment item has three aspects of configuration details:
    public String entityName;
    public String action;
    public JsonObject value;
}
```
An `AvatarData` object is the smallest unit of configuration, for example, hairstyle change or cheek adjustment.
<table>
<tr>
	<th style="text-align:center">Hairstyle Change</th>
	<th style="text-align:center">Cheek Adjustment</th>
</tr>
<tr>
	<td><img src="https://qcloudimg.tencent-cloud.cn/raw/6c7cf2b3775fef1d72d2b95b19af878c.png"></td>
	<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9c4699e9cf0f361a728b76aa34b6486a.png"></td>
</tr>
</table>


- If an item is the selector type, configure it by changing the value of `selected` in `AvatarData`. For example, suppose there are four types of glasses: A, B, C, and D. If the user selects A, set `selected` of A to `true` and that of B, C, and D to `false`. If the user selects B, set `selected` of B to `true` and that of A, C, and D to `false`.
- If an item is the slider type, configure it by changing `value` in `AvatarData`. The `value` field is a JSON object that includes multiple key-value pairs. Set the `value` of a key-value pair to the slider value.

## More About `AvatarData`
The three key fields of `AvatarData` are `entityName`, `action`, and `value`, whose values are automatically entered when the SDK parses the configuration data. In most cases, you won’t need to deal with the details of these three fields. However, for slider data, you need to parse the key-value pairs in the `value` field and configure them based on the slider values set on the UI.
The three key fields of `AvatarData` are [entityName](#entityName), [action](#action), and [value](#action).

[](id:entityName)
### `entityName`

`entityName` specifies which part of an avatar is to be edited, for example, face, eyes, hair, shirt, or shoes.

[](id:action)
### `action` and `value`
The `action` field indicates the action to be performed on `entityName`. Five `action` options are defined in `AvatarAction.java` in the SDK, which are detailed below:

| action         | Description                                                         | Requirements for `value`                                                    |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| changeColor    | Changes the colors of the current material, which include the basic color and emission color.           | `value` must be a JSON object and is required. It is generated automatically by the material customization tool.                               |
| changeTexture  | Modifies the maps of the current material, including the color texture map, metal/roughness texture map, ambient occlusion (AO) map, normal map, and emission map. | `value` must be a JSON object and is required. It is generated automatically by the material customization tool.                               |
| shapeValue     | Modifies the blendshape value. This action is often used for fine-tuning of facial features.               |  `value` must be a JSON object (in which `key` is the shape name and `value` is a float) and is required. It is generated automatically by the material customization tool. |
| replace        | Replaces a submodel, for example, glasses, hairstyles, or clothes.                       |  `value` must be a JSON object that describes the 3D transformation information, model path, and material path of the new submodel. It is generated automatically by the material customization tool. To hide a submodel, set it to `null`. |
| basicTransform | Adjusts the position, rotation, and scaling settings. This action is often used to zoom in/out or change the angle to switch between the full- and half-length views.  | `value` must be a JSON object and is required. It is generated automatically by the material customization tool.                             |

## Configuring Avatar Customization Data

Avatar configurations are stored in the `resources` folder (in `material/custom_configs/resources`):
![](https://qcloudimg.tencent-cloud.cn/raw/fcc5d2d5173afe13008b8369c63b1a32.png)

In most cases, the configuration files are generated automatically and don't need to be configured manually.
To automatically generate the configurations, design your materials using Tencent Effect Studio according to our standards and run the “resource_generator_gui” app we provide (only available on macOS currently). For details, see [Tencent Cloud Avatar Design Manual](https://doc.weixin.qq.com/doc/w3_ALoA-gYYAAgV0MAAbjtQfO4EWXhI9?scode=AJEAIQdfAAoU7K9sLCAGMA3QZFAAg&version=4.0.19.6020&platform=win).



