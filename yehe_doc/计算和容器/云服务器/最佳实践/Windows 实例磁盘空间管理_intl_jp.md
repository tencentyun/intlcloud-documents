## 操作シナリオ
このドキュメントでは、Windows Server 2012 R2のTencent Cloud CVMを例に、Windowsインスタンスのディスク容量が不足している場合に容量を解放する方法と、ディスクの日常的な保守を行う方法について説明します。

## 操作手順

### ディスクの空き容量を増やす
ディスク容量不足の問題は、[大容量ファイルの削除](#deleteLargerFiles)または[不要ファイルの削除](#deleteObsoleteFiles)によって解決できます。ファイルをクリーンアップしても実際のニーズを満たすことができない場合は、ディスクの容量拡張を選択してディスク容量を拡張します。詳細については、[容量拡張ケースの概要](https://intl.cloud.tencent.com/document/product/362/31600)をご参照ください。
<span id="deleteLargerFiles"></span>
#### 大容量ファイルの削除
1. [RDPファイルを使用してWindowsインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5435)します。また、実際の操作方法により、[リモートデスクトップ接続を使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32498)することもできます。
2. 下部ツールバーの<img src="https://main.qcloudimg.com/raw/dcdf8e1ebc35bd6db1edaceff6784db2.png" style="margin:-5px 0px">を選択して、「このコンピュータ」ウィンドウを開きます。
3. 「このコンピュータ」で、クリーンアップするディスクを選択し、**Crtl+F**を押して検索ツールを開きます。
4. 【検索】>【サイズ】を選択し、システムで設定されたサイズに基づいてメニューから必要に応じてファイルをフィルタリングします。以下の通りです。
![](https://main.qcloudimg.com/raw/48a1033c6b978dfe6de1b2dc6d8bcdd3.png)
> 「このコンピュータ」の右上隅にある検索ボックスで、ファイルのサイズをカスタマイズして検索することもできます。例：
>- 「サイズ：>500M」と入力すると、ディスクの500Mを超えたファイルが検索されます。
>- 「サイズ：>100M<500M」と入力すると、ディスクの100Mを超えて且つ500M未満のファイルが検索されます。
>

<span id="deleteObsoleteFiles"></span>
#### 不要ファイルの削除
1. <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-5px 0px">を選択して、「サーバーマネージャ」を開きます。
2.【役割と機能の追加】をクリックして、「役割と機能の追加ウィザード」画面が表示されます。
3.「役割と機能の追加ウィザード」ウィンドウで、【次へ】をクリックします。
4.「インストールタイプを選択」画面で、【役割ベースまたは機能ベースのインストール】を選択して、3回続けて【次へ】をクリックしてください。以下の通りです。
![](https://main.qcloudimg.com/raw/d25dc913281f8cb5c688dd9cc62b8d73.png)
5. 「機能の選択」画面で「インクと手書きサービス」と「デスクトップエクスペリエンス」をチェックし、表示されたプロンプトボックスで【OK】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/f1bf18c4598597ef86428bd4bbd77c15.png)
6. 【次へ】を選択し、【インストール】をクリックします。インストールが完了したら、画面の通知メッセージを参照してサーバーを再起動します。
7. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px">を選択し、右上隅の<img src="https://main.qcloudimg.com/raw/4851c97390178d2d8ae2e6385756eb3b.png" style="margin:-5px 0px">をクリックします。検索ボックスに【ディスク管理】を入力して検索します。
8. 表示された「ディスククリーンアップ」ウィンドウで、対応するディスクを選択してクリーンアップを開始します。以下の通りです。
![](https://main.qcloudimg.com/raw/69e2c653c6304a450463cdf07bf5a3ef.png)

### ディスクの日常的な保守
#### 定期的にプログラムを削除する
「コントロールパネル」の「プログラムのアンインストールまたは変更」を選択して、使用しなくなったプログラムを定期的にクリーンアップできます。以下の通りです。
![](https://main.qcloudimg.com/raw/b9294f1e79429dbdb8a7800cfdb6d6b4.png)


#### コンソールでディスク使用状況を表示する
Cloud Monitor機能は、CVMインスタンスが作成されると自動的に有効になります。次の手順を実行して、コンソールからCVMのディスク使用状況を表示することができます。
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/instance/index)にログインし、「インスタンス」ページに進みます。
2. ターゲットインスタンスのID /名前を選択して、インスタンスの詳細ページに入ります。
3. インスタンスの詳細ページで、【監視】タブを選択すると、そのインスタンスのディスク使用状況が表示されます。以下の通りです。
![](https://main.qcloudimg.com/raw/19f00a883ed73ba1c636830f06d3f00d.png)
