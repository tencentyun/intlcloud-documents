<dx-alert infotype="notice" title="">
WebRDPは、Windowsインスタンスのデフォルトのログイン方法です。ローカルのログインクライアントをダウンロードすることなく、CVMコンソールからワンクリックでWindowsインスタンスにログインできます。ログイン方式については、[標準方式を使用してWindowsインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/41018)をご参照ください。
</dx-alert>


## 概要
RDPはRemote Desktop Protocolの略称であり。お客様のローカルコンピュータがリモートコンピュータに接続できるようにするためにMicrosoftが開発したマルチチャネルプロトコルです。 Tencent Cloudは、Windows CVMへのログインにRDP方式を推奨しています。このドキュメントは、RDPファイルを使用してWindowsインスタンスにログインする方法について説明します。

## サポートされるシステム
Windows、Linuxと Mac OSは全てRDPを使用してCVMにログインすることができます。

##  前提条件

- Windowsインスタンスにリモートログインするには、インスタンスの管理者アカウントとパスワードを取得する必要があります。
  - インスタンス作成時に、システムによるパスワードのランダム発行を選択した場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
  - ログインパスワードを設定済みの場合は、そのパスワードを使用してログインしてください。パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスはパブリックIPがすでに購入され、インスタンスに関連付けられたセキュリティグループの中で、送信元がWebShellのプロキシIPとなるリモートログインポート（デフォルトは3389）を開放しています。
  - クイック設定でCVMインスタンスを購入した場合、ポートはデフォルトで開かれます。
  - カスタム設定経由でCVMインスタンスを購入した場合は、[セキュリティグループの応用例](https://intl.cloud.tencent.com/document/product/213/32369)を参照して、ポートを手動で開くことができます。
- インスタンスのパブリックネットワーク帯域幅が 5Mbit/s 以上であることを確認してください。そうでない場合、リモートデスクトップの応答が遅くなる可能性があります。ネットワーク帯域幅の調整が必要な場合は、[ネットワーク設定の調整](https://intl.cloud.tencent.com/document/product/213/15517)をご参照ください。


## 操作手順
<dx-tabs>
::: Windows システム[](id:windowsRDP)
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
 -**リストモード**：インスタンスの管理ページで、ログインするWindows CVM インスタンスを選択して、右側にある**ログイン**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)
 -**タブモード**：下図のように、ログインしたいWindows CVMタブを選択し、**ログイン**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)
3. 開いた「標準ログイン | Windowsインスタンス」ウィンドウの中から、**RDPファイルのダウンロード**を選択し、RDPファイルをローカルにダウンロードします。
<dx-alert infotype="explain" title="">
リモートデスクトップ接続で使われているポート番号を変更した場合は、RDPファイルを変更し、IPアドレスの後ろに：ポートを追加する必要があります。
</dx-alert>
<img src="https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png"/>
4. ローカルにダウンロードしたRDPファイルをダブルクリックして開き、パスワードを入力します。最後に「OK」をクリックすればリモート接続が許可されます。
  - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
  - パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。

:::
::: Linux システム[](id:LinuxRDP)


<dx-alert infotype="explain" title="">
リモートデスクトップクライアントとしてrdesktopを使用することをお勧めします。詳細については、[rdesktop公式説明](http://www.rdesktop.org/)をご参照ください。
</dx-alert>


1. 以下のコマンドを実行し、rdesktop がインストールされているかどうかを確認します。
```
rdesktop
```
   - rdesktopをインストールしている場合、[ステップ4](#step04)を実行してください。
   - command not foundというプロンプトが表示された場合、rdesktopをインストールされていないことを示し、[ステップ2](#step02)を実行してください。
2. [](id:step02)ターミナルウィンドウで以下のコマンドを実行してrdesktopインストールパッケージをダウンロードします。この手順はrdesktop 1.8.3バージョンを例とします。
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
最新のインストールパッケージが必要な場合は、[GitHub rdesktopページ](https://github.com/rdesktop/rdesktop/releases)にアクセスして最新のインストールパッケージをさがし、コマンドラインを最新のインストールパスに置き換えます。
3. rdesktopをインストールするディレクトリで、以下のコマンドを実行し、rdesktopを解凍してインストールします。
```
tar xvzf rdesktop-<x.x.x>.tar.gz ##x.x.xをダウンロードしたバージョン番号に置き換えます 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. [](id:step04)以下のコマンドを実行してWindowsインスタンスにリモートで接続できます。
<dx-alert infotype="explain" title="">
例の中のパラメータをご自分のパラメータに変更してください。
</dx-alert>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
   - `Administrator` は前提条件で入手した管理者アカウントです。
   - `<your-password>` は設定されたログインパスワードです。
      システムのデフォルトパスワードを使用してインスタンスにログインする場合、[サイト内メール](https://console.cloud.tencent.com/message)からパスワードを取得してください。パスワードを忘れた場合、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
   - `<hostname or IP address>`は、お客様のWindowsインスタンスのパブリックIPまたはカスタムドメイン名となります。インスタンスのパブリックIPの取得方法は、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。

:::
::: MacOS システム[](id:MacRDP)


<dx-alert infotype="explain" title="">
- 以下の操作は Microsoft Remote Desktop for Macの例です。マイクロソフトは2017年にRemote Desktopクライアントのダウンロードリンクの提供を正式に停止し、現在は、子会社のHockeyAppがベータ版を配布しています。 [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac)でベータ版をダウンロードすることができます。
- 以下の操作は、Windows Server 2012 R2 OSのCVMインスタンスに接続する方法を例に説明します。
</dx-alert>


1. Microsoft Remote Desktop for Mac をローカルコンピューターにダウンロードしてインストールします。
2. MRDを起動して、下図に示すように**Add Desktop**をクリックします。
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. 表示された「Add Desktop」ウィンドウで、以下の手順に従って、接続を作成します。下図に示すように：
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
     1.「PC name」にCVMインスタンスのパブリックIPアドレスを入力します。パブリックIPアドレスを取得する方法の詳細については、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
     2. **Add**をクリックします。
     3. 他のオプションはデフォルト設定のままで、接続が作成されます。
    ウィンドウで作成された接続を確認できます。下図に示すように：
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. 新規作成した接続をダブルクリックして開き、ポップアップウィンドウでプロンプトに従って、CVMのアカウントとパスワードを入力し、**Continue**をクリックします。
5. システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
6. パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
7. 下図のように、ポップアップしたウィンドウで**Continue**をクリックして、接続を確認します。
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
接続に成功すると、次のページが表示されます。
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
:::
</dx-tabs>

## RDP帯域幅制限の説明[](id:illustrate)
利用可能なネットワーク帯域幅は、RDP経由のログインやCVMの使用体験に直接影響し、アプリケーションプログラムやディスプレイ解像度ごとに、各々のネットワーク構成が必要です。マイクロソフトは、それぞれのユースケースでRDPを使用する時のインスタンスの最小帯域幅要件を提供しています。下表を参照して、インスタンスのネットワーク設定が業務のニーズを確実に満たすようにしてください。そうでない場合、遅延などの問題が発生する可能性があります。


<dx-alert infotype="explain" title="">
インスタンスの帯域幅を調整したい場合は、[ネットワーク設定の調整](https://intl.cloud.tencent.com/document/product/213/15517)をご参照ください。
</dx-alert>

以下のデータは、解像度が1920x1080で、デフォルトのグラフィックモードとH.264/AVC 444グラフィックモードを同時に採用する単一のモニター構成に適用されます。

<table>
<tr>
<th width="15%">シナリオ</th>
<th width="19%">デフォルトモード</th>
<th width="19%">H.264/AVC 444 モード	</th>
<th width="47%">シナリオ説明</th>
</tr>
<tr>
<td>休眠</td>
<td>0.3Kbps	</td>
<td>0.3Kbps</td>
<td>ユーザーがすでに作動を一次停止し、アクティブな画面更新が発生していない状態。</td>
</tr>
<tr>
<td>Microsoft Word</td>
<td>100 - 150 Kbps</td>
<td>200 - 300 Kbps</td>
<td>ユーザーがMicrosoft Word、印刷、図形のペーストをアクティブに使用中で、ドキュメント間の切り替えも行っている状態。</td>
</tr>
<tr>
<td>Microsoft Excel</td>
<td>150 - 200Kbps</td>
<td>400 - 500Kbps</td>
<td>ユーザーがMicrosoft Excelをアクティブに使用中で、同時に公式や図表が含まれた複数のセルを更新している状態。</td>
</tr>
<tr>
<td>Microsoft PowerPoint</td>
<td>4 - 4.5Mbps</td>
<td>1.6 - 1.8Mbps</td>
<td>ユーザーがMicrosoft PowerPoint、印刷、ペーストをアクティブに使用中。またコンテンツが豊富な図形を変更中で、スライドショー効果も使用している状態。</td>
</tr>
<tr>
<td>Web閲覧</td>
<td>6 - 6.5Mbps</td>
<td>0.9 - 1Mbps</td>
<td>ユーザーがグラフィックコンテンツが豊富なウェブサイトをアクティブに閲覧中（横方向および縦方向にページをスクロール）で、その中に複数の静止画や動画が含まれている状態。</td>
</tr>
<tr>
<td>画像ライブラリ</td>
<td>3.3 - 3.6Mbps	</td>
<td>0.7 - 0.8Mbps</td>
<td>ユーザーが画像ライブラリアプリケーションプログラムをアクティブに使用中。画像の閲覧、スケーリング、サイズの調整、回転を行っている状態。</td>
</tr>
<tr>
<td>ビデオ再生</td>
<td>8.5 - 9.5Mbps</td>
<td>2.5 - 2.8Mbps</td>
<td>ユーザーがスクリーンの半分を占有する30FPSのビデオを視聴中。</td>
</tr>
<tr>
<td>フルスクリーンビデオ再生</td>
<td>7.5 - 8.5Mbps</td>
<td>2.5 - 3.1Mbps</td>
<td>ユーザーがフルスクリーンに最大化した30FPSのビデオを視聴中。</td>
</tr>
</table>
