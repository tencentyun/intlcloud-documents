## 操作シナリオ

CVMを作成するときに、**カスタマイズデータ**を指定することでインスタンスを構成できます。CVMが**初回起動**時に、カスタマイズデータがテキストとしてCVMに渡され、テキストが実行されます。一度に複数台のCVMを購入すると、カスタマイズデータは、すべてのCVMの初回起動時に、このテキストを実行します。
本書では、Linux CVMの初回起動時に、PowerShell形式のスクリプトを渡す場合を例に説明します。

## 注意事項
-カスタマイズデータをサポートするLinux OSは、以下のとおりです。
	- 64ビットのOS：CentOS 6.8 64ビット以上、Ubuntu Server 14.04.1 LTS 64ビット以上、suse42.3x86_64です
	- 32ビットのOS：CentOS 6.8 32ビット以上です。
-CVMの初回起動時のみ、テキストを渡すことでコマンドを実行します。
-渡されるテキストはBase64でエンコーディングされている必要があります。**フォーマットの非互換性を避けるためにLinux環境でエンコーディングしてください**。
-rootアカウントを使用して、ユーザーデータによる入力テキストを実行します。スクリプトではsudoコマンドを使用しません。作成されたファイルはすべてrootに属します。root以外のユーザーにファイルアクセス権を許可する必要がある場合は、スクリプトで権限を変更してください。
-起動時に、カスタマイズデータで指定されたタスクを実行すると、サーバーの起動時間が長くなります。数分待って、タスクの完了後にタスクが正常に実行されたかをテストすることをお勧めします。
-この例では、Shellスクリプトは `#!`文字、およびスクリプトを読み取るインタープリタへのパス(通常は`/bin/bash`)で始まる必要があります。

## 操作手順

###  Shellスクリプトの作成
1.次のコマンドを実行して、「script_text.sh」という名前のShellスクリプトファイルを作成します。
```
vi script_text.sh
```
2. **i**または**Insert**を押して、編集モードに切り替え、次の内容を参照し、「script_text.sh」スクリプトファイルに記述して保存します。
```
#!/bin/bash
echo "Hello Tencent Cloud."
```
>Shellスクリプトは、`#!`文字、およびスクリプトを読み取るインタープリタへのパス(通常は`/bin/bash`)で始まる必要があります。Shellスクリプトの詳細については、Linux ドキュメントプロジェクト(tldp.org)の[BASHのプログラミング方法](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)をご参照ください。

<span id="Base64Script"></span>
### Base64でスクリプトファイルをエンコーディングする

1. 次のコマンドを実行して、「script_text.sh」スクリプトファイルに対してBase64エンコーディング操作を実行します。
```
＃ スクリプトに対してBase64エンコーディング操作を実行する
base64 script_text.sh
```
次の情報が返されます。
```
# エンコードされた結果
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2.次のコマンドを実行して、スクリプトのBase64エンコーディングで返された結果を検証します。
```
＃返された結果に対してBase64エンコーディングを実行し、実行が必要なコマンドかどうかを検証します。
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### テキストの伝達

インスタンスを起動するさまざまな方法が提供されています。主に次の2つの状況に分けられています。実際の要件に応じて選択してください。
- [公式サイトまたはコンソールを介して伝達する](#Consoletrans)
- [APIを介して伝達する](#APItrans)

<span id="Consoletrans"></span>
#### 公式サイトまたはコンソールを介して伝達する

1. [インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)を参照してインスタンスを購入します。また下図に示すように「4.セキュリティグループとホストの設定」で[高級設定]をクリックします。
2. 下図に示すように、[高級設定]の[カスタマイズデータ]テキストボックスに、[Base64でスクリプトファイルをエンコーディングする](＃Base64Script)で返されたエンコーディング結果を入力します。
たとえば、Base64でscript_textスクリプトファイルをエンコーディングして返された結果は、`IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==`です。
![](https://main.qcloudimg.com/raw/8905a22d7afa6cc31255a960ed1eea1f.png)
3.画面情報に従ってステップごとに操作して、CVMの作成を完了します。
> Tencent CVMは、オープンソースソフトウェアcloud-initを介してスクリプトを実行します。cloud-initの詳細については、[cloud-initの公式ウェブサイト](https://cloud-init.io/)をご参照ください。

<span id="APItrans"></span>
#### APIを介して伝達する

APIを介してCVMを作成する場合、[Base64でスクリプトファイルをエンコーディングする](＃Base64Script)で返されたエンコーディング結果をRunInstancesインターフェースのUserDataパラメータに代入することにより、テキストを渡すことができます。
たとえば、UserDataパラメータ付きのCVMのリクエストパラメータを作成する場合、その例は次のとおりです。
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<パブリックリクエストパラメータ>
```
