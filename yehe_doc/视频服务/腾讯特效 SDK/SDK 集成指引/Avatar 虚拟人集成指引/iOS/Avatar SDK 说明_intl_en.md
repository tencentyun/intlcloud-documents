## SDK Integration

For how to download and integrate the SDK, how to set the license, as well as how to run a demo project, see [Integrating Tencent Effect SDK](https://intl.cloud.tencent.com/document/product/1143/45384).

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
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/8dab03ae9b380cca30b7fb1408a82bdd.jpg" width=650></td>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/8fe57503adf3f4f269de09edc178459f.jpg" width=550></td>
</tr>
</table>


The section below offers descriptions of the APIs of `XMagicApi`, including the APIs for data loading, avatar customization, and photo-based avatar customization.

### 1. Get the avatar source data (`getAvatarConfig`)
```swift
+ (NSDictionary <NSString *, NSArray *>* _Nullable)getAvatarConfig:(NSString * _Nullable)resPath exportedAvatar:(NSString *_Nullable)exportedAvatar;
```

- **Input parameters**:
	- `resPath`: The absolute path of avatar materials on the user’s mobile device, such as `/var/mobile/Containers/Data/Application/C82F1F7A-01A1-4404-8CF6-131B26B4DA1A/Library/Caches/avatarMotionRes.bundle/avatar_v2.0_male`.
	- **exportedAvatar**: The avatar configuration data (a JSON string) saved from the last time the user customized an avatar. If an avatar is customized for the first time or no configuration data is saved, pass in `nil`.
- **Output parameters**:
	This API returns an `NSDictionary` object, in which `key` is the category (for details, see the `TEDefine` class below) and `value` is the data of the category. After the application layer gets the dictionary data, display it on the UI as needed.

### 2. Load the avatar materials (`loadAvatar`)
```swift
- (void)loadAvatar:(NSString * _Nullable)resPath exportedAvatar:(NSString * _Nullable)exportedAvatar;
```
- **Input parameters**:
	- `resPath`: The absolute path of avatar materials on the user’s mobile device, such as `/var/mobile/Containers/Data/Application/C82F1F7A-01A1-4404-8CF6-131B26B4DA1A/Library/Caches/avatarMotionRes.bundle/avatar_v2.0_male`.
	- `exportedAvatar`: The avatar configuration data (a JSON string) saved from the last time the user customized an avatar. If an avatar is customized for the first time or no configuration data is saved, pass in `nil`.
- **Output parameters**:
This API returns an `NSDictionary` object, in which `key` is the category (for details, see the `TEDefine` class below) and `value` is the data of the category. After the application layer gets the dictionary data, display it on the UI as needed.

### 3. Customize the face and dress up (`updateAvatar`)
```swift
- (void)updateAvatar:(NSArray<AvatarData *> *_Nonnull)avatarDataList;
```

When this API is called, the avatar preview will be updated in real time. Each `AvatarData` object corresponds to a configuration (such as changing the hairstyle). You can pass multiple `AvatarData` objects to an API call to edit multiple aspects of an avatar, for example, change the hairstyle and hair color. The API will validate the `AvatarData` objects passed in. If an object is valid, it will be passed to the SDK; if not, a callback will be sent.
- For example, if an `AvatarData` object is passed in to change the hairstyle, but the hair model file (specified by `value` in `AvatarData`) cannot be found on the local device, the `AvatarData` object will be considered invalid.
- Also, if an `AvatarData` object is passed in to change the iris image, but the image file (specified by `value` in `AvatarData`) cannot be found on the local device, the `AvatarData` object will be considered invalid.

### 4. Export avatar settings (`exportAvatar`)
```swift
+ (NSString *_Nullable)exportAvatar:(NSArray <AvatarData *>*_Nullable)avatarDataList;
```

When the user edits their avatar, the value of `selected` or shape values in `AvatarData` will change. After editing, a new `AvatarData` list will be generated and can be exported as a JSON string. You can save it locally or upload it to the server.
The string is exported for the following purposes:
- The next time you call **loadAvatar** of `XMagicApi` to load the avatar materials, you need to set `customConfigs` of `XMagicProperty` to the JSON string so that the preview will remember the avatar settings from the last time.
- Also, you need to pass in this JSON string when you call `getAllAvatarData` to update `selected` and the shape values in the avatar source data.


### 5. Customize an avatar based on a photo (`createAvatarByPhoto`)
For this API to work, the SDK must be connected to the internet.
```swift
+ (void)createAvatarByPhoto:(NSString * _Nullable)photoPath avatarResPaths:(NSArray <NSString *>* _Nullable)avatarResPaths isMale:(BOOL)isMale success:(nullable void (^)(NSString *_Nullable matchedResPath, NSString *_Nullable srcData))success failure:(nullable void (^)(NSInteger code, NSString *_Nullable msg))failure;
```

- **photoPath**: The photo path. Make sure that the face is in the center of the photo. Ideally, the photo should include only one face. If there are multiple, the SDK will select one randomly. To ensure the recognition results, the short side of the photo should preferably be longer than 500 px.
- **avatarResPaths**: You can pass in multiple sets of avatar materials, and the SDK will select the most suitable set based on the photo analysis result.
>! Currently, only one set of materials is supported. If multiple sets are passed in, the SDK will use the first one.
- **isMale**: Whether the person is male. Currently, this property is not used. However, it may be in the future. We recommend you pass in a correct value.
- **success**: The callback for successful configuration, in which `matchedResPath` indicates the path of the matched materials and `srcData` indicates the matching result (same as the return value of `exportAvatar`).
- **failure**: The callback when configuration fails, in which `code` indicates the error code and `msg` indicates the error message.

### 6. Save the downloaded configuration file (`addAvatarResource`)
```swift
+ (void)addAvatarResource:(NSString * _Nullable)rootPath category:(NSString * _Nullable)category filePath:(NSString * _Nullable)filePath completion:(nullable void (^)(NSError * _Nullable error, NSArray <AvatarData *>* _Nullable avatarList))completion;
```

This API is used if avatar materials are downloaded dynamically. For example, suppose you offer 10 hairstyles and one of them is dynamically downloaded to a device. You need to call this API to pass the path of the downloaded ZIP file to the SDK. The SDK will parse the file and save it to the folder of the corresponding category. When you call `getAllAvatarData` the next time, the SDK will return the newly added data.

Parameters:
- **rootPath**: The root directory of avatar materials, such as `/var/mobile/Containers/Data/Application/C82F1F7A-01A1-4404-8CF6-131B26B4DA1A/Library/Caches/avatarMotionRes.bundle/avatar_v2.0_male`.
- **category**: The category of the downloaded material.
- **zipFilePath**: The local path of the downloaded ZIP file.
- **completion**: The result callback, in which `error` indicates the error message, and `avatarList` indicates the avatar data array obtained after parsing.

### 7. Send a custom event (`sendCustomEvent`)
This API is used to send a custom event, for example, to display the idle status when no face is detected.
```swift
- (void)sendCustomEvent:(NSString * _Nullable)eventKey eventValue:(NSString * _Nullable)eventValue;
```
- **eventKey**: The key of the custom event. For details, see `AvatarCustomEventKey` of `TEDefine`.
- **eventValue**: The value of the custom event, which is a JSON string. For example, you can convert `@{@"enabel" : @(YES)}` to a JSON string or directly enter `@"{\\"enable\\" : true}"`.

### 8. Call `AvatarData`
The `AvatarData` class is at the core of the above APIs. `AvatarData` contains the following fields:
```
/// @brief The configuration type.
@interface AvatarData : NSObject
// Such as face shape changing or eye adjustment. If the standard categories defined in `TEDefine` cannot meet your requirements, you can customize a category (make sure it’s not the same as an existing one). This filed cannot be empty.
@property (nonatomic, copy) NSString * _Nonnull category;
// The ID of an avatar configuration item. For example, each type of glasses has a unique ID. So does each adjustment item. This field cannot be empty.
@property (nonatomic, copy) NSString * _Nonnull Id;
// The type, which can be `selector` or `AvatarDataTypeSlider`.
@property (nonatomic, assign) AvatarDataType type;
/// If `type` is `selector`, this field indicates whether the item is selected.
@property (nonatomic, assign) BOOL isSelected;

/// The part of an avatar to be edited, for example, face, eyes, hair, shirt, or shoes. For how to configure this, refer to our documentation.
@property (nonatomic, copy) NSString * _Nonnull entityName;
/// The action to be performed on `entityName`. For details, see our documentation.
@property (nonatomic, copy) NSString * _Nonnull action;
/// The details of the action to be performed on `entityName`. For details, see our documentation.
@property (nonatomic, copy) NSDictionary * _Nonnull value;
@end
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

## More about `AvatarData`
The SDK gets `AvatarData` by parsing the `custom_configs` directory of the material root directory and sends it to the application layer. Generally, you don't need to manually construct `AvatarData`.
The three key fields of `AvatarData` are [entityName](entityName), [action](#action), and [value](#value), whose values are automatically entered when the SDK parses the configuration data. In most cases, you won’t need to deal with the details of these three fields. However, for slider data, you need to parse the key-value pairs in the `value` field and configure them based on the slider values set on the UI.

[](id:entityName)
### `entityName`
`entityName` specifies which part of an avatar is to be edited, for example, face, eyes, hair, shirt, or shoes. Take our demo for example. If you use open the material project (`xxx.studio`) with Tencent Effect Studio, you will see the following list:
<img src="https://qcloudimg.tencent-cloud.cn/raw/06a4860a9b6f1b1cf3350d0dfbfbd68b.png" width=300>
Each item in the list indicates an avatar part. **The item name must be unique in the material project**.

[](id:action)
### `action`
The `action` field indicates the action to be performed on `entityName`. Five `action` options are defined in the SDK, which are detailed below:

| action         | Description                                                         | Requirements for `value`                                                    |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| changeColor    | Changes the colors of the current material, which include the basic color and emission color.           | `value` must be a JSON object and is required. For details, see below.                               |
| changeTexture  | Modifies the maps of the current material, including the color texture map, metal/roughness texture map, ambient occlusion (AO) map, normal map, and emission map. | `value` must be a JSON object and is required. For details, see below.                               |
| shapeValue     | Modifies the blendshape value. This action is often used for fine-tuning of facial features.               |  `value` must be a JSON object (in which `key` is the shape name and `value` is a float) and is required. For details, see below. |
| replace        | Replaces a submodel, for example, glasses, hairstyles, or clothes.                       |  `value` must be a JSON object that describes the 3D transformation information, model path, and material path of the new submodel. To hide a submodel, set it to `null`. For details, see below. |
| basicTransform | Adjusts the position, rotation, and scaling settings. This action is often used to zoom in/out or change the angle to switch between the full- and half-length views. | `value` must be a JSON object and is required. For details, see below. |

[](id:value)
### `value`
<dx-tabs>
::: `action` = `changeColor`
[](id:changeColor)
**Example**:

```swift
{
		"key": "baseColorFactor",
        "value": [43, 26, 23, 255],
		"subMeshIndex":0,
		"materialIndex":0
}
```
- **key**: This field is required. It specifies whether to change the basic color, emission color, or a custom color property of the current material.

The valid values of `key` depend on the shader used by the current material. In the above screenshot, the built-in `lit_fade` shader is used. The basic color is named `baseColorFactor` and the emission color is named `emissiveFactor`, so in this case, `baseColorFactor` and `emissiveFactor` are the valid values of `key`. You can also open the material file to view the `key` values. For example, in the example above, the material file used is `hair.fmaterial`. Find it in the Tencent Effect Studio project and open it. It will look like this:<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/374363dc75275181e05d02a05bb6c2dd.png" width=500>
- **value**: The color in RGBA format. This field is required.
- **subMeshIndex and materialIndex**[](id:subMeshIndex): These two fields are optional. If you do not specify them, `0` will be used.
	In Tencent Effect Studio, a mesh (a submodel such as eyes, hairstyle, or face) is generally not configured with submeshes and has only one material.<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/6c4b6de62f37fb58e74d25ec8b01eaa4.png" width=300>
	<br>Some meshes may also have submeshes and multiple materials.<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/736b84897bb2e784ac0a3d0085591829.png" width=300>
	<br>In such cases, when changing the material color (`changeColor`), you need to specify the material using `subMeshIndex` and `materialIndex`. To determine the values of these two parameters, open `template.json` in the material project directory, find the current mesh, and locate `subMeshConfigs`. For example, search `hair`, and you will see the following `subMesh` settings:
	<img src="https://qcloudimg.tencent-cloud.cn/raw/85e39b3f3492b2aed27a67bbd3394c60.png" width=500>
	<br>Then, you can specify `subMeshIndex` and `materialIndex` to change the color of a specific material.
	:::
	::: `action` = `changeTexture`
	[](id:changeTexture)
	**Example**:
```swift
{
	"switchKey": "baseColorEnableTexture",
	"switchValue": true,
	"key": "baseColorMap",
	"value": "0622-1/Images/face_tex_base_3.png",
	"subMeshIndex":0,
	"materialIndex":0,
	"textureOptions": {
            "wrapS": "REPEAT",
            "wrapT": "REPEAT",
            "magFilter": "LINEAR",
            "minFilter": "LINEAR_MIPMAP_LINEAR",
            "sRGB": false,
            "mipmap": true,
            "samplerType": "SAMPLER_2D"
         }
}
```
- **switchKey and switchValue**: These two fields are required. They determine whether to display texture maps. If `switchValue` is `false`, no texture maps are configured, and you don't need to set other fields. The values of `switchKey` and `key` must match each other.
- **key and value**: These two fields are required if `switchValue` is `true`. `value` is the relative path of the map file to the root directory of materials (as shown in the example above) or the absolute path on the mobile device.
>? Like `key` for `changeColor`, the valid values of `switchKey` and `key` depend on the shader used by the material. For example, `baseColorEnableTexture` and `baseColorMap` in the example above correspond to the built-in color texture shader in Tencent Effect Studio. Other valid values include AO texture and normal texture. We also offer custom shaders such as lipstick and face maps.
> You can open a material file to view the values of `switchKey` and `key` of each map. Take the demo for example. If you open `face.fmaterial`, which is the material file for `face_main`, you will see the following:
><img src="https://qcloudimg.tencent-cloud.cn/raw/0fa0653a62172412aba16b64d1bc172f.png" width=500>
><br>Set `switchKey` and `key` to the switch and key values of the map you want to modify.

- **subMeshIndex and materialIndex**: These two fields are optional. If you do not specify them, `0` will be used. For details, see [action ==  changeColor](#subMeshIndex).
- **textureOptions**: This field is optional. It specifies the map unwrapping and rendering styles. Unless you have special requirements, we recommend you leave this field empty.
:::
::: `action` = `shapeValue`
[](id:shapeValue)
**Example**
```
{
	"chin_length": 0.0,
	"cheek_width": 0.0,
	"chin_width": 0.0
}
```
The example above includes shape names and shape change values. For more information about shape names, see [Tencent Cloud Avatar Design Manual](https://doc.weixin.qq.com/doc/w3_ALoA-gYYAAgV0MAAbjtQfO4EWXhI9?scode=AJEAIQdfAAoU7K9sLCAGMA3QZFAAg&version=4.0.19.6020&platform=win). The value range of shape change values is -1.0 to 1.0.
:::
::: `action` = `replace`
[](id:replace)
When `action` is `replace`, `value` specifies the 3D transformation information, model path, and material path of the submodel. You can find such information of a model in `template.json` in the root directory of materials.
**Example**:
```
{
	"position": {
		"x": -0.424766392,
		"y": -29.969169617,
		"z": -25.769769669
	},
	"rotation": {
		"x": 0,
		"y": 0,
		"z": 0
	},
	"scale": {
		"x": 1,
		"y": 1,
		"z": 1
	},
	"meshResourceKey": "meshFolder/glass_A.fmesh",
	"subMeshConfigs": [{
		"materialResourceKeys": ["/sdcard/xmagic_res/glass_red.fmaterial"]
	}，{
		"materialResourceKeys": ["/sdcard/xmagic_res/test1.fmaterial","/sdcard/xmagic_res/test2.fmaterial"]
	}]
}
```
- **position, rotation, and scale**: These three fields are optional. They specify the position, rotation, and scaling attributes of the model. If they are not specified, the default values will be used. The default values of `position`, `rotation`, and `scale` are `0,0,0`, `0,0,0`, and `1,1,1` respectively.
>! The `rotation` value is in degrees. For example, `45` indicates 45 degrees. It corresponds to the `eEuler` field in `template.json`.
- **meshResourceKey**: This field is required. It specifies the path of the model mesh file. The path can be the relative path of the mesh file to the root directory of materials (as shown in the example) or the absolute path of the file on the mobile device.
- **subMeshConfigs**: This field is required. As [mentioned above](#subMeshIndex), a mesh may contain multiple submeshes, and a submesh may contain multiple materials. `subMeshConfigs` specifies the materials of a mesh to use. `materialResourceKeys` can be the relative path of the material file to the root directory of materials (as shown in the example) or the absolute path of the file on the mobile device.
:::
::: `action` = `basicTransform`
**Example**:
```swift
{
	"position": {
		"x": -0.424766392,
		"y": -29.969169617,
		"z": -25.769769669
	},
	"rotation": {
		"x": 0,
		"y": 0,
		"z": 0
	},
	"scale": {
		"x": 1,
		"y": 1,
		"z": 1
	}
}
```
This action adjusts the position, rotation, and scale of a model. It is often used to zoom in/out or change the camera angle to switch between the full- and half-length views. For details about `position`, `rotation`, and `scale`, see [action = replace](#replace).
:::
</dx-tabs>

## Configuring Avatar Customization Data

Avatar configurations are stored in the `resources` folder (in `material/custom_configs/resources`):
![](https://qcloudimg.tencent-cloud.cn/raw/fcc5d2d5173afe13008b8369c63b1a32.png)

In most cases, the configuration files are generated automatically and don't need to be configured manually.
To automatically generate the configurations, design your materials using Tencent Effect Studio and run the “resource_generator_gui” app we provide (only available on macOS currently). For details, see [Tencent Cloud Avatar Design Manual](https://doc.weixin.qq.com/doc/w3_ALoA-gYYAAgV0MAAbjtQfO4EWXhI9?scode=AJEAIQdfAAoU7K9sLCAGMA3QZFAAg&version=4.0.19.6020&platform=win).



