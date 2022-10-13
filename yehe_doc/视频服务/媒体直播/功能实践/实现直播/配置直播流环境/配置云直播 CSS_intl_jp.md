エンドユーザーがより良いアクセス体験を得られるようにするために、CSSの設定を引き続き行う必要があります。

1. [StreamPackage](https://www.tencentcloud.com/products/mdp)がすでに[CSS](https://www.tencentcloud.com/products/css)製品に接続しているため、システムはCSS内の再生ドメイン名のback-to-origin設定を自動的に完了させます。先ほど作成したStreamPackage Channelに進み、**CDN**タブに切り替え、**Edit Configuration**をクリックして設定を行います。
![](https://qcloudimg.tencent-cloud.cn/raw/91fdb17fa19c8c2cc98a230017b9e2f8.png)

2. ポップアップしたダイアログボックスに、プランニングしたライブストリーミング再生ドメイン名を入力し、送信します。
![](https://qcloudimg.tencent-cloud.cn/raw/3d9b5fc8f4fbffb56fb9a14d17726be5.png)

3. システムの自動設定が完了すると、次のような情報が表示されます。これにはアクセラレーションドメイン名（**Playback Domain Name**）、**CNAME**アドレス、アクセラレーションリージョン（**Acceleration Region**）およびドメイン名のサービスステータス（**Status**）が含まれます。このうち再生ドメイン名のアクセラレーションリージョンはデフォルトでは中国大陸以外および中国香港・マカオ・台湾地区となっています。
![](https://qcloudimg.tencent-cloud.cn/raw/0d0f202a0394c67926da815e460b7ca4.png)

4. ライブストリーミング再生ドメイン名について、例えばアクセス認証、Refererブラックリスト/ホワイトリスト、HTTPSなどのさらに細かい設定を行う必要がある場合は、下のボタン**Go to the CSS CDN Console to Perform More Actions**をクリックするとCSSコンソールにジャンプすることができます。

5. デフォルトの設定でアクセラレーションのニーズが十分に満たされる場合は、この時点でシステムが割り当てた**CNAME**アドレスを記録し、DNSドメイン名管理プラットフォームに進んで、再生ドメイン名のCNAMEの解決設定を完了することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/2696cd0cda9bb9412c4d799457b9698e.png)

6. 最終的にこのライブストリーミングリンクの再生アドレスは、CSS再生ドメイン名にStreamPackageのEndpoint出力パスを加えたものになります。
