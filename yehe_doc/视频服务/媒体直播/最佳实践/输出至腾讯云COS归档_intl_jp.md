StreamLiveは、HLSファイルのTencent Cloud COSへのエクスポート、アーカイブをサポートします。お客様はあらかじめCOSでバケットの作成を完了し、StreamLiveのバケットへのアクセス権を付与する必要があります。

1. COSサービスのアクティブ化とCOSバケットの作成

COSアーカイブへの出力を開始する前に、[Tencent Cloud COSサービスのアクティブ化](https://console.cloud.tencent.com/cos5)をすでに行っていることを確認してください。COSサービスのアクティブ化完了後、[COSバケットコンソール](https://console.cloud.tencent.com/cos5)で【バケットリスト】を選択し、【バケットの作成】をクリックして、近くのリージョンのCOSバケットを作成します。

![img](https://main.qcloudimg.com/raw/258a128f8e010886f7bea5b6dac83c72.png)

2. 出力タイプとしてHLS_ARCHIVEを選択します。StreamLiveコンソールに戻り、出力を設定するときに、出力タイプとしてHLS_ARCHIVEを選択します。

![img](https://main.qcloudimg.com/raw/5e782e85e27d4f860d9921cc86f1165f.png)

3. StreamLiveのCOSバケットへのアクセス権を承認します。StreamLiveにCOSバケットへのアクセス権を承認していない場合、COS宛先フィールドはグレー表示になり、入力ができません。プロンプトで【click here】をクリックして、権限承認プロンプトボックスにジャンプします。【Authorize Now】をクリックして、権限承認インターフェースに移動します。【Grant】をクリックして権限承認を完了します。

![img](https://main.qcloudimg.com/raw/5327f143f1fc7482c68225e8abad3c82.png))![img](https://main.qcloudimg.com/raw/3b3a91b1e9053f9ac0b6c9bc2955e12c.png)

権限付与が完了したら、StreamLiveインターフェースに戻り、【Authorization completed】を選択します。この時点で、COS Destinationフィールドに入力できるようになります。

![img](https://main.qcloudimg.com/raw/ee8f5a51ec6fb2642e570a9c67f91865.png))![img](https://main.qcloudimg.com/raw/41fc5c9c4a18d04b54f6585241231688.png)

4. COSアーカイブアドレスを入力します。作成したCOSバケットに基づいてCOSアーカイブアドレスを入力できます。形式は次のとおりです。http://.cos..myqcloud.com/path。

5. 設定を保存して送信します。このとき、続けて[StreamLiveチャネル管理](https://intl.cloud.tencent.com/document/product/1048/45214)のその他のchannel設定を完了し、送信して保存することができます。




