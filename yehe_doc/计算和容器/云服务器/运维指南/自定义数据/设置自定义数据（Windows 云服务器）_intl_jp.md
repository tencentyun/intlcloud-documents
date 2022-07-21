## 操作シナリオ

Cloud Virtual Machine(CVM)を作成する際、**カスタムデータ**を指定することでインスタンスを設定できます。CVMの**初回起動**時には、カスタムデータがテキストとしてCVMに渡され、そのテキストが実行されます。一度に複数のCVMを購入した場合、カスタムデータはすべてのCVMを最初に起動したときにそのテキストが実行されます。

ここでは、Windows CVMの初回起動時に、PowerShell形式で渡されるスクリプトを例に取って説明します。

## 注意事項

- カスタマイズデータをサポートするWindows OSは、以下のとおりです。
 - Windows Server 2019 データセンターバージョン64ビット英語版</td>
 - Windows Server 2016 データセンターバージョン64ビット英語版</td>
 - Windows Server 2012 R2 データセンターバージョン64ビット英語版</td>
- CVMの初回起動時のみ、テキストを渡すことでコマンドを実行します。
- Base64エンコードの前に、カスタムデータの内容は16KBを超えることはできません。
- カスタムデータはBase64エンコードによって渡されます。Base64ではないスクリプトファイルを直接コピーする場合は、「Base64形式のテキストとして入力」ボックスにチェックを入れないでください。
- 起動時に、カスタマイズデータで指定されたタスクを実行すると、サーバーの起動時間が長くなります。数分待って、タスクの完了後にタスクが正常に実行されたかをテストすることをお勧めします。
- この例では、PowerShellタグを使用して、&lt;powershell&gt;&lt;/powershell&gt;タグなどのWindows PowerShellスクリプトを指定してください。

## 操作手順

### テキストの準備

実際のニーズに合わせてテキストを準備してください。


#### PowerShellスクリプト[](id:PowerShellScript)
PowerShellタグを使用して、PowerShellスクリプトファイルを準備します。
例えば、CVMのC:ドライブに「Hello Tencent Cloud.」という内容の「tencentcloud.txt」ファイルを作成する必要がある場合、PowerShellタグを使用して、以下のような内容を準備することができます。
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```


#### Base64エンコードスクリプト[](id:Base64Script)

1. 次のコマンドを実行して、「script_text.ps1」という名前のPowerShellスクリプトファイルを作成します。
```shell
vi script_text.ps1
```
2. **i**を押して編集モードに切り替え、次の内容を参照し、「script_text.ps1」スクリプトファイルに記述して保存します。
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```
3. 次のコマンドを実行して、「script_text.ps1」スクリプトファイルに対してBase64エンコード操作を実行します。
```shell
base64 script_text.ps1
```
以下の情報を返します。
```shell
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### テキストを渡す

インスタンスを起動するさまざまな方法を提供しています。主に次の2つの方法があり、実際のニーズに合わせてお選びください。

<dx-tabs>
::: 公式サイトまたはコンソールから渡す[](id:Consoletrans)

1. 下図に示すように、[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)を参照してインスタンスを購入し、「2.ホストの設定」で**詳細設定**をクリックしてください。
![](https://qcloudimg.tencent-cloud.cn/raw/283fb3e0e1400d4ba5725c8b6a1ea279.png)
2. 「詳細設定」において、実際のニーズに応じて「カスタムデータ」のテキストボックスに準備したテキスト内容を入力します。
 - PowerShellスクリプト：[PowerShellスクリプト](#PowerShellScript)を直接入力します。
 - Base64エンコードスクリプト：下図のように、まず「base64形式のテキストとして入力」にチェックを入れてから、[Base64エンコードスクリプト](#Base64Script)を入力する必要があります。
 ![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. 画面情報に従ってステップごとに操作し、CVMの作成を完了します。
:::
::: APIから渡す[](id:APItrans)
APIを介してCVMを作成する場合、[Base64エンコードスクリプト](#Base64Script)で返されたエンコード結果をRunInstancesインターフェースのUserDataパラメータに代入することにより、テキストを渡すことができます。
例えば、UserDataパラメータを持つCVMへのリクエストパラメータを作成する場合、以下のような例があります。
```shell
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Version=2017-03-12
&Placement.Zone=ap-guangzhou-2
&ImageId=img-pmqg1cw7
&UserData=PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAuXHRlbmNlbnRjbG91ZC50go=
&<パブリックリクエストパラメータ>
```
:::
</dx-tabs>



### カスタムデータ設定の検証

1. CVMにログインします。
2. OSのインターフェースでC:\ドライブを開き、`tencentcloud.txt`テキストファイルが存在するかどうかを確認します。
下図に示すように、`tencentcloud.txt`テキストファイルが存在する場合、設定が成功したことを意味します。
![](https://main.qcloudimg.com/raw/9f94ec922111734a489b9730d66168c3.png)


### 実行ログの確認
`C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\cloudbase-init.log`ファイルを確認すると、スクリプトの実行ログを取得できます。

