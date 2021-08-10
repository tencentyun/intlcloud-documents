このチュートリアルにより、CSSサービスをスピーディーに理解することができます。CSSサービスをテスト運用する前に、CSSの[価格一覧](https://intl.cloud.tencent.com/document/product/267/2819)に目を通し、誤解が生じることがないように、**課金項目**と**料金**を確認しておくことをお勧めします。

<span id="step0"></span>
## 準備作業

1. [Tencent Cloudアカウント](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb)にログインし、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)、を完了していること。実名認証を行っていないユーザーは中国本土のCSSインスタンスを購入できません。
2. [Tencent Cloud CSSサービスアクティブ化ページ](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)に入り、『Tencent Cloudサービス契約』の同意にチェックを入れ、【アクティブ化申請】をクリックすればCSSサービスをアクティブ化できます。

<span id="step1"></span>
## 手順1：ドメイン名の追加
CSSサービスを使用するには、少なくとも**2**つのドメイン名が必要です。1つは**プッシュドメイン名**、もう1つは**再生ドメイン名**です。プッシュと再生に同じドメイン名を使用することはできません。

<span id="step1_1"></span>
1. 独自ドメイン名を準備します。中国本土（大陸）で使用する場合はドメイン名のICP登録を済ませている必要があります。
2. CSSコンソールにログインし、[【ドメイン名管理】](https://console.cloud.tencent.com/live/domainmanage)に入って、【ドメイン名の追加】をクリックします。
3. 独自ドメイン名の追加ページに入り、ICP登録済みのドメイン名を入力して、ドメイン名のタイプを選択し、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/bee8085a9d29641ddab913fdcd9c75ab.png)
>?
>- CSSは、デフォルトでテストドメイン名 `xxxx.livepush.myqcloud.com`を提供しています。このドメイン名でプッシュテストを行うことはできますが、正式なサービスでこのドメイン名をプッシュドメイン名として使用することはお勧めしません。
>- ドメイン名の追加に成功すると、【ドメイン名管理】のドメイン名リストでドメイン名情報を確認することができます。追加したドメイン名の管理を行いたい場合は、[ドメイン名管理](https://intl.cloud.tencent.com/document/product/267/31056)をご参照ください。
>- その他のCSSドメイン名関連情報については、[CSS基本関連のご質問](https://intl.cloud.tencent.com/document/product/267/7968)をご参照ください。
<span id="step1_1_1"></span>
4. ドメイン名の追加に成功すると、システムが自動的にCNAMEドメイン名（サフィックスは`.tlivecdn.com`または`.tlivepush.com`）を割り当てます。CNAMEドメイン名は直接アクセスできません。ドメイン名サービスプロバイダのところでCNAME設定を完了させる必要があり、設定が有効になるとCSSサービスを享受できるようになります。例として、DNSサービスプロバイダがTencent Cloudとなる場合のCNAMEレコード追加の操作手順は次のようになります。
	1. [ドメイン名サービスコンソール](https://console.cloud.tencent.com/domain)にログインします。
	2. CNAMEを追加する必要のあるドメイン名を選択し、【解決】をクリックします。
	3. ドメイン名解決のページに入り、【レコードの追加】をクリックします。
	4.  新しく追加した列で、ホストレコードとしてドメイン名プレフィックスを入力し、レコードタイプはCNAMEを選択し、レコード値としてCNAMEドメイン名を入力します。
	5. 【保存】をクリックするとCNAMEレコードが追加できます。
>!
>- CNAMEに成功した後は、通常、有効になるまでに一定の時間を要します。CNAMEに成功しない場合はCSSを使用できません。
>- ドメイン名のCNAMEに成功すると、CSSコンソールの[【ドメイン名管理】](https://console.cloud.tencent.com/live/domainmanage)リストでドメイン名CNAMEのアドレス状態の記号が![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png)に変更されているのが確認できます。
>- CNAME操作後の検出で失敗が続く場合は、ドメイン名登録サービスプロバイダに問い合わせることをお勧めします。
>- 他のDNSサービスプロバイダを使用する場合、その他の操作については、[CNAME設定](https://intl.cloud.tencent.com/document/product/267/31057)をご参照ください。


<span id="step2"></span>
## 手順2：プッシュアドレスの取得
1. 【CSSツールボックス】> [【アドレスジェネレーター】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を選択します。
2. アドレスジェネレーターのページに入り、次の設定を行います。
   1. 生成タイプは**プッシュドメイン名**を選択します。
   2. ドメイン名管理で追加済みのプッシュドメイン名を選択します。
   3. AppNameを入力します。デフォルトは`live`です。
   4. カスタマイズされたストリーム名StreamNameを入力します（例：liveteststream）。
   5. アドレスの期限切れ時間を選択します（例：`2021-05-31 23:59:59`）。
   5. 【アドレスの生成】をクリックすると、プッシュアドレスを生成できます。
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)

>? 
>- プッシュアドレスの構成は、`live`がデフォルトのAppName、`txSecret`が再生プッシュの署名、`txTime`がプッシュアドレスの有効時間となります。
>- 上記方法以外にも、CSSコンソールの[【ドメイン名管理】](https://console.cloud.tencent.com/live/domainmanage)でプッシュドメイン名を選択して、【管理】をクリックし、【プッシュ設定】を選択して、プッシュアドレスの期限切れ時間とカスタマイズされたストリーム名StreamNameを入力し、【プッシュアドレスの生成】をクリックすると、プッシュアドレスを生成できます。
>- 実際の業務のニーズに応じて、プッシュアドレスの生成前に対応する[機能テンプレート](https://intl.cloud.tencent.com/document/product/267/34223)を設定して作成し、プッシュドメイン名に関連付けることができます。付加価値機能の料金については、[価格一覧](https://intl.cloud.tencent.com/document/product/267/2819)をご参照ください。

<span id="step3"></span>
## 手順3：CSSプッシュ

業務シナリオに応じて、生成したプッシュアドレスを対応するプッシュソフトウェアに入力することができます。
- PC端末プッシュには、OBSプッシュを使用することをお勧めします。具体的な操作については、[OBSプッシュ](https://intl.cloud.tencent.com/document/product/267/31569)をご参照ください。
- Web端末プッシュには、[【Webプッシュ】](https://console.cloud.tencent.com/live/tools/webpush)を使用することをお勧めします。プッシュしたいドメイン名を選択して、カスタマイズしたストリーム名StreamNameを入力し、アドレスの有効期限を選択してから、カメラをオンにして、【プッシュ開始】をクリックすればOKです。
- モバイルプッシュは、【モバイルライブストリーミングMLVB】>【プッシュデモ（カメラプッシュ）】を選択して、レコーディングプッシュアドレスを手入力、または2次元コードをスキャンしてアドレス編集枠内に取り込み、【プッシュ開始】をクリックすればプッシュが完了します。

>? カスタマイズしたAppには、Tencent Cloudが提供する[モバイルライブストリーミングSDK](https://intl.cloud.tencent.com/document/product/1071)を統合することで、プッシュ機能を実装できます。

<span id="step4"></span>
## 手順4：再生アドレスの取得

1. プッシュに成功した後、[【ストリーム管理】](https://console.cloud.tencent.com/live/streammanage)>【オンラインストリーム】を選択して、プッシュアドレスの状態を確認し、【テスト】をクリックしてオンライン再生を視聴します。
2. 【CSSツールボックス】>[【アドレスジェネレーター】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を選択して再生アドレスを取得し、このページで次のように設定します。
   1. 生成タイプは、**再生ドメイン名**を選択します。
   2. ドメイン名管理で追加済みの再生ドメイン名を選択します。
   3. AppNameを入力します。デフォルトは`live`です。
   4. プッシュアドレスと同一のStreamNameを入力します。対応するストリームを再生するためには、再生アドレスのStreamNameとプッシュアドレスのStreamNameを一致させる必要があります。
   5. アドレスの期限切れ時間を選択します（例：`2021-05-31 23:59:59`）。
   5. 【アドレスの生成】をクリックすると、再生アドレスを生成できます。
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
<span id="step4_1"></span>
3. 業務シナリオに応じて、次の方式を用いてCSSストリームが正常に再生できるかどうかテストすることができます。
   1. PC端末のCSSストリームテストには、[VLC](https://intl.cloud.tencent.com/document/product/267/32483) などのツールを使用して再生体験を行うことをお勧めします。具体的な内容は、[再生の実践](https://intl.cloud.tencent.com/document/product/267/31559)をご参照ください。
   2. Web端末の再生テストには、Player+の[TCPlayerLiteプレーヤー](https://cloud.tencent.com/document/product/881/20207)を選択して再生することをお勧めします。具体的な内容は、[CSS再生](https://intl.cloud.tencent.com/document/product/267/31559)をご参照ください。
   4. モバイル端末のCSSストリームテストには、[Tencent CloudツールキットApp](https://intl.cloud.tencent.com/zh/document/product/1071/38147）#rtmpdemo)をダウンロードしてインストールすることをお勧めします。開いたら、【モバイルライブストリーミングMLVB】>【標準ライブストリーミング再生】を選択し、レコーディング再生アドレスを手入力、または2次元コードをスキャンしてアドレス編集枠内に取り込み、左下角の再生ボタンをクリックすれば、再生して視聴できます。

>? Appの中でプッシュ/再生を行う必要がある場合は、[モバイルライブストリーミングSDK](https://intl.cloud.tencent.com/product/mlvb)を統合すれば、CSSサービスと結合させて使用することができます。テスト運用プロセスにおいて問題に遭遇したときは、CSSの[よくあるご質問](https://intl.cloud.tencent.com/document/product/267/7968)のQAをご覧いただくことをお勧めします。

## 関連操作
- **CSSレコーディング**を有効にしたい場合は、レコーディングテンプレートを作成し、ドメイン名との関連付けを設定することができます。関連ドキュメントについては、[レコーディングテンプレートの作成](https://intl.cloud.tencent.com/document/product/267/34223)をご参照ください。
- **CSSトランスコード**を有効にしたい場合は、トランスコードテンプレートを作成し、ドメイン名との関連付けを設定することができます。関連ドキュメントについては、[トランスコードテンプレートの作成](https://intl.cloud.tencent.com/document/product/267/31071)をご参照ください。
- **CSSウォーターマーク**を有効にしたい場合は、ウォーターマークテンプレートを作成し、ドメイン名との関連付けを設定することができます。関連ドキュメントについては、[ウォーターマークテンプレートの作成](https://intl.cloud.tencent.com/document/product/267/31073)をご参照ください。
- **CSSスクリーンキャプチャ・ポルノ検出**を有効にしたい場合は、スクリーンキャプチャ・ポルノ検出テンプレートを作成し、ドメイン名との関連付けを設定することができます。関連ドキュメントについては、[スクリーンキャプチャ・ポルノ検出テンプレートの作成](https://intl.cloud.tencent.com/document/product/267/31072)をご参照ください。
- **ライブミクスストリーミング機能**を実装したい場合は、ミクスストリーミングAPIを呼び出して実装することができます。関連ドキュメントについては、[ライブミクスストリーミング](https://intl.cloud.tencent.com/document/product/267/35997)をご参照ください。




## よくあるご質問
- [プッシュ、ライブストリーミング、オンデマンドとは何ですか。](https://intl.cloud.tencent.com/document/product/267/7968#.E6.8E.A8.E6.B5.81.E3.80.81.E7.9B.B4.E6.92.AD.E5.92.8C.E7.82.B9.E6.92.AD.E5.88.86.E5.88.AB.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
- [どのようなプッシュプロトコルがサポートされているのですか。](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.8E.A8.E6.B5.81.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [どのような再生プロトコルがサポートされているのですか。](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.92.AD.E6.94.BE.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [再生アドレスはどのような構成ですか。](https://intl.cloud.tencent.com/document/product/267/7968#.E6.92.AD.E6.94.BE.E5.9C.B0.E5.9D.80.E7.94.B1.E4.BB.80.E4.B9.88.E7.BB.84.E6.88.90.EF.BC.9F)
- [どのように複数のライブストリーミングURLをスプライシングして生成しますか。](https://intl.cloud.tencent.com/document/product/267/38393)
