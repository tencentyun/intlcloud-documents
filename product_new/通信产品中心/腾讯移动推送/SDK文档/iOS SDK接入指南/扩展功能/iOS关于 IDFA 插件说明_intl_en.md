

## Feature
On the iOS platform, IDFA is a relatively effective identification parameter for the ability of TPNS to push targeted messages, so the TPNS SDK uses a plugin approach to implement on-demand integration.

## Integration Steps

Steps to integrate the IDFA module with the TPNS SDK for iOS:
1. Open the `idfa` directory in the downloaded SDK package and get the `libxgidfa.a` static library file.
2. Add the `libxgidfa.a` static library file to the project to complete the integration of the IDFA plugin as shown below:
![](https://main.qcloudimg.com/raw/72be25d88cf59ef62827dea69acd04f8.png)

**Note**

If you want to collect IDFAs but do not place any ads, you can use the following method to pass App Store review:

1. Serve advertisements within the app

This is an in-app advertising service, suitable for use cases where applications have in-app ads integrated. Select this option if needed.

2. Attribute this application installation to a previously served advertisement

This is used to track and record the number of installations brought by the ads and must be selected.

3. Attribute an action taken within this app to a previously served advertisement

This is used to track and record user behaviors after ad installations and must be selected.

4. Limit Ad Tracking setting in iOS

This item is an acknowledgment item and needs to be selected.






