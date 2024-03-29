## シナリオ

ここでは、主にゲームサーバーセッションの確認方法をご説明します。これは、バックエンドの中のプロセスに対応しており、クラウドAPIの呼び出しによって、クライアントにゲームサーバーセッションがアサインされ、GSEがゲームサーバーセッションを空いているプロセスにアサインします。

## 前提条件

[GSE申請書](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6)を記入して利用資格を取得し、サーバーフリートを作成済みであること。

## 操作手順

1. [GSEコンソール](https://console.cloud.tencent.com/gse/asset)にログインし、サーバーフリートを作成します。詳細については、[サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)をご参照ください。
2. 作成できたサーバーフリートの**ID**をクリックして、サーバーフリートの詳細情報に入り、**ゲームサーバーセッション**をクリックして、ゲームサーバーセッションに入ります。詳細情報の説明は次のとおりです。
	- **ゲームサーバーセッションID**：デフォルトではシステムが自動生成します。    
	- **名称**：[CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139) APIを呼び出す時に入力します。
	- **ステータス**：ゲームサーバーセッションのステータスは、未定義、アクティブ、アクティベート中、終了、終了中、異常に分かれます。
	- **インスタンスタイプ**：デフォルトでは自動生成です。
	- **IP**：デフォルトでは自動生成です。
	- **ポート**：自動生成が可能です。開発者が対戦サービスの中でアサインすることもできます。
	- **プレイヤーセッション**：ACTIVEまたはRESERVED状態にあるプレイヤーセッション数が含まれます。
		- ACTIVEとはゲームサーバーに接続済みであることを指します。
		- RESERVEDとはゲームサーバーセッションの中でプレイヤーのためにスロットがすでにアサインされていますが、プレイヤーが接続していない状態を指します。
	- **作成時間**：ゲームサーバーセッションを作成した時間で、表示形式は yyyy-mm-dd hh:mm:ssです。前から後ろまたは後ろから前に配列することができます。
	- **稼働時間**：開始から現在までの稼働時間を表し、表示形式は xxd xxh xxm xxsです。前から後ろまたは後ろから前の順番で配列できます。
![](https://main.qcloudimg.com/raw/d568f8afde784c06bd37cc3cee71cd5c.png)




