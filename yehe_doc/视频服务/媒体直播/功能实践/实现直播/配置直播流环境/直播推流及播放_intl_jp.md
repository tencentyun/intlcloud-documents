ここではOBS、VLCをプッシュおよび再生ツールとする場合を例とします。OBSのプッシュ設定でStreamLiveのInputプッシュアドレスを入力します。1行目のサーバーにはプッシュドメイン名+アプリケーション名を、2行目のストリームキーにはストリーム名をそれぞれ入力します。下の図をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/d19308151baf27053d3ef774f416274c.png)

VLCを開き、FileメニューでOpen Networkを選択し、ネットワークライブストリーミングアドレスを入力します。ここで、先ほど事前に記録したStreamPackageのEndpointアドレスを入力し、その中のドメイン名をCSSに設定済みの再生ドメイン名の代わりに入力すると、再生を行うことができます。
![](https://qcloudimg.tencent-cloud.cn/raw/e5d6e5f9c304f6b38fffafca19c0b456.png)

これで、StreamLive+StreamPackage+CSSを合わせて構築した、信頼性の高いCSSプラットフォームが正常に安定して動作できるようになりました。
![](https://qcloudimg.tencent-cloud.cn/raw/3096992f56506043045b681624e12770.png)