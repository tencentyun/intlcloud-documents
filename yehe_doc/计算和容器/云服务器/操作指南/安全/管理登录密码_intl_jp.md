## 操作シナリオ
Cloud Virtual Machine のアカウントとパスワードは、CVM にログインするための資格情報です。本ドキュメントでは、CVM にログインする時にパスワードを使用および管理する方法について説明します。

## 制限条件

パスワードを設定する場合、以下の制限条件を満たす必要があります：
- **Linux インスタンス**：パスワードの長さは8～30文字で、12文字以上のパスワードを推奨し、「/」で始めることはできず、少なくとも3つの項目（`a～z`、`A～Z`、`0～9`と`<code>()`~!@#$%^&*-+=_|{}[]:;'<>,.?/</code>の特殊記号）を含む必要があります。
- **Windows インスタンス**：パスワードの長さは12～30文字で、「/」で始めることはできず、少なくとも3つの項目（`a～z`、`A～Z`、`0～9`と<code>()`~!@#$%^&*-+=_|{}[]:;'<>,.?/</code>）を含む必要があり、ユーザー名を含むことができません。

## 操作手順

### 初期パスワードを設定する
CVMを購入する場合、選択された設定方法によって初期パスワードの設定が異なっています。
 - [**カスタマイズ設定**](https://buy.intl.cloud.tencent.com/cvm?regionId=4&projectId=-1)の方法でインスタンスを作成します。作成プロセス中に、初期パスワードを設定する方法は、ログイン方法によって異なります。
<table>
	<tr><th>ログイン方法</th><th>説明</th></tr>
	<tr><td>パスワードを自動生成</td><td>初期パスワードはEメールとコンソールの <a href="https://console.cloud.tencent.com/message">サイト内メッセージ</a> を介して送信します。</td></tr>
	<tr><td>直ちに暗号鍵に関連付けます</td><td><b>デフォルトではオフです</b>ユーザー名前とパスワードでログインできます。今後パスワードが必要な場合は、CVMコンソールにログインして、<a href="https://intl.cloud.tencent.com/document/product/213/16566">パスワードをリセットしてください</a>。</td></tr>
	<tr><td>パスワード設定</td><td>カスタムパスワードは初期パスワードです。</td></tr>
</table>


### パスワードを確認する

システムで自動的に生成したログイン用パスワードはEメールとコンソール[サイト内メッセージ](https://console.cloud.tencent.com/message)を介して送信させていただきます。以下の操作はサイト内メッセージを例として説明します。
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
2. 右上の<img src="https://qcloudimg.tencent-cloud.cn/raw/d47b595ce159b2946f5fbbe10509569a.png" style="margin: -3px 0px;"></img>をクリックし、その製品情報を選択します。下図の通りです：
![](https://main.qcloudimg.com/raw/e3c624a805d2f5776807df44bd373b59.png)
この製品の情報画面にアクセスし、パスワードを確認できます。
![](https://main.qcloudimg.com/raw/73bef8b11ded3d0cee5441d3d3218e25.png)

### パスワードのリセット

[インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566)をご参照ください。
	
	
