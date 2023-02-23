## ユースケース

セキュリティ識別子(SID)はWindows OSにおいてコンピューターとユーザーを識別します。同一イメージに基づいて作り出されたCVMインスタンスのSIDが同じであるため、ドメインに参加できない問題を引き起こす可能性があります。Windowsドメイン環境を構築したい場合、ドメインに参加できるためにSIDを修正する必要があります。
このドキュメントは、 Windows Server 2012 OSのCVMを例として、システムに付属しているsysprep及びsidchg ツールを使用して、SIDを修正する方法について説明します。

## 注意事項

- 本説明では Windows Server 2008 R2 、Windows Server 2012 及び Windows Server 2016にのみ適用しています。
- 一括でSIDを修正する必要がある場合、カスタマイズイメージ（「sysprepを実行してイメージを作成する」を選択する）を作成することにより修正できます。
-  SIDの修正によりデータの損失やシステムの破損などの問題が発生する可能性があるため、事前にシステムディスクのスナップショットまたはイメージを作成することを推奨します。

## 操作方法

### sysprepを使用してSIDを変更する



<dx-alert infotype="notice" title="">
- sysprepを使用してSIDを変更した後、IP構成情報などを含む多くのシステムパラメーターを手動でリセットする必要があります。
- sysprepを使用してSIDを変更した後、C:\Users\Administratorがリセットされ、システムディスクデータの一部が消去されるため、データをバックアップしてください。
</dx-alert>


1. [VNC を使用してCVMにログインする](https://intl.cloud.tencent.com/document/product/213/32496)。
2. OSインターフェースで、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"> > **実行**を右クリックし、**cmd**を入力し、**Enter**を押して、管理者コマンドラインツールを開きます。
3. [](id:step_03)は、管理者コマンドラインで、以下のコマンドを実行して、現在のネットワーク設定を保存します。</span>
```shellsession
ipconfig /all
```
4. 管理者コマンドラインで、以下のコマンドを実行して、 sysprepツールを開きます。
```shellsession
C:\Windows\System32\Sysprep\sysprep.exe
```
5. 開いた「システム準備ツール 3.14」ウインドウで、以下の設定を行います。
- **システムクリーンアップ操作**システムのアウトオブボックスエクスペリエンス（OOBE）に入る**に設定し、「全般」にチェックを入れます。
   - **シャットダウンオプション**を**再起動**に設定します。
6. **確定**をクリックし、システムが自動的に再起動します。
7. 起動された後、ガイドに従って設定（例えば言語の選択、パスワードのリセットなど）を完成させます。
8. OSインターフェースで、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"> > **実行**を右クリックし、**cmd**を入力し、**Enter**を押して、管理者コマンドラインツールを開きます。
9. 以下のコマンドを実行して、 SIDが変更されたことを確認します。
```shellsession
whoami /user
```
次のような情報が返されると、SIDが変更されたことを示します。
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)

10.  [手順3](#step_03)で保存されたネットワーク構成情報に従って、、ENIの関連情報（例えば、IPアドレス、ゲートウェイアドレス、DNS など）を再設定します。


### sidchg を使用してSIDを変更する

1. CVMにログインします。
2. IEブラウザでsidchgツールにアクセスしてダウンロードします。
sidchgツールのダウンロードアドレス：`http://www.stratesave.com/html/sidchg.html`です
3. 管理者コマンドラインツールを使用して、以下のコマンドを実行して、sidchgツールを開きます。下図に示すように：
例えば、sidchgツールは C: ディスクに保存され、名称は sidchg64-2.0p.exeとなります。
![](https://main.qcloudimg.com/raw/284926ae1eae88228fb009f247b82068.png)
その中で、`/R` は修正した後自動的に再起動することを示し、`/S` は修正した後閉じることを示し、使用の詳細情報は [SIDCHG の公式説明](http://www.stratesave.com/html/sidchg.html)をご参照ください。
4. インターフェースでの提示に従って、 license keyまたはtrial keyを入力し、 **Enter**を押します。
5. インターフェースの提示に従って、**Y**を入力し、**Enter**を押します。下図に示すように：
![](https://main.qcloudimg.com/raw/43c19634475517b183402d15fa32e962.png)
6. SIDを修正するためのプロンプトボックスで、**確定**をクリックし、SIDのリセットを行います。下図に示すように：
リセットプロセス中に、システムが再起動されます。
![](https://main.qcloudimg.com/raw/b59ec21417cc0de1fd7d851fcd8a2a3b.png)
7. 起動完了後、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;"> > **実行**を右クリックし、**cmd**を入力し、**Enter**を押して、管理者コマンドラインツールを開きます。
8. 以下のコマンドを実行して、SIDが変更されたことを確認します。
```shellsession
whoami /user
```
次のような情報が返されると、SIDが変更されたことを示します。
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)


