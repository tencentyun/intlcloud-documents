## 学習目標

本段階のチュートリアルを学習すると、ビデオを暗号化し、Super playerを使用して暗号化後のビデオを再生する方法を把握することができます。

これを読む前に、先にSuper playerガイドの[段階1：Super playerを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098) と[段階2：防犯リンクを有効にした後のビデオ再生](https://intl.cloud.tencent.com/document/product/266/38292) 編の部分を確実に学習しておくようにしてください。本チュートリアルでは [段階1](https://intl.cloud.tencent.com/document/product/266/38098) 編でアクティブ化したアカウントおよびアップロードしたビデオを使用し、 [段階2](https://intl.cloud.tencent.com/document/product/266/38292)にしたがって防犯リンクを有効化する必要があります。

## 手順1：ビデオの暗号化
1. VODコンソールにログインし、【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)と選択し、処理したいビデオ（FileId：528xxx3757278095）にチェックを入れ、【ビデオ処理】をクリックします。
2. ビデオ処理の画面で：
 * 【処理タイプ】は【タスクフロー】を選択します。
 * 【タスクフローテンプレート】は【SimpleAesEncryptPreset】を選択します。
<img src="https://main.qcloudimg.com/raw/4cc8649c21b5c60305b925120f84d7e6.png" width="" /><span>
>? 
>- SimpleAesEncryptPresetはプリセットのタスクフローです。テンプレート12のアダプティブビットレートストリーム、テンプレート10のスクリーンキャプチャによるタイトル画像作成、テンプレート10のキャプチャしたスプライトイメージを使用します。
>- テンプレート12のアダプティブビットレートストリーミングはトランスコーディングして暗号化したマルチビットレートによる出力です。
3. 【OK】をクリックし、「ビデオ状態」欄が「処理中」から「正常」に変わり、ビデオ処理完了と表示されるのを待ちます。
![](https://main.qcloudimg.com/raw/885b68427d36faefe8f2bb5b489e1e19.png)
4. ビデオ「操作」バーの下の【管理】をクリックし、管理画面に入ります。
 * 「基本情報」タグを選択すると、生成したタイトル画像、および暗号化したアダプティブビットレートストリーミングの出力（テンプレートID：12）を見ることができます。
 * 「スクリーンキャプチャ情報」タグを選択すると、生成したスプライトイメージ（テンプレートID：10）を見ることができます。


##  手順2：プレビューによる再生体験

前の手順で、ビデオをすでにアップロードし、ビデオに対する処理を行いました。ここでは、3種類の端末のSuper playerを使用して、再生の効果を素早く体験します。

1. 【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)と選択して、**手順1**のアップロードおよび処理済みのビデオを探し、「操作」バーの下の【管理】をクリックして、【Super playerプレビュー】を選択します。
2. 【Super player設定】はbasicDrmPresetを選択します。

 >? basicDrmPresetはプリセットのSuper player設定で、テンプレート12のアダプティブビットレートストリームの出力、テンプレート10のキャプチャしたスプライトイメージの出力に使用します。
3. デフォルトの配信ドメイン名が防犯リンクを有効にしているため、【再生制御】のオプションカードで、プレビュー時の防犯リンクの期限切れ時間、テスト視聴時間などの選定をサポートしています。ここではデフォルトのパラメータを維持します（再生の防犯リンクの期限切れ時間はデフォルトで1日、プレビュー時間、最大再生可能IP数は入力しません）。
 
4. 【Webプレーヤー】の中で、プレーヤーの中間のボタンをクリックすると、 Web端末での再生が体験できます。
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />


## 手順3： Demoを使用して検証

暗号化したビデオを再生できるようにするためには、Super playerで有効期間内の署名を使用する必要があります。以下、署名ツールを使用して素早く署名を生成する方法を紹介します。

1. [Super player - 署名生成ツール](https://vods.cloud.tencent.com/signature/super-player-sign.html)の画面を開き、パラメータを入力します。
 * 【ユーザーappId】：ビデオが属するappId：1400xxx357を入力します（使用するのがサブアプリケーションの場合は、サブアプリケーションのappIdを入力します）。
 * 【ビデオfileId】：ビデオのFileId：528xxx3757278095を記入します。
 * 【現在のUnixタイムスタンプ】：ツールが自動生成した現在のUnix時間（1591756516）。入力不要です。
 * 【Super player設定】：プリセットのSuper player設定名：basicDrmPresetを入力します。
 * 【署名期限切れUnix タイムスタンプ】：署名自身の期限切れ時間。未入力可、デフォルトは1日後に期限切れ。
 * 【リンク期限切れ時間】：Keyリンク不正アクセス防止期限切れ時間。6時間後の16進数Unix 時間：5ee09b44を入力します。
 * 【防犯リンクKey】：入力の前に取得した防犯リンクKey：2WExxx48eWを入力します。
>!basicDrmPresetはプリセットのSuper player設定で、テンプレート12のアダプティブビットレートストリームの出力、テンプレート10のキャプチャしたスプライトイメージの出力に使用します。
2. 【署名の生成】をクリックします。生成できた署名が【署名生成結果】のテキストボックスに表示されます。


Super playerの署名を取得した後、[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/tencentyun/SuperPlayer_Android)、[iOS](https://github.com/tencentyun/SuperPlayer_iOS)の3種類の端末のSuper playerのDemoを使用してそれぞれ検証することができます。詳細内容は、Demoのソースコードをご参照ください。
>?コンソールの【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)>【Super playerプレビュー】の中で、プレビューのビデオに対応するWebプレーヤーのソースコードを取得でき、これを直接参照して使用できるようにしています。
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## まとめ

このチュートリアルの学習を終えると、ビデオの暗号化の方法、およびSuper playerを使用して暗号化後のビデオを再生する方法を理解できたことになります。
