


このドキュメントでは、主にイメージリソースを使用してサーバーフリートを作成する方法について説明しています。

## 前提条件

 [Tencent CVM](https://intl.cloud.tencent.com/product/cvm)をすでに保有していること。

## 操作手順

1.[CVMコンソール](https://console.cloud.tencent.com/cvm/instance/index?rid=1)にログインし、左側ナビゲーションメニューの【インスタンス】をクリックして、インスタンス管理ページに進みます。  
2.インスタンス管理ページで、イメージを作成するインスタンスを選択します。詳細については、[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)をご参照ください。
3. イメージの作成に成功したら、イメージリソースを対応するTencent CVMにアップロードし、起動プロセスをパス `/local/game/` の下に配置して、GSEを開始できるようにします。

