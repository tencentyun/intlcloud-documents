## 学習目標

VODでは、リンク不正アクセス防止設定をサポートし、有効時間、再生人数、再生時間などの制御を実装します。本段階のチュートリアルを学習すると、リンク不正アクセス防止を有効にした後に、プレーヤーを使用してビデオを再生する方法を理解できるようになります。

お読みになる前に、プレーヤーガイドの[第1段階：プレーヤーを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)の部分をすでに学習しているか確認してください。このチュートリアルでは、[第1段階](https://intl.cloud.tencent.com/document/product/266/38098)でアクティブ化したアカウントとアップロードしたビデオを使用します。

## ステップ1：リンク不正アクセス防止の有効化

アカウントにおけるデフォルトの配信ドメイン名でKeyリンク不正アクセス防止を有効にしたケースを例にします。
>! 本番環境の現行のネットワークドメイン名に対して直接リンク不正アクセス防止を有効にしないでください。現行のネットワークのビデオが再生できなくなります。

1. VODコンソールにログインし、【配信と再生の設定】 >[ 【ドメイン名管理】 ](https://console.cloud.tencent.com/vod/distribute-play/domain)を選択し、「デフォルト配信ドメイン名」の【設定】をクリックして設定画面に進みます。
<img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. 「Keyリンク不正アクセス防止」の右側の【編集】をクリックして、【Keyリンク不正アクセス防止の有効化】を開き、【ランダムKeyの生成】をクリックしてランダムKey（2WExxx48eW）を生成します。生成できたKeyをコピーしてから、【OK】をクリックすると保存が有効になります。
![](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## ステップ2：プレビューによる再生体験

前の手順では、デフォルトの配信ドメインに対するリンク不正アクセス防止を有効化しました。ここでは、3種類の端末のプレーヤーを使用して、再生結果を素早く体験します。

1. 【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)を選択し、**ステップ1**でアップロードして処理したビデオを探し、「操作」バーの下にある【管理】をクリックし、【プレーヤープレビュー】を選択します。
2. 【プレーヤー設定】はdefaultを選択します。
>? defaultはプリセットのプレーヤー設定で、テンプレート10を再生してアダプティブビットレートストリーミングに変換して出力する際や、テンプレート10でスプライトイメージをキャプチャして出力する際に使用します。

 <img src="https://qcloudimg.tencent-cloud.cn/raw/e66e46d10480c5fb00a2881b275a9cdc.png" width="660" />
3. デフォルト配信ドメイン名がリンク不正アクセス防止を有効にしているため、【再生制御】のオプションタブで、プレビュー時のリンク不正アクセス防止の期限、テスト視聴時間などの選定をサポートしています。ここではデフォルトのパラメータを維持します（再生のリンク不正アクセス防止の期限はデフォルトで1日、プレビュー時間、最大再生可能IP数は入力しません）。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/f08e553a9519fb9974935374f4b4051d.png" width="662" />
4. 【Webプレーヤー】の中で、プレーヤーの中間のボタンをクリックすると、 Web端末での再生が体験できます。
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />
5. 【モバイル端末プレーヤー】で、【スキャンコードのダウンロード】をクリックし、「Tencent Cloudツールキット」をインストールします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0e72b414ee3dc8084dda39d8a5d5c91.png" width="522" />
6. 携帯電話でTencent Cloudツールキットを開き、【プレーヤー】を選択し、右上隅のスキャンコードをクリックすると、モバイル端末で再生を体験できます。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/06e77f14c2e1020e8936ce1ab30a6ca3.png" width="422" />

## ステップ3： Demoを使用して検証

リンク不正アクセス防止を有効にした後、ビデオを再生できるようにするためには、プレーヤーに有効期限内の署名を使用する必要があります。署名ツールを使用して素早く署名を発行できます。

1. [プレーヤー - 署名発行ツール](https://vods.cloud.tencent.com/signature/super-player-sign.html)のページを開き、パラメータを入力します。

 * 【ユーザーappId】：ビデオが属するappId：1400xxx357を入力します（使用するのがサブアプリケーションの場合は、サブアプリケーションのappIdを入力します）。
 * 【ビデオfileId】：ビデオのfileId：528xxx3757278095を入力します。
 * 【現在のUnixタイムスタンプ】：ツールが自動生成した現在のUnix時間（1591516390）。入力不要です。
 * 【署名期限Unixタイムスタンプ】：署名自身の期限。未入力可、デフォルトは1日後に期限切れ。
 * 【リンク期限】：Keyリンク不正アクセス防止期限。6時間後の16進数Unix 時間：5edcf146を入力します。
 * 【リンク不正アクセス防止Key】：前のステップで取得したリンク不正アクセス防止Key：2WExxx48eWを入力します。

2. 【署名の発行】をクリックします。発行された署名が「署名発行結果」のテキストボックスに表示されます。

プレーヤーの署名を取得した後、それぞれ、[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/LiteAVSDK/Player_Android)、[iOS](https://github.com/LiteAVSDK/Player_iOS)という3つの端末のプレーヤーDemoで検証を行えます。詳細については、Demoのソースコードをご参照ください。
>?コンソールの【メディア資産管理】 >[ 【ビデオ管理】 ](https://console.cloud.tencent.com/vod/media)> 【プレーヤープレビュー】では、プレビュービデオに対応するWebプレーヤーのソースコードを取得し、直接参照、使用することができます。
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## まとめ

このチュートリアルの学習を終えると、リンク不正アクセス防止を有効にし、プレーヤーを使用してビデオを再生する方法を理解できたことになります。

次のことをしたい場合：
再生するビデオの内容や形式をカスタマイズする場合、[第3段階：再生内容と形式のカスタマイズ](https://intl.cloud.tencent.com/document/product/266/38293)をご参照ください。
- ビデオの暗号化と暗号化されたビデオを再生する場合、[第4段階：暗号化したビデオの再生](https://intl.cloud.tencent.com/document/product/266/38294)をご参照ください。
