## Android
### Version 2.5.0.207 Released on October 25, 2022
- Introduced avatar features.
- Added support for muting and unmuting audio effects.
- Added a callback API for `updateProperties`.
- Added the `setBundleToLightEngine` API, which is used to dynamically add AI model-based resources.
- Added support for code obfuscation.
- Deleted the `LogUtils` class in the SDK.


### Version 2.4.2.324 Released on September 13, 2022
Fixed the issue where the blush, contour, and lipstick effects fail to work in some cases.


### Version 2.4.2.322 Released on July 19, 2022
Fixed some effect errors.

### Version 2.4.2.317 Released on July 13, 2022
Deleted `beacon.aar`. If you update from a version earlier than v2.4.2.317, the new version will not include `beacon.aar`.

### Version 2.4.2 Released on July 7, 2022
- Optimized the face detection algorithm to fix unstable recognition and tracking performance in some scenarios.
- The parameters of the `updateProperty` API are now validated. For details about the parameter requirements, see [updateProperty](https://intl.cloud.tencent.com/document/product/1143/45399).
- Fixed the issue where the value returned by `isDeviceSupport` is sometimes inaccurate.
- Added `beacon.aar` to the `libs` directory of the SDK. You need to copy it to your project. If your project already has a beacon, it may cause a conflict. To avoid this, do not import the AAR file.
- Added support for Unity. For details, see the `Unity` folder in the SDK package.

## iOS
### Version 2.5.0.250 Released on October 31, 2022
- Added support for muting audio effects.
- Introduced avatar features.
- Added support for compilation on an emulator.
- Fixed known memory leak issues.

### Version 2.4.2.114 Released on July 19, 2022
- Fixed some effect errors.
- Reduced the package size.

### Version 2.4.2 Released on July 7, 2022
- Optimized the face detection algorithm to fix unstable recognition and tracking performance in some scenarios.
- Added support for dynamically downloading effect resources for the demo.
- Fixed failure to use custom filter images.
- Updated the API documentation.
