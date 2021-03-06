
## 設定シナリオ

Tencent Cloud CDNのリソースキャッシュは、リクエストによってトリガーされます。ユーザーがリソースへのアクセスリクエストを開始したときに、リクエストを受け取ったCDNノードがリクエストされたリソースをキャッシュしていない場合は、リクエストをオリジンサーバーに転送してリソースを取り出します。リソースを正常に取り出した後（2XXステータスコードが返されます）、リソースはノードにキャッシュされ、ユーザーに返されます。

お客様はCDNノードにキャッシュされたリソースを直接管理することはできません。オリジンサーバーのリソースが変更されてもCDNノードがレガシーリソースをキャッシュしてユーザーに返すことが心配な場合は、ノードキャッシュルールを設定することで、ある程度制御することができます。

>! ご利用のアクセラレーションドメイン名サービス地域がグローバルアクセラレーションの場合、【キャッシュルール設定】はグローバルに有効になり、中国国内と中国国外との差異化設定に対応しません。

## 設定ガイド

### 設定の確認

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のメニューバーで【ドメイン名管理】を選択し、ドメイン名操作列の【管理】をクリックして、ドメイン名設定画面に入ります。タブを【キャッシュ設定】に切り替えると、【キャッシュルール設定】が表示されます。

アクセラレーションドメイン名にアクセスする場合。

- 静的アクセラレーションを選択した場合、通常の動的ファイル（php、jsp、asp、aspxなど）のデフォルトのキャッシュ期間は0秒で（すなわち、キャッシュしない）、他のすべてのファイルタイプのキャッシュ期間はデフォルトで30日間です。
- ダウンロードアクセラレーション、ストリーミングメディアVODアクセラレーションサービスタイプを選択した場合、すべてのファイルのデフォルトのキャッシュ有効期限は30日間です。

![](https://main.qcloudimg.com/raw/2a1b53ba28e0de9b2262048751a6aa9a.png)

### 新しいルール

必要に応じて、キャッシュルールを追加できます。基本モードと詳細モードに分けられ、デフォルトは基本モードです。

>! 詳細モードで設定して送信すると、包括的にアップグレードされ、基本モードに復元できなくなります。

### 基本モード

各CDNノードのキャッシュリソースには「期限切れ時間」があります。リクエストされたキャッシュリソースが期限切れになると、ノードにまだキャッシュがある場合でも、無効と判定され、再度back-to-originしてプルバックされます。基本モードでは、特定のファイルタイプのノード上で設定されるキャッシュ時間を指定できます。
<img src="https://main.qcloudimg.com/raw/5a3d0ab3635c241e3e800d80a338077e.png" height="299" width="439" />


#### プラットフォームポリシー

ユーザーが特定のサービスリソースをリクエストすると、オリジンサーバーに対応するHTTP Response HeaderにCache-Controlフィールドが含まれている場合、デフォルトのプラットフォームポリシーは次の通りです。

- Cache-ControlフィールドがMax-Ageの場合、このリソースに対するキャッシュ時間は設定されているキャッシュ有効期限に準じ、Max-Ageの指定時間は継承されません。
- Cache-Controlフィールドはno-cache 、no-storeまたはprivateである場合、CDNノードはこのリソースをキャッシュしません。
- Cache-Controlフィールドがなく、リクエストがCDNキャッシュにヒットした場合、CDNはデフォルトで`Cache-Control:max-age = 600`ヘッダーを追加します。

#### キャッシュ期限切れの詳細設定

キャッシュ期限切れの詳細設定を有効にすると、ユーザーは、オリジンサーバーのHTTP Response Header Cache-ControlのMax-Age値を調整することにより、ノードキャッシュの有効期限を動的に調整できます。

高度なキャッシュ設定を有効にした後、CDNは設定されたノードキャッシュの有効期限をMax-Age値と比較し、小さい方をノードキャッシュの有効期限として使用します。

- オリジンサーバーの`/index.html`に設定されたMax-Ageが200秒で、CDNに設定されたキャッシュ有効期限が600秒の場合、ファイルがノードにおける実際のキャッシュ有効期限は200秒となります。
- オリジンサーバーの`/index.html`に設定されたMax-Ageが800秒で、CDNに設定されたキャッシュ有効期限が600秒の場合、ファイルがノードにおける実際のキャッシュ有効期限は600秒となります。

>! キャッシュ期限切れの詳細設定を有効にした後、オリジンサーバーがLast-Modifiedフィールドを返さない場合、CDNはデフォルトでLast-Modifiedフィールドを追加し、10分ごとにその値を変更します。

### 詳細モード

詳細モードでは、特定のファイルタイプにより多くのノードキャッシング動作を設定できます。

- オリジンサーバーに準じる：オリジンサーバーのCache-Controlヘッダーに準じます。
- キャッシュ：ノード上のリソースのキャッシュ時間を設定します。キャッシングを強制するかどうか（すなわち、オリジンサーバーのCache-Control: no-store/no-cache/privateを無視するかどうか）を追加で設定できます。
- キャッシュしない：back-to-originしてリソースを取得します。

<img src="https://main.qcloudimg.com/raw/d1513ea3dd6f515462d32fba82af9099.png" height="275" width="439" />


#### 制約の設定

- 1つのドメイン名で最大20件までのキャッシュルールを追加できます。
- 複数件のルールは優先順位を変更できます。最下位ルールの優先順位が最上位のものよりも高くなります。
- ファイルタイプ/フォルダ/フルパスファイルは、最大100グループのコンテンツを入力できます。
- 基本モード・詳細モード：キャッシュ時間は365日間を超えることはできません。
- 詳細モード：キャッシング動作が「キャッシュ」として選択されて、強制キャッシングを「有効」にすると、CDNは設定されたキャッシングルールに従ってキャッシュします。強制キャッシングを「無効」にすると、オリジンサーバーがCache-Control: no-store/no-cache/privateの場合、CDNはリソースをノードにキャッシュせず、back-to-originしてリソースを取得します。

### ルールの変更

追加されたキャッシングルールは変更できます。キャッシュキールール操作欄の【変更】をクリックして変更します

### ルールの削除

追加されたキャッシュルールは削除できます。キャッシュルール操作欄の【削除】をクリックして削除します。





## 設定例

アクセラレーションドメイン名`www.test.com`の【キャッシュルール設定】が以下の場合、

![](https://main.qcloudimg.com/raw/d20eef1466f92b72b8d63a4d58cd4c17.png)

実際のキャッシュ設定は以下のとおりです。

- `www.test.com/abc.jpg`リリースノードキャッシュ期間は10日間です。
- `www.test.com/def.php`リソースはノードにキャッシュされません。



