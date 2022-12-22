AvatarはTencent Effectの機能の一部であるため、接続の際はEffectのアクセスドキュメントを参照した上でAvatar素材をロードする必要があります。Effectを接続済みの場合は、下記のステップ1の内容を無視してください。
1. Tencent Effectのドキュメントに従って接続します。[Tencent Effectの独立した統合](https://intl.cloud.tencent.com/document/product/1143/45385)をご参照ください。
2. 次の方法に従ってAvatar素材をロードします。

## Avatar機能を使用するための具体的な手順

### ステップ1：Demo内のファイルのコピー
1. 対応するdemoプロジェクトを公式サイトからダウンロードし、解凍します。
2. Demo内の`demo/app/assets/MotionRes/avatarRes`フォルダをご自身のプロジェクトにコピーします（Demoと同じ位置にします）。
3. Demo内の`com.tencent.demo.avatar`フォルダ下のすべてのクラスをプロジェクトにコピーします。

### ステップ2：重要コードの追加
Demo内の`com.tencent.demo.avatar.AvatarActivity`クラスを参照し、次のコードを追加します
1. ページのxmlファイル内でパネル情報を設定します。

```xml
	<com.tencent.demo.avatar.view.AvatarPanel
			 android:id="@+id/avatar_panel"
			 android:layout_width="match_parent"
			 android:layout_height="300dp"
			 app:layout_constraintBottom_toBottomOf="parent" />
```
2. ページ内でパネルオブジェクトを取得し、対応するデータコールバックインターフェースを設定します。
```java
 avatarPanel.setAvatarPanelCallBack(new AvatarPanelCallBack() {
					 @Override
					 public void onItemChecked(AvatarIcon avatarIcon) {
							 if (avatarIcon.avatarData == null && URLUtil.isNetworkUrl(avatarIcon.downloadUrl)) {  //ここは動的ダウンロードが必要であることを表します
									 downloadAvatarData(avatarIcon, () -> updateConfig(avatarIcon));
							 }else{
									 updateConfig(avatarIcon);
							 }
					 }

					 @Override
					 public void onItemValueChange(AvatarIcon avatarIcon) {
							 updateConfig(avatarIcon);
					 }

					 @Override
					 public boolean onShowPage(AvatarPageInf avatarPageInf, AvatarIcon avatarIcon){
							 if ( avatarIcon.avatarData == null && URLUtil.isNetworkUrl(avatarIcon.downloadUrl)) {  //ここは動的ダウンロードが必要であることを表します
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
3. パネルデータを取得し、パネルに設定します。
```java
AvatarResManager.getInstance().getAvatarData(avatarResName, false, allData -> avatarPanel.initView(allData));
```
4. xmagicApiオブジェクトを作成し、アバター制作リソースをロードします。
```java
private void initXMagic() {
		if (mXmagicApi == null) {
				mXmagicApi = XmagicApiWrapper.createXmagicApi(getApplicationContext(), false, null);
				AvatarResManager.getInstance().loadAvatarRes(mXmagicApi, avatarResName, !isCaptureMod);
				if(isCaptureMod){  //写真撮影によるアバター制作の場合は設定するデータを手動で取得し、手動で設定する必要があります
						List<AvatarData> avatarDataList = AvatarResManager.getUsedAvatarData(avatarPanel.getMainTabList());
						mXmagicApi.updateAvatarConfig(avatarDataList);
				}
				setAvatarPlaneType();
		}else{
				mXmagicApi.onResume();
		}
}
```
5. Avatar属性を保存します。Demo内のsaveAvatarConfigsメソッドを参照できます。
```java
/**
 * ユーザーの設定した属性またはデフォルトの属性値を保存します
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
6. 背景の切り替えはDemo内のchangeAvatarBgTypeメソッドを参照します。
```java
/**
 * 背景の切り替え
 */
private void changeAvatarBgType() {
		if (currentAvatarType == AvatarResManager.AvatarType.VIRTUAL_BG) {
				currentAvatarType = AvatarResManager.AvatarType.REAL_BG;
		}else{
				currentAvatarType = AvatarResManager.AvatarType.VIRTUAL_BG;
		}
		saveCurrentAvatarType();
		setAvatarPlaneType();
}

/**
 * モデル背景タイプの設定
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