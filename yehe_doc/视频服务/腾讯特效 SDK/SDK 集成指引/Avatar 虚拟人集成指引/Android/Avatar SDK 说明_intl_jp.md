## SDKへのアクセス
SDKのダウンロード、接続、認証、Demoクイックスタートについては、[Tencent Effectの独立した統合](https://intl.cloud.tencent.com/document/product/1143/45385)をご参照ください。

## アバター制作素材の準備

現在Tencentでは、SDKと共にいくつかのアバター制作、着せ替え素材をご提供しています。素材はSDKの解凍後の`MotionRes/avatarRes`ディレクトリ内にあります。他の動的エフェクト素材と同様に、プロジェクトのassetsディレクトリにcopyする必要があります。
![](https://qcloudimg.tencent-cloud.cn/raw/f712ea1424c224b5cac36403c4c218bf.png)

## アバター制作フローとSDKインターフェース
<table>
<tr>
	<th style="text-align:center">アバター制作フロー</th>
	<th style="text-align:center">写真撮影によるアバター制作のフロー</th>
</tr>
<tr>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/744618a7c9dfb622b3bd0e19e2d4969f.jpg" width=650></td>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/343aea35f8fd235f15cb029402577373.jpg" width=550></td>
</tr>
</table>


XMagicApiのロードデータ、アバター制作、エクスポート設定、写真撮影アバター制作インターフェースの詳細は次のとおりです。

### 1. Avatar素材のロード（loadAvatar）
```java
public void loadAvatar(XmagicProperty<?> property, UpdatePropertyListener updatePropertyListener)
```
Avatar素材と一般的な動的エフェクト素材のロード方法は類似しています。loadAvatarインターフェースとSDKのupdatePropertyインターフェースは等価です。このため[updatePropertyインターフェースの説明とDemoコード](https://intl.cloud.tencent.com/document/product/1143/45399)をご参照ください。

### 2. Avatarソースデータのロード（getAvatarConfig）
```java
public static Map<String,List<AvatarData>> getAvatarConfig(String avatarResPath, String savedAvatarConfigs)
```

- 入力パラメータ：
	- **avatarResPath**：avatar素材のスマートフォン上の絶対パスです。例：`/data/data/com.tencent.pitumotiondemo.effects/files/xmagic/MotionRes/avatarRes/animoji_0624`。
	- **savedAvatarConfigs**：ユーザーが前回のアバター制作後に保存したデータであり、JSON形式の文字列です。初めて使用する場合またはユーザーがそれまでに保存したことがない場合、この値はnullとなります。
- 出力パラメータ：
  mapの形式で返します。mapのkeyはデータのcategoryです。詳細についてはAvatarCategoryクラスをご覧ください。mapのvalueはこのcategory下のすべてのデータです。アプリケーション層でこのmapを取得した後、必要に応じて希望のUIスタイルを表示します。

### 3. アバター制作、着せ替え（updateAvatar）

```java
public void updateAvatar(List<AvatarData> avatarDataList, UpdateAvatarConfigListener upDataAvatarConfigListener)
```

呼び出すと現在の素材のプレビューキャラクターをリアルタイムに更新します。1つのAvatarDataオブジェクトは1つのアトミック設定であり（髪型変更など），一度に複数のアトミック設定を渡すことができます（髪型と髪色の両方を変更するなど）。このインターフェースは渡されるAvatarDataの有効性をチェックし、有効なものはSDKに設定し、無効なデータにはcallbackを返します。
- 例えば髪型の変更を要求しているのに、髪のモデルファイル（AvatarDataのvalueフィールド内に設定）がローカルに見つからない場合、このAvatarDataは無効と判断されます。
- また例えば、瞳マップの変更を要求しているのに、マップファイル（AvatarDataのvalueフィールド内に設定）がローカルに見つからない場合、このAvatarDataは無効と判断されます。

### 4. アバター制作設定のエクスポート（exportAvatar）

```java
public static String exportAvatar(List<AvatarData> avatarDataList)
```
ユーザーがアバターを制作する際、AvatarDataのselectedステータスまたはブレンドシェイプ値を変更する場合があります。制作完了後、新しいフルAvatarDataリストを渡すとjson文字列をエクスポートできます。この文字列はローカルに保存することも、サーバーにアップロードすることもできます。
このエクスポートされた文字列には2つの用途があります。
- 次回再びXMagicApiのloadAvatarインターフェースでこのAvatar素材をダウンロードする際、このJSON文字列をXMagicPropertyのcustomConfigsフィールドに設定する必要があります。こうすることで、ユーザーが前回作成したキャラクターをプレビューで表示することができます。
- 上記のように、getAllAvatarDataを呼び出す際にこのパラメータを渡すことで、Avatarソースデータ内の選択状態およびブレンドシェイプ値を変更できるようにする必要があります。

### 5. 写真撮影、アバター制作（createAvatarByPhoto）
このインターフェースにはネットワーク接続が必要です。

```java
public void createAvatarByPhoto(String photoPath, List<String> avatarResPaths, boolean isMale,
            final FaceAttributeListener faceAttributeListener)
```

- **photoPath**：写真のパスです。顔が確実に画面の中央に位置するようにしてください。画面内に含まれる顔は1つだけにすることをお勧めします。複数の顔がある場合、SDKはその中の1つを選択します。写真の短辺は500px以上を推奨します。これより小さいと認識効果に影響する可能性があります。
- **avatarResPaths**：複数のAvatar素材セットを渡すことができます。SDKは写真の分析結果に基づいて、最も適した素材のセットを選択し、自動的にアバター制作を行います。注：現在は1セットのみをサポートしています。複数のセットを渡した場合、SDKは最初の1セットのみを使用します。
- **isMale**：男性かどうか。この属性は現在使用されていませんが、今後SDKが最適化される場合を考え、正確に渡すことをお勧めします。
- **faceAttributeListener**：失敗した場合は、`void onError(int errCode, String msg)`をコールバックします。成功した場合は、`void onFinish(String matchedResPath, String srcData)`をコールバックします。 最初のパラメータはマッチしたAvatar素材パス、2番目のパラメータはマッチ結果です。上記で述べたexportAvatarインターフェースからの戻り値は同じ意味となります。
- onErrorのエラーコードは`FaceAttributeHelper.java`で定義します。具体的には次のとおりです。

```
    public static final int ERROR_NO_AUTH = 1;//権限がありません
    public static final int ERROR_RES_INVALID = 5;//渡されたAvatar素材のパスが無効です
    public static final int ERROR_PHOTO_INVALID = 10;//写真の読み取りに失敗しました
    public static final int ERROR_NETWORK_REQUEST_FAILED = 20;//ネットワークリクエストに失敗しました
    public static final int ERROR_DATA_PARSE_FAILED = 30;//ネットワークから返されたデータの解析に失敗しました
    public static final int ERROR_ANALYZE_FAILED = 40;//顔の分析に失敗しました
    public static final int ERROR_AVATAR_SOURCE_DATA_EMPTY = 50;//Avatarソースデータのロードに失敗しました
```

### 6. ダウンロードした設定ファイルを対応するフォルダ内に配置する（addAvatarResource）

```
public static Pair<Integer, List<AvatarData>> addAvatarResource(String resourceRootPath, String category, String zipFilePath)
```

このインターフェースは主にAvatarパーツの動的ダウンロードのシナリオに用いられます。例としては、Avatar素材内に10種類の髪型があり、その後1種類の髪型をクライアントに動的に送信したい場合、ダウンロード完了後に圧縮パッケージを取得してからこのインターフェースを呼び出し、圧縮パッケージのパスをSDKに渡します。SDKはこの圧縮パッケージを解析し、対応するcategoryディレクトリ下に保存します。getAllAvatarDataインターフェースを次に呼び出す際、SDKは新たに追加されたこのデータを解析することができます。
パラメータの説明：

- **resourceRootPath**：Avatar素材のルートディレクトリです。例えば/data/data/com.tencent.pitumotiondemo.effects/files/xmagic/MotionRes/avatarRes/animoji_0624などです
- **category**：ダウンロードしたこのパーツのカテゴリーです
- **zipFilePath**：ダウンロードしたzipパッケージのアドレスです
インターフェースは`Pair<Integer, List<AvatarData>>`を返します。pair.firstはエラーコード、pair.secondは新たに追加されたデータの集合です。
エラーコードは次のとおりです。

```
    public interface AvatarActionErrorCode {
        int OK = 0;
        int ADD_AVATAR_RES_INVALID_PARAMS = 1000;
        int ADD_AVATAR_RES_ROOT_RESOURCE_NOT_EXIST = 1001;
        int ADD_AVATAR_RES_ZIP_FILE_NOT_EXIST = 1002;
        int ADD_AVATAR_RES_UNZIP_FILE_FAILED = 1003;
        int ADD_AVATAR_RES_COPY_FILE_FAILED = 1004;
    }
```

### 7. AvatarDataの呼び出し
上記のインターフェースのコアはすべてAvatarDataクラスです。その主な内容は次のとおりです。
```
public class AvatarData {
    /**
     * selectorタイプのデータです。例えば眼鏡の場合、さまざまな種類の眼鏡があっても、使用する際に選択できるのはその中の1つだけです。
     */
    public static final int TYPE_SELECTOR = 0;

    /**
     * スライダー調整タイプのデータです。例えば頬の幅を調整するなどです。
     */
    public static final int TYPE_SLIDER = 1;

    // 例えば、輪郭、目の微調整などです。AvatarCategory.javaでは標準のcategoryを定義し、それでニーズを満たせない場合はcategory文字列をカスタマイズすることもできます。既存のものと競合しなければ問題ありません
    //空にすることはできません。
    public String category;

    // 具体的な各itemまたは各微調整項目を識別します。
    // 例えば各眼鏡にはすべて個々のidがあり、微調整項目の各グループにもすべて個々のidがあります。
    //空にすることはできません。
    public String id;

    //TYPE_SELECTORまたはTYPE_SLIDER
    public int type;

    //selectorタイプの場合は、現在選択されているものの有無を表します
    public boolean selected = false;

    //各アイコンまたは微調整項目の各グループのバックグラウンドはすべて具体的な設定の詳細である、次の3要素に対応しています。
    public String entityName;
    public String action;
    public JsonObject value;
}
```
1つのAvatarDataオブジェクトは1つのアトミック設定です（髪型変更、 頬の調整など）。
<table>
<tr>
	<th style="text-align:center">髪型変更</th>
	<th style="text-align:center">頬の調整</th>
</tr>
<tr>
	<td><img src="https://qcloudimg.tencent-cloud.cn/raw/6c7cf2b3775fef1d72d2b95b19af878c.png"></td>
	<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9c4699e9cf0f361a728b76aa34b6486a.png"></td>
</tr>
</table>


- アバター制作の際、データがselectorタイプの場合は、AvatarDataのselectedフィールドを変更します。例えばA、B、C、Dという4種類の眼鏡があり、Aをデフォルトで選択している場合、Aのselectedはtrue、B、C、Dはfalseとなります。ユーザーが眼鏡Bを選択した場合、それはBのselectedをtrueにし、A、C、Dをfalseにすることになります。
- アバター制作の際、データがsliderタイプの場合は、AvatarDataのvalueフィールドを変更します。valueフィールドはJsonObjectであり、その中にはいくつかのkey-valueペアがあります。key-valueの中のvalueをスライダーの値に変更するだけです。

## AvatarDataの高度な説明
AvatarDataの中で、アバター制作において重要な役割を果たすものはentityName、action、valueの3つのフィールドです。これら3つのフィールドの値は、SDKが素材設定を解析する際に自動的に入力されます。多くの場合、この3つのフィールドの意味を理解する必要はありませんが、UI層で表示する際、スライダータイプの場合は、value内のブレンドシェイプkey-valueを解析し、UIの操作と対応させる必要があります。
このうち、AvatarDataの要素は[entityName](#entityName)、[action](#action)、[value](#action)のフィールドに分けられます

[](id:entityName)
### entityNameフィールド

アバター制作の際は、どの部位（顔、目、髪、トップス、靴など）を制作するかを明確に指定する必要があります。entityNameフィールドはこれらの体の部位の名前を記述するためのものです。

[](id:action)
### actionおよびvalueフィールド
actionフィールドはentityNameに対してどの操作（action）を実行するかを表します。SDK内では5種類のactionを定義し、いずれも`AvatarAction.java`で定義します。各actionの意味およびvalueの要件は次のとおりです。

| action         | 意味                                                         | value要件                                                    |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| changeColor    | 現在のマテリアルの色を変更します。基本色、放射光色などの色属性が含まれます           | JsonObjectタイプ。入力必須です。素材制作ツールによって自動生成されます。              |
| changeTexture  | 現在のマテリアルのマップを変更します。色のテクスチャマップ、金属の粗さのテクスチャマップ、AOテクスチャマップ、法線テクスチャマップ、放射光テクスチャマップなどが含まれます | JsonObjectタイプ。入力必須です。素材制作ツールによって自動生成されます。              |
| shapeValue     | blendShape値を変更します。通常、顔の細部のブレンドシェイプの微調整に用いられます               | JsonObjectタイプ。このうちkeyはブレンドシェイプ名、valueはfloatタイプの値です。入力必須です。素材制作ツールによって自動生成されます。 |
| replace        | サブモデルの置き換え（眼鏡、髪型、衣服などの置き換えなど）                       | JsonObjectタイプ。内部には新しいサブモデルの3D変換情報、モデルパス、マテリアルパスを記述しています。現在の位置にあるサブモデルを非表示にしたい場合はnullを使用します。素材制作ツールによって自動生成されます。 |
| basicTransform | 位置、回転、ズームを調整します。通常はカメラの遠近、角度の調整に用いることで、モデルの全身と半身アングルの切り替えを実現します | JsonObjectタイプ。入力必須です。素材制作ツールによって自動生成されます。              |

## Avatar制作・着せ替えデータの設定

avatar属性設定はresourcesフォルダ下に配置します（パス：`素材/custom_configs/resources`）。
![](https://qcloudimg.tencent-cloud.cn/raw/fcc5d2d5173afe13008b8369c63b1a32.png)

これらの設定ファイルは自動生成されるため、通常は手動で設定する必要はありません。自動生成の方法は次のとおりです。
設計者は設計仕様に従い、TencentEffectStudioを使用してキャラクターのセットを設計後、Tencentの提供するresource_generator_guiというApp（現在はMacOSプラットフォームのみサポートしています）を実行するだけでこの設定を自動生成できます。詳細については[設計仕様の説明](https://doc.weixin.qq.com/doc/w3_ALoA-gYYAAgV0MAAbjtQfO4EWXhI9?scode=AJEAIQdfAAoU7K9sLCAGMA3QZFAAg&version=4.0.19.6020&platform=win)をご参照ください。

