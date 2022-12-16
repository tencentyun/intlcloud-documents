
## Version 1.3.1 Released on November 29, 2022

**Note**

The new version relies on `tuicall-engine-webrtc@1.2.1`. To use this version, please update `tuicall-engine-webrtc` first.

**New features**

- Optimized the style.
- Added support for listening for the change of call type by the caller before a call is answered.
- Added support for device testing in the basic demo.

**Bug fixing**

- Fixed an internal logic error that occurs when the user hangs up.

## Version 1.3.0 Released on November 14, 2022

**Note**

- Before you update to this version, please read the [update guide](./Updated%20Guidline.md).

**New features**

- The call view can now automatically adapt to portrait mode on mobile webpages.
- Added support for local camera preview when making a call.
- Added support for device testing before a call in the basic demo.

**Bug fixing**

- Fixed the issue where the TIM instance is not entirely terminated after `TUICallKitServer.destroy()`.
- Fixed the issue where the caller receives a no response notification when the callee is busy.
- Fixed failure to package TypeScript types in the context of Vite.

**API changes**

- If an error occurs after `TUICallKitServer.call()` or `TUICallKitServer.groupCall()` is called, the `beforeCalling` callback is no longer returned. You can use “try…catch” to catch the error.

## Version 1.2.0 Released on November 03, 2022

**New features**

- Adapted to the new version of the TUICallEngine SDK.

## Version 1.1.0 Released on October 21, 2022

**New features**

- Added support for full screen during a call.
- Added support for call window minimizing using `<TUICallKitMini/>`.

**Bug fixing**

- Fixed known issues and improved stability.

## Version 1.0.3 Released on October 14, 2022

**New features**

- Added support for quick user ID copying and one-click window opening.

## Version 1.0.2 Released on September 30, 2022

**New features**

- Added demonstrations and more detailed directions to the integration guide.

**Bug fixing**

- Fixed the issue where device status is not shown when the user enters a room for the first time.
- Fixed occasional failure to load icons when Webpack is used for packaging.
- Fixed several known style issues.

## Version 1.0.1 Released on September 26, 2022

**New features**

- Added support for hiding the mic icon of the callee when making a call.

**Bug fixing**

- Changed the SDKAppID input restriction in the basic demo to numeric.

## Version 1.0.0 Released on September 23, 2022

- [TUICallKit basic demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md)
- [Integration (TUICallKit)](https://www.tencentcloud.com/document/product/647/50993)
- [API Documentation (TUICallKit)](https://www.tencentcloud.com/document/product/647/51015)
- [UI Customization (TUICallKit)](https://www.tencentcloud.com/document/product/647/50997)
- [FAQs (Web)](https://www.tencentcloud.com/document/product/647/51024)