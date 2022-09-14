Web DemoはIM TUIKitを基に実装され、TUIKitにはセッション、チャット、グループ、 個人プロファイル管理などの機能が含まれ、TUIKitを基に積み木のように独自のサービスロジックを素早く構築できます。

## デモンストレーション

### セッション管理

| セッションの開始 | セッションリスト | セッションリスト管理 |
| --- | --- | --- |
| ![](https://qcloudimg.tencent-cloud.cn/raw/562deec9715ae2c50f65e8d40c4d7cac.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/990204616a1c551c36ff5bdc57caa66c.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/695589f54d4ac0b9bb9bc24eb97c7e6d.png) |

### チャット管理

| メッセージリスト | メッセージ送信 | グループチャット管理 |
| --- | --- | --- |
| ![](https://qcloudimg.tencent-cloud.cn/raw/8cb4fd0813a7ce0f3cab8468098dd896.png) |![](https://qcloudimg.tencent-cloud.cn/raw/f931993108c14ba3b2e628e4ed50a316.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/bb9b0449eb712f9e6fececfdb199418a.png) |



| 機能  | 説明  |
| --- | --- |
| セッション管理 | 1. ユーザーによる1人/多人数のセッションの開始に使用<br/>2. ユーザーのセッションリストの表示に使用<br/>3. ユーザーのセッションリストの管理に使用 |
| チャット管理 | 1. メッセージリストの表示に使用<br/>2. メッセージの送信に使用<br/>3. グループチャットの管理に使用 |


## クイックスタートステップ

### ステップ1：ソースコードのダウンロード

実際のサービス要求に基づいて、SDKと付属の[Demoソースコード](https://github.com/TencentCloud/TIMSDK)をダウンロードします。

```shell
# コマンドラインの実行
git clone https://github.com/TencentCloud/TIMSDK.git

# Webプロジェクトに参加

cd TIMSDK/Web/Demo

# demo依存のインストール
npm install

cd TIMSDK/Web/Demo/src/TUIKit

# TUIKit依存のインストール
npm install
```

### ステップ2：初期化
1. 端末のディレクトリのプロジェクトを開いて、対応するGenerateTestUserSigファイルを見つけてください。パス：/debug/GenerateTestUserSig.js。
2. GenerateTestUserSigファイルの関連パラメータを設定します。そのうち、SDKAppIDとキーなどの情報は、[IMコンソール](https://console.cloud.tencent.com/im)から取得し、対象のアプリケーションカードをクリックして、アプリケーションの基本設定ページに移動します。 [![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)](https://camo.githubusercontent.com/20575292024f27b76db87d6688e57f16d38b579b249054466668b596975dd30e/68747470733a2f2f71636c6f7564696d672e74656e63656e742d636c6f75642e636e2f7261772f65343335333332636461386439656337666561323162643935663761306362612e706e67)
3. **基本情報**のところで、**キーの表示**をクリックし、GenerateTestUserSigファイルにキー情報をコピーして保存します。


> !ここで言及するUserSigの取得方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適しています**。UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し、動的にUserSigを取得します。詳細については、[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

### ステップ3：プロジェクトの起動

```shell
# プロジェクトの起動
npm run serve
```

- [SDK APIマニュアル](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [SDK更新ログ](https://intl.cloud.tencent.com/document/product/1047/34281)
- [Demoソースコード](https://github.com/TencentCloud/TIMSDK/tree/master/Web/Demo)
