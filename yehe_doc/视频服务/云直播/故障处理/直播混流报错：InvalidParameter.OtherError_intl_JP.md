 ## 現象の説明
ミクスストリーミングを開始するときに、エラー報告をリマインドします。`InvalidParameter.OtherError`。

## 考えられる原因
- ミクスストリーミングの入力ソースストリームの解像度が2000を超えている。
- 特定のストリームに、20チャネルを超える同時ミクスストリーミングがある。
- アカウントはチャネルモードなのに、作成した共通ミクスストリーミングインターフェースを使用している。

## 解決方法
対応するサブエラーコードに従って、適切な処理を行います。以下に、一般的なエラーの処理方法を示します。

[](id:error1)
#### エラー報告1：`"Message":"InnerErrCode : [ -10021 ],IrnerErrMsg: [ Params Error ]"`
現在、ミクスストリーミングバックエンドでは、2000以下の解像度をサポートしています。`-10021`でエラーが報告された場合、通常、ミクスストリーミングは解像度の幅または高さが2000を超えるストリームを入力されています。

1. FFplayを使用してCSSストリームを再生し、ソースストリームの解像度を確認します。下図のように`1920*1080`である場合、制限はトリガーされません。
   使用コマンド：`ffplay -i 「再生アドレス」`。
   ![](https://main.qcloudimg.com/raw/cf074af38048408dc5b35c6db451770c.png)  
2. [VLCツールの再生](https://intl.cloud.tencent.com/document/product/267/32483)を使用する場合。
   - 【VLC】>【メディア】>【ネットワークストリーミングを開く】>【ネットワーク】を開き、アドレスを入力した後、ネットワークのCSSストリームをプルすることを確認します。
   - 【ツール】>【メディア情報】>【コーダ・デコーダ】を開くと、CSSストリームの解像度を表示できます。
     

[](id:error2)
#### エラー報告2：`"Message":"InnerErrCode:[ -41 ],InnerErrMsg: [ ]"`

ミクスストリーミングバックエンドは現在、20チャネル未満の同一ストリームの同時ミクスストリーミング数のみをサポートしています。通常、複数のキャスターがライブコマースを行う場合にのみ、同じ時間に同じチャネルのストリームを使用して、ミクスストリーミングセッションsessionとして複数回入力する必要があります。

これらの問題のほとんどは、ミクスストリーミングセッションsessionの作成によって生じます。ミクスストリーミング後にキャンセル操作を行う必要はなく、そのまま配信されるため、特定のストリームIDが複数のミクスストリーミングセッションsessionで共有されることになります。

Tencent CloudのCSSミクスストリーミングで、バックグラウンドストリームが切断されていない場合、切断されたストリーミング画面は最後のフレームで停止し、ミクスストリーミング画面に表示されます。画面に停止している最後のフレームをキャンセルするには、共通ミクスストリーミングインターフェースを呼び出し、キャンセルする必要があります。バックグラウンドストリームが切断されると、画面全体がスタックします。
- ストリームが15分以内に同じストリームIDで再度プッシュに成功すると、ミクスストリーミングは自動的に再開します。
- 2つのストリームが切断されている場合、ミクスストリーミングは15分後に自動的にキャンセルされます。


[](id:error3)
#### エラー報告3：`"Message":"InnerErrCode:[ -4 ],InnerErrMsg: [ get liveconfig failed! ]"`

このエラーは、旧バージョンのコンソールのアカウント（チャネルモード）を使用し、顧客サーバーで新しいバージョンのCSS API 3.0[ライブミクスストリーミングインターフェース](https://intl.cloud.tencent.com/document/product/267/35997)を呼び出したときに報告されます。

[CSSコンソールのアップグレード](https://intl.cloud.tencent.com/zh/document/product/267)で新しいバージョン（ライブストリーミングコードモード）にすれば、エラー報告の問題が解消されます。

[](id:error4)
#### エラー報告4：`"Message":"input stream num is not match the template id!"`

このエラーは、Tencentが提供するデフォルトのミクスストリーミングテンプレートが使用されているのに、ミクスストリーミング出力ストリームがテンプレートの要件と一致しないために報告されます。
例：10テンプレートを使用する場合、2つの入力ソースが必要です。390テンプレートを使用する場合、3つの入力ソースが必要です。これは`2つのオーディオ・ビデオストリーミング`+`1つのバックグラウンドキャンバス`です。

パラメータ設定の詳細と実際の操作については、[共通ミクスストリーミング > MixStreamTemplateIdインターフェース](https://intl.cloud.tencent.com/document/product/267/35997)をご参照ください。




[](id:error5)
#### エラー報告5：`"Message":"InnerErrCode:[ -300 ],InnerErrMsg: [ outputstreamid not avaliable, outputstreamid alread use as background in other sessionid ]"`

これは、ミクスストリーミングセッションsessionAがあり、バックグラウンド+出力ストリームとしてstreamAを使用し、その後ミクスストリーミングセッションsessionBが開始されることによります。出力ストリームがstreamAも出力する場合、このエラーが発生します。

後で再度開始されるミクスストリーミングセッションsessionBにおいて、**出力するOutputStreamNameというストリーム名**と**sessionAセッションIDの出力ストリーム名**を**同じにならないストリーム名**に設定することをお勧めします。



[](id:error6)
#### エラー報告6：`"Message":"InnerErrCode:[ -2 ],InnerErrMsg: [ small picture out of the background ]"`
小画面がバックグラウンドレイヤーよりも大きい場合、例えば、バックグラウンドが解像度`1920*1080`のキャンバスであり、小画面の幅と高さの解像度が`1280*720`で、オフセットX`（LocationX）+ 1280 >1920`またはオフセットY`（LocationY）+ 720 >1080`のときに、上記のエラーが報告されます。
- 出力画面のXオフセット。パラメータ設定に関するアドバイスについては、[共通ミクスストリーミングレイアウトパラメータ > LocationX](hhttps://intl.cloud.tencent.com/zh/document/product/267/30767#CommonMixLayoutParams)をご参照ください。
- 出力画面のYオフセット。パラメータ設定に関するアドバイスについては、[共通ミクスストリーミングレイアウトパラメータ > LocationY](hhttps://intl.cloud.tencent.com/zh/document/product/267/30767#CommonMixLayoutParams)をご参照ください。
- これ以外のクラウドミクスストリーミングテンプレートの使用例については、 [クラウドミクスストリーミング](https://intl.cloud.tencent.com/document/product/267/37665)をご参照ください。


[](id:error7)
#### エラー報告7：`"Message":"InnerErrCode:[ -111 ],InnerErrMsg: [ output_stream_type is [0],but output_stream_id xxxxx is not in input stream list ]"`
これは、設定したミクスストリーミングパラメータにおいて、[OutputStreamType](https://cloud.tencent.com/document/api/267/20474#CommonMixOutputParams)がデフォルトで0に設定されているのに、実際に出力されるストリームID名に入力したストリーム名がリストにないことから報告されるエラーです。
次の事項にご注意ください。
- 入力したOutputStreamTypeパラメータが0の場合、または入力パラメータ値がない場合は、出力OutputStreamNameパラメータに入力ストリーム名のうちの1つを設定する必要があります。
- 生成されたミクスストリーミングOutputStreamNameストリーム名を新しいストリームにすることを望む場合は、 OutputStreamTypeパラメータを1に設定する必要があります。
- OutputStreamTypeパラメータが1に設定されている場合、OutputStreamNameはInputStreamListに表示できず、ライブストリーミングバックエンドに同じIDのストリームは存在できません。

