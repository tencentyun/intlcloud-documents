Avatars are a capability of the Tencent Effect SDK. To use it, you need to integrate the SDK first and then add the avatar materials. If you have already integrated the SDK, skip the first step:
1. Integrate the SDK. For detailed directions, see [Integrating Tencent Effect SDK](https://intl.cloud.tencent.com/document/product/1143/45385).
2. Follow the steps below to load the avatar materials.

## Directions

### Step 1. Copy demo files
1. Download the demo project from our website and decompress it.
2. Copy the `demo/app/assets/MotionRes/avatarRes` folder in the demo to the same location in your project.
3. Copy all the classes in the `com.tencent.demo.avatar` folder of the demo to your project.

### Step 2. Add code
Add the following code (you can refer to the `com.tencent.demo.avatar.AvatarActivity` class of the demo):
1. Configure panel information in the XML file of your UI.
```xml
	<com.tencent.demo.avatar.view.AvatarPanel
			 android:id="@+id/avatar_panel"
			 android:layout_width="match_parent"
			 android:layout_height="300dp"
			 app:layout_constraintBottom_toBottomOf="parent" />
```
2. Get the panel object on your UI and configure the callbacks:
```java
 avatarPanel.setAvatarPanelCallBack(new AvatarPanelCallBack() {
					 @Override
					 public void onItemChecked(AvatarIcon avatarIcon) {
							 if (avatarIcon.avatarData == null && URLUtil.isNetworkUrl(avatarIcon.downloadUrl)) {  // It indicates to perform dynamic download.
									 downloadAvatarData(avatarIcon, () -> updateConfig(avatarIcon));
							 } else {
									 updateConfig(avatarIcon);
							 }
					 }

					 @Override
					 public void onItemValueChange(AvatarIcon avatarIcon) {
							 updateConfig(avatarIcon);
					 }

					 @Override
					 public boolean onShowPage(AvatarPageInf avatarPageInf, AvatarIcon avatarIcon){
							 if ( avatarIcon.avatarData == null && URLUtil.isNetworkUrl(avatarIcon.downloadUrl)) {  // It indicates to perform dynamic download.
									 downloadAvatarData(avatarIcon, () -> {
											 if(avatarPageInf!=null){
													 avatarPageInf.refresh();
											 }
									 });
									 return false;
							 }
							 return true;
					 }

					 private void updateConfig(AvatarIcon avatarIcon) {
							 if (mXmagicApi != null && avatarIcon != null) {
									 List<AvatarData> avatarConfigList = new ArrayList<>();
									 avatarConfigList.add(avatarIcon.avatarData);
									 mXmagicApi.updateAvatarConfig(avatarConfigList);
							 }
					 }
			 });
```
3. Get and configure the panel data.
```java
AvatarResManager.getInstance().getAvatarData(avatarResName, false, allData -> avatarPanel.initView(allData));
```
4. Create an `xmagicApi` object and load the avatar resources:
```java
private void initXMagic() {
		if (mXmagicApi == null) {
				mXmagicApi = XmagicApiWrapper.createXmagicApi(getApplicationContext(), false, null);
				AvatarResManager.getInstance().loadAvatarRes(mXmagicApi, avatarResName, !isCaptureMod);
				if(isCaptureMod){  // For photo-based avatar customization, you need to manually get and set the data.
						List<AvatarData> avatarDataList = AvatarResManager.getUsedAvatarData(avatarPanel.getMainTabList());
						mXmagicApi.updateAvatarConfig(avatarDataList);
				}
				setAvatarPlaneType();
		} else {
				mXmagicApi.onResume();
		}
}
```
5. Save the avatar properties (you can refer to `saveAvatarConfigs` in the demo):
```java
/**
 * Save the property values set by the user or the default property values.
 */
private void saveAvatarConfigs() {
		if (mXmagicApi != null && avatarPanel != null) {
				List<AvatarData> avatarDataList = AvatarResManager.getUsedAvatarData(avatarPanel.getMainTabList());
				new Thread(() -> {
						String content = XmagicApi.exportAvatarConfig(avatarDataList);
						boolean result = FileUtil.writeContentToFile(AvatarResManager.getAvatarConfigsDir(), AvatarResManager.getAvatarConfigsFileName(avatarResName), content);
						String tip = result ? "save avatar data successfully " : "Save avatar data failed";
						runOnUiThread(() -> Toast.makeText(getApplicationContext(), tip, Toast.LENGTH_LONG).show());
				}).start();
		}
}
```
6. Change the background (you can refer to `changeAvatarBgType` in the demo):
```java
/**
 * Switch the background.
 */
private void changeAvatarBgType() {
		if (currentAvatarType == AvatarResManager.AvatarType.VIRTUAL_BG) {
				currentAvatarType = AvatarResManager.AvatarType.REAL_BG;
		} else {
				currentAvatarType = AvatarResManager.AvatarType.VIRTUAL_BG;
		}
		saveCurrentAvatarType();
		setAvatarPlaneType();
}

/**
 * Set the model background type.
 */
private void setAvatarPlaneType() {
		AvatarData avatarData = AvatarResManager
						.getInstance().getAvatarPlaneTypeConfig(avatarResName, currentAvatarType);
		if (mXmagicApi != null && avatarData != null) {
				List<AvatarData> avatarDataList = new ArrayList<>();
				avatarDataList.add(avatarData);
				mXmagicApi.updateAvatarConfig(avatarDataList);
		}
}
```

