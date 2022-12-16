## ご使用にあたっての注意事項

### Demo機能紹介

ここではビデオのアップロード、トランスコードのフローを例に、開発者にVODの[イベント通知システム](https://intl.cloud.tencent.com/document/product/266/33948) の使用方法について表示します。

### アーキテクチャおよびフロー

Demoは、クラウド関数（SCF）を基にHTTPサービスを構築して、VODからのイベント通知リクエストを受信するのに使用します。このサービスは、NewFileUpload（[ビデオアップロード完了イベント通知](https://intl.cloud.tencent.com/document/product/266/33950)）および ProcedureStateChanged（[タスクフロー状態の変更](https://intl.cloud.tencent.com/document/product/266/33953)）を処理することによって、ビデオトランスコードの開始およびトランスコード結果の取得を実現します。

システムは主に4つの構成部分に及びます：コンソール、API Gateway、Serverless Cloud Function、VODであり、このうちAPI GatewayおよびServerless Cloud Functionは、下図に示すとおりこのDemoのデプロイオブジェクトです。
<img src="https://qcloudimg.tencent-cloud.cn/raw/ec5a27df9988417547c884df4ac28816.png" width="550">

具体的な業務フローは次のとおりです：

1. コンソールでビデオをVODにアップロードします。
2. VODバックエンドはNewFileUploadイベント通知リクエストを起動してDemoに送ります。
3. Demoはイベント通知コンテンツを解析し、VODの [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) インターフェースを呼び出して、アップロードされたばかりのビデオのトランスコードを開始します。使用するトランスコードテンプレートは [システムプリセットテンプレート](https://intl.cloud.tencent.com/document/product/266/33932) の100010および100020です。
4. VODはトランスコードタスクを完了後、DemoへのProcedureStateChangedイベント通知リクエストを開始します。
5. Demoはイベント通知コンテンツを解析して、トランスコードされた出力ファイルのURLをSCFログに出力します。

> ?DemoのSCFコードはPython3.6を使用して開発されており、このほかSCFはPython2.7、Node.js、Golang、PHP、Javaなどの複数のプログラミング言語もサポートしています。開発者は状況に応じて自由に選択できます。詳細は [SCF開発ガイド](https://intl.cloud.tencent.com/document/product/583/11061)をご参照ください。

### 費用

ここで提供するVODイベント通知の受信サービスであるDemoは無料のオープンソースですが、構築および使用のプロセスにおいて以下の費用が発生することがあります。

- Tencent CloudのCloud Virtual Machine（CVM）インスタンスの購入は、サービスデプロイスクリプトの実行に使用します。詳細は [CVM料金](https://intl.cloud.tencent.com/document/product/213/2180)をご参照ください。
- SCFを使用して署名配布サービスを提供するには、 [SCF料金](https://intl.cloud.tencent.com/document/product/583/12284) および [SCF無料限度額](https://intl.cloud.tencent.com/document/product/583/12282)をご参照ください。
- Tencent Cloud API Gatewayを使用して、 SCFのために外部ネットワークインターフェースを提供します。詳細は [API Gateway料金](https://intl.cloud.tencent.com/document/product/628/11771)をご参照ください。
- VODのストレージ容量はアップロードしたビデオの保存に使用します。詳細は [ストレージ料金](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)をご参照ください。
- VODのトランスコードサービスは、ビデオをトランスコードするのに使用します。詳細は [トランスコード料金](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)をご参照ください。

<span id="p0"></span>
### 本番環境への影響の回避

イベント通知受信サービスDemoの業務ロジックはVODイベント通知システムで使用します。このため、デプロイプロセスでは、開発者がイベント通知アドレスを設定する必要があります。そのアカウントがVODに基づく本番環境をすでに有していると、イベント通知アドレスの変更は業務上の不具合を生じることがあります。**操作前には本番環境に影響しないことを必ず確認し、確定できない場合は、すべて新しいアカウントに交換して Demoをデプロイしてください**。

## イベント通知受信サービスのクイックデプロイ
<span id="p1"></span>
### 手順1：Tencent Cloud CVMの準備

デプロイスクリプトは、1台のTencent Cloud CVM上で実行させる必要があります。要件は次のとおりです。

- リージョン：任意。
- モデル：公式サイトは最低構成（1コア1GB）であればOKです。
- パブリックネットワーク：パブリックIPを有する必要があります。帯域幅は1Mbps以上。
- OS：公式パブリックイメージ`Ubuntu Server 16.04.1 LTS 64ビット`または`Ubuntu Server 18.04.1 LTS 64ビット`。

CVMの購入方法は [操作ガイド - インスタンス作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。システムの再インストール方法は [操作ガイド - システム再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

>!
>- イベント通知受信サービスDemo自身はCVMに依存していません。CVMを使用してデプロイスクリプトを実行しているだけです。
>- 上述の条件に適合するTencent Cloud CVMがない場合は、その他のパブリックネットワークアクセスを備えたLinux（CentOS、Debianなど）またはMac機器でデプロイスクリプトを実行することもできます。ただし、OSの違いによってスクリプトの特定のコマンドを修正する必要があります。具体的な修正方式については、開発者自身で検索してください。
<span id="p2"></span>
### 手順2：VODのアクティブ化

[クイックスタート - 手順1](https://intl.cloud.tencent.com/document/product/266/8757) を参照してVODサービスをアクティブにします。
<span id="p3"></span>
### 手順3：APIキーおよびAPPIDの取得

イベント通知受信サービスDemoのデプロイおよび実行では、開発者のAPIキー（すなわちSecretIdおよびSecretKey）およびAPPIDを使用する必要があります。

- まだキーを作成していない場合は、 [キードキュメントの作成](https://intl.cloud.tencent.com/document/product/598/34228) を参照して、新しいAPIキーを作成してください。キーを作成済の場合は、 [キードキュメントの表示](https://intl.cloud.tencent.com/document/product/598/34228) を参照してAPIキーを取得してください。
- コンソールの [アカウント情報](https://console.cloud.tencent.com/developer) 画面で下部に示すとおり、APPIDを表示することができます。
  ![](https://main.qcloudimg.com/raw/6c9fe4238232392c8d914f9ebf0f53aa.png)
<span id="p4"></span>
### 手順4：イベント通知受信サービスのデプロイ

 [手順1で準備したCVM](#p1)（ログイン方法の詳細は [操作ガイド - Linuxにログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください）にログインして、リモートターミナルで以下のコマンドを入力して実行します。

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;export APPID=125xxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/callback_scf_en.sh
```

>?コマンドの SECRET_ID、SECRET_KEY 、APPIDを [手順3](#p3) で取得したコンテンツに割り当ててください。

このコマンドでは、GithubからDemoソースコードをダウンロードして、スクリプトのインストールを自動的に実行します。インストールのプロセスには数分間必要になり（CVMのネットワーク状況次第）、その間、リモートターミナルは以下に示す情報を出力します。

```
[2020-06-05 17:16:08]npmの検査を開始します。
[2020-06-05 17:16:12]npmのインストール成功。
[2020-06-05 17:16:12]ServerLessのインストール開始。
[2020-06-05 17:16:13]Serverlessのインストール成功。
[2020-06-05 17:16:14]VODのイベント通知受信サービスのデプロイ開始。
[2020-06-05 17:16:24]VODのイベント通知受信サービスのデプロイ完了。
[2020-06-05 17:16:26]サービスアドレス：https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/callback
```

出力ログのイベント通知受信サービスアドレス（例の`https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/callback`）をコピーします。

> !出力ログで以下に示す警告が現れた場合は、通常CVMはデプロイしたばかりのサービスドメイン名を直ちに解析できないことから、その警告は無視してもかまいません。
> ```
> [2020-04-25 17:18:44]警告：イベント通知受信サービステストをクリアしていません。
> ```

### 手順5：イベント通知アドレスの設定

 [本番環境への影響の回避](#p0) の節で記述したとおり、操作前にまずオンライン業務がVODイベント通知に依存していないことを確認してください。

 [VODコンソール](https://console.cloud.tencent.com/vod/callback)にログインして、【設定】をクリックし、コールバックモードで【通常のコールバック】を選択します。コールバックURLとして [手順4](#p4)で取得したイベント通知受信サービスアドレスを入力します。すべてのコールバックイベントを確認して、下図に示すとおり【OK】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/0e5631bc9013b6e30283a7ac5411e332.png)

>!コンソールに2個のコールバックURL設定（2.0バージョン形式および3.0バージョン形式）が同時にあった場合は、3.0バージョンを設定してください。

### 手順6：Demoテスト

 [ビデオのアップロード - ローカルからのアップロード手順](https://intl.cloud.tencent.com/document/product/266/33890) の説明に従って、1個のテストビデオをVODにアップロードして、アップロード中にデフォルトの【アップロードのみ、ビデオは実施しない】を選択します。アップロードの完了後は、「アップロード済み」タブの画面でそのビデオの状態が「処理中」になっていることが確認できます。このことは、DemoがNewFileUploadイベント通知を受信して、トランスコードリクエストを起動させたことを示しています。


ビデオ処理が完了するのを待ってから（ステータスが「正常」に変わります）、【クイックビュー】をクリックすれば、画面右側に、そのビデオの2つのトランスコードされたビデオがあることが確認できます。

[SCFコンソールログ画面](https://console.cloud.tencent.com/scf/list-detail?rid=1&ns=vod_demo&id=callback&menu=log) にログインして、SCFのログを表示します。最新のログで、2個のトランスコードされたファイルのURLが印刷されていることが確認できます。実際のユースケースでは、開発者はSCFを使用してURLを自身のデータベースに記録するか、その他のチャンネルを通じて視聴者に公開することができます。
>?SCFログにはいくらかのディレイが生じることがあります。画面上にログが見当たらない場合は、1～2分間待ってから【リセット】をクリックして更新してください。
<span id="design"></span>
## システム設計の説明

### インターフェースプロトコル

イベント通知受信関数は、API Gatewayによって外部にインターフェースを提供します。具体的なインターフェースプロトコルについては、 [ビデオアップロード完了イベント通知](https://intl.cloud.tencent.com/document/product/266/33950) および [タスクフロー状態の変更](https://intl.cloud.tencent.com/document/product/266/33953)をご参照ください。

### イベント通知受信サービスコードの解釈

1. `main_handler()`はエントリー関数です。
2. `parse_conf_file()`を呼び出して、`config.json`ファイルから設定情報を読み取ります。設定項目の説明は以下のとおりです。
<table>
<thead>
<tr>
<th>フィールド</th>
<th>データ型</th>
<th>機能</th>
</tr>
</thead>
<tbody><tr>
<td>secret_id</td>
<td>String</td>
<td>APIキー</td>
</tr>
<tr>
<td>secret_key</td>
<td>String</td>
<td>APIキー</td>
</tr>
<tr>
<td>region</td>
<td>String</td>
<td>TencentCloud APIリクエストリージョン。VODについて自由に入力できます</td>
</tr>
<tr>
<td>definitions</td>
<td>Array of Integer</td>
<td>トランスコードテンプレート</td>
</tr>
<tr>
<td>subappid</td>
<td>Integer</td>
<td>イベント通知が <a href="https://intl.cloud.tencent.com/document/product/266/33987" target="_blank">VODサブアプリケーション</a>からきているか</td>
</tr>
</tbody></table>
3. NewFileUpload タイプのイベント通知の場合、`deal_new_file_event()`を呼び出してリクエストを解析して、その中から新しくアップロードされたビデオの FileIdを取得します。
```
           if event_type == "NewFileUpload":
               fileid = deal_new_file_event(body)
               if fileid is None:
                   return ERR_RETURN
```
4. `trans_media()`を呼び出してトランスコードを開始し、Tencent Cloud APIの応答パケットをSCFログに出力して、VODのイベント通知サービスに返します。
```
               rsp = trans_media(configuration, fileid)
               if rsp is None:
                   return ERR_RETURN
               print(rsp)
```
5. `trans_media()`でTencent Cloud APIのSDKを呼び出して `ProcessMedia` リクエストを開始します。
```
        cred = credential.Credential(conf["secret_id"], conf["secret_key"])
        client = vod_client.VodClient(cred, conf["region"])

        method = getattr(models, API_NAME + "Request")
        req = method()
        req.from_json_string(json.dumps(params))

        method = getattr(client, API_NAME)
        rsp = method(req)
        return rsp
```
6. ProcedureStateChanged タイプのイベント通知の場合、`deal_procedure_event()`を呼び出してリクエストを解釈して、トランスコード出力ビデオURLを取得しSCFログに出力します。
```
           elif event_type == "ProcedureStateChanged":
               rsp = deal_procedure_event(body)
               if rsp is None:
                   return ERR_RETURN
```

   
