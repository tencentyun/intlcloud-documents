ユーザーがより細かい粒度でドメイン名クエリーや管理権限を設定できるように、CDNアクセス権限ポリシーが完全にアップグレードされました。ユーザーは、カスタムポリシーステートメントを使用することにより、ドメイン名レベルの権限設定を実現することが可能になります。

1.  [アクセス管理コンソール](https://console.cloud.tencent.com/cam/overview)にログインし、【Policies】メニューをクリックして、ポリシー管理ページに入り、【 Create Custom Policy】をクリックします。
![](https://main.qcloudimg.com/raw/6570c1642d59bf00b5dee346f48ddf0e.png)
2. 【Create by Policy Generator】を選択します。
![](https://main.qcloudimg.com/raw/12a78b0a490d6cd95a4427b92710400f.png)
3. サービスのドロップダウンリストで【CDN】を選択し、権限付与が必要な機能セットを選択します。完全な読み取り/書き込み権限を付与する場合は、【All】にチェックを入れてすべてのサービスを選択できます。機能とコンソールとのマッピング関係については、[Action マッピングテーブル](https://cloud.tencent.com/document/product/228/41867)をご参照ください。
![](https://main.qcloudimg.com/raw/16c968c01bb9811df5a6356f4a364928.png)
4. リソースの欄に権限付与が必要なドメイン名を入力します。`* `はすべてのドメイン名を示します。設定が完了した後、【Add Statement】をクリックして【Next】をクリックすると、ポリシーが作成されます。作成したポリシーを既存のユーザ/ユーザグループに関連付ければ、権限を付与することができます。
![](https://main.qcloudimg.com/raw/0497f341d3ad51b56e07682aadc23ba8.png)

