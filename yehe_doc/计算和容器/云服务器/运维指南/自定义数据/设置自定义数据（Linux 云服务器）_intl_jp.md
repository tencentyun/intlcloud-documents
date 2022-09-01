## 操作シナリオ

Cloud Virtual Machine(CVM)を作成する際、**カスタムデータ**を指定することでインスタンスを設定できます。CVMの**初回起動**時には、カスタムデータがテキストとしてCVMに渡され、そのテキストが実行されます。一度に複数のCVMを購入した場合、カスタムデータはすべてのCVMを最初に起動したときにそのテキストが実行されます。

このドキュメントでは、Linux CVMの初回起動時に、Shell形式のスクリプトを渡す場合を例に説明します。

## 注意事項
- カスタマイズデータをサポートするLinux OSは、以下のとおりです。
	- 64ビットのOS：CentOS 6.8 64ビット以上、Ubuntu Server 14.04.1 LTS 64ビット以上、suse42.3x86_64
	- 32ビットのOS：CentOS 6.8 32ビット以上
- CVMの初回起動時のみ、テキストを渡すことでコマンドを実行します。
- 渡されるテキストはBase64でエンコーディングされている必要があります。**Linux環境でエンコーディングを行い、フォーマットの非互換性を避けてください**。
- rootアカウントを使用して、ユーザーデータによる入力テキストを実行します。スクリプトではsudoコマンドを使用しません。作成されたファイルはすべてrootに属します。root以外のユーザーにファイルアクセス権を許可する必要がある場合は、スクリプトで権限を変更してください。
- 起動時に、カスタマイズデータで指定されたタスクを実行すると、サーバーの起動時間が長くなります。数分待って、タスクの完了後にタスクが正常に実行されたかをテストすることをお勧めします。
- この例では、Shellスクリプトは `#!`文字、およびスクリプトを読み取るインタープリターへのパス（通常は`/bin/bash`）で始まる必要があります。

## 操作手順

### Shellスクリプトの作成
1. 次のコマンドを実行して、「script_text.sh」という名前のShellスクリプトファイルを作成します。
```shellsession
vi script_text.sh
```
2. **i**を押して編集モードに切り替え、次の内容を参照し、「script_text.sh」スクリプトファイルに記述して保存します。
```bash
#!/bin/bash
echo "Hello Tencent Cloud."
```
<dx-alert infotype="notice" title="">
Shellスクリプトは必ず`#!`文字およびスクリプトを読み取るインタープリターへのパス（通常は `/bin/bash`）で始まる必要があります。Shellスクリプトの詳細については、Linux ドキュメントプロジェクト (tldp.org)の [BASHのプログラミング方法](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)。
</dx-alert>




### Base64エンコードスクリプトを使用する[](id:Base64Script)

1. 次のコマンドを実行して、「script_text.sh」スクリプトファイルに対してBase64エンコード操作を実行します。
```shellsession
# スクリプトに対してBase64エンコーディング操作を実行する
base64 script_text.sh
```
以下の情報を返します。
```shellsession
# エンコードされた結果
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2. 次のコマンドを実行し、Base64でscript_textスクリプトファイルをエンコーディングして返された結果を検証します。
```shellsession
# 返された結果に対してBase64エンコーディングを実行し、実行が必要なコマンドかどうかを検証します。
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### テキストを渡す

インスタンスを起動するさまざまな方法を提供しています。主に次の2つの方法があり、実際のニーズに合わせてお選びください。
<dx-tabs>
::: 公式サイトまたはコンソールから渡す[](id:Consoletrans)
1. 下図に示すように、[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)を参照してインスタンスを購入し、「2.ホストの設定」のステップで**詳細設定**をクリックしてください。
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. 「高度な設定」の「カスタマイズデータ」 テキストボックス内に、 [使用Base64コードスクリプト文件](#Base64Script)を入力して返された結果は下図に示すとおりです。
たとえば、Base64でscript_textスクリプトファイルをエンコーディングして返された結果は `IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==`です。
![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. 画面情報に従ってステップごとに操作し、CVMの作成を完了します。
<dx-alert infotype="explain" title="">
Tencent CVMはオープンソースソフトウェアcloud-initを介してスクリプトを実行します。cloud-initの詳細については[cloud-init公式サイト](https://cloud-init.io/)をご参照ください。
</dx-alert>


:::
::: APIから渡す[](id:APItrans)
APIを介してCVMを作成する場合、[Base64でコードスクリプトファイルをエンコーディングする](#Base64Script) で返されたエンコーディング結果をRunInstancesインターフェースのUserDataパラメータに代入することにより、テキストを渡すことができます。
例えば、UserDataパラメータを持つCVMへのリクエストパラメータを作成する場合、以下のような例があります。
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<パブリックリクエストパラメータ>
```

:::
</dx-tabs>

### 実行ログの確認
サーバーの作成に成功すると、次のコマンドを実行して、スクリプト実行ログを確認することができます：
```shellsession
cat /var/log/cloud-init-output.log
```

