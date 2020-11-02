## 概要

CVMを作成する時に、**カスタムデータ**を指定することでインスタンスを構成できます。CVMの**初回起動時**に、カスタムデータがテキスト形式でCVMに渡され、実行されます。一度に複数のCVMインスタンスを購入する場合、カスタムデータは、すべてのCVMの初回起動時にこのテキストを実行します。
本書では、PowerShellスクリプトを定義し、それを使用してWindows CVMインスタンスを構成する方法について説明します。

## 注意事項

- カスタムデータをサポートするWindows OSには次のものが含まれています。
- Windows Server 2019 Datacenter Edition 64ビット 中国語/英語版
 - Windows Server 2016 Datacenter Edition 64ビット 中国語/英語版
 - Windows Server 2012 R2 Datacenter Edition 64ビット 中国語/英語版
- スクリプトは、インスタンスの初回（初めて起動）したときしか実行されない。
- カスタムデータのコンテンツは、Base64エンコードの前に16KBを超えてはいけません。
- カスタムデータはBase64でエンコードされてから渡されます。base64以外のスクリプトファイルを直接コピーする場合は、【base64形式のテキストとして入力】を選択しないでください。
- 起動時に、カスタムデータで指定されたタスクを実行すると、サーバーの起動時間が長くなります。数分間待ってから、タスクが完了した後にタスクが正常に実行されたかどうかをテストすることをお勧めします。
- この例では、&lt;powershell&gt;&lt;/powershell&gt;などのPowerShellタグを使用してWindows PowerShellスクリプトを指定してください。

## 操作手順

### スクリプトを準備する

実際のニーズに応じてスクリプトを準備してください。

<span id="PowerShellScript"></span>
#### PowerShell スクリプト
PowerShellタグを使用して、1つのPowerShellスクリプトファイルを準備します。
たとえば、CVMのC:ドライブでコンテンツが「Hello Tencent Cloud．」である「tencentcloud.txt」ファイルを作成する必要がある場合、PowerShellタブを使用して次の内容を準備できます。
```
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```

<span id="Base64Script"></span>
#### スクリプトをBase64でエンコードする

1.次のコマンドを実行して、「script_text.ps1」という名前の PowerShellスクリプトファイルを作成します。
```
vi script_text.ps1
```
2. **i**を押して編集モードに切り替え、以下の内容を入力して保存します。
```
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```
3. 次のコマンドを実行して、「script_text.ps1」スクリプトファイルをBase64でエンコードします。
```
base64 script_text.ps1
```
次の情報が返されます。
```
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### スクリプトを渡す

インスタンスを起動するためのさまざまなオプションが提供されています。主に次の2つの方法があり、実際のニーズに応じて選択してください。
- [公式サイトまたはコンソールによって渡す](#Consoletrans)
- [APIによって渡す](#APItrans)

<span id="Consoletrans"></span>
#### 公式サイトまたはコンソールによって渡す

1. [インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)を参照してインスタンスを購入します。また下図に示すように、「4.セキュリティグループとCVMの設定」で【詳細設定】をクリックします。
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. 【詳細設定】では、実際のニーズに応じて、「カスタムデータ」のテキストボックスに用意されたスクリプトの内容を入力します。
 - PowerShellスクリプト：[PowerShell スクリプト](#PowerShellScript)を直接入力します。
 - Base64でエンコードされたスクリプト：先に【base64形式のテキストとして入力】にチェックを入れてから、[Base64でエンコードされたスクリプト](#Base64Script)を入力する必要があります。
 ![1558602155668](https://main.qcloudimg.com/raw/24926b2c2675e2d6959adcf62054f5b1.png)
3.画面情報に従って実行して、CVMの作成を完了します。

<span id="APItrans"></span>
#### APIによって渡す

Tencent Cloud APIを使用してCVMインスタンスを作成することを選択した場合、[Base64でエンコードされたスクリプト](#Base64Script)で返されたエンコードされた結果をRunInstancesインターフェースのUserDataパラメータに代入することにより、テキストを渡すことができます。
たとえば、UserDataパラメータ付きのCVMのリクエストパラメータを作成する場合、例は次のとおりです。
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAuXHRlbmNlbnRjbG91ZC50eHQKPC9wb3dlcnNoZWxsPgo=
  &<Common request parameter>
```

### カスタムデータの設定を検証する

1.CVMインスタンスにログインします。
2. OS画面で、 C:ドライブを開き、「tencentcloud.txt」テキストファイルがあるかどうかを確認します。
「tencentcloud.txt」テキストファイルがある場合は、設定が成功したことを意味します。以下に示すように：
![](https://main.qcloudimg.com/raw/9f94ec922111734a489b9730d66168c3.png)


