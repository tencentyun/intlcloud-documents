## Demo UIの説明
<img src="https://qcloudimg.tencent-cloud.cn/raw/1b25592a83e2e7f38ded001ca8c0b93b.png" style="zoom: 67%;" />

## 実現方式
パネル設定情報は任意のパスに配置できます。Demoではassetsに配置し、Demoでパネルファイルを初めて使用する際にインストールディレクトリ下にコピーします。
![](https://qcloudimg.tencent-cloud.cn/raw/b178070d012fca8cbbf275c0b1e84f44.png)

**Json構造とUIパネルの対応関係**：

- 左側のitemが右側ページの第1階層メニューに対応します。headは最初のiconで選択した内容です。
<img src="https://qcloudimg.tencent-cloud.cn/raw/6547824e221494545e5353e8dce5e1cc.png" style="zoom:67%;" />
- 左側の赤枠のsubTabsは右側の第2階層メニューに対応します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/0cb8236d813fc9ec278b7026063a7b88.png" style="zoom:67%;" />
- 左側のiconのデータはresourcesフォルダ内で設定します。右側に表示されるのはパネルの設定データであり、両者はパネルデータの**categoryでバインドします**。SDKはresourcesフォルダ内のデータを解析し、対応するmapに入力します。mapのkeyはcategoryの値であるため、Demoでは`panel.json`ファイルの解析が完了すると、SDKの提供するメソッドによってデータを取得してバインドできるようになります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/2ad79a0d0efcb34cc5c1816975badfd8.png" style="zoom:67%;" />

## Demoの重要クラスの説明
パス：`com.tencent.demo.avater.AvatarResManager.java`

### 1. Avatarリソースのロード
```java
/**
     * Avatarリソースのロードに使用します
     *
     * @param xmagicApi      XmagicApiオブジェクト
     * @param avatarResName  名前
     * @param avatarSaveData モデルのデフォルト設定をロードします。ない場合はnullを渡します
     */
    public void loadAvatarRes(XmagicApi xmagicApi, String avatarResName, String avatarSaveData)
```

### 2. パネルデータの取得
```java
 /**
     * avatarのパネルデータを取得します。
     *
     * @param avatarResName      avatar素材名
     * @param avatarDataCallBack このメソッドはファイルにアクセスするため、サブスレッド内でファイル操作を行います。データの取得後はメインスレッドでコールバックを行います
     *                           返されるデータにはresourcesフォルダ下のデータが含まれています
     */
    public void getAvatarData(String avatarResName, String avatarSaveData, LoadAvatarDataCallBack avatarDataCallBack)
```

### 3. パネルデータから、ユーザーの設定した属性またはデフォルトの属性を解析します
```java
//パネルの設定ファイルから、ユーザーの設定した属性またはデフォルトの属性を解析します
public static List<AvatarData> getUsedAvatarData(List<MainTab> mainTabList) 
```

###  4. モデル切り替え背景データの取得
```java
 /**
     * 対応するplane Configデータを取得します
     *
     * @param avatarResName リソース名
     * @param avatarType    背景タイプ
     * @return
     */
    public AvatarData getAvatarPlaneTypeConfig(String avatarResName, AvatarBgType avatarBgType) 
```

## 付録

[MainTab.java](#maintab)、[SubTab.java](#subtab)内のフィールドの説明です。

### MainTab

| フィールド | タイプ  | 入力必須かどうか | 意味  |
| ----------- | ----------- | ----------- | ----------- |
| id   | String| はい | メインメニューの一意の識別子。メインメニューを区別するために用いられるため、グローバルで一意である必要があります |
| label| String| いいえ | 第1階層メニュー名（Demoでは現在この名称を表示していません）       |
| iconUrl        | String| はい | 画像アドレス。選択していない場合の画像アドレスです |
| checkedIconUrl | String| はい | 画像アドレス。選択している場合の画像アドレスです |
| subTabs | [SubTabタイプリスト](#subtab) | はい       | 第2階層メニューのリスト |

### SubTab

| フィールド | タイプ     | 入力必須かどうか | 意味 |
| --------------- | -------- | -------- | ----------- |
| label | String   | 是       | 第2階層メニュー名 |
| category | String   | はい       | 第2階層メニューのカテゴリータイプ。SDKの`com.tencent.xmagic.avatar.AvatarCategory`クラスで定義します |
| relatedCategory | String   | いいえ       | 依存関係の識別に使用します。例：髪型と髪色に依存関係があり、髪型変更の際もユーザーが前回設定した髪色を使用する必要があるような場合、髪型内にこのフィールドを設定する必要があります。値は髪色内のcategoryフィールドの値です（依存関係は現時点ではtype値がTYPE_SELECTORタイプのデータにしか存在しません） |
| avatarDataList  | リストタイプ | はい | [AvatarIconタイプリストデータ](#avataricon) |

### AvatarIcon

| フィールド | タイプ | 入力必須かどうか | 意味 |
| ----------- | ----------- | ----------- | ----------- |
|id| String| はい |各属性のID。SDKが返すAvatarDataデータ内のIDに対応します |
| icon | String| はい       | 画像アドレスまたはARGB色値（”#FF0085CF“）    |
| type | Int   | はい       | UI表示タイプ。`AvatarData.TYPE_SLIDER`はスライダータイプ、`AvatarData.TYPE_SELECTOR`はiconタイプです |
| selected    | boolean | はい       | typeがAvatarData.TYPE_SELECTORタイプの場合、このフィールドはそのitemが選択されているかどうかを表します |
| downloadUrl | String| いいえ | 設定ファイルのダウンロードアドレス。設定ファイルの動的ダウンロードに使用します |
| category    | String| はい | SubTab内のcategoryと同義です             |
| labels | Map&lt;String, String&gt; | いいえ       | typeがAvatarData.TYPE_SLIDERタイプの場合は値があり、パネルの左側に表示されるlabelに配置されます |
| avatarData  | AvatarData      | はい       | SDKはアバター制作属性操作クラスを定義しています |