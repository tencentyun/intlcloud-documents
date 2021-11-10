

## ご使用にあたっての注意事項

### 内容紹介

ここでは開発者にVODでビデオをトランスコードする方法およびトランスコードした後の出力結果を取得する方法をご紹介します。

### 料金

ここで提供するコードは無償のオープンソースですが、使用過程において以下の料金が発生することがあります。

- Tencent Cloud APIのリクエストスクリプトの実行に使用するため、Tencent CloudのCloud Virtual Machine（CVM）を購入します。詳細については [CVM料金](https://intl.cloud.tencent.com/document/product/213/2180)をご参照ください。
- VODのストレージ容量はアップロードしたビデオの保存に使用します。詳細は [ストレージ料金](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。
- VODのトランスコードサービスは、ビデオをトランスコードするのに使用します。詳細は [トランスコード料金](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。
- VODのトラフィックはビデオ再生に使用されます。詳細は [トラフィック課金](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。

### パラメータ紹介
Tencent Cloud VODビデオトランスコードは現在、以下のビデオフォーマットをサポートしています。
<table>
   <tr>
      <th width="0px" style="text-align:center">パラメータ</td>
      <th width="0px" style="text-align:center">タイプ</td>
      <th width="0px"  style="text-align:center">詳細説明</td>
   </tr>
   <tr>
      <td rowspan='2' style="text-align:center">入力形式</td>
      <td>コンテナ形式</td>
      <td>WMV、RM、MOV、MPEG、MP4、3GP、FLV、AVI、RMVB、TS、ASF、MPG、WEBM、MKV 、M3U8、WM、ASX、RAM、MPE、VOB、DAT、MP4V、M4V、F4V、MXF、QT、OGG</td>
   </tr>
   <tr>
      <td>ビデオコーデック形式</td>
      <td>AV1、AVS2、H.264/AVC、H.263、 H.263+、H.265、MPEG-1、MPEG-2、MPEG-4、MJPEG、VP8、VP9、Quicktime、RealVideo、Windows Media Video</td>
   </tr>
   <tr>
      <td rowspan='4' style="text-align:center">出力形式</td>
      <td rowspan='3'>コンテナ形式</td>
      <td>ビデオ：FLV、MP4、HLS（m3u8+ts）</td>
   </tr>
   <tr>
      <td>オーディオ：MP3、MP4、OGG、FLAC、m4a</td>
   </tr>
   <tr>
      <td>画像：GIF、WEBP</td>
   </tr>
   <tr>
      <td>ビデオコーデック形式</td>
      <td>H.264/AVC, H.265/HEVC,AV1</td>
   </tr>
</table>

トランスコードの目標仕様には、エンコード形式、解像度、ビットレートなどのパラメータがあります。VODではトランスコードテンプレートを使用してトランスコードパラメータのグループを表します。トランスコードテンプレートによって、以下のトランスコード関連パラメータを指定することができます。 [ビデオ処理の概要](https://intl.cloud.tencent.com/document/product/266/33930）をご参照ください。
<table>
   <tr>
      <th width="108px" style="text-align:center" >分類</td>
      <th width="200px" style="text-align:center">パラメータ</td>
      <th width="0px"  style="text-align:center">説明</td>
   </tr>
   <tr>
      <td rowspan='7' width="0px" style="text-align:center">ビデオコーデック</td>
      <td>コーデック（Codec）</td>
      <td>H.264、H.265およびAV1コーデックをサポート</td>
   </tr>
	  <tr>
      <td>ビットレート（Bitrate）</td>
      <td>サポートするビデオビットレートの範囲：10kbps～35Mbps</td>
   </tr>
	    <tr>
      <td>フレームレート（Frame Rate）</td>
      <td>サポートするフレームレートの範囲：1fps～60fps。一般的なフレームレートは24fps、25fps、30fps</td>
   </tr>
	    <tr>
      <td>解像度（Resolution）</td>
      <td><li>サポートする幅の範囲：128px ～4096px</li><br><li>サポートする高さの範囲：128px ～4096px</li><br></td>
   </tr>
	    <tr>
      <td>GOP長さ</td>
      <td>サポートするGOP長さの範囲：1秒～10秒</td>
   </tr>
	    <tr>
      <td>プロファイル（Profile）</td>
      <td><li>ビデオコーデックがH.264の時は、Baseline、Main、Highのプロファイルをサポートします</li><br><li>ビデオコーデックがH.265の時は、Mainのプロファイルのみをサポートします</li><br></td>
   </tr>
	    <tr>
      <td>カラースペース（Color Space）</td>
      <td>YUV420Pをサポートします</td>
   </tr>
</table>

>?
>- **コーデック**：特定の圧縮技術によって、任意のビデオフォーマットのファイルを、別のビデオフォーマットファイルに変換する方法を指します。H265はH.264に比べてさらに先進的なコーデックトランスコードを採用し、元の画質が低下しない前提で、ビットレートを大幅に削減し、再生帯域幅を削減できます。
>- **ビットレート**：エンコーダが1秒間に発生させるデータの大きさで、単位はkbpsとし、800kbpsの場合、エンコーダが1秒間に800kbのデータを生成することを表わします。
>- **フレームレート（FPS）**：1秒間に何枚のフレームが必要かを指します。
>- **解像度**：単位インチの中に含まれる画素のドット数。
>- **GOP**：通常は2つのフレームの間隔を指します

通常のトランスコードについては、その明瞭度により、使用に推奨されるビットレート、解像度および設定区間は下表に示すとおりです。

| **明瞭度** | **推奨ビットレート** | **推奨解像度** | **解像度区間**            |
| ------- | -------- | --------- | -------------------- |
| SD      | 600      | 640x480   | 標準 SD（短辺 ≤ 480px）    |
| HD      | 2000      | 1280x720   | 高精細度 HD（短辺 ≤ 720px）    |
| FHD      | 4000      | 1920x1080   | フル高精細度 FHD（短辺 ≤ 1080px）    |
| 2K      | 6000     | 2560x1440 | 2K（短辺 ≤ 1440px）      |
| 4K      | 8000     | 3840x2160 | 4K（短辺 ≤ 2160px）      |

Tencent Cloud VOD特有の超高速HD（TESHD）は画質の修復と増強、コンテンツアダプティブパラメータの選択、V265エンコーダなど一連のビデオ処理ソリューションを統合しています。ビデオにさらに小さく、さらに明瞭なトランスコード方法を提供し、ネットワークリソースの低消費を保証すると同時に、さらに優れた視覚体験をユーザーにもたらします。VODも各種の解像度をプリセットしました。具体的なパラメータは次のとおりです。

| **明瞭度** | **推奨ビットレート** | **推奨解像度** | **解像度区間**            |
| ------- | -------- | --------- | -------------------- |
| SD      | 350または設定しない      | 640x480   | 標準 SD（短辺 ≤ 480px）    |
| HD      | 1350または設定しない      | 1280x720   | 高精細度 HD（短辺 ≤ 720px）    |
| FHD      | 2700または設定しない      | 1920x1080   | フル高精細度FHD（短辺 ≤ 1080px）    |
| 2K      | 3500または設定しない  | 2560x1440 | 2K（短辺 ≤ 1440px）      |
| 4K      | 7500または設定しない  | 3840x2160 | 4K（短辺 ≤ 2160px）      |

>?設定しない場合、超高速HD（TESHD）はビデオソースのインテリジェント分析に基づき、ビデオの最低ビットレートを設定します。

## コンソールでのトランスコードの開始

### 手順1：VODのアクティブ化[](id:p11)

[クイックスタート - 手順1](https://intl.cloud.tencent.com/document/product/266/8757) を参照してVODサービスをアクティブにします。

### 手順2：ビデオのアップロード[](id:p12)

[クイックスタート - 手順2](https://intl.cloud.tencent.com/document/product/266/8757) を参照して、1個のテストビデオをアップロードします。 [ここ](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) をクリックして、Demoで使用されるテストビデオを表示します。対応するFileIdは下図に示すとおり8602268010602075659です。
![](https://qcloudimg.tencent-cloud.cn/raw/9d10415aff42613a6b9899c552d053d2.png)

>?トランスコードに時間がかかりすぎないように、短めのビデオファイルを使用してテストすることをお勧めします（例えば数十秒間のビデオ）。

### 手順3：トランスコードの開始[](id:p13)

コンソールの [ビデオ管理](https://console.cloud.tencent.com/vod/media) 画面でアップロードされたテストビデオにチェックを入れた後、【ビデオ処理】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/9d10415aff42613a6b9899c552d053d2.png)
ポップアップウィンドウで処理タイプを【トランスコード】に選択してから、【トランスコードテンプレート】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/bb552a5454fe649f2b61edf2d5fe50fa.png)
必要なトランスコードテンプレートを選択してから【OK】をクリックします。このDemoでは、プリセットテンプレートのSTD-H264-MP4-360P（テンプレートID 100010）およびSTD-H264-MP4-540P（テンプレートID 100020）を例にしています。カスタマイズしたトランスコードテンプレートを使用する場合は、[テンプレート設定ドキュメント](https://intl.cloud.tencent.com/document/product/266/14059)をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/d26764d535ee63e216969e21ee7e6e46.png)
【OK】をクリックしてトランスコードを開始します。
![](https://qcloudimg.tencent-cloud.cn/raw/e370f7ee3ae245e5b97d47fa383e2be8.png)
「ビデオ管理」画面でテストビデオのステータスが「処理中」になっていることを確認できます。これはビデオがトランスコードされていることを示します。
![](https://qcloudimg.tencent-cloud.cn/raw/9c329fbf018cd251c2280d2df453f041.png)

### 手順4：トランスコードの結果を確認[](id:p14)

コンソールの [ビデオ管理](https://console.cloud.tencent.com/vod/media) 画面でテストビデオのステータスが「正常」に変わるのを待ちます。これはトランスコーディングが完了したことを示します。テストビデオの右側の【管理】をクリックしてビデオ管理画面に進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/be5fa72994d786fa6737bf3590d4324f.png)
「基本情報」タブ画面の【標準トランスコーディングリスト】で STD-H264-MP4-360P と STD-H264-MP4-540Pの2つの仕様で出力されます。開発者は右側の【プレビュー】をクリックしてビデオを直接視聴できます。さらに【アドレスコピー】をクリックしてトランスコードされたビデオのURLをコピーして、その他のチャネルによって視聴者に公開することもできます。
![](https://qcloudimg.tencent-cloud.cn/raw/48867ad69971690bc6a528cf9f14473c.png)

## Tencent Cloud APIを呼び出してトランスコードを開始

### 手順1：Tencent Cloud CVMの準備[](id:p21)

Tencent Cloud APIのリクエストスクリプトは、1台のTencent Cloud CVM上で実行させる必要があります。要件は次のとおりです。

- リージョン：任意。
- モデル：公式サイトは最低構成（1コア1GB）であればOKです。
- パブリックネットワーク：パブリックIPを有する必要があります。帯域幅は1Mbps以上。
- OS：公式パブリックイメージ`Ubuntu Server 16.04.1 LTS 64ビット`または`Ubuntu Server 18.04.1 LTS 64ビット`。

CVMの購入方法は [操作ガイド - インスタンス作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。システムの再インストール方法は [操作ガイド - システム再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

>!上述の条件に適合するTencent Cloud CVMがない場合は、その他のパブリックネットワークアクセスを備えたLinux（CentOS、Debianなど）またはMac機器でスクリプトを実行することもできます。ただし、OSの違いによってスクリプトの特定のコマンドを修正する必要があります。具体的な修正方式については、開発者自身で検索してください。

### 手順2：APIキーの取得[](id:p22)

Tencent Cloud APIのリクエストにはAPIキー（SecretIdおよびSecretKey）が必要です。まだキーを作成していない場合は、[キー作成ドキュメント](https://intl.cloud.tencent.com/document/product/598/34228) を参照して、新しいAPIキーを作成してください。キーを作成済の場合は、 [キー表示ドキュメント](https://intl.cloud.tencent.com/document/product/598/34228) を参照してAPIキーを取得してください。

### 手順3：VODのアクティブ化[](id:p23)

[クイックスタート - 手順1](https://intl.cloud.tencent.com/document/product/266/8757) を参照してVODサービスをアクティブにします。

### 手順4：ビデオのアップロード[](id:p24)
[クイックスタート - 手順2](https://intl.cloud.tencent.com/document/product/266/8757) を参照して、1個のテストビデオをアップロードします。 [ここ](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) をクリックして、Demoで使用されるテストビデオを表示します。対応するFileIdは下図に示すとおり5285890804162014755です。
![](https://qcloudimg.tencent-cloud.cn/raw/fb2ac8243834a909cee60aaf19426bea.png)

>?トランスコードに時間がかかりすぎないように、短めのビデオファイルを使用してテストすることをお勧めします（例えば数十秒間のビデオ）。


### 手順5：トランスコードの開始[](id:p25)

[手順1](#p21) で準備したCVM（ログイン方法の詳細は [操作ガイド - Linuxにログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください）にログインして、リモートターミナルで以下のコマンドを入力して実行します。
```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/transcode_api.sh
```
>?コマンドの中のSECRET_IDおよびSECRET_KEYに [手順2](#p22) で取得したコンテンツに割り当ててください。

このコマンドでは、GithubからDemoソースコードをダウンロードして、インストールスクリプトを自動的に実行します。インストールのプロセスには数分間必要になり（CVMのネットワーク状況次第）、その間、リモートターミナルは以下に示す情報を出力します。
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

### 手順6：トランスコードの結果を確認[](id:p14)

「ビデオ管理」画面でテストビデオのステータスが「処理中」になっていることを確認できます。これはビデオがトランスコードされていることを示します。
![](https://qcloudimg.tencent-cloud.cn/raw/5fcd99f766d6587f1644daac23c10d4d.png)
テストビデオのステータスが「正常」に変わるのを待ちます。これはトランスコードが完了したことを示します。テストビデオの右側の【管理】をクリックすると、ビデオ管理画面に進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/be5fa72994d786fa6737bf3590d4324f.png)
「基本情報」タブ画面の【標準トランスコーディングリスト】で、対応する仕様のビデオが出力されます。開発者は右側の【プレビュー】をクリックしてビデオを直接視聴できます。さらに【アドレスコピー】をクリックしてトランスコードされたビデオのURLをコピーして、その他のチャネルによって視聴者に公開することもできます。
![](https://qcloudimg.tencent-cloud.cn/raw/9067b71ebcac7658c58222499f47fcf0.png)

## ビデオアップロード後の自動トランスコード（タスクフロー）

VODは、コンソールからのアップロード、サーバーからのアップロード、クライアントからのアップロード、URLからのプルアップロードなどの複数の種類のビデオアップロード方法があります（詳細は [メディアアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760) をご参照ください）。アップロード方法はすべて指定した1個の [タスクフロー](https://intl.cloud.tencent.com/document/product/266/33931)をサポートしていて、アップロードの完了後にトランスコードを自動的にトリガーします。

## ビデオアップロード後の自動トランスコード（イベント通知）

VODバックエンドは、ビデオアップロードの完了後およびトランスコードタスクの完了後に、 [イベントの通知](https://intl.cloud.tencent.com/document/product/266/33948) リクエストを開始します。イベント通知システムを使用して、新しくアップロードされたビデオのトランスコードを開始し、イベント通知によってトランスコード結果を自動的に取得できます（ここに表示した方法は、コンソールでトランスコード結果を手動で表示するものです）。イベント通知の使用方法は、ベストプラクティスのドキュメント単独の[イベント通知の受信](https://intl.cloud.tencent.com/document/product/266/37542)に詳細な説明があります。

