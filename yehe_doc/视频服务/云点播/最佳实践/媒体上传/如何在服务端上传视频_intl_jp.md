## ご使用にあたっての注意事項

### 内容紹介

ここでは、ビデオファイルをローカルのサーバーからVODにアップロードする方法をご紹介します。

### 費用

ここで提供するコードは無償のオープンソースですが、使用過程において以下の費用が発生することがあります。

- Tencent CloudのCloud Virtual Machine（CVM）インスタンスの購入は、アップロードスクリプトの実行に使用します。詳細は [CVM料金](https://intl.cloud.tencent.com/document/product/213/2180)をご参照ください。
- VODのストレージ容量はアップロードをプルしたビデオの保存に使用します。詳細は [ストレージ料金](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)をご参照ください。

##  CVMのビデオをVODにアップロード

### 手順1：Tencent Cloud CVMの準備<span id="p1"></span>

アップロードスクリプトは、1台のTencent Cloud CVM上で実行させる必要があります。要件は次のとおりです。

- リージョン：任意。
- モデル：公式サイトは最低構成（1コア1GB）であればOKです。
- パブリックネットワーク：パブリックIPを有する必要があります。帯域幅は1Mbps以上。
- OS：公式パブリックイメージ`Ubuntu Server 16.04.1 LTS 64ビット`または`Ubuntu Server 18.04.1 LTS 64ビット`。

CVMの購入方法は [操作ガイド - インスタンス作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。システムの再インストール方法は [操作ガイド - システム再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

>!上述の条件に適合するTencent Cloud CVMがない場合は、その他のパブリックネットワークアクセスを備えたLinux（CentOS、Debianなど）またはMac機器でスクリプトを実行することもできます。ただし、OSの違いによってスクリプトの特定のコマンドを修正する必要があります。具体的な修正方式については、開発者自身で検索してください。

### 手順2：VODのアクティブ化<span id="p2"></span>

[クイックスタート - 手順1](https://intl.cloud.tencent.com/document/product/266/8757) を参照してVODサービスをアクティブにします。

### 手順3：APIキーの取得<span id="p3"></span>

ビデオのアップロードのリクエストにはAPIキー（SecretIdおよびSecretKey）が必要です。まだキーを作成していない場合は、 [キードキュメントの作成](https://intl.cloud.tencent.com/document/product/598/34228) を参照して、新しいAPIキーを作成してください。キーを作成済の場合は、 [キードキュメントの表示](https://intl.cloud.tencent.com/document/product/598/34228) を参照してAPIキーを取得してください。

### 手順4：コードのダウンロードおよびSDKのインストール<span id="p4"></span>

 [手順1](#p1) で準備したCVM（ログイン方法の詳細は [操作ガイド - Linuxにログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください）にログインして、リモートターミナルで以下のコマンドを入力して実行します。

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/server_upload.sh
```

>?コマンドの中のSECRET_IDおよびSECRET_KEYに [手順3](#p3) で取得したコンテンツに割り当ててください。

このコマンドでは、GithubからDemoソースコードをダウンロードして、スクリプトのインストールを自動的に実行します。インストールのプロセスには数分間必要になり（CVMのネットワーク状況次第）、その間、リモートターミナルは類似した以下の情報を出力します。

```
[2020-06-23 19:56:31]pip3のインストール開始。
[2020-06-23 19:56:34]pip3のインストール成功。
[2020-06-23 19:56:34]VOD PythonアップロードSDKのインストールを開始。
[2020-06-23 19:56:36]VOD PythonアップロードSDKのインストール完了。
[2020-06-23 19:56:36]SDKパラメータの設定開始。
[2020-06-23 19:56:36]SDKパラメータの設定完了。
```

### 手順5：ビデオのアップロード<span id="p5"></span>

アップロードの開始前に、CVMでビデオファイルおよびカバーピクチャ（オプション）を準備しておく必要があります。ビデオをCVMにアップロードするのに不都合がある場合は、リモートターミナルで以下のコマンドを実行して、テストビデオおよびテストカバーをCVMにダウンロードすることができます。

```
ubuntu@VM-69-2-ubuntu:~$ wget http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/7a9b2b565285890804459281865/v.f100010.mp4 -O ~/vod-server-demo/server_upload/tencent_cloud.mp4; wget http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/8aa658d15285890804459940822/5285890804459940825.jpg -O ~/vod-server-demo/server_upload/tencent_cloud.jpg
```

`server_upload.py`スクリプトを実行してトランスコードを開始：

```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/server_upload/; python3 server_upload.py ./tencent_cloud.mp4 ./tencent_cloud.jpg
```

>?コマンドのビデオパスおよびカバー画像のパスを実際のファイルパスに置換してください。そのうち、カバー画像のパスのパラメータがオプションで、空のままにすると、アップロード後のビデオにカバーは付きません。

このコマンドは、 tencent_cloud.mp4 ビデオを VODにアップロードすると同時に、アップロードした tencent_cloud.jpg 画像をそのカバーにします。アップロードの完了後、リモートターミナルは以下のような情報を出力します。

```
{"CoverUrl": "http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/8aa658d15285890804459940822/5285890804459940825.jpg", "FileId": "5285890804459940822", "MediaUrl": "http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/8aa658d15285890804459940822/f0.mp4", "RequestId": "84a7fb42-9f05-4acd-9cc8-843690b188ce"}
```

>?自身のビデオを使用してテストを行う場合は、CVM帯域幅が不足のためにアップロード時間がかかりすぎないように、小さめのビデオファイル（例えば数MB）を使用することをお勧めします。

### 手順6：結果の表示<span id="p6"></span>

コンソールの [ビデオ管理](https://console.cloud.tencent.com/vod/media) 画面で、アップロードしたビデオファイルおよびカバーを見ることができます。

## コードの解釈

1. `main()`はスクリプトのエントリー。
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
<td>procedure</td>
<td>String</td>
<td>タスクフロー名。ビデオのアップロード完了後、そのタスクフローは自動的にトリガーされます。デフォルトは空です。</td>
</tr>
<tr>
<td>subappid</td>
<td>String</td>
<td>ビデオを <a href="https://intl.cloud.tencent.com/document/product/266/33987" target="_blank">VODサブアプリケーション</a>にアップロードしますか</td>
</tr>
</tbody></table>

	>?このDemoは、`procedure`および`subappid`の2つのアップロードパラメータのみをサポートしています。すべての機能については、[PythonアップロードSDKインターフェースの記述](https://intl.cloud.tencent.com/document/product/266/33917)をご参照ください。
3. コマンドラインパラメータから、アップロードするビデオファイルのローカルパスおよびカバー画像パス（カバーがある場合）を取得してから、`upload_media()`を呼び出してアップロードを開始します。
```
       if len(sys.argv) < 2:
           usage()
           return
       video_path = sys.argv[1]
       cover_path = sys.argv[2] if len(sys.argv) > 2 else ""
   
       # アップロードの開始
       rsp = upload_media(configuration, video_path, cover_path)
```
4. `upload_media()`で、Python SDKが提供する方法を使用して、1個のアップロードインスタンス`client`を構築します。その後、`req`にアップロードパラメータを設定して、最後にアップロードを開始します。
   ```
           client = VodUploadClient(conf["secret_id"], conf["secret_key"])
           req = VodUploadRequest()
   
           req.MediaFilePath = video
           if cover != "":
               req.CoverFilePath = cover
           if conf["procedure"] != "":
               req.Procedure = conf["procedure"]
           req.SubAppId = int(conf["subappid"])
   
           rsp = client.upload("ap-guangzhou", req)
           return rsp
   ```
>!`client.upload()`の最初のパラメータ（`"ap-guangzhou"`）は、アップロードされたインスタンスのアクセスリージョンです。ビデオのアップロードされたビデオのストレージリージョンではありません。そのパラメータは`"ap-guangzhou"`に固定するだけです。アップロードしたビデオのストレージリージョンを指定する場合は、`req.StorageRegion`パラメータを設定してください。

## その他の機能

VOD サーバーからアップロードするSDKは、その他の機能もサポートしています。ビデオ名、分類、期限切れなどを設定する場合の詳細情報は、対応する言語の SDK開発ガイドをご参照ください。

- [Java](https://intl.cloud.tencent.com/document/product/266/33914)
- [C#](https://intl.cloud.tencent.com/document/product/266/33915)
- [PHP](https://intl.cloud.tencent.com/document/product/266/33916)
- [Python](https://intl.cloud.tencent.com/document/product/266/33917)
- [Golang](https://intl.cloud.tencent.com/document/product/266/33919)

