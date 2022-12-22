Avatar는 Tencent Effect SDK의 기능입니다. 사용하기 위해서는 먼저 SDK 연동 후 Avatar 소재를 추가해야 합니다. SDK를 이미 통합한 경우 첫 번째 단계를 건너뜁니다.
1. SDK를 통합합니다. 자세한 지침은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45385)를 참고하십시오.
2. 아래 순서에 따라 Avatar 소재를 로딩합니다.

## Avatar 기능 단계

### 1단계: Demo 파일 복사
1. 당사 웹사이트에서 demo 프로젝트를 다운로드하고 압축을 해제합니다.
2. Demo의 `demo/app/assets/MotionRes/avatarRes` 폴더를 프로젝트의 동일한 위치에 복사합니다.
3. Demo의 `com.tencent.demo.avatar` 폴더에 있는 모든 클래스를 프로젝트에 복사합니다.

### 2단계: 코드 추가
다음 코드를 추가합니다(Demo의 `com.tencent.demo.avatar.AvatarActivity` 클래스 참고)
1. UI의 xml 파일에서 패널 정보를 구성합니다.
```xml
	<com.tencent.demo.avatar.view.AvatarPanel
			 android:id="@+id/avatar_panel"
			 android:layout_width="match_parent"
			 android:layout_height="300dp"
			 app:layout_constraintBottom_toBottomOf="parent" />
```
2. UI에서 패널 객체를 가져오고 콜백을 구성합니다.
```java
 avatarPanel.setAvatarPanelCallBack(new AvatarPanelCallBack() {
					 @Override
					 public void onItemChecked(AvatarIcon avatarIcon) {
							 if (avatarIcon.avatarData == null && URLUtil.isNetworkUrl(avatarIcon.downloadUrl)) {  //동적 다운로드를 수행함을 나타냅니다
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
							 if ( avatarIcon.avatarData == null && URLUtil.isNetworkUrl(avatarIcon.downloadUrl)) {  //동적 다운로드를 수행함을 나타냅니다
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
3. 패널 데이터를 가져오고 구성합니다.
```java
AvatarResManager.getInstance().getAvatarData(avatarResName, false, allData -> avatarPanel.initView(allData));
```
4. xmagicApi 객체를 생성하고 아바타 리소스를 로딩합니다.
```java
private void initXMagic() {
		if (mXmagicApi == null) {
				mXmagicApi = XmagicApiWrapper.createXmagicApi(getApplicationContext(), false, null);
				AvatarResManager.getInstance().loadAvatarRes(mXmagicApi, avatarResName, !isCaptureMod);
				if(isCaptureMod){  //사진 기반 아바타 사용자 지정을 위해서는 수동으로 데이터를 가져와서 설정해야 합니다
						List<AvatarData> avatarDataList = AvatarResManager.getUsedAvatarData(avatarPanel.getMainTabList());
						mXmagicApi.updateAvatarConfig(avatarDataList);
				}
				setAvatarPlaneType();
		} else {
				mXmagicApi.onResume();
		}
}
```
5. Avatar 속성을 저장합니다(Demo에서 saveAvatarConfigs를 참고할 수 있음)
```java
/**
 * 사용자가 설정한 속성 값 또는 기본 속성 값 저장
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
6. 배경 전환(Demo에서 changeAvatarBgType 참고):
```java
/**
 * 배경 전환
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
 * 모델 배경 유형 설정
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

