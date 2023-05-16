## 問題の説明

リモートデスクトップ接続クライアントを使用してWindowsインスタンスにログインする場合は、次のエラーが発生します。
- 「認証エラーが発生しました。この関数に提供されたトークンは無効です」。
- 「認証エラーが発生しました。要求された関数はサポートされていません」。

## 問題の分析

Microsoftは2018年3月にセキュリティ更新プログラムを公開しました。このセキュリティ更新プログラムは、認証プロセス中にCredSSPプロトコルが要求を検証する方法を修正することにより、CredSSPのリモートでコードが実行される脆弱性を解決します。 クライアントとサーバーの両方にセキュリティ更新プログラムをインストールする必要があります。そうしないと、そうしなければ「問題の説明」のような状況が発生する可能性があります。
インスタンスにリモートでログインできない場合、主に次の3つの原因が考えられます。 

- 原因 1:セキュリティ更新プログラムはサーバーにインストールされていますが、クライアントにはインストールされておらず、「強制的に更新されたクライアント」ポリシーが構成されています。
- 原因 2：セキュリティ更新プログラムはクライアントにインストールされていますが、サーバーにはインストールされておらず、「強制的に更新されたクライアント」ポリシーが構成されています。
- 原因 3：セキュリティ更新プログラムはクライアントにインストールされていますが、サーバーにはインストールされておらず、「緩和」ポリシーが構成されています。

## 対処方法



<dx-alert infotype="explain" title="">
ローカルクライアントのみをアップグレードする場合は、[解決策 1：セキュリティ更新プログラムのインストール（推奨）](#step4)を直接実行してください。
</dx-alert>


### VNC経由でCVMにログインする

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 下図のように、インスタンスの管理画面で目的のCVMインスタンスを見つけ、**ログイン**をクリックします。
![CVMリストページ](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. ポップアップした「標準ログイン | Windowsインスタンス」ウィンドウで、**VNCログイン**を選択します。
4. 下図のように、ポップアップしたログインウィンドウの中で、左上の「リモートコマンドの送信」を選択し、 **Ctrl-Alt-Delete**をクリックしてシステムログイン画面に進みます。
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)
5. ログインパスワードを入力し、**Enter**を押せば、Windows CVMにログインできます。


### 解決策 1：セキュリティ更新プログラムのインストール（推奨）[](id:step4)

パッチが適用されていないクライアントまたはサーバーにセキュリティ更新プログラムをインストールします。各システムに対応する更新の状況については、[CVE-2018-0886 | CredSSPのリモートでコードが実行される脆弱性](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)をご参照ください。このソリューションではWindows Server 2016を例とします。
その他のOSの場合は、以下の操作を参照して**Windows Update**に進んでください。

- Windows Server 2012：<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width: 22px;"></img> > **コントロールパネル** > **システムとセキュリティ** > **Windows Update**
- Windows Server 2008：**スタート** > **コントロールパネル** > **システムとセキュリティ** > **Windows Update**
- Windows10：<img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;"></img> > **設定** > **更新とセキュリティ**
- Windows 7：<img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin:-3px 0px;width: 28px;"></img> > **コントロールパネル** > **システムとセキュリティ** > **Windows Update**


1. OSの画面で、<img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;"></img>をクリックし、表示されたメニューから**設定**をクリックします。
2. 「設定」が表示されます。**更新とセキュリティ**をクリックします。
3. 「更新とセキュリティ」画面が表示されます。画面の左側から**Windows Update**をクリックし、右側に表示された**更新プログラムのチェック**をクリックします。
4. 画面の表示に従って、**インストールの開始**をクリックします。
5. インストールの完了後にインスタンスを再起動すると、更新が完了します。

### 解決策 2. ポリシーの設定変更

セキュリティ更新プログラムがインストールされているCVMインスタンスで、**暗号化オラクルの修復**ポリシーを「脆弱」に設定します。このソリューションでは、Windows Server 2016を例とします。操作手順は次のとおりです。

<dx-alert infotype="notice" title="">
Windows 10 HomeのOSで、グループポリシーエディタがない場合は、レジストリを変更することで実装できます。操作手順については、[解決策 3：レジストリの変更](#Plan3)をご参照ください。
</dx-alert>


1. OS画面で、<img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin:-3px 0px;"></img>をクリックし、**gpedit.msc**と入力し、**Enter**を押して、「ローカルグループポリシーエディタ」を開きます。
<dx-alert infotype="explain" title="">
ショートカットキー「**Win+R**」を使用して実行画面を開くこともできます。
</dx-alert>
2. 左側ナビゲーションツリーで、**コンピューターの構成>管理用テンプレート>システム>資格情報の委任**を選択し、暗号化オラクルの修復をダブルクリックします。
3. 「暗号化オラクルの修復」画面が表示されます。**有効**を選択し、**保護レベル**を**脆弱**に設定します。
4. **OK**をクリックして設定を完了します。


### 解決策 3：レジストリの変更[](id:Plan3)

1. OS画面で、<img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin:-3px 0px;"></img>をクリックし、**regedit**と入力し、**Enter**を押して、レジストリエディタを開きます。
<dx-alert infotype="explain" title="">
ショートカットキー「**Win+R**」を使用して実行画面を開くこともできます。
</dx-alert>
2. 左側ナビゲーションツリーで、順に**コンピュータ** > **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Microsoft** > **Windows** > **CurrentVersion** > **Policies** > **System** > **CredSSP** > **Parameters** ディレクトリを開きます。
<dx-alert infotype="explain" title="">
ディレクトリパスが存在しない場合は、手動で作成してください。
</dx-alert>
4. **Parameters**を右クリックし、**新規作成** > **DWORD(32ビット)値**を選択し、ファイル名を「AllowEncryptionOracle」とします。
4. 新規作成した「AllowEncryptionOracle」ファイルをダブルクリックし、「数値データ」を「2」に設定し、**OK**をクリックします。
6. インスタンスを再起動します。

## 関連ドキュメント

- [CVE-2018-0886 | CredSSPのリモートでコードが実行される脆弱性](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [CVE-2018-0886のCredSSPの更新プログラム](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)

