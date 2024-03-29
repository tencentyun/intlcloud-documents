## 操作シナリオ 

業務のオンライン化およびアップグレードのシナリオでは、リリースプロセスの安定性およびアプリケーションの安定性が非常に重要です。このドキュメントでは、主にアプリケーションの再デプロイ時に、バッチごとのデプロイを使用してデプロイを安定させる方法を紹介します。 

バッチごとのデプロイ機能では複数回バッチでのアプリケーションのデプロイをサポートしていますが、各バッチは対応する一部の実行インスタンスにのみ更新を実行します。また、一時停止によりロールバック機能を手動で検証し、リアルタイムに故障の影響およびデプロイプロセスの変動を避けることができます。 


## 前提条件 

アプリケーションの初回のデプロイを完了していない場合は、[アプリケーションの作成とデプロイ](https://intl.cloud.tencent.com/document/product/1094/40362)をご参照ください。  

## 操作手順 

1. [TEMコンソール](https://console.cloud.tencent.com/tem)にログインして、左側のナビゲーションバーで【アプリケーション管理】をクリックし、アプリケーションリストページに入ります。 
2. 目的のアプリケーションを選択してアプリケーションIDをクリックし、アプリケーション詳細ページに移動します。 
3. アプリケーション詳細ページの【インスタンスリスト】で【デプロイ】をクリックし、再びデプロイの詳細ページに移動します。    
	![](https://main.qcloudimg.com/raw/f5a2311e83d298273c933d89eab92671.png)
4. デプロイ詳細ページの【デプロイポリシー】で、自分のバッチごとのデプロイを設定します。    
	![](https://main.qcloudimg.com/raw/344bdbf8f0239a1e0d2c9f9a5f434d4e.png)
   - アプリケーション内に複数の実行インスタンスが存在する場合、再デプロイすると自動的にバッチごとのデプロイがトリガーされます。 
   - 少バッチ検証：合計インスタンス数の50％以内の検証バッチを規定することができます。そのバッチの実行が終了すると、残りのバッチを有効にするかを手動で確認する必要があります。
   - バッチのデプロイ：デプロイするバッチ回数を選択すると、インスタンス総数は各バッチに平均的に割り当てられます。
   - 実行方式：次のバッチを手動で開始、または次のバッチを自動（5分間隔）で開始します。
   - デプロイフローチャート：デプロイフローとバッチの詳細を確認します。
5. 【デプロイ】をクリックして【インスタンスリスト】ページに移動し、デプロイを開始します。    
	![](https://main.qcloudimg.com/raw/be40523f08eaf6f04a0a5f0535f8d4d3.png)
6. 【アプリケーションの概要】をクリックすると【詳細の表示】が表示され、【リリースリスト】でバッチごとのデプロイフローを確認および操作することができます。    
	![](https://main.qcloudimg.com/raw/dce950b78faa40a66b7b9ff4eaa131ed.png)
	ロールバック：現在のデプロイプロセスを終了し、すべてのインスタンスを前回のバージョンに戻します。
