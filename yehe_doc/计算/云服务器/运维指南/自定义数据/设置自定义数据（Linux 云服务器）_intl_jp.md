## シナリオ

CVMを作成するときに、**カスタムデータ**を指定することでインスタンスを設定できます。CVMを**初回起動**時に、カスタムデータがテキスト形式でCVMに渡されて実行されます。一度に複数のCVMを購入する場合、カスタムデータは、すべてのCVMの初回起動時にこのテキストを実行します。
このドキュメントでは、Linux CVMの初回起動時に、Shell形式のスクリプトを渡す方法について説明します。

## 注意事項
- カスタムデータをサポートするLinux OSは、以下のとおりです。
	- 64ビットOS：CentOS 6.8 64ビット以降のバージョン、Ubuntu Server 14.04.1 LTS 64ビット以降のバージョン、およびsuse42.3x86_64
	- 32ビットOS：CentOS 6.8 32ビット以降のバージョン
- CVMの初回起動時のみ、テキストを渡すことによってコマンドを実行できます。
- カスタムデータはBase64でエンコードしてから渡す必要があります。**フォーマットの非互換性を避けるために、カスタムデータをLinux環境でエンコードしてください**。
- rootアカウントを使用して、カスタムデータを実行します。スクリプトではsudoコマンドを使用しません。rootユーザーは、作成したすべてのファイルにアクセスできます。他のユーザーにアクセス権限を付与する必要がある場合は、スクリプトで権限を変更してください。　
- 起動時に、カスタムデータで指定されたタスクを実行すると、CVMの起動時間が長くなります。数分待って、タスクの完了後にタスクが正常に実行されるかどうかをテストすることをお勧めします。
- この例では、Shellスクリプトは `#!`文字、およびスクリプトを読み取るインタープリターへのパス（通常は`/bin/bash`）で始まる必要があります。

## 操作手順

###  Shellスクリプトの作成
1.  次のコマンドを実行して、「script_text.sh」という名前のShellスクリプトファイルを作成します。
```
vi script_text.sh
```
2. **i**を押して編集モードに切り替え、次のように入力して「script_text.sh」スクリプトファイルを保存します。
```
#!/bin/bash
echo "Hello Tencent Cloud."
```
> Shellスクリプトは、`#!`文字、およびスクリプトを読み取るインタープリターへのパス（通常は`/bin/bash`）で始まる必要があります。Shellスクリプトの詳細については、Linux ドキュメントプロジェクト（tldp.org）の[BASHプログラミング](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)をご参照ください。

<span id="Base64Script"></span>
### Base64でスクリプトをエンコード

1. 次のコマンドを実行して、「script_text.sh」スクリプトファイルに対してBase64エンコード操作を実行します。
```
# スクリプトに対してBase64エンコード操作を実行します。
base64 script_text.sh
```
次の情報が返されます。
```
# エンコードされた結果
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2. 次のコマンドを実行して、スクリプトのBase64エンコードで返された結果を検証します。
```
# 返された結果に対してBase64エンコードを実行し、実行が必要なコマンドかどうかを検証します。
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### テキストを渡す

インスタンスを起動するさまざまな方法が提供されます。主に次の2つの方法があり、実際のニーズに応じて選択してください。
- [公式サイトまたはコンソールによって渡す](#Consoletrans)
- [APIによって渡す](#APItrans)

<span id="Consoletrans"></span>
#### 公式サイトまたはコンソールによって渡す

1. 下図に示すように、[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)を参照してインスタンスを購入します。また「4.セキュリティグループとCVMの設定」で【高度な設定】をクリックします。
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. 下図に示すように、「高度な設定」の「カスタムデータ」テキストボックスに、[Base64でスクリプトファイルをエンコード](#Base64Script)で返されたエンコード結果を入力します。
たとえば、script_textスクリプトのBase64エンコード結果はIyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg ==です。
![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3.  画面情報に従ってステップごとに操作して、CVMインスタンスを作成します。
> Tencent CVMは、オープンソースソフトウェアcloud-initを介してスクリプトを実行します。cloud-initの詳細については、[cloud-initの公式ウェブサイト](https://cloud-init.io/)をご参照ください。

<span id="APItrans"></span>
#### APIによって渡す

APIを介してCVMを作成する場合、[Base64でスクリプトファイルをエンコード](#Base64Script) で返されたエンコード結果をRunInstances APIのUserDataパラメータに代入することにより、テキストを渡すことができます。
たとえば、UserDataパラメータ付きのCVMのリクエストパラメータを作成する場合、その例は次のとおりです。
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<パブリックリクエストパラメータ>
```
