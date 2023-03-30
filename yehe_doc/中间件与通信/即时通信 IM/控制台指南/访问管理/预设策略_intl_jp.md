>>!ここでは主に**Instant Messaging（IM）**のCloud Access Management（CAM）機能関連コンテンツについて紹介します。他製品のCAM関連コンテンツについては、[CAMサポート製品]をご参照ください。(https://intl.cloud.tencent.com/document/product/598/10588)。
>
>IMのCAMは、実質的にはサブアカウントをポリシーにバインドするか、またはポリシーをサブアカウントに付与します。開発者は、コンソールのプリセットポリシーを直接使用して、いくつかの簡単な承認操作を行うことができます。複雑な権限付与の操作については、 [カスタムポリシー](https://intl.cloud.tencent.com/document/product/1047/38088)をご参照ください。
>IMは現在、次のようなプリセットポリシーを提供しています。
>
><table class="table"><thead><tr><th>ポリシー名</th><th>ポリシーの説明</th></tr></thead>
><tbody><tr><td>QcloudAVCFullAccess</td><td>IM完全な読み取り/書き込みアクセス権限</td></tr>
><tr><td>QcloudIMReadOnlyAccess</td><td>IM読み取り専用アクセス権限</td></tr></tbody></table>
>
>## プリセットポリシー使用例
>
>### IM権限を持つサブアカウントの作成
>
>
>1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[**ユーザーリスト**](https://console.cloud.tencent.com/cam)にアクセスし、**ユーザーの作成**をクリックします。
>2. 「ユーザーの作成」ページで**カスタム作成**を選択し、「サブユーザーの作成」ページに進みます。
>>?CAM[サブユーザーのカスタム作成](https://intl.cloud.tencent.com/document/product/598/13674)の操作ガイドに従って、「ユーザー権限の設定」までの手順を完了してください。
>3. 「ユーザー権限の設定」ページにおいて、次の事項を実施します。
>  1. プリセットポリシー`Instant Messaging`を検索して、チェックを入れます。
>  2. **次のステップ**をクリックします。
>4. 「情報と権限のチェック」フィールドの下にある**完了**をクリックして、サブユーザーの作成を完了します。成功ページで、サブユーザーのログインリンクとセキュリティ証明書をダウンロードして保管します。そこには、次のような情報が含まれます。
><table class="table"><tbody><tr><td>情報</ td> <td>ソース</ td> <td>機能</td><td>保存する必要はありますか</td></tr>
><tr><td>ログインリンク</td><td>ページにコピー</td><td>コンソールにログインする際に便利で、ルートアカウントへの入力の手順を省略できます</td><td>いいえ</td></tr>
><tr><td>ユーザー名</td><td>セキュリティ証明書CSVファイル</td><td>コンソールにログインするときに入力します</td><td>はい</td></tr>
><tr><td>パスワード</td><td>セキュリティ証明書CSVファイル</td><td>コンソールにログインするときに入力します</td><td>はい</td></tr>
><tr><td>SecretId</td><td>セキュリティ証明書CSVファイル</td><td>サーバーAPIを呼び出すときに使用します。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675" target="_blank">アクセスキー</a>をご参照ください</td><td>はい</td></tr>
><tr><td>SecretKey</td><td>セキュリティ証明書CSVファイル</td><td>サーバーAPIを呼び出すときに使用します。詳細については、<a href="https://intl.cloud.tencent.com/document/product/598/32675" target="_blank">アクセスキー</a>をご参照ください</td><td>はい</td></tr></tbody></table>
>5. 前述のログインリンクとセキュリティ証明書を許可された当事者に提供します。許可された当事者は、サブユーザーを使用して、IMコンソールへのアクセスやIMサーバーAPIのリクエストなど、IMでのすべての操作を実行できます。
>
>### 既存のサブアカウントへのIM権限の付与
>
>
>1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[**ユーザーリスト**](https://console.cloud.tencent.com/cam)にアクセスし、権限を付与したいサブアカウントをクリックします。
>2. 「ユーザー詳細」ページの権限フィールドで、**ポリシーの追加**をクリックします。サブアカウントの権限が空でない場合は、**ポリシーの関連付け**をクリックします。
>3. **ポリシーリストからポリシーの関連付けを選択**を選択し、プリセットポリシー`Instant Messaging`を検索してチェックを入れます。その後はページの指示に従って、権限付与の手順を完了します。 
>
>
>### サブアカウントのIM権限の解除
>
>
>1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[**ユーザーリスト**](https://console.cloud.tencent.com/cam)にアクセスし、権限を解除したいサブアカウントをクリックします。
>2. 「ユーザー詳細」ページの権限フィールドでプリセットポリシー`Instant Messaging`を見つけ、右側の**解除**をクリックします。ページの指示に従って、権限の解除の手順を完了します。
