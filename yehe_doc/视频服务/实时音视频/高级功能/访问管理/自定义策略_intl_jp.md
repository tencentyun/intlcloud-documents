>!ここでは主に**Tencent Real-Time CommunicationTRTC **のCloud Access Management（CAM）機能関連コンテンツについて紹介します。他製品のCAM関連コンテンツについては、[CAMサポート製品](https://intl.cloud.tencent.com/document/product/598/10588)をご参照ください。

TRTCのCAMにおいて[プリセットポリシー](https://intl.cloud.tencent.com/document/product/647/39550)を使用して権限付与を行うのは簡便ではありますが、プリセットポリシーは権限制御の粒度が比較的粗く、[TRTCアプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)や[Tencent Cloud API](https://intl.cloud.tencent.com/product/api)の粒度まで細分化することができません。きめ細かい権限制御機能を必要とする場合は、カスタムポリシーを作成する必要があります。

## カスタムポリシーの作成方法

カスタムポリシーを作成するには、さまざまな方法があります。次の表に、それぞれの方法の比較を示します。具体的な操作手順については、以下の文章をご参照ください。
<table>
<thead><tr><th width="20%%">エントリーの作成</th><th>作成方法</th><th>効果（Effect）</th><th>リソース（Resource）</th><th>操作（Action）</th><th>柔軟性</th><th>難易度</th></tr>
</thead>
<tbody><tr>
<td><a href="https://console.cloud.tencent.com/cam/policy">CAMコンソール</a></td>
<td>ポリシージェネレーター</td>
<td>手動選択</td>
<td>構文の記述</td>
<td>手動選択</td>
<td>中</td>
<td>中</td>
</tr>
<tr>
<td><a href="https://console.cloud.tencent.com/cam/policy">CAMコンソール</a></td>
<td>ポリシー構文</td>
<td>構文の記述</td>
<td>構文の記述</td>
<td>構文の記述</td>
<td>高</td>
<td>高</td>
</tr>
<tr>
<td>CAMサーバーAPI</td>
<td><a href="https://intl.cloud.tencent.com/document/product/598/32248">CreatePolicy</a></td>
<td>構文の記述</td>
<td>構文の記述</td>
<td>構文の記述</td>
<td>高</td>
<td>高</td>
</tr>
</tbody></table>

> ?
>- TRTCは、製品の機能またはアイテムに応じたカスタムポリシーの作成は**サポートしていません**。
>- **手動選択**とは、ユーザーがコンソールに表示される候補リストからオブジェクトを選択することを意味します。
> - **構文の記述**とは、[アクセスポリシー構文](#grammar)によってオブジェクトを記述することを意味します。

<span id="grammar"></span>
## アクセスポリシー構文
<span id="s_grammar"></span>
### リソース構文の記述

上記のように、TRTC権限管理のリソース粒度はアプリケーションです。アプリケーションのポリシー構文の記述法は、[CAMリソース記述法](https://intl.cloud.tencent.com/document/product/598/10606)に従います。以下の例では、開発者のルートアカウントIDは12345678で、開発者は、SDKAppIDがそれぞれ1400000000、1400000001および1400000002のアプリケーションを3つ作成しています。

- TRTCのすべてのアプリケーションのポリシー構文の記述
```
  "resource": [
    "qcs::trtc::uin/12345678:sdkappid/*"
  ]
```
- 単一アプリケーションのポリシー構文の記述
```
  "resource": [
    "qcs::trtc::uin/12345678:sdkappid/1400000001"
  ]
```
- 複数アプリケーションのポリシー構文の記述
```
  "resource": [
    "qcs::trtc::uin/12345678:sdkappid/1400000000",
    "qcs::trtc::uin/12345678:sdkappid/1400000001"
  ]
```
<span id="c_grammar)"></span>
### 操作構文の記述

上記のとおり、TRTCの権限管理の操作粒度はTencent Cloud APIです。詳細については、[権限付与可能なリソースと操作](https://intl.cloud.tencent.com/document/product/647/39549)をご参照ください。次の例では、`DescribeAppStatList`（アプリケーションリストの取得）、`DescribeSdkAppInfo`（アプリケーション情報の取得）などのTencent Cloud APIを例として取り上げています。
- TRTCのすべてのTencent Cloud APIのポリシー構文の記述
```
  "action": [
    "name/trtc:*"
  ]
```
- 単一のTencent Cloud APIを操作する際のポリシー構文の記述
```
  "action": [
    "name/trtc:DescribeAppStatList"
  ]
```
- 複数のTencent Cloud APIを操作する際のポリシー構文の記述
```
  "action": [
    "name/trtc:DescribeAppStatList",
    "name/trtc:DescribeTrtcAppAndAccountInfo"
  ]
```

## カスタムポリシー使用例

### ポリシージェネレーターの使用

以下の例では、カスタムポリシーを作成します。このポリシーはサーバーAPI`RemoveUser`を除くすべての操作を、TRTCアプリケーション1400000001で実行できます。

1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[【ポリシー】](https://console.cloud.tencent.com/cam/policy)にアクセスし、【カスタムポリシーの新規作成】をクリックします。
2. 【ポリシージェネレーターで作成】を選択して、ポリシー作成ページに進みます。
3. サービスと操作を選択します。
   - 【効果(Effect)】設定項目は、【許可】を選択します。
   - 【サービス(Service)】設定項目は、【TRTC】を選択します。
   - 【操作(Action)】設定項目は、すべての項目にチェックを入れます。
   - 【リソース(Resource)】設定項目には、[リソース構文の記述](#s_grammar)の説明に従って`qcs::trtc::uin/12345678:sdkappid/1400000001`を入力します。
   - 【条件(Condition)】設定項目は設定不要です。
   - 【ステートメントの追加】をクリックすると、ページの一番下に「TRTCアプリケーション1400000001に対するあらゆる操作を許可する」というステートメントが表示されます。
4. 同じページに別のステートメントを続けて追加します。
   - 【効果(Effect)】設定項目は、【拒否】を選択します。
   - 【サービス(Service)】設定項目は、【TRTC】を選択します。
   - 【操作(Action)】設定項目は、`RemoveUser`（検索機能で速やかに見つけられます）にチェックを入れます。
   - 【リソース(Resource)】設定項目には、[リソース構文の記述](#s_grammar)の説明に従って`qcs::trtc::uin/12345678:sdkappid/1400000001`を入力します。
   - 【条件(Condition)】設定項目は設定不要です。
   - 【ステートメントの追加】をクリックすると、ページの一番下に「TRTCアプリケーション1400000001に対する`RemoveUser`操作を拒否する」というステートメントが表示されます。
5. 【次のステップ】をクリックし、必要に応じてポリシー名を変更します（または変更しなくてもかまいません）。
6. 【完了】をクリックし、カスタムポリシーの作成を完了します。

その後、このポリシーを他のサブアカウントに付与する方法は、[TRTCの完全な読み取り/書き込みアクセス権限を既存のサブアカウントに付与する](https://intl.cloud.tencent.com/document/product/647/39550#FullRW)と同様です。


### ポリシー構文の使用

以下の例では、カスタムポリシーを作成します。このポリシーは、1400000001と1400000002という2つのTRTCサブアプリケーションですべての操作を実行できますが、1400000001の`PRemoveUser`操作は拒否します。

1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[【ポリシー】](https://console.cloud.tencent.com/cam/policy)にアクセスし、【カスタムポリシーの新規作成】をクリックします。
2. 【ポリシー構文で作成】を選択し、ポリシー作成ページに進みます。
3. 【テンプレートタイプの選択】ボックスで【空白テンプレート】を選択します。
   
   >?ポリシーテンプレートは、新しいポリシーが既存のポリシー（プリセットポリシーまたはカスタムポリシー）をコピーしてから、それをベースとして調整が行われることを意味します。実際の使用においては、開発者は状況に応じて適切なポリシーテンプレートを選択することで、ポリシー内容の難しい入力と作業の負荷を軽減することができます。
4. 【次のステップ】をクリックし、必要に応じてポリシー名を変更します（または変更しなくてもかまいません）。
5. 【ポリシー内容の編集】ボックスにポリシー内容を入力します。この例のポリシーの内容は次のとおりです。
```
   {
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/trtc:*"
            ],
            "resource": [
                "qcs::trtc::uin/12345678:sdkappid/1400000001",
                "qcs::trtc::uin/12345678:sdkappid/1400000002"
            ]
        },
        {
            "effect": "deny",
            "action": [
                "name/trtc:RemoveUser"
            ],
            "resource": [
                "qcs::trtc::uin/12345678:sdkappid/1400000001"
            ]
        }
    ]
   }
```
>? ポリシーの内容は、[CAMポリシー構文ロジック](https://intl.cloud.tencent.com/document/product/598/10603)に従う必要があります。リソースと操作という2つの要素の構文は、それぞれ上述の[リソース構文の記述](#s_grammar)と [操作構文の記述](#c_grammar)のとおりです。
6. 【ポリシーの作成】をクリックして、カスタムポリシーの作成を完了します。

その後、このポリシーを他のサブアカウントに付与する方法は、[TRTCの完全な読み取り/書き込みアクセス権限を既存のサブアカウントに付与する](https://intl.cloud.tencent.com/document/product/647/39550#FullRW)と同様です。

### CAMが提供するサーバーAPIの使用

ほとんどの開発者にとって、コンソールで権限管理操作が完了すれば、ビジネスニーズが満たされたことになります。ただし、権限管理機能を自動化・システム化する必要がある場合は、サーバーAPIを使用することができます。
ポリシー関連のサーバーAPIはCAMに属します。詳細については、[CAM公式ウェブサイトドキュメント](https://intl.cloud.tencent.com/document/product/598)をご参照ください。ここには、いくつかの主なインターフェースだけをリストアップしています。

- [ポリシーの作成](https://intl.cloud.tencent.com/document/product/598/32248)
- [ポリシーの削除](https://intl.cloud.tencent.com/document/product/598/32247)
- [ユーザーへのポリシーのバインド](https://intl.cloud.tencent.com/document/product/598/32249)
- [ユーザーにバインドしたポリシーの解除](https://intl.cloud.tencent.com/document/product/598/32245)
