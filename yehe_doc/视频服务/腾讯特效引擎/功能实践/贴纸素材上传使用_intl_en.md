This document describes how to put purchased or self-created materials into a demo project and use them.

## iOS
The code related to the initialization of the resource package for the iOS demo is in `BeautyViewModel.m`, and the method to initialize the sticker material list is **setupData**.

1. Place your sticker material name (directory name) on the **_motion2DMenuIDS** list.
2. Copy the material package to **resources/2dMotionRes.bundle** in the demo and recompile and rerun the demo.

> ?The bundle where the sticker is located is only related to where the sticker is displayed but has nothing to do with the sticker type.

## Android

The code related to the initialization of the resource package for the Android demo is in **XmagicResParser.java**, and the method to initialize the sticker material list is **parseMotion**.

1. Add your sticker material name (directory name) to the string **motionResStr** at any position (note the comma).
2. Copy the material package to the **src/main/assets/MotionRes/2dMotionRes** directory in the demo and recompile and rerun the demo.

#### Example
If your sticker material folder is named **video_mymotion**, you need to change:
```java
final String MotionResStr = "video_lianliancaomei:lovely strawberry," +
......
```
to
```java
final String MotionResStr = "video_mymotion:my stickers," +
                            "video_lianliancaomei:lovely strawberry," +
......
```
> !The material package can be copied to other **xxxMotionRes** directories. This only affects where the sticker is displayed in the demo but has nothing to do with the sticker type.

