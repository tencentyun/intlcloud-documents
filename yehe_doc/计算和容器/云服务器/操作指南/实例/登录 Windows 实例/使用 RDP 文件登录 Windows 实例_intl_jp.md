>! 現在、Windowsインスタンスのログイン方式のデフォルトは**標準ログイン方式（WebRDP）**となり、コンソール経由でWindowsインスタンスにワンクリックログインできます。ローカルにダウンロードしてクライアントにログインする必要はありません。
>

## 概要
RDPはRemote Desktop Protocolの略称であり。お客様のローカルコンピュータがリモートコンピュータに接続できるようにするためにMicrosoftが開発したマルチチャネルプロトコルです。 Tencent Cloudは、Windows CVMへのログインにRDP方式を推奨しています。このドキュメントは、RDPファイルを使用してWindowsインスタンスにログインする方法について説明します。

## サポートされるシステム
Windows、Linuxと Mac OSは全てRDPを使用してCVMにログインすることができます。

## 前提条件

- Windowsインスタンスにリモートログインするには、インスタンスの管理者アカウント番号と対応するパスワードを獲得する必要があります。
 - インスタンス作成時に、システムによるパスワードのランダム発行を選択した場合は、[サイト内メッセージ](https://console.cloud.tencent.com/message)にアクセスして取得してください。
 - ログインパスワードを設定済みの場合は、そのパスワードを使用してログインしてください。パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- お客様のCVMインスタンスはパブリックIPがすでに購入され、インスタンスに関連付けしたセキュリティグループの中で、送信元がWebRDPのプロキシIPとなるリモートログインポート（デフォルトは3389）を開放しています。
 - クイック設定経由でCVMを購入した場合、デフォルトの状態ではアクティブになっています。
 - カスタム設定経由でCVMを購入した場合は、[Windows CVMへのRDPリモート接続の許可](https://intl.cloud.tencent.com/document/product/213/32369)を参照して、手動でアクセスを許可してください。
- お客様のインスタンスのパブリックネットワーク帯域幅≥5Mbit/sとなるように確約してください。そうでない場合、リモートデスクトップにラグが生じます。ネットワーク帯域幅の調整が必要な場合は、[ネットワーク設定の調整](https://intl.cloud.tencent.com/document/product/213/15517)をご参照ください。


## 操作手順
<dx-tabs>
::: Windows\sシステムでは\sRDP\sを使用してログインします[](id:windowsRDP)
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理ページで、ログインしたいWindows CVMを選択して、**ログイン**をクリックします。下図のとおりです。
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. 開いた「標準ログイン | Windowsインスタンス」ウィンドウの中から、**RDPファイルのダウンロード**を選択し、RDPファイルをローカルにダウンロードします。
>?リモートログインポートを変更した場合は、RDPファイルを変更し、IPアドレスの後ろに`：port`を追加する必要があります。
>
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. ローカルにダウンロードしたRDPファイルをダブルクリックして開き、パスワードを入力して、**OK**をクリックすれば、Windows CVMにリモート接続されます。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
:::
::: Linux\sシステムでは\sRDP\sを使用してログインします[](id:LinuxRDP)
>?対応するリモートデスクトップ接続プログラムをインストールする必要がある場合は、rdesktopを使用して接続することをお勧めします。詳細は [rdesktop 公式説明](http://www.rdesktop.org/)をご参照ください。
>
1. 以下のコマンドを実行し、システムにrdesktopをインストールされているかどうかを確認します。
```
rdesktop
```
 - rdesktopをインストールしている場合、[ステップ4](#step04)を実行してください。
 - command not foundというプロンプトが表示された場合、rdesktopをインストールされていないことを示し、[ステップ2](#step02)を実行してください。
2. [](id:step02)端末で以下のコマンドを実行し、rdesktopのインストールパッケージをダウンロードします。この手順ではrdesktop 1.8.3バージョンを例示します。
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
``` 最新のインストールパッケージが必要な場合は、[GitHub rdesktopページ](https://github.com/rdesktop/rdesktop/releases)にアクセスして最新のインストールパッケージをさがし、コマンドラインを最新のインストールパスに置き換えます。
3. rdesktopをインストールするディレクトリで、以下のコマンドを実行し、rdesktopを解凍してインストールします。
```
tar xvzf rdesktop-<x.x.x>.tar.gz ##x.x.xをダウンロードしたバージョン番号に置き換えます 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. [](id:step04)以下のコマンドを実行し、Windowsのインスタンスにリモートで接続します。</span>
>? 例中のパラメータを自身のパラメータに変更してください。
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` は前提条件で入手した管理者アカウントです。
 - `<your-password>` は設定されたログインパスワードです。
   システムのデフォルトパスワードを使用してインスタンスにログインする場合、[サイト内メール](https://console.cloud.tencent.com/message)から取得してください。パスワードを忘れた場合、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
 - `<hostname or IP address>`は、お客様のWindowsインスタンスのパブリックIPまたはカスタムドメイン名となります。インスタンスのパブリックIPの取得方法は、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
:::
::: MacOS\sシステムでは\sRDP\sを使用してログインします[](id:MacRDP)
>?
>- 以下の操作は Microsoft Remote Desktop for Mac の例です。マイクロソフトは2017年に Remote Desktop クライアントのダウンロードリンクの提供を正式に停止し、現在は、子会社の HockeyApp が Beta 版を配布しています。 [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac)で Beta 版をダウンロードすることができます。
>- 以下の操作は Windows Server 2012 R2  OSに接続されているCloud Virtual Machine を例として説明します。
>
1. Microsoft Remote Desktop for Macをダウンロードして、ローカルにインストールします。
2. MRDを起動して、【Add Desktop】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. 表示された「Add Desktop」ウィンドウで、以下の手順に従って、接続を作成します。下図に示すように：
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1.「PC name」にCVMのパブリックネットワークIPを入力します。取得方法については、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
    2. 【Add】をクリックして、接続の作成を確認します。
    3. 他のオプションはデフォルト設定のままで、接続が作成されます。
    ウィンドウで作成された接続を確認できます。下図に示すように：
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4.新しく作成した接続をダブルクリックして開き、ポップアップウィンドウでプロンプトに従って、CVMのアカウントとパスワードを入力し、【Continue】をクリックしてください。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
5. ポップアップウインドウで【Continue】をクリックし、接続を確認します。下図に示すように：
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
接続に完了すると、 以下に示すように、Windows CVM画面が表示されます
![](https://main.qcloudimg.com/raw/5a524210acd13624af7263b6de3aea54.png)
:::
</dx-tabs>

## RDP帯域幅制限の説明[](id:illustrate)
ネットワークの使用可能な帯域幅は、RDP経由のログインやCVMの使用体験に直接影響し、アプリケーションプログラムやディスプレイ解像度ごとに、各々のネットワーク設定が必要です。マイクロソフトは、それぞれのユースケースでRDPを使用する時のインスタンスの最小帯域幅要件を提供しています。下表を参照して、インスタンスのネットワーク設定が業務のニーズを確実に満たすようにしてください。そうでない場合、ラグなどの問題が生じます。
>?インスタンスの帯域幅を調整したい場合は、[ネットワーク設定の調整](https://intl.cloud.tencent.com/document/product/213/15517)をご参照ください。
>
以下のデータは、1920 × 1080の解像度を採用し、デフォルトのグラフィックモードおよびH.264/AVC 444グラフィックモードを同時に採用するシングルモニターの設定に適用するものです。

<table>
<tr>
<th width="15%">方式</th>
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
