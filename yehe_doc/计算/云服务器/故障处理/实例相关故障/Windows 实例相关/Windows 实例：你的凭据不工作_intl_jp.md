## 問題の説明

Windows OSのローカルコンピュータがRDPプロトコル（MSTSCなど）により、リモートデスクトップ接続を使用してWindows CVMにログインすると、次のエラーが表示されます。
お使いの資格情報は機能しませんでした。XXX.XXX.XXX.XXX への接続に使用された資格情報は機能しませんでした。新しい資格情報を入力してください。
![](https://main.qcloudimg.com/raw/47a299873e3df8f1f160c1594fc56644.png)

## 処理手順
>? Windows Server 2012 OSを例にしていますが、OSのバージョンが異なるため、操作手順の詳細はわずかに異なります。
> 以下の手順に従ってトラブルシューティングを行い、各手順が実行した後、Windows CVMに再接続して問題が解決されたか確認します。問題が解決されていない場合は、次の手順に進みます。

### ステップ1：ネットワークアクセスポリシーを変更する
- [VNCを使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32496)します。
2. OS画面で、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> をクリックして、「Windows PowerShell」ウインドウを開きます。
3. 「Windows PowerShell」ウィンドウで、**gpedit.msc**を入力し、**Enter**キーを押すと、「ローカルグループポリシーエディター」を起動します。
4. 左側のナビゲーションで、【コンピュータの構成】>【ポリシー】>【Windows の設定】>【セキュリティの設定】>【ローカルポリシー】>【セキュリティ オプション】ディレクトリを順次展開します。
5. 【セキュリティオプション】の【ネットワークアクセス：ローカルアカウントの共有とセキュリティモデル】を探して開きます。以下の通りです。
![](https://main.qcloudimg.com/raw/4ffb48c55d2f4aeedee127d97a4378ee.png)
6. 【クラシック – ローカルユーザーがローカルユーザーとして認証する】を選択し、【OK】をクリックします。以下の通りです。
![](https://main.qcloudimg.com/raw/0f460bef7a7e35e1295149bb1f5f0d03.png)
7. Windows CVMに再接続し、接続に成功したか確認します。
 - はい、タスクは終了しました。
 - いいえ、ステップ2（資格情報の委任を変更する）を実行してください。

### ステップ2：資格情報の委任を変更する
1. 「ローカルグループポリシーエディター」の左側のナビゲーションバーで、【コンピューターの構成】>【ポリシー】>【管理用テンプレート】>【システム】>【資格情報の委任 】ディレクトリを順次展開します。
2. 【資格情報の委任 】の【NTLMのみのサーバー認証で保存された資格情報の委任を許可する】を見つけて有効にします。以下の通りです。
![](https://main.qcloudimg.com/raw/7643737fdfa2be299c21f6bc82b0165b.png)
3.  設定を有効にし、「表示」をクリックします。Windows 資格情報を使用して接続したいサーバーのIPアドレスやホスト名を指定します。ホスト名を指定する前に、「TERMSRV/」をつける必要があります。すべてのサーバーへの接続を許可したい場合は、「＊」を使用します。
![](https://main.qcloudimg.com/raw/6a9af6aa4c3c3b3c4d1b9eba53d202b1.png)
4.【OK】をクリックします。
5. OS画面で、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> をクリックして、「Windows PowerShell」ウインドウを開きます。
6. 「Windows PowerShell」ウィンドウで、**gpupdate/force**を入力し、**Enter**キーを押してグループポリシーを更新します。以下の通りです。
![](https://main.qcloudimg.com/raw/98d0b757e65e3617145c05513ba652dc.png)
7. Windows CVMに再接続し、接続に成功したか確認します。
 - はい、タスクは終了しました。
 - いいえ、ステップ3（ローカル資格情報の設定）を実行してください。

### ステップ3：ローカル資格情報の設定
2. OS画面で、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > 【コントロールパネル】>【ユーザーアカウント】をクリックし、【資格情報マネージャー】の【Windows 資格情報の管理】を選択すると、Windows資格情報画面に進みます。以下の通りです。
![](https://main.qcloudimg.com/raw/2726e3d109fdaadd1d90a1f3e692601a.png)
2. Windowsの資格情報の下に、現在ログインしているCVMの資格情報があるかどうかを確認します。
 - ない場合は、次のステップに進み、Windows資格情報を追加します。
 - ある場合は、ステップ4（CVMのパスワード保護共有の無効設定）を実行してください。
3. 【Windows資格情報の追加】をクリックして、Windows資格情報追加画面に進みます。以下の通りです。
![](https://main.qcloudimg.com/raw/87077862379ea7d9e86d5fdc7e0af1da.png)
4. 現在ログインしているCVMのIPアドレス、ユーザー名とパスワードを入力し、【OK】をクリックします。
>?
> - CVMのIPアドレスは、CVMインスタンスのパブリックIPアドレスを指します。詳細については、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
> - Windowsインスタンスのデフォルトのユーザー名は`Administrator`であり、パスワードはインスタンスの作成時に設定されます。ログインパスワードを忘れた場合は、 [インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566) をご参照ください。
>
5. Windows CVMに再接続し、接続に成功したか確認します。
 - はい、タスクは終了しました。
 - いいえ、ステップ4（CVMのパスワード保護共有の無効設定）を実行してください。

### ステップ4：CVMのパスワード保護共有の無効設定
1. OS画面で、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > 【コントロールパネル】>【ネットワークとインターネット】>【ネットワークと共有センター】>【共有の詳細設定の変更】をクリックして、共有設定画面に進みます。以下の通りです。
![](https://main.qcloudimg.com/raw/d1cc8fd023642654091d1b152bb67ef1.png)
2. 【すべてのネットワーク】タブを展開し、【パスワード保護共有】の下で【パスワード保護共有を無効にする】を選択し、【変更の保存】をクリックします。
3. Windows CVMに再接続し、接続に成功したか確認します。
 - はい、タスクは終了しました。
 - いいえ、[チケットを送信](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) して問題を報告してください。


