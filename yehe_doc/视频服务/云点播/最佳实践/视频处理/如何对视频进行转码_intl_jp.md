

## ご使用にあたっての注意事項

### 内容紹介

ここでは開発者にVODでビデオをトランスコードする方法およびトランスコードした後の出力結果を取得する方法をご紹介します。

### 費用

ここで提供するコードは無償のオープンソースですが、使用過程において以下の費用が発生することがあります。

- Tencent CloudのCloud Virtual Machine（CVM）インスタンスの購入は、TencentCloud API のリクエストスクリプトの実行に使用します。詳細は [CVM料金](https://intl.cloud.tencent.com/document/product/213/2180)をご参照ください。
- VODのストレージ容量はアップロードしたビデオの保存に使用します。詳細は [ストレージ料金](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)をご参照ください。
- VODのトランスコードサービスは、ビデオをトランスコードするのに使用します。詳細は [トランスコード料金](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)をご参照ください。
- VODのトラフィックはビデオ再生に使用されます。詳細は [トラフィック課金](https://intl.cloud.tencent.com/document/product/266/14666#.E5.8A.A0.E9.80.9F.E6.9C.8D.E5.8A.A1.3Cspan-id.3D.22speed.22.3E.3C.2Fspan.3E)をご参照ください。

## コンソールでのトランスコードの開始

### 手順1：VODのアクティブ化<span id="p11"></span>

[クイックスタート - 手順1](https://intl.cloud.tencent.com/document/product/266/8757) を参照してVODサービスをアクティブにします。

### 手順2：ビデオのアップロード<span id="p12"></span>

[クイックスタート - 手順2](https://intl.cloud.tencent.com/document/product/266/8757) を参照して、1個のテストビデオをアップロードします。 [ここ](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) をクリックして、Demoで使用されるテストビデオを表示します。対応するFileIdは下図に示すとおり5285890804162014755です。
![](https://main.qcloudimg.com/raw/f8aa62bd40ab37b8cdd371798d4ff1e9.png)
>?トランスコードに時間がかかりすぎないように、短めのビデオファイルを使用してテストすることをお勧めします（例えば数十秒間のビデオ）。

### 手順3：トランスコードの開始<span id="p13"></span>

コンソールの [ビデオ管理](https://console.cloud.tencent.com/vod/media) 画面でアップロードされたテストビデオにチェックを入れた後、【VC】をクリックします：
![](https://main.qcloudimg.com/raw/cf6d8e0fa032b2a76acfd918cf5c3146.png)
ポップアップウィンドウで処理タイプを【トランスコード】に選択してから、【トランスコードテンプレート】をクリックします。
![](https://main.qcloudimg.com/raw/fc857eebabee8b5c547774fed0fe2814.png)
必要なトランスコードテンプレートを選択してから【OK】をクリックします。このDemoでは、プリセットテンプレートのMP4-FLU（テンプレートID 100010）およびMP4-SD（テンプレートID 100020）を例にしています。カスタマイズしたトランスコードテンプレートを使用する場合は、[テンプレート設定ドキュメント](https://intl.cloud.tencent.com/document/product/266/14059)をご参照ください。
![](https://main.qcloudimg.com/raw/e82be691470090beccf1ea27dbdcb4c3.png)
【OK】をクリックしてトランスコードを開始します。
![](https://main.qcloudimg.com/raw/f52ec218600e19af3e42359a90d03298.png)
「ビデオ管理」画面でテストビデオのステータスが「処理中」になっていることを確認できます。これはビデオがトランスコードされていることを示します。
![](https://main.qcloudimg.com/raw/30d3c90f55970568f55ce09be4cdb32b.png)

### 手順4：トランスコード結果の表示<span id="p14"></span>

コンソールの [ビデオ管理](https://console.cloud.tencent.com/vod/media) 画面でテストビデオのステータスが「正常」に変わるのを待ちます。これはトランスコーディングが完了したことを示します。テストビデオの右側の【管理】をクリックしてビデオ管理画面に進みます。
![](https://main.qcloudimg.com/raw/694f1b000cea813d12397fcb1c3a86a0.png)
「基本情報」タブ画面の【標準トランスコーディングリスト】でMP4-FLUおよびMP4-SDの2つの仕様で出力されます。開発者は右側の【プレビュー】をクリックしてビデオを直接視聴できます。さらに【アドレスコピー】をクリックしてトランスコードされたビデオのURLをコピーして、その他のチャンネルによって視聴者に公開することもできます。
![](https://main.qcloudimg.com/raw/38db47dcfbd840bd6d67478ce42fd1cd.png)

## Tencent Cloud APIを呼び出してトランスコードを開始

### 手順1：Tencent Cloud CVMの準備<span id="p21"></span>

Tencent Cloud APIのリクエストは、1台のTencent Cloud CVM上で実行させる必要があります。要件は次のとおりです。

- リージョン：任意。
- モデル：公式サイトは最低構成（1コア1GB）であればOKです。
- パブリックネットワーク：パブリックIPを有する必要があります。帯域幅は1Mbps以上。
- OS：公式パブリックイメージ`Ubuntu Server 16.04.1 LTS 64ビット`または`Ubuntu Server 18.04.1 LTS 64ビット`。

CVMの購入方法は [操作ガイド - インスタンス作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。システムの再インストール方法は [操作ガイド - システム再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

>!上述の条件に適合するTencent Cloud CVMがない場合は、その他のパブリックネットワークアクセスを備えたLinux（CentOS、Debianなど）またはMac機器でスクリプトを実行することもできます。ただし、OSの違いによってスクリプトの特定のコマンドを修正する必要があります。具体的な修正方式については、開発者自身で検索してください。

### 手順2：APIキーの取得<span id="p22"></span>

Tencent Cloud APIのリクエストにはAPIキー（SecretIdおよびSecretKey）が必要です。まだキーを作成していない場合は、 [キードキュメントの作成](https://intl.cloud.tencent.com/document/product/598/34228) を参照して、新しいAPIキーを作成してください。キーを作成済の場合は、 [キードキュメントの表示](https://intl.cloud.tencent.com/document/product/598/34228) を参照してAPIキーを取得してください。

### 手順3：VODのアクティブ化<span id="p23"></span>

[クイックスタート - 手順1](https://intl.cloud.tencent.com/document/product/266/8757) を参照してVODサービスをアクティブにします。

### 手順4：ビデオのアップロード<span id="p24"></span>
[クイックスタート - 手順2](https://intl.cloud.tencent.com/document/product/266/8757) を参照して、1個のテストビデオをアップロードします。 [ここ](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) をクリックして、Demoで使用されるテストビデオを表示します。対応するFileIdは下図に示すとおり5285890804162014755です。
![](https://main.qcloudimg.com/raw/f8aa62bd40ab37b8cdd371798d4ff1e9.png)
>?トランスコードに時間がかかりすぎないように、短めのビデオファイルを使用してテストすることをお勧めします（例えば数十秒間のビデオ）。


### 手順5：トランスコードの開始<span id="p25"></span>

 [手順1](#p21) で準備したCVM（ログイン方法の詳細は [操作ガイド - Linuxにログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください）にログインして、リモートターミナルで以下のコマンドを入力して実行します。
```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/transcode_api.sh
```
>?コマンドの中のSECRET_IDおよびSECRET_KEYに [手順2](#p22) で取得したコンテンツに割り当ててください。

このコマンドでは、GithubからDemoソースコードをダウンロードして、スクリプトのインストールを自動的に実行します。インストールのプロセスには数分間必要になり（CVMのネットワーク状況次第）、その間、リモートターミナルは以下に示す情報を出力します。
```
  [2020-06-15 20:39:56]pip3のインストール開始。
  [2020-06-15 20:40:06]pip3のインストール成功。
  [2020-06-15 20:40:06]Tencent Cloud API Python SDKのインストール開始。
  [2020-06-15 20:40:07]Tencent Cloud API Python SDKのインストール完了。
  [2020-06-15 20:40:07]APIパラメータの設定開始。
  [2020-06-15 20:40:07]APIパラメータの設定完了。
```
`process_media.py` スクリプトを実行してトランスコードを開始：
```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/transcode_api/; python3 process_media.py 5285890804162014755
```
>?コマンドの5285890804162014755を [手順4](#p24) で取得して実際のFileId に置換します。

このコマンドは、5285890804162014755のビデオに [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) リクエストを開始して、VOD [プリセットトランスコードテンプレート](https://intl.cloud.tencent.com/document/product/266/33932) 100010および100020の2つの仕様に基づいてトランスコードし、リクエストの応答内容を出力します：
```
{"TaskId": "1400329073-procedurev2-f6bf6f01612369b6db30f2224792a2aft0", "RequestId": "809918fb-791c-4937-b684-5027ba6bc5f0"}
```

### 手順6：トランスコード結果の表示<span id="p14"></span>

「ビデオ管理」画面でテストビデオのステータスが「処理中」になっていることを確認できます。これはビデオがトランスコードされていることを示します。
![](https://main.qcloudimg.com/raw/30d3c90f55970568f55ce09be4cdb32b.png)
テストビデオのステータスが「正常」に変わるのを待ちます。これはトランスコードが完了したことを示します。テストビデオの右側の【管理】をクリックすると、ビデオ管理画面に進みます。
![](https://main.qcloudimg.com/raw/694f1b000cea813d12397fcb1c3a86a0.png)
「基本情報」タブ画面の【標準トランスコーディングリスト】でMP4-FLUおよびMP4-SDの2つの仕様で出力されます。開発者は右側の【プレビュー】をクリックしてビデオを直接視聴できます。さらに【アドレスコピー】をクリックしてトランスコードされたビデオのURLをコピーして、その他のチャンネルによって視聴者に公開することもできます。
![](https://main.qcloudimg.com/raw/38db47dcfbd840bd6d67478ce42fd1cd.png)

## ビデオアップロード後の自動トランスコード（タスクフロー）

VODは、コンソールからのアップロード、サーバーからのアップロード、クライアントからのアップロード、URLからのプルアップロードなどの複数の種類のビデオアップロード方法があります（詳細は [メディアアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760) をご参照ください）。アップロード方法はすべて指定した1個の [タスクフロー](https://intl.cloud.tencent.com/document/product/266/33931)をサポートしていて、アップロードの完了後にトランスコードを自動的にトリガーします。

## ビデオアップロード後の自動トランスコード（イベント通知）

VODバックエンドは、ビデオアップロードの完了後およびトランスコードタスクの完了後に、 [イベントの通知](https://intl.cloud.tencent.com/document/product/266/33948) リクエストを開始します。イベント通知システムを使用して、新しくアップロードされたビデオのトランスコードを開始し、イベント通知によってトランスコード結果を自動的に取得できます（ここに表示した方法は、コンソールでトランスコード結果を手動で表示するものです）。
イベント通知の使用方法は、ベストプラクティスのドキュメントの[イベント通知の受信](https://intl.cloud.tencent.com/document/product/266/37542) に詳細な説明があります。
