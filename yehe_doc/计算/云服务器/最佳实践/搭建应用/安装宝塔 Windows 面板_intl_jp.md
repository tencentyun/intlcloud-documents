## 概要
BTパネルは、LinuxおよびWindowsシステムをサポートする使いやすく、一生無料で使える強力でインタラクティブなサーバー管理ソフトウェアです。BTパネルでは、LAMP、LNMP、Webサイト、データベース、FTP、SSLをワンクリックで設定でき、Web側からサーバーを簡単に管理できます。

このドキュメントでは、WindowsオペレーティングシステムのCVMで、Tencent Cloud Market Mirrorを介してBTパネルを速やかにインストールする方法について説明します。


## 操作手順

### CVMの作成時のBTパネルインストール


<dx-alert infotype="notice" title="">
購入したCVMにBTパネルをインストールする場合は、[システムの再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をして、イメージ市場で対応するイメージを選択し、環境の導入を完了できます。海外の一部の地域のCVMでは、イメージ市場におけるシステムの再インストールがサポートされていません。別の地域のCVMを使用することをお勧めします。インストールの詳細については[BTパネルの公式サイト](https://www.bt.cn/)をご参照ください。
</dx-alert>

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、インスタンス管理ページの**新規作成**をクリックします。
2. ページの指示に従ってモデルを選択し、「イメージ」で**イメージ市場**>**イメージ市場から選択する**をクリックします。下図の通りです：
<dx-alert infotype="notice" title="">
- 海外の一部の地域のCVMでは、イメージ市場におけるCVMの新規作成がサポートされていません。選択した地域に**イメージ市場**がない場合、他のイメージ市場をサポートする地域を選択してください。
- 2 GB以上のメモリと40 GB以上のシステムディスクを備えたインスタンス構成をお勧めします。
3. 「イメージ市場」ウィンドウのの検索ボックスで、**運用保守ツール**を選択し、「BT」と入力して<img src="https://main.qcloudimg.com/raw/70c20e0ff30f88eef20d6b540d6ef804.png" style="margin:-3px 0px">をクリックします。
4. 希望のイメージを選択します。このドキュメントでは、**BT Windowsパネル公式版（WAMP/WNMP/Tomcat/Node.js）**を例とします。**無料利用**をクリックします。
5. インスタンスに関連付けられるセキュリティグループにはポート8888をオープンするためのインバウンドルールを追加してください。詳細については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。
ストレージメディア、帯域幅などの他の設定は実際のニーズに合わせて選択して、最後に購入を選択しBTパネルの作成を完了します。


### パネルログイン情報の取得
1. CVMにログインします。詳細については、[標準方式を使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/41018)をご参照ください。
2. オペレーティングシステムの画面で、左下の<img src="https://qcloudimg.tencent-cloud.cn/raw/c6e9910fc4f983d45729b4f6924e8273.png" style="margin:-3px 0px">を右クリックし、ポップアップメニューから**実行**をクリックします。
3. cmdウィンドウで次のコマンドを実行すると、ログイン情報を取得します。
```
bt default
```
結果が返された後。 BT パネルのアドレスとログイン情報を記録します。


### BTパネルのログイン
1. ローカルコンピュータでブラウザを開き、取得したBTパネルのアドレスにアクセスします。
```shell
http://云服务器公网 IP:8888/xxxx
```
2. レコードの「username」と「password」を入力し、**ログイン**をクリックします。
3. [利用規約に同意します]のチェックを入れ、**パネルへ進む**をクリックします。
4. 実際のビジネスニーズに応じて、インストールするコンポーネントと導入Webサイトをパネルから選択します。
