このドキュメントは、Tencent Cloud Virtual Machine（CVM）インスタンスの使用をすばやく開始するのに役立ちます。 

## 1.CVMの概要
Cloud Virtual Machine（CVM）はTencent Cloudが提供する拡張可能なクラウド コンピューティング サービスです。CVMを使用することで、リソース使用量の見積もりと初期投資は必要ありません。そして、短時間で任意の数のCVMを迅速に起動し、リアルタイムにアプリケーションをデプロイできます。


## 2. CVMについて学ぶ
CVMインスタンスの詳細については、次のドキュメントをご参照ください。
- [CVMはどのように動作しますか？](https://intl.cloud.tencent.com/document/product/213/495)
- [CVMはどのように請求されますか？](https://intl.cloud.tencent.com/document/product/213/2180)
- [CVMの使用に関する制限？](https://intl.cloud.tencent.com/document/product/213/15379)
- [CVMの一般的な概念](https://intl.cloud.tencent.com/document/product/213/38678)


## 3. CVMインスタンスの作成
[CVM購入ページ](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.91351132.770173325.1571651505)に移動し、ページ情報を注意深く確認し、CVMの地域、モデル、イメージ、パブリックネットワークの帯域幅、購入数量、有効期間を柔軟に選択して、ビジネスニーズに合わせてCVMインスタンスを購入できます。
カスタムCVMの作成方法については、 [Linux CVM設定のカスタマイズ](https://intl.cloud.tencent.com/document/product/213/10517)または [Windows CVM設定のカスタマイズ](https://intl.cloud.tencent.com/document/product/213/10516)ドキュメントをご参照ください。次の図に示すように：
![](https://main.qcloudimg.com/raw/40c2812ff1294f901238cc3e39ba25f9.png)

## 4. CVMインスタンスにログイン
CVMインスタンスを購入した後、購入したCVMインスタンスにログインできます。詳細については、次のドキュメントをご参照ください。
 - [Linuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/5436)
 - [Windowsインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/5435)


次に、ローカルファイルをCVMに保存するか、CVMを個人用仮想マシンまたはWebサイトを構築するためのサーバーとして使用できます。より多くの情報が必要な場合は、以下のコンテンツを参照して、さらに理解して使用してください。


## 5. 関連情報

### コンソール機能の概要
| 機能 | 参考ドキュメント |
|---------|---------|
| CVMインスタンスの作成 | [インスタンス作成ガイドライン](https://intl.cloud.tencent.com/document/product/213/36302) |
| ルールに従ってインスタンス/CVMに名前を付ける | [名に連続した番号をつける/パターン文字列を指定して名前を付ける](https://intl.cloud.tencent.com/document/product/213/32020) |
| CVMインスタンス設定のアップグレードまたはダウングレード | [インスタンス設定の変更](https://intl.cloud.tencent.com/document/product/213/2178) |
| CVMの暗号化されたログイン方法としてSSHキーを使用し、それを管理する | [SSHキーの管理](https://intl.cloud.tencent.com/document/product/213/16691) |
| インスタンスのログインパスワードを変更またはリセットする| [インスタンスパスワードのリセット](https://intl.cloud.tencent.com/document/product/213/16566) |
|CVMインスタンスの破棄、リリース、または返却| [インスタンスの破棄/返却](https://intl.cloud.tencent.com/document/product/213/4930) |
| 特定の地域のインスタンス情報 | [インスタンスのエクスポート](https://intl.cloud.tencent.com/document/product/213/16563) |
| CVMインスタンスと関連リソースを検索する| クロスリージョン検索 |
| 新しいカスタムイメージを作成し、このイメージを使用して、元のインスタンスと同じカスタム構成の新しいインスタンスを作成する| [カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942) |
| 他のユーザーから共有イメージを取得し、必要なコンポーネントを取得して、カスタムコンテンツを追加する | [カスタムイメージを共有](https://intl.cloud.tencent.com/document/product/213/4944) |
| ローカルまたは他のプラットフォームのサーバーシステムディスクイメージファイルをCVMのカスタムイメージにインポートする | [イメージのインポートの概要](https://intl.cloud.tencent.com/document/product/213/4945) |
| Linuxイメージの作成とエクスポート | [Linuxイメージの作成](https://intl.cloud.tencent.com/document/product/213/17814) |
| Windowsイメージの作成とエクスポート | [Windowsイメージの作成](https://intl.cloud.tencent.com/document/product/213/17815) |
| ソースサーバー上のシステムとアプリケーションをIDCまたは他のクラウドプラットフォームからTencent Cloudに移行する | [オンライン移行の概要](https://intl.cloud.tencent.com/document/product/213/35639) |
| クラウドディスクを拡張してストレージ容量を増やす | [クラウドディスクの拡張](https://intl.cloud.tencent.com/document/product/213/32377) |
| パブリックIPをEIPに変換して、インスタンスの障害をマスクする | [EIP](https://intl.cloud.tencent.com/document/product/213/16586) |
| IPv6 CIDRブロックを使用してCVMを作成し、ENIに対してIPv6を有効にして、プライベートネットワークとパブリックネットワークを経由してIPv6通信を実現する | [IPv6の構成](https://intl.cloud.tencent.com/document/product/213/34836) |
| ユースケースに基づいてセキュリティグループを設定する | [シナリオ](https://intl.cloud.tencent.com/document/product/213/32369) |
| さまざまな側面（ビジネス、用途、担当者など）からCVMリソースを分類および管理する | [タグを使用してインスタンスを管理](https://intl.cloud.tencent.com/document/product/213/19548) |
| CVMインスタンスのCPU、メモリ、ネットワーク帯域幅、ディスクなどの監視データを表示する | [インスタンス監視データを取得](https://intl.cloud.tencent.com/document/product/213/5178) |

### 高度な使用方法
CVM上に自分の個人的なウェブサイトやフォーラムを構築することができます。詳細については、[Webサイトの作成方法](https://intl.cloud.tencent.com/document/product/213/34815)をご参照ください。

### 開発者ツール
Tencent Cloud APIは、製品を便利かつ迅速に使用するのに役立ち、少量のコードでクラウド製品を迅速に管理できます。また、API Explorer、TCCLI、SDK、API Inspectorなどのさまざまなツールを提供します。Tencent Cloud APIクイックスタートドキュメントを参照して、API関連の情報を確認し、使用を開始できます。


## 6.フィードバックと提案
Tencent Cloud CVMの製品およびサービスを使用する上で何らかの質問や助言がある場合は、以下の方法でフィードバックしてください。後ほど専門スタッフがお客様の質問に回答いたします。
- リンク、コンテンツ、APIエラーなど、製品ドキュメントに何らかの問題がある場合には、ドキュメントの下部にある【フィードバックを送信】をクリックするか、問題のあるコンテンツを選択してフィードバックを送信できます。
- 製品関連の質問がある場合には、[チケットを提出して](https://console.cloud.tencent.com/workorder/category)サポートを求めることができます。

  


