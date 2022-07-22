## Dynamically downloading resources
To reduce the SDK package size, you can dynamically download the necessary module resources and animated effect resources (`MotionRes`, not available in some basic editions of the SDK) from a URL and, after download, pass the path of the resources to the SDK.

1. Upload a ZIP file of the effect resources to the cloud and generate a URL such as `https://server address/LightCore.bundle.zip`.
2. In your project, download the file from the URL and decompress it to the sandbox (for example: `Documents/Xmagic`).
![](https://qcloudimg.tencent-cloud.cn/raw/f90fe608cc12156a3b4b778f0ad4d969.png)   
3. When initializing the SDK, pass in the path of the sandbox to `root_path`.
```objectivec
 NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
                              @"root_path":_filePath ,//_filePath is the folder to which effect resources are downloaded: Documents/Xmagic,
                              @"tnn_"
                              @"beauty_config":beautyConfigJson
 };
 // Init beauty kit                                 @"root_path":Documents/Xmagic,
 self.beautyKit = [[XMagic alloc] initWithRenderSize:_inputSize assetsDict:assetsDict];
```
4. Set the icons for different effects and get the images from the downloaded files.
```objectivec
NSMutableArray *arrayModels = [NSMutableArray array];
for (NSDictionary* dict in motionArray) {
	BeautyCellModel* model = [BeautyCellModel beautyWithDict:dict];
	// Load default mainbundle path of motionres
	if ([model.title isEqualToString:NSLocalizedString(@"item_none_label",nil)]) {
		model.icon = [NSString stringWithFormat:@"%@/%@.png", [[NSBundle mainBundle] bundlePath], model.key];
		[arrayModels addObject:model];
	} else {
		if(_useNetResource && _filePath != nil){ //When using resources from the internet
			NSString *DirPath = [_filePath stringByAppendingPathComponent:@"2dMotionRes.bundle/"]; //Get the absolute path of effect resources
			model.icon = [NSString stringWithFormat:@"%@/%@/template.png", DirPath, model.key];
		}else{
			model.icon = [NSString stringWithFormat:@"%@/%@/template.png", [[NSBundle mainBundle] pathForResource:@"2dMotionRes" ofType:@"bundle"], model.key];
		}
		if ([fileManager fileExistsAtPath:model.icon]) {
			[arrayModels addObject:model];
		}
	}
}
```
5. Set parameters for effects (For details, see [API Documentation](https://intl.cloud.tencent.com/document/product/1143/48646)).
```objectivec
/// @brief Configure effects
/// @param propertyType: The effect type, which is a string. Valid values: beauty, lut, motion.
/// @param propertyName: The effect name.
/// @param propertyValue: The effect value.
/// @param extraInfo: A reserved parameter, which can be used for dictionary configuration.
/// @return: If 0 is returned, the configuration is successful. If other values are returned, the configuration has failed.
/// @note: Notes
/**
| Effect Type | Effect Name | Effect Value| Description  | Remarks |
| :---- | :---- |:---- | :---- | :---- |
|  beauty  | Name of beautification effect | Effect strength |Beautification effect API | - |
|  lut  | Filter path + Filter name | Filter strength | Filter API | - |
|  motion  | Name of animated effect | Path of animated effect | Animated effect API| Make sure the path you pass in is writable. For ZIP files, you must manually unzip them first if you want to build the resources into your app.   |
**/
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

## Examples
### Configuring a beautification effect
No extra configuration is needed for beautification or body retouch effects. The SDK will automatically use the resource files downloaded. Below is a request sample for the skin brightening effect.
```objectivec
[self.beautyKitRef configPropertyWithType:@"beauty" withName:@"beauty.whiten" withData:@"30" withExtraInfo:nil];
```
Request parameters:

| Parameter          | Value            |
| ------------- | ------------- |
| propertyType  | beauty        |
| propertyName  | beauty.whiten |
| propertyValue | 30            |
| extraInfo     | nil           |

### Configuring filter effects
For filter effects, you need to configure `key` first. You can use the SDK’s built-in effect resources or resources downloaded from the internet.
```objectivec
NSString *key = [_model.lutIDs[index] path];
if (key != nil) {
    key = [@"lut.bundle/" stringByAppendingPathComponent:key];//The relative path of the filter effect image
}
if(_useNetResource && _filePath != nil){ //If a resource downloaded from the internet is used
    key = [_filePath stringByAppendingPathComponent:key];//Get the absolute path of the image
}
[self.beautyKitRef configPropertyWithType:@"lut" withName:key withData:[NSString 
stringWithFormat:@"%f",value] withExtraInfo:nil];
```

### Configuring the brightening filter
Request parameters:

| Parameter          | Value (Local Resource) | Value (Internet Resource)                                     | Remarks     |
| ------------- | ------------------------ | ------------------------------------------------------------ | -------- |
| propertyType  | lut                      | lut                                                          |     -     |
| propertyName  | lut.bundle/n_baixi.png   | `/var/mobile/Containers/Data/Application/25C7D01A-73F6-4F1B-AEB6-5EE03A221D18/Documents/Xmagic/lut.bundle/n_baixi.png` | The file path. |
| propertyValue | 60.000000                | 60.000000                                                    |    -      |
| extraInfo     | null                     | null                                                         |      -    |

### Configuring animated, makeup, and keying effects
For animated, makeup, and keying effects, you need to configure `propertyValue` first. You can use the SDK’s built-in effect resources or resources downloaded from the internet.
```objectivec
NSString *key = [_model.motionIDs[index] key];
        NSString *path = [_model.motionIDs[index] path];
        NSString *motionRootPath = path==nil?[[NSBundle mainBundle] pathForResource:@"MotionRes" ofType:@"bundle"]:path;
        if(_useNetResource && _filePath != nil){ //If a resource downloaded from the internet is used
            motionRootPath = [_filePath stringByAppendingPathComponent:@"2dMotionRes.bundle"];//Get the absolute path of `2dMotionRes`
        }
        [self.beautyKitRef configPropertyWithType:@"motion" withName:key withData:motionRootPath withExtraInfo:nil];
```

### Configuring the animated 2D cute effect
Request parameters:

| Parameter          | Value (Local Resource) | Value (Internet Resource)                                     | Remarks     |
| ------------- | ------------- | ------------- | -------- |
| propertyType  | motion | motion |        -  |
| propertyName  | video_keaituya | video_keaituya |       -   |
| propertyValue | `/private/var/containers/Bundle/Application/FD2D7912-E58E-4584-B7E4-8715B8D2338F/BeautyDemo.app/2dMotionRes.bundle` | `/var/mobile/Containers/Data/Application/25C7D01A-73F6-4F1B-AEB6-5EE03A221D18/Documents/Xmagic/2dMotionRes.bundle` | The file path. |
| extraInfo     | nil | nil |     -     |

