## 操作シナリオ

TEMは、**アプリケーションインスタンス+CFS**を通じて静的ウェブサイトリソースホスティング機能を提供します。ここでは、業界で人気のある静的ウェブサイトサービス[Hugo](https://gohugo.io/)を例として取り上げ、静的リソースホスティングのベストプラクティスをご提供します。以下では、Hugoを介してパーソナルな静的ブログを作成し、次にTEMを介してリバースプロキシアプリケーションをデプロイし、CFSと連携して静的リソースを管理し、最後にTEMが提供するアクセス設定を介してパブリックネットワーク上のパーソナルな静的ブログへのアクセスを提供します。

全体的な流れは、以下のとおりです。
<dx-steps>
- [静的ウェブサイトのローカル開発](#step1)
- [静的ウェブサイトのリソースをTencent Cloud CFSにアップロードします](#step2)
- [TEMにnginxアプリケーションをデプロイしてCFSを関連付けます](#step3)
- [TEMでnginxネットワークアクセスを設定し、外部アクセスアドレスを提供します](#step4)
- [（オプション）ドメイン名を設定します](#step5)
- [（オプション）Webファイアウォールを設定します](#step6)
- [（オプション）CDNを設定し、アクセスをアクセラレーションします](#step7)
</dx-steps>


## 操作手順

### 手順1：Hugoを使用してローカルで静的ブログを作成する[](id:step1)

1. Hugoをインストールします（[Install Hugo](https://gohugo.io/getting-started/installing/)をご参照ください）。
   MacOSシステムを例として、次のコマンドを使用してインストールします。
   ```
   brew install hugo
   ```

2. 次のコマンドを実行して、静的サイトを作成します。
   ```
   hugo new site quickstart
   ```

3. 次のコマンドを実行して、トピックを追加します。
   ```
   cd quickstart
   git init
   git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
   echo theme = \"ananke\" >> config.toml
   ```

4. 次のコマンドを実行して、ブログを追加します。
   ```
   hugo new posts/my-first-post.md
   ```

5. 次のコマンドを実行して、静的ページを作成します。
   ```
   hugo -D
   ```

6. 作成された静的コンテンツは、quickstartプロジェクトの`public/`ディレクトリに保存されます。
   ![](https://main.qcloudimg.com/raw/1719df20926f87db5edd93d32dbde0fd.png)


### 手順2：静的なブログコンテンツをCFSにアップロードする[](id:step2)

1. [CFS：ファイルシステムとマウントポイントの作成](https://intl.cloud.tencent.com/document/product/582/9132)を参照して、CFSファイルシステムを購入します。
>!購入したCFSファイルシステムの**リージョン**、**VPCネットワーク**は、アプリケーションがTEMにデプロイされているリージョンと一致している必要があります。

2. [CFS：LinuxクライアントでCFSファイルシステムを使用する](https://intl.cloud.tencent.com/document/product/582/11523)または[CFS：WindowsクライアントでCFSファイルシステムを使用する](https://intl.cloud.tencent.com/document/product/582/11524)を参照して、hugoによって作成された`public/`ディレクトリ内のファイルをCFSファイルシステムのルートディレクトリまたはサブディレクトリにアップロードします。

### 手順3： [TEMにnginxアプリケーションをデプロイしてCFSを関連付ける[](id:step3)

1. [TEMコンソール](https://console.cloud.tencent.com/tem)にログインして、上記で購入したCFSインスタンスをアプリケーションがデプロイされている環境に関連付けます。
![](https://main.qcloudimg.com/raw/d2858f803e8474380c1206915e03e626.png)

2. 【[アプリケーション管理](https://console.cloud.tencent.com/tem/service)】ページで、hugoという名前のアプリケーションを作成します。
![](https://main.qcloudimg.com/raw/bfc007fc364660b1c5daad9338d335a2.png)

3. アプリケーションをデプロイし、【永続ストレージ】モジュールで関連付けたCFSストレージリソースを選択します。
![](https://main.qcloudimg.com/raw/f2572a6c66c2fee650d76023743e8878.png)


### 手順4：TEMでnginxのネットワークアクセスを設定する[](id:step4)
<dx-tabs>
::: 方法1：転送ルールを設定する（推奨）
1. 【[アプリケーション管理](https://console.cloud.tencent.com/tem/service)】ページで、作成したアプリケーションの「ID」をクリックして、アプリケーションの基本情報ページに進みます。
2. アプリケーションの基本情報ページの【アクセス設定】モジュールで、【設定に進む】をクリックして環境アクセス設定ページに進みます。
![](https://main.qcloudimg.com/raw/4f16499afcd31f7b4136c8d5a16f1c61.png)


3. 環境アクセス設定ページで、【新規作成】をクリックしてアクセス設定ルールを作成します。
![](https://main.qcloudimg.com/raw/e8440aca09c91e9708f79b541be0b654.png)


4. 【完了】をクリックすると、以下のIPアドレスが取得できます。
![](https://main.qcloudimg.com/raw/eff13968a748aee73038c5872eeba877.png)

作成されたアドレスを介してhugoサービスにアクセスします。

![](https://main.qcloudimg.com/raw/9b76fee79a65e46760235629b05f244f.png)
:::
::: 方法2：パブリックネットワークCLBを設定する
1. 【[アプリケーション管理](https://console.cloud.tencent.com/tem/service)】ページで、作成したアプリケーションの「ID」をクリックして、アプリケーションの基本情報ページに進みます。
2. アプリケーションの基本情報ページの【アクセス設定】モジュールで、右上隅の【編集と更新】をクリックしてパブリックネットワークCLBを追加します。
![](https://main.qcloudimg.com/raw/6918a7617bf37075720c5e52a0a6380e.png)

3. パブリックネットワークアクセス方法を選択し、ポートマッピング関係を入力します。
![](https://main.qcloudimg.com/raw/6a489898e6a838ef7fb7ec8d4aac0dae.png)

4. 【サブミット】をクリックすると、以下のパブリックネットワークアクセスIPを取得できます。
![](https://main.qcloudimg.com/raw/5bdaa679fb1c13315cec399826af2a1a.png)

作成されたアドレスを介してhugoサービスにアクセスします。

![](https://main.qcloudimg.com/raw/fceeebcacde7f9b68a726d7777b8ca90.png)
:::
</dx-tabs>


### 手順5：（オプション）ドメイン名を設定する[](id:step5)

1. ドメイン名を登録します。
2. ドメイン名を上記で作成したCLBインスタンスに関連付けると、ドメイン名を介して静的ウェブサイトにアクセスできるようになります。[ドメイン名がCLBを指定するようにDNS解決DNSPodを設定する](https://intl.cloud.tencent.com/document/product/214/8975)をご参照ください。

### 手順6： （オプション）ファイアウォールを設定する[](id:step6)

**転送構成**の設定を介して静的ウェブサイトにアクセスする場合は、Tencent Cloudの[Web Application Firewall](https://intl.cloud.tencent.com/product/waf)と組み合わせて静的ウェブサイトのセキュリティ保護を行うことができます。詳細な設定については、[Cloud Load Balanceのリスニングドメイン名に対してWebセキュリティ保護を実行するようにWAFを設定する](https://intl.cloud.tencent.com/document/product/214/38751)をご参照ください。

### 手順7： （オプション）CDNを設定する[](id:step7)

より良いユーザーエクスペリエンスを提供するために、静的ウェブサイトは通常、CDNと組み合わせてアクセスをアクセラレーションします。ホスティングされている静的ウェブサイトはTencent Cloud CDNと組み合わせることができます。[Tencent Cloud CDN初心者ガイド](https://intl.cloud.tencent.com/document/product/228/36383)をご参照ください。
