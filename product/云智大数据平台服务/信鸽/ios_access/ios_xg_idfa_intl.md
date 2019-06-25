**This document applies to iOS TPNS <font color="#FF0000">SDK v1.0+ and later</font>**

## Feature Description
IDFA is a relatively effective identification parameter of TPNS's ability to push targeted messages on the iOS platform, so TPNS SDK uses a plugin to implement on-demand integration.

## Integration Steps

Follow these steps to integrate IDFA module with iOS TPNS SDK:
1. Open the idfa directory in the downloaded SDK package and get the libxgidfa.a static library file.
2. Add the libxgidfa.a static library file to the project to complete the integration of the IDFA plugin, as shown in the figure below:
![](https://main.qcloudimg.com/raw/9cdc0bd4925e7a989c9f0de08d4db0d8.png)

**Note**

If you want to collect IDFAs but did not place any ads, you can use the following method to pass App Store review:
![](http://docs.developer.qq.com/mta/assets/用户画像.png)

1.Serve advertisements within the app

This is an in-app advertising service and well suited for uses cases integrating ads in apps. Select this option if needed.

2.Attribute this app installation to a previously served advertisement.

This is used to track and count the amount of installations brought by the ads and needs to be selected.

3.Attribute an action taken within this app to a previously served advertisement

This is used to track and count the user actions brought by ad installations and needs to be selected.

4.Limit Ad Tracking setting in iOS

This is an acknowledgment item and must be selected.






