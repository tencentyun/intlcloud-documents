>>!ここでは主に**Instant Messaging（IM）**のCloud Access Management（CAM）機能関連コンテンツについて紹介します。他製品のCAM関連コンテンツについては、[CAMサポート製品]をご参照ください。(https://intl.cloud.tencent.com/document/product/598/10588)。
>
>IMのCAMにおいて[プリセットポリシー](https://intl.cloud.tencent.com/document/product/1047/38087)を使用して権限付与を行うのは簡便ではありますが、プリセットポリシーは権限制御の粒度が比較的粗く、IMアプリケーションや[Tencent Cloud API](https://intl.cloud.tencent.com/product/api)の粒度まで細分化することができません。きめ細かいアクセス制御機能を必要とする場合は、カスタムポリシーを作成する必要があります。
>
>
>## カスタムポリシーの作成方法
>
>カスタムポリシーを作成するには、さまざまな方法があります。次の表に、それぞれの方法の比較を示します。具体的な操作手順については、以下の文章をご参照ください。
>
><table class="table"><thead><tr><th>エントリーの作成</th><th>作成方法</th><th>効果(Effect)</th><th>リソース(Resource)</th><th>操作(Action)</th><th>柔軟性</th><th>難易度</th></tr></thead>
><tbody><tr><td><a href="https://console.cloud.tencent.com/cam/policy" target="_blank">CAMコンソール</a></td><td>ポリシージェネレーター</td><td>手動選択</td><td>構文の記述</td><td>手動選択</td><td>中</td><td>中</td></tr>
><tr><td><a href="https://console.cloud.tencent.com/cam/policy" target="_blank">CAMコンソール</a></td><td>ポリシー構文</td><td>構文の記述</td><td>構文の記述</td><td>構文の記述</td><td>高</td><td>高</td></tr>
><tr><td>CAMサーバーAPI</td><td><a href="https://intl.cloud.tencent.com/document/product/598/32248" target="_blank">CreatePolicy</a></td><td>構文の記述</td><td>構文の記述</td><td>構文の記述</td><td>高</td><td>高</td></tr></tbody></table>
>
>
>>?
>>- IMは、製品の機能またはアイテムに応じたカスタムポリシーの作成は__サポートしていません__。
>>- __手動選択__とは、ユーザーがコンソールに表示される候補リストからオブジェクトを選択することを意味します。
>>- __構文の記述__は [アクセスポリシー構文](#.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) によってオブジェクトを記述します。
>
>## アクセスポリシー構文
>
>### リソース構文の記述
>
>上記のように、IM権限管理のリソース粒度はアプリケーションです。アプリケーションのポリシー構文の記述法は、[CAMリソース記述法](https://intl.cloud.tencent.com/document/product/598/10606)に従います。以下の例では、開発者のルートアカウントIDは12345678で、開発者は、SDKAppIDがそれぞれ1400000000、1400000001および1400000002のアプリケーションを3つ作成しています。
>
>- IMのすべてのアプリケーションのポリシー構文の記述
>```
>"resource": [
>  "qcs::im::uin/12345678:sdkappid/*"
>]
>```
>- 単一アプリケーションのポリシー構文の記述
>```
>"resource": [
>  "qcs::im::uin/12345678:sdkappid/1400000001"
>]
>```
>- 複数アプリケーションのポリシー構文の記述
>```
>"resource": [
>  "qcs::im::uin/12345678:sdkappid/1400000000",
>  "qcs::im::uin/12345678:sdkappid/1400000001"
>]
>```
>
>### 操作構文の記述
>上記のとおり、TRTCの権限管理の操作粒度はTencent Cloud APIです。次の例では、`DescribeAppStatList`（アプリケーションリストの取得）、`DescribeSdkAppInfo`（アプリケーション情報の取得）などのTencent Cloud APIを例として取り上げています。
>- IMのすべてのTencent Cloud APIのポリシー構文の記述
>```
>"action": [
>  "name/im:*"
>]
>```
>- 単一のTencentCloud APIを操作する際のポリシー構文の記述
>```
>"action": [
>  "name/im:DescribeAppStatList"
>]
>```
>- 複数のTencentCloud APIを操作する際のポリシー構文の記述
>```
>"action": [
>  "name/im:DescribeAppStatList",
>  "name/im:DescribeTrtcAppAndAccountInfo"
>]
>```
>
>## カスタムポリシーのユースケース
>
>### ポリシージェネレーターの使用
>
>次の例では、カスタムポリシーを作成しています。このポリシーは、1400000001に対するIMアプリケーションのあらゆる操作を許可します。
>1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[**ポリシー**](https://console.cloud.tencent.com/cam/policy)にアクセスし、**カスタムポリシーの新規作成**をクリックします。
>2. **ポリシージェネレーターで作成**を選択して、ポリシー作成ページに進みます。
>3. サービスと操作を選択します。
>	- **効果(Effect)**設定項目は、**許可**を選択します。
>	- **サービス(Service)**設定項目は、**IM**を選択します。
>	- **操作(Action)**設定項目は、すべての項目にチェックを入れます。
>	- **リソース(Resource)**設定項目は、 [リソース構文の記述](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0)に従って`qcs::im::uin/12345678:sdkappid/1400000001`と入力します。
>	- **条件(Condition)**設定項目は設定不要です。
>	- **ステートメントの追加**をクリックすると、ページの一番下に「IMアプリケーション1400000001に対するあらゆる操作を許可する」というステートメントが表示されます。
>4. 同じページに別のステートメントを追加し続けます。
>	- **効果(Effect)**設定項目は、**拒否**を選択します。
>	- **サービス(Service)**設定項目は、**IM**を選択します。
>	- **操作(Action)**設定項目は、`RemoveUser`（検索機能で速やかに見つけられます）にチェックを入れます。
>	- **リソース(Resource)**設定項目は、 [リソース構文の記述](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0)に従って`qcs::im::uin/12345678:sdkappid/1400000001`と入力します。
>	- **条件(Condition)**設定項目は設定不要です。
>	- **ステートメントの追加**をクリックすると、ページの一番下に「IMアプリケーション1400000001に対する`RemoveUser`操作を拒否する」というステートメントが表示されます。
>5. **次のステップ**をクリックし、必要に応じてポリシー名を変更します（または変更しなくてもかまいません）。
>6. **完了**をクリックし、カスタムポリシーの作成を完了します。
>
>
>その後、このポリシーを他のサブアカウントに付与する方法は、[IMの読み取り/書き込みアクセス権限を既存のサブアカウントに付与する](https://intl.cloud.tencent.com/document/product/1047/38087)と同様です。
>
>
>### ポリシー構文の使用
>
>次の例では、カスタムポリシーを作成します。このポリシーは、1400000001と1400000002という2つのIMアプリケーションに対するあらゆる操作を許可します。
>
>
>1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[**ポリシー**](https://console.cloud.tencent.com/cam/policy)にアクセスし、**カスタムポリシーの新規作成**をクリックします。
>2. **ポリシー構文で作成**を選択し、ポリシー作成ページに進みます。
>3. **テンプレートタイプの選択**ボックスで**空白テンプレート**を選択します。
> >?ポリシーテンプレートは、新しいポリシーが既存のポリシー（プリセットポリシーまたはカスタムポリシー）をコピーしてから、それをベースとして調整が行われることを意味します。実際の使用においては、開発者は状況に応じて適切なポリシーテンプレートを選択することで、ポリシー内容の難しい入力と作業の負荷を軽減することができます。 
>4. **次のステップ**をクリックし、必要に応じてポリシー名を変更します（または変更しなくてもかまいません）。
>5. **ポリシー内容の編集**ボックスにポリシー内容を入力します。この例のポリシーの内容は次のとおりです。
>```
>{
> "version": "2.0",
> "statement": [
>     {
>         "effect": "allow",
>         "action": [
>             "name/im:*"
>         ],
>         "resource": [
>             "qcs::im::uin/12345678:sdkappid/1400000001",
>             "qcs::im::uin/12345678:sdkappid/1400000002"
>         ]
>     },
>     {
>         "effect": "deny",
>         "action": [
>             "name/im:RemoveUser"
>         ],
>         "resource": [
>             "qcs::im::uin/12345678:sdkappid/1400000001"
>         ]
>     }
> ]
>}
>```
>>?ポリシー内容は、[CAMポリシー構文ロジック](https://intl.cloud.tencent.com/document/product/598/33415)に従う必要があります。そのうちリソースと操作の2つの要素の構文については、上記の[リソース構文の記述](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0)と[操作構文の記述](#.E6.93.8D.E4.BD.9C.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0)をご参照ください。
>6. **ポリシーの作成**をクリックして、カスタムポリシーの作成を完了します。
>その後、このポリシーを他のサブアカウントに付与する方法は、[IMの読み取り/書き込みアクセス権限を既存のサブアカウントに付与する](https://intl.cloud.tencent.com/document/product/1047/38087)と同様です。
>
>### CAMが提供するサーバー側APIの使用
>
>ほとんどの開発者にとって、コンソールで権限管理操作が完了すれば、ビジネスニーズが満たされたことになります。ただし、権限管理機能を自動化・システム化する必要がある場合は、サーバー側APIを使用することができます。
>ポリシー関連のサーバー側APIはCAMに属します。詳細については、[CAM公式ウェブサイトドキュメント](https://intl.cloud.tencent.com/document/product/598)をご参照ください。ここには、いくつかの主なインターフェースだけをリストアップしています。
>
>- [ポリシーの作成](https://intl.cloud.tencent.com/document/product/598/32248)
>- [ポリシーの削除](https://intl.cloud.tencent.com/document/product/598/32247)
>- [ユーザーへのポリシーのバインド](https://intl.cloud.tencent.com/document/product/598/32249)
>- [ユーザーにバインドしたポリシーの解除](https://intl.cloud.tencent.com/document/product/598/32245)
