## シナリオ
Microsoft Remote Desktop (以下MRDと呼ぶ）は、MicrosoftがMac向けに提供しているリモートデスクトップ接続アプリです。このドキュメントでは、MacOSでMRDを使用して、Windows Server 2012 R2システムがインストールされているTencent Cloud CVMにファイルをアップロードする方法について説明します。 

## 前提条件
- MRDをダウンロードしてローカルコンピューターにインストールしました。このドキュメントでは、Microsoft Remote Desktop for Macを例として説明します。Microsoft社は、2017年にRemote Desktopクライアントへのダウンロードリンクの提供を停止し、ベータ版のリリースは、その子会社であるHockeyAppによって提供されます。ベータ版をダウンロードするには、[Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac)にアクセスしてください。
- MRDはMacOS10.10以降のバージョンをサポートします。サポートされているOSを使用してください。
- Windows CVMを購入しました。

## 操作手順
### パブリックIPを取得する
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、インスタンスリストページに移動して、ファイルをアップロードするCVMのパブリックIPを記録します。次の図に示すように：
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)

### ファイルをアップロードする
1. MRDを起動し、【Add Desktop】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
2. 表示されるダイアログボックスで、以下の手順に従って、アップロードするフォルダを選択し、Windows CVMとの接続を確立します。次の図に示すように：
![](https://main.qcloudimg.com/raw/fc241ce8e4744bde57476ea823fcef72.png)
  1. 「PC name」に CVMのパブリックIPアドレスを入力します。
  2.【Folders】をクリックして、フォルダリストに切り替えます。
  3. 左下隅の<img src="https://main.qcloudimg.com/raw/89e7a3ff040849307cd1eb8bd878a2db.png" style="margin:-3px 0px">をクリックして、表示されるダイアログボックスでアップロードするフォルダを選択します。
  4. 選択が完了したら、アップロードするフォルダのリストを確認して、【Add】をクリックします。
  5. 他のオプションはデフォルト設定のままにして、接続を作成します。
ウィンドウで作成された接続を確認できます。次の図に示すように：
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4.新しく作成した接続をダブルクリックして開き、表示されるダイアログボックスでプロンプトに従って、CVMのアカウントとパスワードを入力し、【Continue】をクリックしてください。
>?
>- Windows CVMのデフォルトアカウントは`Administrator`です。
>- システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
>- パスワードを忘れた場合、[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)を行ってください。
>
5. 表示されるダイアログボックスで【Continue】をクリックして、接続を確立します。次の図に示すように：
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
接続が成功すると、次のページが表示されます。
![](https://main.qcloudimg.com/raw/5a524210acd13624af7263b6de3aea54.png)
6. 左下隅の<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px">>をクリックし、【My Computer】を選択して、共有フォルダが表示されます。
8. 共有フォルダをダブルクリックして開き、アップロードする必要があるローカルファイルをWindows CVMの別のドライブにコピーします。
例えば、フォルダ内のAファイルをWindows CVMのCドライブにコピーします。

### ファイルをダウンロードする
Windows CVMからローカルコンピューターにファイルをダウンロードする必要がある場合は、必要なファイルをWindows CVMから共有フォルダにコピーして、ファイルのダウンロード操作を完了することができ​ます。 


