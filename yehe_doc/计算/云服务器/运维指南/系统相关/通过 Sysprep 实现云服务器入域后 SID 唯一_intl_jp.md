## ユースケース
インスタンスをドメインに参加させ、ドメインアカウントを使用してWindows CVMにログインする必要があるユーザーの場合、カスタマイズイメージを作成する前に、Sysprep操作を実行してドメイン内の一意のSIDを確認する必要があります。そうしないと、カスタマイズイメージによって作成されたCVMと元のインスタンスに同じSIDなどの同一の情報が含まれているため、インスタンスをドメインに参加させることができません。ご利用のWindows CVMがドメインに参加させる必要がない場合は、この操作をスキップしてください。

このドキュメントでは、Windows Server 2012 R2 64ビットOSを例に、Windows OSでSysprepを実行して、Windows CVMがドメインに参加させた後にSIDを一意にする方法を説明します。

Sysprepの詳細については、`https://technet.microsoft.com/zh-cn/library/cc721940(v=ws.10).aspx`をご参照ください。


## 注意事項

- Windows CVMは、正規のWindows OSであり、アクティブ化されている必要があります。
- Windows CVMが非パブリックイメージによって作成されている場合、当CVMは元のイメージに付属するSysprepバージョンのみをサポートし、Sysprepは常に`%WINDIR%\system32\sysprep`ディレクトリから実行する必要があります。
- 残りのWindowsリセットカウントが1以上である必要があります。そうでない場合、Sysprepをカプセル化できません。
`slmgr.vbs / dlv`コマンドを実行することで、残りのWindowsリセットカウントを確認できます。
- Windows CVMのCloudbase-Initアカウントは、Cloudbase-Initエージェントプログラムの組み込みアカウントであり、CVMの起動時にメタデータを取得し、関連する設定を実行するために使用されます。このアカウントを変更または削除するか、エージェントプログラムCloudbase-Initをアンマウントすると、このCVMで作成されたカスタマイズイメージによって生成されたCVMが初期化されるときに、カスタマイズ情報が失われる可能性があります。したがって、Cloudbase-initアカウントを変更または削除することはお勧めしません。  

## 前提条件

- 管理者として [Windows CVMにログイン](https://intl.cloud.tencent.com/document/product/213/5435)しました。　
- すでに [Windows CVMにCloudbase-Initをインストール](https://intl.cloud.tencent.com/document/product/213/32364)しました。

## 操作手順

1. OSのインターフェースで、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png"></img>をクリックして、Windows PowerShell画面を開きます。
2. Windows PowerShellウィンドウで次のコマンドを実行して、Cloudbase-initツールのインストールパスに入ります。
> Cloudbase-initツールが`C:\Program Files\Cloudbase Solutions\` ディレクトリにインストールされていると仮定します。
>
```
cd 'C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf'
```
3. 次のコマンドを実行して、Windowsシステムをカプセル化します。
> 
> - 次のコマンドを実行する際に、コマンドに`/unattend:Unattend.xml`を含める必要があります。そうしないと、現在ご利用のCVMのユーザー名、パスワードなどの重要な設定情報がリセットされます。以降このイメージを使用してCVMを作成するときに、ログイン方法として「Follow image」を選択した場合、 CVMの起動後に CVMのユーザー名とパスワードを手動でリセットする必要があります。
> - 以下のコマンドを実行すると、CVMは自動的にシャットダウンします。後でこのイメージを使用して作成された各CVMに一意のSIDがあることを確保するために、カスタマイズイメージを作成する前にCVMを再起動しないでください。再起動すると、コマンドは現在のCVMに対してのみ有効です。  
> - Windows Server 2012およびWindows Server 2012 R2 OSの場合、次のコマンドを実行すると、 このCVMのアカウント（Administrator）とパスワードが削除されます。CVMを再起動した後、アカウントとパスワードをリセットし、新しくパスワードを適切に保管してください。詳細については、[インスタンスのパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)をご参照してください。
> 
```
C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /unattend:Unattend.xml
```
4. [カスタマイズイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)を参照して、Sysprep操作を実行したCVMインスタンスをイメージに作成し、そのイメージを使用してCVMインスタンスを作成します。 
このように、新規作成されたすべてのCVMインスタンスは、ドメインに参加した後、一意のSIDを持つようになります。
> `whoami /user`コマンドを実行すると、 CVMのSIDを確認できます。
>


