このチュートリアルでは、CSSサービスをすばやく理解していただくためのガイドを提供します。CSSサービスを体験される前に、混乱を避けるために、事前にCSSの[CSS Pricing](https://intl.cloud.tencent.com/document/product/267/2819)を読んで、**課金項目**と**料金**について承知していただくことをお勧めします。

<span id="step0"></span>
## 準備

1.[Tencent Cloudアカウント](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb) を登録して、 実名認証を完了する必要があります。実名認証を行っていないユーザーは、中国本土のCSSインスタンスを購入できません。								

2. [CSS service activation page](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)に入って、『Tencent Cloud Service Agreement』にチェックを入れて、【Apply for Activation】をクリックして、CSSサービスをアクティブにすることができます。

<span id="step1"></span>
## ステップ1：ドメイン名を追加する
CSSサービスを使用するには、少なくとも**2つ**のドメイン名が必要です。1つを**プッシュドメイン名**とし、もう1つを**再生ドメイン名**として使用します。プッシュと再生で同じドメイン名を使用することはできません。

<span id="step1_1_1"></span>
1. 独自のドメイン名を用意します。中国本土で使用する場合は、ドメイン名のICP登録を完了する必要があります。
2. CSSコンソールにログインし、[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)に入って、【Add Domain】をクリックします。
3. 独自のドメイン名追加ページを入力し、ICP登録済みのドメイン名を入力し、ドメイン名の種類を選択して、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/bee8085a9d29641ddab913fdcd9c75ab.png)
>?
>- CSSは、デフォルトでテストドメイン名 `xxxx.livepush.myqcloud.com`を提供します。このドメイン名をプッシュテストに使用できますが、正式なサービスでこのドメイン名をプッシュドメイン名として使用することはお勧めしません。
>- ドメイン名が正常に追加されると、【Domain Management】のドメイン名リストからドメイン名情報を確認できます。追加済みのドメイン名を管理する必要がある場合は、[Domain Management](https://intl.cloud.tencent.com/document/product/267/31056)をご参照ください。
>- ライブブロードキャストドメイン名の詳細については、[Basic CSS Features](https://intl.cloud.tencent.com/document/product/267/7968)をご参照ください。
<span id="step1_1_1"></span>
4.ドメイン名が正常に追加されると、システムは自動的にCNAMEドメイン名（サフィックスが`.liveplay.myqcloud.com`）を割り当てます。CNAMEドメイン名に直接アクセスすることはできません。ドメインネームサービスプロバイダーでCNAMEの設定を完了する必要があります。設定が有効になると、CSSサービスをご利用できます。例として、DNSサービスプロバイダーをTencent Cloudとする場合、CNAMEレコードの追加手順は次のとおりです。
	1. [Tencent Cloud Domain Name Service Console](https://console.cloud.tencent.com/domain)にログインします。
	2. CNAMEを追加する必要のあるドメイン名を選択し、【Resolve】をクリックします。
	3. ドメイン名解決ページに入り、【Add Record】をクリックします。
	4. 新しい列に、ホストレコードとしてドメイン名プレフィックスを入力し、CNAMEとしてレコードタイプを選択し、レコード値としてCNAMEドメイン名を入力します。
	5. 【Save】をクリックしてCNAMEレコードを追加します。
>!
>- CNAMEが正常に追加された後、通常、有効になるまでに少し時間がかかります。CNAME設定が失敗した場合、CSSは使用できません。
>- ドメイン名CNAMEが有効になると、CSSコンソールの[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)リストで、ドメイン名CNAMEアドレスのステータス記号が<img src="https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png"></img>に変更したことがわかります。
>- CNAME操作後に常に検出に失敗する場合は、ドメイン名登録サービスプロバイダにお問い合わせください。
>- 他のDNSサービスプロバイダーを使用している場合、その他の操作については[CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057)をご参照ください。


<span id="step2"></span>
## ステップ2：プッシュアドレスを取得する

1. コンソールを開き、【Accessibility Tools】 > [【Address Generator】](https：//console.cloud.tencent.com/live/addrgenerator/addrgenerator)を選択してプッシュURLを生成します。
2. アドレスジェネレータページに入り、次のように設定します。
   1. 生成タイプの選択：**プッシュドメイン名**。
   2. ドメイン名管理で追加したプッシュドメイン名を選択します。
   3. カスタムストリーム名StreamNameを入力します（例：liveteststream）。
   4. アドレスの期限切れ時間を選択します（例：2019-10-18  23:59:59）。
   5. 【Generate Address】をクリックすると、プッシュアドレスが生成されます。
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)

> ?
>- プッシュアドレスの構成は次のとおりです。`live`はデフォルトのAppNameで、 `txSecret`はプッシュストリームを再生するための署名で、`txTime`はプッシュアドレスの有効期間です。
>- 上記の方法に加えて、CSSコンソールの[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)でプッシュドメイン名を選択し、【Manage】をクリックして、【Push Configuration】を選択し、プッシュアドレスの期限切れ時間とカスタムストリーム名StreamNameを入力し、【Generate Push Address】をクリックしてプッシュアドレスを生成します。
>- 実際のサービス要件に応じて、プッシュURLを生成する前に、対応する[機能テンプレート](https://intl.cloud.tencent.com/document/product/267/34223)）を設定して作成し、それをプッシュドメインに関連付けることができます。付加価値機能の価格については、[Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819)をご覧ください。

<span id="step3"></span>
## ステップ3：ライブストリームをプッシュする

サービスシナリオに応じて、生成されたプッシュアドレスを対応するプッシュソフトウェアに入力できます。
- PC側のプッシュには、OBSプッシュをお勧めします。操作の詳細については、[Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569)をご参照ください。
- Webプッシュの場合、【CSS Toolkit】> [【Web Push】](https://console.cloud.tencent.com/live/tools/webpush)を使用して、プッシュするドメイン名を選択し、カスタマイズされたストリーム名StreamNameを入力することをお勧めします。アドレスの期限切れ時間を選択し、カメラを有効にして、【Strat Push】をクリックします。
- モバイル端末でプッシュする場合は、Tencent Video Cloud Demoをダウンロードしてインストールし、【MLVB】> 【カメラプッシュ】を選択し、プッシュアドレスを手動またはQRコードをスキャンしてアドレスボックスに入力し、左下隅にある「Start」ボタンをタップして、プッシュを開始します。

<span id="step4"></span>

## ステップ4：再生URLを取得する

1.ストリームが正常にプッシュされたら、[【Stream Management】](https://console.cloud.tencent.com/live/streammanage)>【Online Stream】を選択し、プッシュアドレスのステータスを確認し、【Test】をクリックしてオンラインで再生して視聴します。
2. 【Auxiliary Tools】> [【Address Generator】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を選択して再生URLを取得し、このページで以下のように設定します。
   1. 生成タイプの選択：**再生ドメイン名**。
   2. ドメイン名管理で追加したドメイン名を選択します。
   3. プッシュアドレスと同じStreamNameを入力します。対応するストリームを再生するには、再生URLStreamNameがプッシュアドレスStreamNameと同じである必要があります。
   4. アドレスの期限切れを選択します（例：2019-10-13  23:59:59）。
   5. 【Generate Address】をクリックすると、再生URLが生成されます。
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
<span id="step4_1"></span>
3. サービスシナリオに応じて、次の方法でライブブロードキャストストリームを正常に再生できるかどうかをテストできます。
   1. PCでのライブストリームテストでは、[VLC](https://intl.cloud.tencent.com/document/product/267/32483) などのツールを使用して体験することをお勧めします。詳細については、[CSS Playback](https://intl.cloud.tencent.com/document/product/267/31559)をご参照ください。
   2. Web側の再生テストでは、プレーヤーSDKに搭載されているTCPlayerLiteプレーヤーで再生することをお勧めします。詳細については、[CSS Playback](https://intl.cloud.tencent.com/document/product/267/31559)をご参照ください。
   3. モバイル端末でのライブストリームテストでは、Tencent Video Cloud Demoをダウンロードしてインストールすることをお勧めします。【MLVB】> 【 CSS Pull】を開いて選択し、手動で入力するかQRコードをスキャンして、アドレスボックスに再生URLを入力し、左下隅の「Play」ボタンをタップして。再生して視聴します。

## 関連する操作
- **CSSレコーディング**を有効にする必要がある場合は、レコーディングテンプレートを作成し、ドメイン名と設定を関連付けることができます。関連ドキュメントについては、[CSS Recording](https://intl.cloud.tencent.com/document/product/267/34223)をご参照ください。
- **CSSトランスコーディング**を有効にする必要がある場合は、トランスコーディングテンプレートを作成し、ドメイン名と設定を関連付けることができます。関連ドキュメントについては、[Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31071)をご参照ください。
- **CSSウォーターマーク**を有効にする必要がある場合は、ウォーターマークテンプレートを作成し、ドメイン名と設定を関連付けることができます。関連ドキュメントについては、[Watermark Configuration](https://intl.cloud.tencent.com/document/product/267/31073)をご参照ください。
- **CSSスクリーンキャプチャポルノ検出**を有効にする必要がある場合は、スクリーンキャプチャポルノ検出テンプレートを作成し、ドメイン名と設定を関連付けることができます。関連ドキュメントについては、[ Screencapture and Porn Detection Configuration](https://intl.cloud.tencent.com/document/product/267/31072)をご参照ください。
- **CSSストリームミックス機能**を実装するには、ストリームミックスAPIを呼び出すことができます。関連ドキュメントについては、[CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997)をご参照ください。




## よくあるご質問
- [プッシュ、ライブブロードキャスト、VODとはそれぞれ何ですか。](https://intl.cloud.tencent.com/document/product/267/7968#.E6.8E.A8.E6.B5.81.E3.80.81.E7.9B.B4.E6.92.AD.E5.92.8C.E7.82.B9.E6.92.AD.E5.88.86.E5.88.AB.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
- [どのプッシュプロトコルをサポートしますか。](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.8E.A8.E6.B5.81.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [どの再生プロトコルをサポートしますか。](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.92.AD.E6.94.BE.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [再生URLは何で構成されていますか。](https://intl.cloud.tencent.com/document/product/267/7968#.E6.92.AD.E6.94.BE.E5.9C.B0.E5.9D.80.E7.94.B1.E4.BB.80.E4.B9.88.E7.BB.84.E6.88.90.EF.BC.9F)
