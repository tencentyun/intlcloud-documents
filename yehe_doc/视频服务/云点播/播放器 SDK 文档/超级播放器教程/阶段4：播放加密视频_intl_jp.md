## 学習目標

本段階のチュートリアルを学習することで、ビデオを暗号化し、Super Playerを使用して暗号化後のビデオを再生する方法を把握することができます。

これを読む前に、先にSuper playerガイドの[段階1：Super playerを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098) と[段階2：リンク不正アクセス防止を有効にした後のビデオ再生](https://intl.cloud.tencent.com/document/product/266/38292) セクションを確実に学習しておくようにしてください。本チュートリアルでは[段階1](https://intl.cloud.tencent.com/document/product/266/38098) セクションでアクティブ化したアカウントおよびアップロードしたビデオを使用し、[段階2](https://intl.cloud.tencent.com/document/product/266/38292)にしたがってリンク不正アクセス防止を有効化する必要があります。

[](id:step1)
## 手順1：ビデオの暗号化
1. VODコンソールにログインし、**メディア資産管理**>[**ビデオ管理**](https://console.cloud.tencent.com/vod/media)を選択し、処理するビデオ（FileId：528xxx3757278095）にチェックを入れて、**メディアプロセッシングサービス**をクリックします。
2. メディアプロセッシングサービスの画面で：
 - **処理タイプ**は**タスクフロー**を選択します。
 - **タスクフローのテンプレート**は**SimpleAesEncryptPreset**を選択します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/810b84b193ad96be992810e3877b1ac7.png" width="700" /><span>
>? 
>- SimpleAesEncryptPresetはプリセットのタスクフローです。テンプレート12を使用してアダプティブビットレートストリーミングへのトランスコーディングを行い、テンプレート10をしようしてカバー画像のキャプチャを行い、テンプレート10を使用してスプライトイメージのキャプチャを行います。
>- テンプレート12のアダプティブビットレートストリーミングはトランスコーディングして暗号化したマルチビットレートによる出力です。
3. **OK**をクリックします。「ビデオ状態」欄が「処理中」から「正常」に変わると、ビデオの処理が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/da5e02a95cf19cae9146e009874ccf55.png)
4. ビデオの「操作」欄の下の**管理**をクリックし、管理画面に入ります：
 - 「基本情報」タブを選択すると、生成したカバー画像、および暗号化したアダプティブビットレートストリーミングの出力（テンプレートID：12）が表示されます。
 - 「スクリーンキャプチャ情報」タグを選択すると、生成したスプライトイメージ（テンプレートID：10）を見ることができます。

[](id:step2)
##  手順2：プレビューによる再生体験

前の手順で、ビデオをすでにアップロードし、ビデオに対する処理を行いました。ここでは、3種類の端末のSuper playerを使用して、再生の効果を素早く体験します。

1. **メディア資産管理**>[**ビデオ管理**](https://console.cloud.tencent.com/vod/media)を選択して、**手順1**によるアップロード済み、処理済みのビデオを見つけ、「操作」バーの下の**管理**をクリックして、**Super Playerプレビュー**を選択します。
2. **Super Player設定**はbasicDrmPresetを選択します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/60418fcab52a70fc2fbcf7056f7929f2.png" width="722" />
>? basicDrmPresetはプリセットのSuper player設定で、テンプレート12を使用したアダプティブビットレートストリーミングへのトランスコーディングの出力、およびテンプレート10を使用したスプライトイメージキャプチャの出力に使用します。
3. デフォルトの配信ドメイン名がリンク不正アクセス防止を有効にしているため、**再生制御**のタブは、プレビュー時のリンク不正アクセス防止の有効期限、トライアル視聴時間の長さなどの選定をサポートしています。ここではデフォルトのパラメータを維持できます（再生リンク不正アクセス防止の有効期限はデフォルトで1日で、トライアル視聴時間の長さ、最大再生可能IP数は記入不要です）。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/5968a5d6428bff9c3e3e0e1d4ce7431e.png" width="722" />
4. **Webプレーヤー**の中で、プレーヤーの中央のボタンをクリックすると、Web端末での再生が体験できます。
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />
5. **モバイルプレイヤー**の中で、**QRコードをスキャンしてダウンロードする**をクリックして、「Tencent Cloud Toolkit」をインストールします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0e72b414ee3dc8084dda39d8a5d5c91.png" style="zoom:67%;" />
6. モバイル端末で再生・体験するには、携帯電話でTencent Cloud Toolkitを開き、**Player>Super Player**を選択してから、右上隅のボタンをクリックしてQRコードをスキャンします。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/06e77f14c2e1020e8936ce1ab30a6ca3.png" width="522" />

[](id:step3)
## 手順3：Demoを使用して検証

暗号化したビデオを再生できるようにするためには、Super playerで有効期間内の署名を使用する必要があります。以下、署名ツールを使用して署名をクイック発行する方法を紹介します。

1. [Super player - 署名生成ツール](https://vods.cloud.tencent.com/signature/super-player-sign.html)の画面を開き、パラメータを入力します。
 - **ユーザーappId**：ビデオが属するappId：1400xxx357を入力します（サブアプリケーションが使用される場合は、サブアプリケーションのappIdを入力します）。
 - **ビデオfileId**：ビデオのFileId：528xxx3757278095を入力します。
 - **現在のUnixタイムスタンプ**：ツールが現在のUnix時間（1591756516）を自動的に生成しているため、記入不要です。
 - **Super Player設定**：プリセットのSuper Player設定名：basicDrmPresetを入力します。
 - **署名期限切れUnixタイムスタンプ**：署名自身の有効期限（未記入可、デフォルトでは1日後に期限切れ）。
 - **リンクの有効期限**：Keyリンク不正アクセス防止の有効期限。6時間後の16進数Unix時間：5ee09b44を入力します。
 - **リンク不正アクセス防止Key**：前に取得したリンク不正アクセス防止Key：2WExxx48eWを入力します。
>!basicDrmPresetはプリセットのSuper player設定で、テンプレート12を使用したアダプティブビットレートストリーミングへのトランスコーディングの出力、およびテンプレート10を使用したスプライトイメージキャプチャの出力に使用します。
2. **署名の生成**をクリックします。生成した署名が**署名生成結果**のテキストボックスに表示されます。

  

Super Playerの署名を取得すると、[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/LiteAVSDK/Player_Android)、[iOS](https://github.com/LiteAVSDK/Player_iOS)の3種類の端末のSuper PlayerのDemoを使用してそれぞれ検証することができます。詳細については、Demoのソースコードをご参照ください。
>?コンソールの**メディア資産管理**>[**ビデオ管理**](https://console.cloud.tencent.com/vod/media)>**Super Playerプレビュー**の中で、プレビューのビデオに対応するWebプレーヤーのソースコードを取得でき、これを直接参照して使用できるようにしています。
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## まとめ

このチュートリアルの学習を終えると、ビデオの暗号化の方法、およびSuper playerを使用して暗号化後のビデオを再生する方法を理解できたことになります。

