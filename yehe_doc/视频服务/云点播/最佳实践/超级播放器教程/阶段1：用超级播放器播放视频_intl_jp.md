## 学習目標
この段階のチュートリアルを学習すると、ビデオをVODにアップロードしてビデオ処理を行った後、Super playerで再生する機能が理解できるようになります。

## 前提条件
本チュートリアルを開始する前に、次の前提条件を満たしていることを確認してください。

### VODのアクティブ化
VODをアクティブにする必要があります。手順は以下のとおりです。

1. [Tencent Cloudのアカウント](https://intl.cloud.tencent.com/document/product/378/17985)登録を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了させます。実名認証が済んでいないユーザーは中国国内でVODサービスを購入できません。
2. VODサービスを購入します。具体的な方法は、[課金概要](https://intl.cloud.tencent.com/document/product/266/2838)をご参照ください。
3. 【クラウド製品】>【Video Service】>[【VOD】](https://console.cloud.tencent.com/vod)と選択し、VODコンソールに入ります。

これで、VODのアクティブ化の手順が完了しました。

### ホットリンク防止機能は無効を維持

自分のデフォルトの配信ドメイン名を確認する必要があります。ホットリンク防止は有効になっていません。

1. VODコンソールにログインし、【配信と再生の設定】>[【Domain Management】](https://console.cloud.tencent.com/vod/distribute-play/domain)と選択し、「デフォルトの配信ドメイン名」の操作バーの下の【設定】をクリックして、設定画面に入ります。
<img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. 「Refererホットリンク防止」と「Keyホットリンク防止」の状態を確認し、いずれも「無効」状態であることを確認します。
![](https://qcloudimg.tencent-cloud.cn/raw/12689eb5bed63fc76cd7d88e38907c09.png)


## 手順1：ビデオのアップロードおよび処理
この手順では、ビデオのアップロードの仕方、さらにビデオをアダプティブビットレートストリームに変換し、タイトル画面とスプライトイメージをキャプチャする方法について指導します。

1. VODコンソールにログインし、【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)と選択して、【ビデオのアップロード】をクリックします。
![](https://main.qcloudimg.com/raw/b1ad4f0706ad1cd24044c8420a759868.png)
2. アップロードインターフェースで、【ローカルからのアップロード】を選択し、【ビデオの選択】をクリックしてローカルビデオをアップロードします。その他の設定は以下のとおりです。
 * 【ビデオ処理】は【アップロード後に自動的にビデオ処理を実行】を選択します。
 * 【処理タイプ】は【タスクフロー】を選択します。
 * 【タスクフローテンプレート】は【LongVideoPreset】を選択します。
 >?LongVideoPreset はプリセットのタスクフローです。テンプレート10のアダプティブビットレートストリーム、テンプレート10のスクリーンキャプチャによるタイトル画像作成、テンプレート10のキャプチャしたスプライトイメージを使用します。
![](https://main.qcloudimg.com/raw/c5d53f748ce95ab0c8accea42687256a.png)
3. 【アップロード開始】をクリックすると、「アップロード中」の画面に入ります。アップロードが完了するのを待ちます。
4. 【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)と選択し、新しくアップロードしたビデオ（FileId：528xxx3757278095）を探します。その中のIDがアップロードしたビデオのFileIdです。
![](https://main.qcloudimg.com/raw/f2b3744a3c42a07863db0b7545dd892f.png)
>?「ビデオの状態」が【処理中】から【正常】に変わるのを待ちます。ビデオ処理の完了が表示されます。
5. 新しくアップロードしたビデオの「操作」バーの下の【管理】をクリックして、管理画面に入ります。
 - 「基本情報」タグを選択すると、生成したタイトル画像、およびアダプティブビットレートストリーミングの出力（テンプレートID：10）を見ることができます。
 - 「スクリーンキャプチャ情報」タグを選択すると、生成したスプライトイメージ（テンプレートID：10）を見ることができます。

## 手順2：プレビューによる再生体験

前の手順で、ビデオをすでにアップロードし、ビデオに対する処理を行いました。ここでは、3種類の端末のSuper playerを使用して、再生の効果を素早く体験します。

1. 【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)と選択して、**手順1**のアップロードおよび処理済みのビデオを探し、「操作」バーの下の【管理】をクリックして、【Super playerプレビュー】を選択します。
2. 【Super player設定】はdefaultを選択します。
>? defaultはプリセットのSuper player設定で、テンプレート10のアダプティブビットレートストリームの出力、テンプレート10のキャプチャしたスプライトイメージの出力に使用します。
 <img src="https://main.qcloudimg.com/raw/17e2552964195c6919239d2d13a0d012.png" width="500" />
4. 【Webプレーヤー】の中で、プレーヤーの中間のボタンをクリックすると、 Web端末での再生が体験できます。
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />

## 手順3： Demo を使用して体験

[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/tencentyun/SuperPlayer_Android)、[iOS](https://github.com/tencentyun/SuperPlayer_iOS)の3種類の端末のSuper playerのDemoを使用してそれぞれ検証することができます。具体的な内容は、Demo のソースコードをご参照ください。
>?コンソールの【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)>【Super playerプレビュー】の中で、プレビューのビデオに対応するWebプレーヤーのソースコードを取得でき、これを直接参照して使用できるようにしています。
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## まとめ

このチュートリアルの学習を終え、ビデオをVODにアップロードし、ビデオ処理を行った後にSuper playerで再生する方法の初歩が理解できたことになります。

次のことをしたい場合：
- Keyホットリンク防止を有効化した後にビデオを再生する場合は、 [段階2：ホットリンク防止後のビデオ再生の有効化](https://intl.cloud.tencent.com/document/product/266/38292)をご参照ください。
- ビデオ再生時の内容と形式をカスタマイズする場合は、[段階3：再生内容と形式のカスタマイズ](https://intl.cloud.tencent.com/document/product/266/38293)をご参照ください。
- ビデオを暗号化し、暗号化後のビデオを再生する場合は、 [段階4：暗号化したビデオの再生](https://intl.cloud.tencent.com/document/product/266/38294)をご参照ください。
