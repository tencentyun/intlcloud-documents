## ご使用にあたっての注意事項

### 内容紹介

ここではネットワークのビデオ（URL形式での提供）をVODにプルする方法をご紹介します。

### 費用

ここで提供するコードは無償のオープンソースですが、使用過程において以下の費用が発生することがあります。

- Tencent CloudのCloud Virtual Machine（CVM）インスタンスの購入は、APIのリクエストスクリプトの実行に使用します。詳細は [CVM料金](https://intl.cloud.tencent.com/document/product/213/2180)をご参照ください。

- VODのストレージ容量はアップロードをプルしたビデオの保存に使用します。詳細は [ストレージ料金](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)をご参照ください。


### 制限

VODが提供するURLからのプル機能には以下の制限があります。

- URLはビデオファイルを直接ポイントする必要がありますが、ビデオWebサイト画面へのリンクにすることはできません。
- URL にホットリンク防止のタイムスタンプが付いている場合は、ホットリンク防止の制限（有効期間、アクセス数など）に十分な余裕があることを確認してください。余裕がない場合はアクセスが失敗する恐れがあります。
- Refererホットリンク防止のURLを有効にすることをサポートしません。
-  DASH（MPDファイルタイプ）をサポートしません。
- プルするオブジェクトがHLS（M3U8ファイルタイプ）である場合、Media Segment（通常はTSファイルタイプ）のURI要件はパラメータのない相対パスでなければなりません。

## コンソールでのプルによるアップロード
<span id="p11"></span>
### 手順1：VODのアクティブ化

[クイックスタート - 手順1](https://intl.cloud.tencent.com/document/product/266/8757) を参照してVODサービスをアクティブにします。
<span id="p12"></span>
### 手順2：プルタスクの作成

VODコンソールの [アップロード画面](https://console.cloud.tencent.com/vod/media/upload)にアクセスして、アップロード方式は【ビデオのプル】を選択してから【行の追加】をクリックして、プルするビデのURLに入力します（ここでは [テストビデオURL](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) を例にして、それ以外の項目はオプション です。開発者は必要に応じて入力入できます）。最後に左下隅の【ビデオのプル】をクリックします：

![](https://main.qcloudimg.com/raw/3871a2c05ca1f26f62e0518cb3943309.png)
>?ビデオのプルに要する時間は、 ビデオファイルのサイズに正比例します。長時間待つことのないように、テストには小さめのビデオ（例えば数10MB以下）を選択することをお勧めします。
<span id="p13"></span>
### 手順3：プル結果の表示

1～2分間待つと（ビデオファイルのサイズによって異なります）、 [メディア資産管理画面](https://console.cloud.tencent.com/vod/media) でプルが完了したビデオが表示されます。

![](https://main.qcloudimg.com/raw/7329a44db45f6cc11fa48ac41ae9cf7c.png)
>?プルのプロセス中に、ブラウザがメディア資産管理画面で動かなくなった場合は、画面をリフレッシュ しない限り、プルが完了したビデオは表示されません。

## Tencent Cloud APIを呼び出してプルによるアップロード
<span id="p21"></span>
### 手順1：Tencent Cloud CVMの準備

Tencent Cloud APIのリクエストは、1台のTencent Cloud CVM上で実行させる必要があります。要件は次のとおりです。

- リージョン：任意。
- モデル：公式サイトは最低構成（1コア1GB）であればOKです。
- パブリックネットワーク：パブリックIPを有する必要があります。帯域幅は1Mbps以上。
- OS：公式パブリックイメージ`Ubuntu Server 16.04.1 LTS 64ビット`または`Ubuntu Server 18.04.1 LTS 64ビット`。

CVMの購入方法は [操作ガイド - インスタンス作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。システムの再インストール方法は [操作ガイド - システム再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

>!上述の条件に適合するTencent Cloud CVMがない場合は、その他のパブリックネットワークアクセスを備えたLinux（CentOS、Debianなど）またはMac機器でスクリプトを実行することもできます。ただし、OSの違いによってスクリプトの特定のコマンドを修正する必要があります。具体的な修正方式については、開発者自身で検索してください。
<span id="p22"></span>
### 手順2： APIキーの取得

Tencent Cloud APIのリクエストにはAPIキー（SecretIdおよびSecretKey）が必要です。まだキーを作成していない場合は、 [キードキュメントの作成](https://intl.cloud.tencent.com/document/product/598/34228) を参照して、新しいAPIキーを作成してください。キーを作成済の場合は、 [キードキュメントの表示](https://intl.cloud.tencent.com/document/product/598/34228) を参照してAPIキーを取得してください。
<span id="p23"></span>
### 手順3：VODのアクティブ化

[クイックスタート - 手順1](https://intl.cloud.tencent.com/document/product/266/8757) を参照してVODサービスをアクティブにします。
<span id="p24"></span>
### 手順4：プルタスクの起動

 [手順1](#p21) で準備したCVM（ログイン方法の詳細は [操作ガイド - Linuxにログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください）にログインして、リモートターミナルで以下のコマンドを入力して実行します。

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/pull_upload_api.sh
```

>?コマンドの中のSECRET_IDおよびSECRET_KEYに [手順2](#p22) で取得したコンテンツに割り当ててください。

このコマンドでは、GithubからDemoソースコードをダウンロードして、スクリプトのインストールを自動的に実行します。インストールのプロセスには数分間必要になり（CVMのネットワーク状況次第）、その間、リモートターミナルは以下に示す情報を出力します。

```
[2020-07-15 17:40:13]pip3のインストール開始。
[2020-07-15 17:40:39]pip3のインストール成功。
[2020-07-15 17:40:39]Tencent Cloud API Python SDKのインストール開始。
[2020-07-15 17:40:42]Tencent Cloud API Python SDKのインストール完了。
[2020-07-15 17:40:42]APIパラメータの設定開始。
[2020-07-15 17:40:42]APIパラメータの設定完了。
```

`pull_upload.py`スクリプトを実行してトランスコードを開始：

```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/pull_upload_api/; python3 pull_upload.py http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4 API-PullUpload
```

>?コマンドのURLを、プルする実際のビデオアドレスに置換してください。

このコマンドは、指定したURLに [PullUpload](https://intl.cloud.tencent.com/document/product/266/34118) リクエストを開始して、以下の応答のような内容を出力します。

```
{"TaskId": "1400329073-PullUpload-4ea60158fc6f8e611bbfa750eb1fd0a9t0", "RequestId": "4e821b4a-9a29-409f-99cb-b703fa184e50"}
```
<span id="p25"></span>
### 手順5：プル結果の表示

1～2分間待つと（ビデオファイルのサイズによって異なります）、 [メディア資産管理画面](https://console.cloud.tencent.com/vod/media) でプルが完了したビデオが表示されます。

![](https://main.qcloudimg.com/raw/b5d62be7e0f70654483513a6885ff65b.png)
>?プルのプロセス中に、ブラウザがメディア資産管理画面で動かなくなった場合は、画面をリフレッシュ しない限り、プルが完了したビデオは表示されません。
