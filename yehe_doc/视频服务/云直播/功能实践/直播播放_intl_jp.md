## 準備作業
1.  [Tencent CSSサービス](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)をアクティブにし、 [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了します。実名認証を実施していないユーザーは中国国内のCSSインスタンスを購入できません。
2. [CSSコンソール](https://console.cloud.tencent.com/live/livestat)に アクセスし、プッシュアドレスを取得して、CSSプッシュを実現します。具体的な操作については、 [CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)をご参照ください 。
3. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)を選択して、【ドメイン名の追加】クリックし、ICP登録済みのドメイン名を入力して、タイプは【再生ドメイン名】を選択し、【保存】をクリックしてください。
>!
>- 再生ドメイン名がない場合は、他のドメイン名サービスプロバイダからドメイン名を購入することができます。
>-  ドメイン名を購入済みで、かつドメイン名のICP登録を実施していない場合は、Tencent Cloudのドメイン名ICP登録に移動し、ICP登録を行ってください。また他のドメイン名サービスプロバイダでICP登録を行うこともできます。

4.  [ドメイン名サービスコンソール](https://console.cloud.tencent.com/domain)にログインし、追加済みの再生ドメイン名に対するCNAME設定を行います。具体的な操作については、 [ドメイン名CNAME設定](https://intl.cloud.tencent.com/document/product/267/31057)をご参照ください。

## 再生アドレスの取得
CSSコンソールの【補助ツール】>[【アドレスジェネレーター】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)に移動して、再生アドレスを取得し、このページで次の設定を行います。
- 生成タイプ：**再生ドメイン名**を選択します。
- ドメイン名管理に追加済みの再生ドメイン名を選択します。
- プッシュアドレスと同一のStreamNameを入力します。対応するストリームを再生するためには、再生アドレスのStreamNameはプッシュアドレスのStreamNameと一致させる必要があります。
- 選択アドレスの期限切れ時間を選択します（例：`2019-12-13  23:59:59`）。
- 【アドレスの生成】をクリックします。
  ![](https://main.qcloudimg.com/raw/a2f130098eb40df252956ffb3752d230.png)
>-  上記方法以外にも、CSSコンソールの[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)で再生ドメイン名を選択して、【管理】をクリックし、【再生設定】を選択して、再生アドレスの期限切れ時間とプッシュアドレスと同一のStreamNameを入力し、【再生アドレスの生成】をクリックして、アドレスを生成することができます。

## CSS再生
まず [CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)を実施する必要があり、プッシュが正常に実行された後、再生アドレスを介してライブストリーミング画面を確認することができます。業務のシナリオに基づき、次の方式でライブストリーミングテストを実施することができます。

### シナリオ1： PC での再生
[ VLC](https://intl.cloud.tencent.com/document/product/267/32483)、FFmepg および [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/player/demo/player.html)  などのツールを使用して再生することができます。
![](https://main.qcloudimg.com/raw/d7aa3b16f0a76ed2a6bd6102be04ddaf.png)
### シナリオ2：モバイルでの再生
1.  Tencent Video Cloud Demoをダウンロードし、インストールします。
2. 【MLVB】>【CSSプル】を開き、選択します。
3. 入力ボックスに再生アドレスを入力するか、または再生アドレスの2次元コードをスキャンして入力します。
4. 左下隅の再生ボタンをクリックし、再生して視聴します。

>? Appまたはミニプログラムでプッシュ/再生を実施する必要がある場合は、MLVB SDKを統合し、CSSサービスと連携して使用できます。MLVB SDKはRTMP、HTTP-FLV、HLS再生プロトコルをサポートしています。

### シナリオ3：ミニプログラムでの再生
1. WeChatでミニプログラム 「Tencent Video Cloud」を検索し、【CSS再生】を選択します。
2. 【コードスキャン】ボタンをクリックし、再生アドレスを変換した2次元コードをスキャンします。
3. 左下隅の再生ボタンをクリックし、再生して視聴します。

### シナリオ4：Webでの再生
Tencent Cloudの強力なバックエンド機能とAI技術に基づき、CSSとVODの強力な再生能力を提供する、プレーヤーSDKの TCPlayerLite を選択して再生することをお勧めします。Player+ は、Tencent Video Cloud CSS、VODサービスと深く融合し、スムーズで安定した再生パフォーマンスを実現し、広告の配置、データモニタリングなどの機能を統合しています。
>! 現在、市販される大多数のスマホブラウザはHTTP-FLV再生をサポートしていないため、Tencent Cloudは、Web再生時のプロトコル選択に際し、PCブラウザでは、HTTP-FLVプロトコルを使用してライブストリーミングを再生し、スマホブラウザではHLSを使用してライブストリーミングを再生することを推奨しています。


## よくあるご質問
- [どのような再生プロトコルがサポートされているのですか？](https://intl.cloud.tencent.com/document/product/267/7968)
- [再生アドレスはどのような構成ですか？](https://intl.cloud.tencent.com/document/product/267/7968)
- [再生トランスコードはどのように使用するのですか？](https://intl.cloud.tencent.com/document/product/267/35598#que2)
- [タイムシフト機能はどのように使用するのですか？](https://intl.cloud.tencent.com/document/product/267/35598#que3)
- [HTTPS再生はどのように使用するのですか？](https://intl.cloud.tencent.com/document/product/267/35598#que4)
- [再生でGlobal Content Deliveryをどのように使用するのですか？](https://intl.cloud.tencent.com/document/product/267/35598#que5)
- [再生ホットリンク保護はどのようにアクティブ化するのですか？](https://intl.cloud.tencent.com/document/product/267/35598#que6)

