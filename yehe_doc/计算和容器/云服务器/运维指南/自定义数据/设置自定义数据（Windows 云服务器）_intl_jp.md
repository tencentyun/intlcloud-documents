## ユースケース

CVMを作成する時に、**カスタムデータ**を指定することでインスタンスを構成できます。CVMを**初回起動**する時に、カスタムデータがテキスト形式でCVMに渡され、実行されます。一度に複数台のCVMを購入する場合、カスタムデータは、すべてのCVMの初回起動時にこのテキストを実行します。

本書では、Windows CVMの初回起動時に、PowerShell形式のスクリプトを渡すことを例として説明します。

## 注意事項

- カスタムデータをサポートするWindows OSには次のものが含まれています：
 - Windows Server 2019データセンター版 64ビット英語
 - Windows Server 2016データセンター版 64ビット英語
 - Windows Server 2012 R2データセンター版 64ビット英語
- CVMの初回起動時のみ、テキストを渡すことでコマンドを実行します。
- カスタムデータのコンテンツは、Base64コーディングの前に16KBを超えてはいけません。
- カスタムデータはBase64エンコードによって渡されます。Base64ではないスクリプトファイルを直接コピーする場合は、「Base64形式のテキストとして入力」ボックスにチェックを入れないでください。
- 起動時に、カスタムデータで指定されたタスクを実行すると、サーバーの起動時間が長くなります。数分間待ってから、タスクが完了した後にタスクが正常に実行されたかどうかをテストすることをお勧めします。
- この例では、&lt;powershell&gt;&lt;/powershell&gt;タグなどのPowerShellタグを使用してWindows PowerShellスクリプトを指定してください。

## 操作手順

### テキストを準備する

実際のニーズに応じてテキストを準備してください。


#### PowerShellスクリプト[](id:PowerShellScript)
PowerShellタグを使用して、1つのPowerShellスクリプトファイルを準備します。
たとえば、CVMのC:ドライブでコンテンツが「Hello Tencent Cloud.」である「tencentcloud.txt」ファイルを作成する必要がある場合、PowerShellタブを使用して次の内容を準備できます：
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```


#### Base64エンコードスクリプト[](id:Base64Script)

1.次のコマンドを実行して、「script_text.ps1」という名前の PowerShellスクリプトファイルを作成します。
```shell
vi script_text.ps1
```
2. **i**を押して編集モードに切り替え、次の内容を参照し、「script_text.ps1」スクリプトファイルに記述して保存します。
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```
1. 次のコマンドを実行して、「script_text.ps1」スクリプトファイルに対してBase64エンコーディング操作を実行します。
```shell
base64 script_text.ps1
```
次の情報が返されます：
```shell
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### テキストを渡す

インスタンスを起動するさまざまな方法が提供されます。主に次の2つの方法があり、実際のニーズに応じて選択してください：

<dx-tabs>
::: 公式サイトまたはコンソールから渡す[](id:Consoletrans)
1. 下図に示すように、[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)を参照してインスタンスを購入し、「2.ネットワークとホストの設定」の**他の設定**から**詳細設定**をクリックしてください：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TKin326_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221208114658.png)
2. 「詳細設定」では、実際のニーズに応じて、「カスタムデータ」のテキストボックスに用意されたテキスト内容を入力します。
 - PowerShellスクリプト：[PowerShell スクリプト](#PowerShellScript)を直接入力します。
 - Base64エンコードスクリプト：下図のように、まず「上記の入力はBase64エンコードを使用しています」にチェックを入れてから、[Base64エンコードスクリプト](#Base64Script)を入力する必要があります：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QkmS577_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221208114852.png)
3.画面情報に従って逐次に操作し、CVMの作成を完了します。
:::
::: APIから渡す[](id:APItrans)
APIを介してCVMを作成する場合、[Base64コーディングスクリプト](＃Base64Script)で返されたコーディング結果をRunInstancesインターフェースのUserDataパラメータに代入することにより、テキストを渡すことができます。
たとえば、UserDataパラメータ付きのCVMのリクエストパラメータを作成する場合、例は次のとおりです：
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



### カスタムデータの設定を検証する

1. CVMにログインします。
2. OS画面で、 C:ドライブを開き、「tencentcloud.txt」テキストファイルがあるかどうかを確認します。
下図に示すように、`tencentcloud.txt`テキストファイルが存在する場合、設定が成功したことを意味します：
![](https://main.qcloudimg.com/raw/9f94ec922111734a489b9730d66168c3.png)


### 実行ログの確認
`C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\cloudbase-init.log`ファイルを確認すると、スクリプトの実行ログを取得できます。

