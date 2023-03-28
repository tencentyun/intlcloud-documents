
## 1.8.3 @2023.01.13
- Added support for adding multiple callback functions to an event callback.
- Added support for deleting specified callback functions.
- Added conversation group related APIs and event callbacks.
- Added support for setting custom conversation data event callbacks.
- Added conversation marking APIs.
- Added the advanced API for getting the conversation list.
- Added group counter related APIs and event callbacks.
- Added the text message translation API.
- Added the API and event callback for getting/subscribing to the total unread message count by filter.

## 1.8.2 @2022.12.06

- Supported Mac M1 chips for build.
- Supported WebGL for build.
- Fixed the parameter types of callbacks such as `GroupGetTopicInfoList` and `ConvGetConvList`.
- Added parameters and callback data logs.

## 1.8.0 @2022.10.11
- Fixed the conversion performance issue involved in first parameter serialization.

## 1.7.9 @2022.09.22
- Fixed iOS build issues.

## 1.7.7 @2022.09.02
- Added English API annotations.
- Added topic, community, user status, and other APIs.
- Upgraded the native SDK.
- Fixed known issues.

## 1.7.6 @2022.06.24
- Supported `string callback data` and `object callback data`.

## 1.7.5 @2022.05.23
- Added APIs for group message read receipts.
- Fixed the issue where the field with a value of `null` was ignored by Newtonsoft serialization.
- Fixed the issue where the `uint64` field in `GroupPendencyResult` was changed to `ulong`.

## 1.6.4 @2022.01.13
- Added SDK support for package manager import.
- Added the feature of adding dependencies after iOS compilation.

## 1.6.0 @2021.12.21
- Switched the underlying cross-platform C APIs.
- Added support for the Windows, macOS, Android, and iOS platforms with unified APIs.
- Note that v1.6.0 is incompatible with earlier versions.


## 1.5.1 @2021.11.24
- Fixed the issue where `-1` is returned for `sequenceid` unexpectedly.
- Added support for macOS.
- Removed the simple message module and enabled the advanced message module for both message receiving and sending.

## 1.5.0 @2021.11.16
- Added support for Windows.


## 1.4.0 @2021.08.03
- Simplified the configuration process on iOS.
- Fixed the IL2CPP packaging error on Android.

## 1.3.1 @2021.05.21

- Fixed known issues.

## 1.3.0 @2021.05.10

- Added the C# model to instantiate data returned by APIs.
- Added the usage of the C# model to `ExampleEntry.cs`.

## 1.2.0 @2021.04.28

- Added `sequenceID` to some message sending APIs to associate message requests and responses.

## 1.1.1 @2021.04.25

- Separated the method of dynamically fetching userSig.

## 1.1.0 @2021.04.15

- Added advanced message APIs.
- Added signaling message APIs.

## 1.0.1 @2021.04.01

- Initialized the project and implemented most APIs.
