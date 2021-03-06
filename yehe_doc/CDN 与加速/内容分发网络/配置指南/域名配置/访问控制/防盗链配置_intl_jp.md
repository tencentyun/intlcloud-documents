## 設定シナリオ
ビジネスリソースへのアクセスのソースを制御する場合、Tencent Cloud CDNはreferer リンク不正アクセス防止設定機能を提供しています。

HTTP Request Header中のrefererフィールドの値にアクセス制御ポリシーを設定することにより、アクセスソースを制御して、悪意のあるユーザーによる盗用を防ぐことができます。


## 設定ガイド
### 設定の確認
[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、メニューバーで【ドメイン名管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定ページに入ります。第2欄の【アクセス制御】からリンク不正アクセス防止設定を確認できます。デフォルトでは、リンク不正アクセス防止設定がオフになっています。
![](https://main.qcloudimg.com/raw/53cfa056e5574aae9c912db36fcbf67b.png)

### 設定を有効にする

スイッチをクリックし、リンク不正アクセス防止のタイプを選択してリストに入力します。空の referを許可するかにチェックを入れて、【確認】をクリックすれば、リンク不正アクセス防止設定を有効にすることができます。
![](https://main.qcloudimg.com/raw/951eb25d77110a01fcd91ab9bfcd1cad.png)
**refererブラックリスト：**

- リクエストされたrefererフィールドがブラックリストに設定されている内容にマッチしている場合、CDNノードはリクエストされた情報を返さず、403ステータスコードが返されます。
- リクエストされたrefererフィールドがブラックリストに設定されている内容にマッチしていない場合、CDNノードはリクエストされた情報を正常に返します。
- **空のrefererを含む**というオプションが選択された場合、refererフィールドが空であるか、refererフィールド（たとえば、ブラウザリクエスト）がない場合、CDNノードはリクエストされた情報を返さず、403ステータスコードが返されます。

**refererホワイトリスト：**
- リクエストされたrefererフィールドがホワイトリストに設定されている内容にマッチしている場合、CDNノードはリクエストされた情報を正常に返します。
- リクエストされたrefererフィールドがホワイトリストに設定されている内容にマッチしていない場合、CDNノードはリクエストされた情報を返さず、403ステータスコードが返されます。
- ホワイトリストを設定する場合、CDNノードはホワイトリストで設定された文字列に一致するリクエストのみを返すことができます。
- **空のrefererを含む** というオプションが選択された場合、refererフィールドが空であるか、refererフィールド（たとえば、ブラウザリクエスト）がない場合、CDNは正常にリクエストされた情報を返します。

**設定の制約：**
+ リンク不正アクセス防止は、ドメイン名/IPルールをサポートしています。IPルールが使用されている場合、プレフィックスマッチングが利用可能です。ドメイン名ルールが使用されている場合、プレフィックスマッチングはサポートされていません。即ち、`www.abc.com`が設定されている場合、`www.abc.com/123`がマッチしますが、`www.abc.com.cn`がマッチしません。`127.0.0.1`が設定されている場合、`127.0.0.1/123`もマッチします。
+ リンク不正アクセス防止は、ワイルドカードマッチングをサポートします。つまり、`*.qq.com`設定されている場合、`www.qq.com`と`a.qq.com`の両方がマッチします。

### 設定を無効にする
リンク不正アクセス防止機能を無効に切り替えることができます。スイッチがオフの場合、以下の既存の設定があっても、この機能は実稼働環境では有効になりません。スイッチがオンの場合、設定がネットワーク全体で有効になる前に、先に設定の再確認を行っています。
![](https://main.qcloudimg.com/raw/0eff7fac96363892b1b95f53fbadf47d.png)

### 地域の特別な設定
アクセラレーションドメイン名がグローバルアクセラレーション用に設定されており、中国本土と中国本土以外のアクセラレーションリージョンに異なるrefererリンク不正アクセス防止を設定する場合は、設定の下にある【特別な設定の追加】をクリックして設定できます。
![](https://main.qcloudimg.com/raw/31d414d5adf37f8a2deadce688962645.png)

> !地域の特別な設定が追加された後、現在では削除することはできません。設定をオフにして無効にできます。

## 設定例

アクセラレーションドメイン名`www.test.com`のリンク不正アクセス防止が次のように設定されている場合、
![](https://main.qcloudimg.com/raw/027832bf7f5df50370257cce662105d8.png)
実際のアクセス状況は次のとおりです。

1.refererが`1.1.1.1`である中国本土のユーザーがリクエストを開始すると、中国本土用に設定されたホワイトリストがヒットし、リクエストされたコンテンツが直接返されます。
2.  refererが空である中国本土以外のユーザーがリクエストを開始すると、中国本土以外用に設定されたブラックリストがヒットし、403コードが返されます。

