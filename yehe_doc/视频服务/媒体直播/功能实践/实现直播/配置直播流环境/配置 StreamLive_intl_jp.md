[StreamLiveコンソール](https://console.tencentcloud.com/mdl/input)に進むと、左側バーに次の4つの機能設定エントリーが並んでいます。
● セキュリティグループ管理 Security Group Management。
● 入力管理 Input Management。
● チャネル管理 Channel Management。
● ウォーターマーク管理 Watermark Management。
続いて、上記の機能についてそれぞれ設定を行います。これらのうち、設定必須項目は上の3項目であり、ウォーターマークは必要に応じて設定するオプション項目です。

1. **Security Group Management**機能ページに進み、**Create Security Group**ボタンをクリックし、ポップアップしたダイアログボックスにセキュリティグループ名とIPホワイトリスト情報を入力します。IPホワイトリストはCIDR形式で入力する必要があります。複数の項目はコンマまたは改行で区切ることができます。
![](https://qcloudimg.tencent-cloud.cn/raw/46e60d979177b96851cb16dc890d6890.png)

2. **Input Management**機能ページに進み、**Create Input**をクリックして設定情報を送信します。
![](https://qcloudimg.tencent-cloud.cn/raw/8041139ea24469f261f31ebb1077f406.png)
- **Type**：プッシュプロトコルのタイプです。例ではRTMP_PUSHとしています。
- **Security Group**：バインドしたセキュリティグループです。作成済みのセキュリティグループ名をプルダウンメニューから選択し、バインドします。
- **Destination**：プッシュターゲットアドレスです。2チャネルプッシュをサポート、すなわちシステムが異なるアベイラビリティーゾーンにプッシュアドレスを設定することで、冗長ライブストリーミングリンクサービスを提供します。ここには少なくとも1つのプッシュアドレスのアプリケーション名**AppName**およびストリーム名**StreamName**を入力する必要があります。

3. **Confirm**をクリックして送信を確認した後、**Input**リストで先ほど作成したInputをクリックして詳細ページに進み、プッシュターゲットアドレスの**Destination**情報を記録します。この情報はこの後の設定の際に使用します。

4. **Channel Management**機能ページに進み、**Create Channel**をクリックし、システムから表示されるフローに従って設定情報を送信します。初めに**Basic Information**でチャネルを命名します。
![](https://qcloudimg.tencent-cloud.cn/raw/dda466604218ebfd491cfbb0dd681fb0.png)

5. **Input Setting**で、先ほど設定した**Input**をこのチャネルのライブストリーミング入力ソースとして追加します。ここでは複数の異なるInputの追加をサポートしており、その後の設定でそれぞれ異なるトランスコード出力設定を行うことができます。ここでは入力ソースが1つの場合を例にしています。
![](https://qcloudimg.tencent-cloud.cn/raw/55c4b71f066c7e18804d029c30da04b1.png)

6. **Output Group Setting**でこのチャネルのトランスコードおよび出力の設定を行います。
- 初めに基本情報を設定し、**Output Group**の命名を行います。出力タイプはプロトコルおよび形式によって3組6項目に分けられ、ここではHLS_STREAM_PACKAGEタイプを選択します。下の**Destination Information**に先ほど記録した**StreamPackage Channel ID**を入力すると、CSSトランスコードおよびパッケージ化されたワークフローがすぐにアクティブ化され、設定作業を簡略化することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/04e6469dc287247e50bf0ff198b04c78.png)
- さらに、セグメントタイプ、セグメント時間、セグメント数などを含むセグメント情報**Segment Information**をすべて入力します。AppleTVなどの特殊なデバイスについて、H.265での再生ニーズがある場合は、ここのセグメントタイプSegment Typeでfmp4を選択し、H.265パッケージタイプPacking Typeでhvc1を選択する必要があります。
![](https://qcloudimg.tencent-cloud.cn/raw/407322c8d120feec4f2fab998f33e4a6.png)

7. ページ下部に移動し、続いてトランスコードテンプレートの設定を行います。オーディオとビデオの結合トランスコードまたはオーディオかビデオのみの独立トランスコード設定を行うことができます。また、マルチビットレート出力設定もサポートしています。
![](https://qcloudimg.tencent-cloud.cn/raw/1f0b9aa788821031bb573eb52d07bbef.png)

8. 最後に最終の出力設定で、ビットレートごとの出力ストリームの命名を行い、対応するトランスコードテンプレート名にチェックを入れ、送信を確認すればすべての情報の設定が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/405e9167353c870d5f687bbc7ce8ecc1.png)

9. 最終的にチャネルリストに戻り、**Operation**列で**Start**をクリックし、このチャネルをアクティベートして起動します。
![](https://qcloudimg.tencent-cloud.cn/raw/7391eea01e3b76709be2a36f309a3f5a.png)