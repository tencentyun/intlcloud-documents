## 概要

Tencent Cloud StreamPackageは、Tencent Cloudが新たにリリースした高品質のビデオパッケージングおよびオリジンサーバープラットフォームです。世界中のユーザーにプロフェッショナルで安全かつ安定したビデオパッケージングおよび配信サービスを提供することをお約束します。ビデオパッケージ配信の難易度を引き下げ、オリジンレジリエンシー（origin resiliency）を高め、動画サプライヤーが安全かつ安定的に大規模なビデオストリームメディアを配信できるようにします。

StreamPackageコンソールは、Channelディメンションをベースとして管理されます。ビデオコンテンツを再構築することにより、エンコード・圧縮されたビデオトラックとオーディオトラックが所定の形式でライブストリーミングオリジンサーバーに配置されます。そのため、動画サプライヤーは、ビデオストリームメディアを大規模・安全・安定的に配信することができます。

## コンソール概要

StreamPackageコンソールは、豊富で役立つ機能とシンプルでフレキシブルなアクセス体験を提供します。StreamPackageコンソールは、Channelディメンションをベースとして管理され、全体をChannel、Input、Endpoint、CDN構成という4つのモジュールに分割できます。

![img](https://main.qcloudimg.com/raw/2d70be467d74639158d0be4ea94692d2.png)

## 前提条件

- CDN再生に用いられるドメイン名（配信にTencent Cloud CSS CDNを使用する必要がある場合）。
- すでに[Tencent Cloud CSSサービスがアクティブ化されています](https://console.cloud.tencent.com/live)。
- [Tencent Cloud StreamPackageコンソール](https://console.cloud.tencent.com/mdp/channel)にログインします。


## 操作手順

### 1.   アベイラビリティーゾーンの選択

現在、Tencent Cloud StreamPackageには、インドのムンバイ、タイのバンコク、韓国のソウルに3つのアベイラビリティーゾーンを提供しており、お客様はここで所在するリージョンを選択することができます。日本の東京などのリージョンでは、アクセラレーションのデプロイがリリースされているところです。他のアベイラビリティーゾーンにおけるアクセラレーションのデプロイのリクエストがある場合は、[お問い合わせください](https://intl.cloud.tencent.com/contact-sales)。

![img](https://main.qcloudimg.com/raw/d939a324316775e3ccef4c4658599b48.png)

### 2.   Channelの作成

Channelとは、入力ストリームと出力ストリームの基本構成です。ユーザーは、作成が完了したChannelをベースとして所定のプロトコルのCSSストリームを入力することも、CSSストリームの出力と配信に対応するback-to-originノード（Endpoint）を作成することもできます。

1. 【Create Channel】をクリックして、新しいChannelを作成します。
2. Channel Nameを入力し、Channel入力プロトコルを選択します（HLS/DASHをサポート）。

![img](https://main.qcloudimg.com/raw/f545e69458ff80b55c6775219d574374.png)

3. 選択したHLS/DASHプロトコルの関連パラメータを入力します。

- **Max Segment Duration**は、このChannelにプッシュするHLS/DASH形式ストリームのts/m4sスライスの最大ファイル分割時間を示します。この設定パラメータのデフォルト値は15sです。
- **Max Playlist Duration**は、このChannelにプッシュするHLS/DASH形式ストリームのm3u8/mpdリストの最大合計時間を示します。この設定パラメータのデフォルト値は600sです。お客様がプッシュしたm3u8/mpdリストの実情に応じて変更できます。

>? お客様が作成したこのChannelがマスタ・スレーブチャネルという2つのストリームを同時にプッシュし、プライマリストリームが異常なときにバックアップストリームにすばやく切り替えることができる場合は、この設定パラメータを分割ファイルの実際の最大時間よりも少し大きく設定することをお勧めします。これによって、より良く、より速やかに切り替えることができます。

4. 【Create】をクリックして、作成を完了します。

### 3.   Channelの確認

#### Channel情報の確認

作成が完了すると、すぐにChannelの詳細画面にジャンプします（Channel名をクリックするか、右側の【Info】をクリックしてChannelの詳細画面に進みます）。詳細画面には、ChannelのName、ID（バックエンドによって自動的に生成されます）、指定された入力プロトコルおよび関連する設定パラメータが表示されます。また、指定されたプロトコルに基づいて2つの入力ポイント（Input）が自動的に生成されます。

![img](https://main.qcloudimg.com/raw/d962c942d07f8303832d070c7d0d2a26.png)

#### Inputの確認

InputはChanne入力の基本単位です。バックエンドは作成済みのChannelをベースとして、2つのInputノードと対応する入力URLを自動的に生成します。ユーザーはCSSストリームをノードのURLにプッシュすることができます。

![img](https://main.qcloudimg.com/raw/9fc040a6cb575be7411327476f0fe7a1.png)

InputモジュールはAuthentication操作をサポートしており、ユーザーは入力ポイント毎に個別にAuthenticationの設定を行うことができます。 ユーザーは操作バーの【Authentication】をクリックしてポップアップボックスに入り、![img](file:///C:/Users/JACKYS~1/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)をクリックしてAuthenticationの設定を開きます。バックエンドがこの入力ノードのUsernameとPasswordを自動的に生成し、http認証モードで認証が行われます。【Rotate credentials】をクリックして、Authentication設定を完了します。

![img](https://main.qcloudimg.com/raw/6927ebe8232a26cb341aa1b69f008e45.png)

>! ユーザーがRotate credentialsを行うと、既存のChannel credentialは無効になります。

#### Endpointsの作成

ユーザーは、Channel毎にback-to-originプルのEndpointノードを作成できます。

1. 【Create Endpoint】をクリックしてノードを作成します。

![img](https://main.qcloudimg.com/raw/ce143b55735dee33f7e708c5ea19f89a.png)

2. Endpoint Nameを入力します。Endpoint Typeは、デフォルトの場合、Channelの入力プロトコルと同様です。

3. ユーザーは必要に応じて、IPブラックリスト/ホワイトリスト、Authkeyなどの機能を有効にするかどうか選択できます。

- IPブラックリスト/ホワイトリスト：適法なストリームのIPセグメントを固定してプルするか、または異常なIPエンドをプッシュすることを拒否します。
- Authkeyの設定：X-TENCENT-PACKAGEによるhttp-headerの認証をサポートしています。

![img](https://main.qcloudimg.com/raw/d6a261b21e2c020365f6aa789c95e0dd.png)

4. 【Create】をクリックして設定を保存すると、作成が完了します。作成済みのEndpointは、編集および削除操作をサポートします。 ユーザーは生成されたEndpoint URLをベースにback-to-originのプル操作を行い、CSSストリームを配信できます。

![img](https://main.qcloudimg.com/raw/219346607e144822c43173ba1e055905.png)

#### CDN配信の設定

StreamPackageは、ChannelでのライブストリーミングCDNの設定をサポートします。設定が完了したら、ライブストリーミングCDNを介してStreamPackage ChannelにおけるCSSストリームを直接配信できます。 これには、まずCSSをアクティブ化し、StreamPackageとCSSの**双方向認証**操作を完了する必要があります。

以下の内容をお読みになる前に、関連用語についてご説明します。

- ライブストリーミングCDN：標準ライブストリーミング（CSS）におけるCDNです。StreamPackageはこの機能を統合および多重化して、StreamPackageのChannelにおけるCSSストリームをCSSのCDNを介してスピーディに配信、再生することができます。
- CDNドメイン名/CDN再生ドメイン名：CSS CDNにおける再生ドメイン名で、CSSストリームの配信に用いられます。

1. CSSサービスのアクティブ化

Tencent CloudのCDNを設定する前に、あらかじめ[Tencent Cloud CSSサービスがアクティブ化されている](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)ことを確認してください。

2. StreamPackageに対するCSSへのアクセス権の付与

StreamPackageコンソールに戻り、CDN配信を設定する必要があるChannelの詳細画面を開き、CDNオプションを選択し、下の【Authorization】をクリックして、StreamPackageに対するCSSサービスへのアクセス権の付与プロセスを開始します。

>? StreamPackageに対するCSSへのアクセス権の付与を完了すると、StreamPackageはChannelにライブストリーミング再生ドメイン名を作成できるようになります。

![img](https://main.qcloudimg.com/raw/d0f1bc546937e0fbbb111bd6d97f2557.png)

**【Click here】をクリックして、StreamPackageに対しCSS CDNの使用権を付与します.**StreamPackage機能を使用するには、StreamPackageがお客様の一部リソースにアクセスできるようにする必要があります。これらのリソースは、サービスロールを介してこれらの権限を付与されたリソースにアクセスし、現在の機能を実装します。【Authorization Now】をクリックして【ロール管理】にジャンプし、【Grant】をクリックして関連サービスAPIへのアクセス権をStreamPackageに付与します。

![img](https://main.qcloudimg.com/raw/c2e6a9006094003091539f31d1d4c63c.png)

![img](https://main.qcloudimg.com/raw/a6476145b574ebbfe7f828dbbbfce984.png)

![img](https://main.qcloudimg.com/raw/b18b2fbb7440d557ee82093d44660258.png)

自動的にStreamPackageコンソールに戻るので、【Authorize completed】をクリックし、StreamPackageにCSS CDNの使用権が付与されたことを確認します。

![img](https://main.qcloudimg.com/raw/2e7a6e29600485b593323658cf738b7d.png)

![img](https://main.qcloudimg.com/raw/3374604fff9c19ec580eb6a43af7f86e.png)

【Next】をクリックして次のステップに進みます。

3. CSSに対するStreamPackageへのアクセス権の付与

**【Click here】をクリックしてCDNコンソールに移動し、CSS CDNに対しStreamPackagsの使用権を付与します。CSSコンソールの権限付与のステータスが【Activated】に変わっています。**

![img](https://main.qcloudimg.com/raw/3be8efcd4c8302b15df46be54daebed4.png)

![img](https://main.qcloudimg.com/raw/c63def0152b6d95901929b7abc093d59.png)

StreamPackageコンソールインターフェースに戻り、【Complete】をクリックして、権限付与が完了したことを確認します。

![img](https://main.qcloudimg.com/raw/2616575aa0b6d56323eafcfac0aec9f8.png)

このとき、CSS CDNに対しStreamPackageの使用権が付与されていることが表示されます。下の【Authorization Completed】をクリック**した時点で、StreamPackageとCSSの双方向の権限付与が完了します（StreamPackageのChannelを介してCDN再生ドメイン名をすばやく作成でき、CSSもChannelに戻ってプルと配信を行うことができます）**

![img](https://main.qcloudimg.com/raw/5e3084a78e0ce61a0a9eabd5a61c9a90.png)

4. CDN再生ドメイン名のすばやい設定

上記の双方向の権限付与が完了したら、CDNオプションバーを開き、【Edit Configuration】をクリックすると、CDNをすばやく設定することができます。

![img](https://main.qcloudimg.com/raw/4d2031b1fe8c42a1a05c7b619291e1dd.png)

CDNの再生に使用するドメイン名を入力し、【Confirm】をクリックすれば、設定完了です。

![img](https://main.qcloudimg.com/raw/ee8a3bf7ab68b655bba010df76bac910.png)

![img](https://main.qcloudimg.com/raw/1fd6d414ef8fb41cee52c0a489c79395.png)

>?
>- 新しく作成された再生ドメイン名の追加が成功した後、システムは一つのCNAMEドメイン名（`.liveplay.myqcloud.com`を拡張子とする）を自動的に割り当てます。CNAMEドメイン名は直接アクセスできませんので、ドメイン名サービスプロバイダでCNAMEの設定を完了する必要があります。設定が有効になると、CSSサービスを利用できるようになります。CNAMEに関する操作については、[CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)
>- StreamPackageに設定されたCDN再生ドメイン名の再生リージョンは、デフォルトでは中国本土以外の海外リージョン（中国香港・中国台湾・中国マカオを含む）になります。中国本土リージョンでライブストリーミングの配信を行う必要がある場合は、中国本土の関連法規制に従って、再生ドメイン名のICP登録を行う必要があります。【Go to CSS CDN console】をクリックしてCSSコンソールに移動し、その他の操作を実行してください。

#### 設定された再生ドメイン名を介した再生

StreamPackageのChanne設定がCDN再生ドメイン名にバインドされたら、Endpointの再生アドレスのドメイン名をCDN再生ドメイン名に置き換えれば正常に再生ができます。

例：

お客様のいずれかのChannelのEndpointプルストリーミングアドレスは、次のとおりです。

http://123456789.ap-seoul.StreamPackage.srclivepull.myqcloud.com/v1/017697a3513109df73abda3c4b26/017697a918bf09dfabc033b04d43/main.m3u8

お客様のCDN再生アドレスは次のとおりです。

http://CDN再生ドメイン名/v1/017697a3513109df73abda3c4b26/017697a918bf09dfabc033b04d43/main.m3u8

設定が完了したら、より良いユーザーエクスペリエンスを確保するために設定を最適化しますので、当社までご連絡ください。

>? ライブストリーミングCDNを使用して配信と再生を行う場合、ライブストリーミングトラフィック料金が発生します。詳細については、[CSS料金](https://intl.cloud.tencent.com/zh/document/product/267/2818?lang=zh&pg=)をご参照ください。

### 4.   Channelの編集と削除

ユーザーはChannelリスト画面で、作成済みのすべてのChannelを管理できます。 操作バーの右側にある【Info】/【Edit】/【Delete】をクリックすると、Channelの詳細を確認したり、Channelの再編集や削除操作を行ったりすることができます。Channelにすでにendpointノードがある場合、削除はサポートされません。Channelを削除する必要がある場合は、まず含まれているすべてのEndpointノードを削除する必要があります。

![img](https://main.qcloudimg.com/raw/bd7b3e8c0033d6591f5b61b2974dc12a.png)