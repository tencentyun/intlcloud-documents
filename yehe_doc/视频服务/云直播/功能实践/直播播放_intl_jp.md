## 準備作業
1. [Tencent CSSサービス](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)をアクティブ化し、 [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了します。実名認証を実施していないユーザーは中国本土のCSSインスタンスを購入できません。
2. [CSSコンソール](https://console.cloud.tencent.com/live/livestat)に アクセスし、プッシュアドレスを取得して、CSSプッシュを実現します。具体的な操作については、 [CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)をご参照ください 。
3. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)を選択して、【ドメイン名の追加】を選択し、ICP登録済みのドメイン名を入力して、【再生ドメイン名】タイプを選択し、【保存】をクリックしてください。
>!
>
>- 再生ドメイン名がない場合は、 [【ドメイン名の登録】](https://intl.cloud.tencent.com/login) に移動し、ドメイン名を購入することが可能です。また、その他のドメイン名サービスプロバイダからドメイン名を購入することもできます。
4. [ドメイン名サービスコンソール](https://console.cloud.tencent.com/domain)にログインし、追加済みの再生ドメイン名にCNAMEの設定を行います。具体的な操作については、 [ドメイン名CNAME設定](https://intl.cloud.tencent.com/document/product/267/31057)をご参照ください。

## 再生アドレスの取得
CSSコンソールの【CSSツールボックス】>[【アドレスジェネレーター】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)に移動して、再生アドレスを取得し、このページで次の設定を行います。
- 生成タイプ：**再生ドメイン名**を選択します。
- ドメイン名管理に追加済みの再生ドメイン名を選択します。
- プッシュアドレスと同一のStreamNameを入力します。対応するストリームを再生するためには、再生アドレスのStreamNameはプッシュアドレスのStreamNameと一致させる必要があります。
- 選択アドレスの期限を選択します（例：`2019-12-13  23:59:59`）。
- 【アドレスの発行】を選択します。
![](https://main.qcloudimg.com/raw/a2f130098eb40df252956ffb3752d230.png)
>?上記方法以外にも、CSSコンソールの[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)で再生ドメイン名を選択して、【管理】をクリックし、【再生設定】を選択し、再生アドレスの期限を選択して、プッシュアドレスと同一のStreamNameを入力し、再生アドレスの発行】を選択するとアドレスの発行が可能です。

## CSS再生
始めに[CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)を実施する必要があり、プッシュが正常に実行された後、再生アドレスを介してライブストリーミング画面を確認することができます。業務のシナリオに基づき、次の方式でライブストリーミングテストを実施することができます。

### シーン1： PCでの再生
[ VLC](https://intl.cloud.tencent.com/document/product/267/32483)、FFmepg および [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/player/demo/player.html)  などのツールを使用して再生することができます。
### シーン2：モバイルでの再生
1. [Tencent Video Cloud Demo](https://intl.cloud.tencent.com/document/product/1071/38147)をダウンロードし、インストールします。
2. 【モバイルライブストリーミング】>【CSSプル】を開き、選択します。
3. 入力ボックスに再生アドレスを入力するか、または再生アドレスの2次元コードをスキャンして入力します。
4. 左下隅の再生ボタンをクリックし、再生して視聴します。

>? Appでプッシュ/再生を実施する場合は[モバイルライブストリーミングSDK](https://intl.cloud.tencent.com/product/mlvb) を統合し、CSSサービスと連携して使用することができます。モバイルライブストリーミングSDKはRTMP、HTTP-FLV、HLS再生プロトコルをサポートしています。

### シーン4：Webでの再生
Tencent Cloudの強力なバックエンド機能とAI技術に基づき、CSSとVODの強力な再生機能を提供する、プレーヤーSDKの TCPlayerLiteを選択して再生することをお勧めします。Player+ は、Tencent Video CSS、VODサービスと深く融合し、スムーズで安定した再生パフォーマンスを実現し、広告の配置、データモニタリングなどの機能を包括しています。
>! 現在、市販で販売されている大多数のスマホブラウザはHTTP-FLV再生をサポートしていないため、Tencent Cloudは、Web再生時のプロトコル選択に際し、ＰＣブラウザでは、HTTP-FLVプロトコルを使用してのライブストリーミング再生、スマホブラウザではHLSを使用してのCSSストリーム再生を推奨しています。


## よくあるご質問
- [どのような再生プロトコルがサポートされているのですか。](https://intl.cloud.tencent.com/document/product/267/7968)
- [再生アドレスはどのような構成ですか。](https://intl.cloud.tencent.com/document/product/267/7968)
- [再生トランスコードはどのように使用するのですか。](https://intl.cloud.tencent.com/document/product/267/35598)
- [タイムシフト視聴はどのように使用するのですか。](https://intl.cloud.tencent.com/document/product/267/35598)
- [HTTPS再生はどのように使用するのですか。](https://intl.cloud.tencent.com/document/product/267/35598)
- [海外アクセラレーションノードをどのように再生に使用するのですか。](https://intl.cloud.tencent.com/document/product/267/35598)
- [再生ホットリンク保護はどのようにアクティブ化するのですか。](https://intl.cloud.tencent.com/document/product/267/35598)

