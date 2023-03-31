[](id:overview)

## Overview

The TUIChat emoji panel is built with emojis, and you can also add custom emojis as needed. This document describes how to add custom emojis.

<table style="text-align:center;vertical-align:middle;width:1000px">
  <tr>
    <th style="text-align:center;" width="200px">Built-in emoji panel<br></th>
    <th style="text-align:center;" width="200px">Custom emoji panel<br></th>
  </tr>
  <tr>
    <td style="text-align:center;"><img style="width:200px" src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/1.PNG"  />    </td>
    <td style="text-align:center;"><img style="width:200px" src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/2.PNG"  />     </td>
	 </tr>
</table>


The emoji panel consists of two parts as shown below:

* The management of emoji resource images, including the display of emoji images.
* The management of emoji groups, including thumbnails of emoji groups and the send button.

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/7.png" style="zoom:30%;" />





[](id:add)

## Adding a Custom Sticker

Add a custom sticker in just two steps:

1. Prepare the emoji resources.
2. Load the sticker when starting the app.

Note that TUIChat is built with the logic for sending and parsing stickers so that you can easily use custom stickers on multiple terminals.

The following describes how to add the `programer` custom sticker as shown below:

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/3.png" style="zoom:25%;" />



[](id:add_prepare)

### Preparing emoji resources

Before adding a sticker, prepare a set of copyrighted emoji resources. Then, package your emoji images into a bundle file as shown below:

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/4.png" style="zoom:30%;" />



[](id:add_load)

### Loading the sticker

Drag the `CustomFaceResource.bundle` custom sticker containing `programer` emoji resources to your Xcode project. Then, load it when starting the app.

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/5.png" style="zoom:30%;" />



```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    app = self;
    // Load the emoji resources when starting the app
    [self setupCustomSticker];    
    return YES;
}

- (void)setupCustomSticker {
    // 1. Get the path of the bundle file of the custom sticker.
    NSString *customFaceBundlePath = [[NSBundle mainBundle] pathForResource:@"CustomFaceResource" ofType:@"bundle"];
    
    // 2. Load the custom emoji group
    // 2.1 Load the `programer` emoji resource images and parse them into `TUIFaceCellData`
    NSMutableArray<TUIFaceCellData *> *faceItems = [NSMutableArray array];
    for (int i = 0; i <= 17; i++) {
        TUIFaceCellData *data = [[TUIFaceCellData alloc] init];
        // The filename of the emoji resource images (the extension can be saved) for multi-terminal connection (which requires that filenames are consistent)
        data.name = [NSString stringWithFormat:@"yz%02d", i];
        // The path of the emoji resource images for local display
        data.path = [customFaceBundlePath stringByAppendingPathComponent:[NSString stringWithFormat:@"programer/%@", data.name]];
        [faceItems addObject:data];
    }
    // 2.2 Create the `programer` emoji group and parse it into `TUIFaceGroup`
    TUIFaceGroup *programGroup = [[TUIFaceGroup alloc] init];
    // Indicate the serial number of the current emoji group on the emoji panel for multi-terminal connection (which can be used together with the emoji name to find an image on the receiver's device)
    // Note that `groupIndex` starts from `0` and indicates the actual position of the current sticker on the emoji panel (`0` is the default value for the built-in `emoji` emoji group)
    programGroup.groupIndex = 1;
    // The root path of the current sticker in the bundle file of the custom emojis
    programGroup.groupPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/"];
    // The emoji resources in the current sticker
    programGroup.faces = faceItems;
    // The layout of the current sticker
    programGroup.rowCount = 2;
    programGroup.itemCountPerRow = 5;
    // The path of the thumbnail of the current sticker (without the extension)
    programGroup.menuPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/menu"];
    
    // 3. Add the `programer` emoji group to the emoji panel
    [TUIConfig.defaultConfig appendFaceGroup:programGroup];
}
```



[](id:add_sync)

### Multi-terminal connection

TUIChat is built with the logic for sending and parsing stickers, and you only need to make sure that the following two attributes are consistent on different platforms:

* The filenames of images in the sticker are consistent; that is, the values of the `name` field in `TUIFaceCellData` are consistent on multiple terminals when the stickers are loaded during app startup.
* The order of stickers on the emoji panel is consistent; that is, the values of the `groupIndex` field in `TUIFaceGroup` are consistent on multiple terminals when the stickers are loaded during app startup.

If the above two values are consistent, TUIChat's built-in logic for sending stickers will send the emoji filename and the index information of the sticker to other terminals for multi-terminal connection.

Note that `groupIndex` starts from `0` and indicates the actual position of the current sticker on the emoji panel (`0` is the default value for the built-in `emoji` emoji group).

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/9.png" style="zoom:40%;" />





[](id:advance_config)

## Advanced Configuration of the Emoji Panel

[](id:advance_config_order)

### Re-sorting emoji groups on the emoji panel

You can re-sort emoji groups on the emoji panel of TUIChat. Specifically, you only need to call the `- appendFaceGroup:` method of `TUIConfig` as needed.

To place the built-in `emoji` emoji group after custom emojis, perform the following steps:

* Get the built-in `TUIConfig.defaultConfig.faceGroups` emoji groups on the current emoji panel.
* Re-sort the emoji groups.
* Assign the value of the list of re-sorted emoji groups to the emoji panel.

```
- (void)setupCustomSticker {
    // 1. Get the path of the bundle file of the custom sticker.
    NSString *customFaceBundlePath = [[NSBundle mainBundle] pathForResource:@"CustomFaceResource" ofType:@"bundle"];
    
    // 2. Load the custom emoji group
    // 2.1 Load the `programer` emoji resource images and parse them into `TUIFaceCellData`
    NSMutableArray<TUIFaceCellData *> *faceItems = [NSMutableArray array];
    for (int i = 0; i <= 17; i++) {
        TUIFaceCellData *data = [[TUIFaceCellData alloc] init];
        // The filename of the emoji resource images (the extension can be saved) for multi-terminal connection (which requires that filenames are consistent)
        data.name = [NSString stringWithFormat:@"yz%02d", i];
        // The path of the emoji resource images for local display
        data.path = [customFaceBundlePath stringByAppendingPathComponent:[NSString stringWithFormat:@"programer/%@", data.name]];
        [faceItems addObject:data];
    }
    // 2.2 Create the `programer` emoji group and parse it into `TUIFaceGroup`
    TUIFaceGroup *programGroup = [[TUIFaceGroup alloc] init];
    // Indicate the serial number of the current emoji group on the emoji panel for multi-terminal connection (which can be used together with the emoji name to find an image on the receiver's device)
    // Note that `groupIndex` starts from `0` and indicates the actual position of the current sticker on the emoji panel (`0` is the default value for the built-in `emoji` emoji group)
    programGroup.groupIndex = 0;
    // The root path of the current sticker in the bundle file of the custom emojis
    programGroup.groupPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/"];
    // The emoji resources in the current sticker
    programGroup.faces = faceItems;
    // The layout of the current sticker
    programGroup.rowCount = 2;
    programGroup.itemCountPerRow = 5;
    // The path of the thumbnail of the current sticker (without the extension)
    programGroup.menuPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/menu"];
    
    // 3. Add the `programer` emoji group to the front of the emoji panel
    // 3.1 Get the built-in emoji groups
    NSMutableArray *faceGroupsMenu = [NSMutableArray arrayWithArray:TUIConfig.defaultConfig.faceGroups];
    // 3.2 Add the `programer` to the front of the emoji groups
    [faceGroupsMenu insertObject:programGroup atIndex:0];
    // 3.3 Re-assign the value to the emoji panel
    TUIConfig.defaultConfig.faceGroups = faceGroupsMenu;
    
    // 4. To retain the order of built-in emojis, add them in the default order
    // [TUIConfig.defaultConfig appendFaceGroup:programGroup];

    // Note that `groupIndex` must be consistent with the actual order.
    // You can directly read and copy the current position
    programGroup.groupIndex = [TUIConfig.defaultConfig.faceGroups indexOfObject:programGroup];
}
```

> ?
>
> The multi-terminal connection of stickers relies on the emoji names and the order of the emoji groups on the panel. Therefore, after adjusting the local order, you need to make sure that the `groupIndex` is consistent with the actual order.





[](id:advance_config_cover)

### Changing the thumbnail of an emoji group

When loading a custom emoji group, you can set the `menuPath` attribute of the `TUIFaceGroup` as the path of the thumbnail (the `@2x.png` extension is not required) to customize the thumbnail of the emoji group.

For example, set the `menu@2x.png` image in the `programer` emoji group as the thumbnail.

```
- (void)setupCustomSticker {
    ....
 		
    // 2.2 Create the `programer` emoji group and parse it into `TUIFaceGroup`
    TUIFaceGroup *programGroup = [[TUIFaceGroup alloc] init];
    ....
    // The path of the thumbnail of the current sticker (without the extension)
    programGroup.menuPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/menu"];
    ....
    
    ....
}
```





[](id:advance_config_style)

### Adjusting the layout of emoji images

Currently, the TUIChat emoji panel supports the following two layouts:

* `rowCount`, which indicates the number of rows of images displayed in the current emoji group.
* `itemCountPerRow`, which indicates the number of emoji images displayed per row.

For example, you can set to display the emoji images in the `programer` emoji group as two rows per page, with up to five images per row.

```
- (void)setupCustomSticker {
    ...
 		
    // 2.2 Create the `programer` emoji group and parse it into `TUIFaceGroup`
    TUIFaceGroup *programGroup = [[TUIFaceGroup alloc] init];
    // The layout of the current sticker
    programGroup.rowCount = 2;
    programGroup.itemCountPerRow = 5;
    
    ...
}
```

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/10.jpg" style="zoom:33%;" />



[](id:render)

## How Sticker Rendering Works

TUIChat is built with the mechanism for sending and rendering stickers, so you can ignore this section.

This section describes how to modify the source code or encode and pass through the content of a custom emoji.

[](id:render_send)

### Sending an emoji

The TUIChat emoji panel contains a `UICollectionView`. When you click an emoji image, the `- faceView:didSelectItemAtIndexPath:` method of the `TUIInputController` will be triggered and send you the name of the selected emoji and the index information of the emoji group on the emoji panel.

You can send an emoji in the callback in two steps:

- Create an emoji message with the emoji name and emoji group index.
- Call the `TUIChat` method to send the emoji message.

```
- (void)faceView:(TUIFaceView *)faceView didSelectItemAtIndexPath:(NSIndexPath *)indexPath
{
    TUIFaceGroup *group = [TUIConfig defaultConfig].faceGroups[indexPath.section];
    TUIFaceCellData *face = group.faces[indexPath.row];
    if(indexPath.section == 0){
        // Built-in emojis need to be displayed in the input box.
        [_inputBar addEmoji:face];
    }
    else{
        // Custom emojis are directly sent to the receiver.
        if (face.name) {
            // Create an emoji message
            V2TIMMessage *message = [[V2TIMManager sharedInstance] createFaceMessage:group.groupIndex data:[face.name dataUsingEncoding:NSUTF8StringEncoding]];
            // Send the message to receiver
            if(_delegate && [_delegate respondsToSelector:@selector(inputController:didSendMessage:)]){
                [_delegate inputController:self didSendMessage:message];
            }
        }
    }
}
```



[](id:render_parse)

### Parsing and rendering an emoji message

After receiving the emoji message from the sender, TUIChat will trigger the `- getCellData:` method of the `TUIFaceMessageCellData` and parse the emoji message into the `TUIFaceMessageCellData` for display.

TUIChat will assign the value of the `TUIMessageCellData` to `TUIFaceMessageCell` for rendering.

For more information on the message parsing process in TUIChat, see [iOS](https://intl.cloud.tencent.com/document/product/1047/50043).

```
+ (TUIMessageCellData *)getCellData:(V2TIMMessage *)message{
    // Parse the emoji information after receiving the message
    V2TIMFaceElem *elem = message.faceElem;
    
    // Create the `TUIFaceMessageCellData` for emoji display
    TUIFaceMessageCellData *faceData = [[TUIFaceMessageCellData alloc] initWithDirection:(message.isSelf ? MsgDirectionOutgoing : MsgDirectionIncoming)];
    // Get the order information of the current emoji group on the emoji panel
    faceData.groupIndex = elem.index;
    // Get the filename of the emoji image
    faceData.faceName = [[NSString alloc] initWithData:elem.data encoding:NSUTF8StringEncoding];
    // Get the specific path of the local sticker of the emoji image based on the name of the emoji image and the emoji group
    for (TUIFaceGroup *group in [TUIConfig defaultConfig].faceGroups) {
        if(group.groupIndex == faceData.groupIndex){
            NSString *path = [group.groupPath stringByAppendingPathComponent:faceData.faceName];
            faceData.path = path;
            break;
        }
    }
    faceData.reuseId = TFaceMessageCell_ReuseId;
    return faceData;
}
```
