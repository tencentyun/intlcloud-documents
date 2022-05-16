CSSプッシュのスクリーンキャプチャ・ポルノ検出機能は、デフォルトでは無効になっています。このドキュメントでは、指定したプッシュのドメイン名に関連付けられたスクリーンキャプチャ・ポルノ検出機能を有効にする方法と、関連付け後にテンプレートをバインド解除してスクリーンキャプチャ・ポルノ検出機能を無効にする方法についてご説明します。

## 注意事項
- テンプレート設定の完了後、**約5分 - 10分**経ってから有効になります。
- スクリーンキャプチャ、ポルノ検出のテンプレート設定後、スクリーンキャプチャ・ポルノ検出結果を受け取るために、コールバックテンプレートを同時に設定する必要があります。コールバックテンプレートの設定については、[コールバック設定](https://intl.cloud.tencent.com/document/product/267/31065)をご参照ください。
- 1つのドメイン名は、1つのスクリーンキャプチャ・ポルノ検出テンプレートにのみ関連付けることができます。関連付けた後、そのドメイン名の下のすべてのストリームは、このテンプレートに従ってスクリーンキャプチャ、ポルノ検出されます。

## 前提条件
 -  [CSSコンソール](https://console.cloud.tencent.com/live)にログインし、 [プッシュドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)の追加が完了していること。 
 - [スクリーンキャプチャ・ポルノ検出テンプレート](https://intl.cloud.tencent.com/document/product/267/31072)を作成していること。


## スクリーンキャプチャ・ポルノ検出テンプレートの関連付け

1. [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)に入り、設定したいプッシュドメイン名または【管理】をクリックしてドメイン名詳細画面に入ります。
2. 【テンプレート設定】のタブを選択し、【Screencapturing and Porn Detection Configuration】のタブ右上角の【編集】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/17f2d3e8f3fff6a1c3eeec09651caf37.png)
3. スクリーンキャプチャ・ポルノ検出の設定テンプレートを選択し、【保存】をクリックすれば設定完了です。
![](https://qcloudimg.tencent-cloud.cn/raw/39d729e20b7bb2b152d29eba3723f382.png)


## スクリーンキャプチャ・ポルノ検出テンプレートのバインド解除
1. [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)に入り、設定したいプッシュドメイン名または【管理】をクリックしてドメイン名詳細画面に入ります。
2. 【テンプレート設定】タブを選択し、【Screencapturing and Porn Detection Configuration】タブの右上隅にある【編集】をクリックします。
3. 対応するテンプレートのチェックをクリックして外し、【保存】をクリックすれば完了です。
![](https://qcloudimg.tencent-cloud.cn/raw/f369adcf9c705a00024c50e8d6f94fea.png)
