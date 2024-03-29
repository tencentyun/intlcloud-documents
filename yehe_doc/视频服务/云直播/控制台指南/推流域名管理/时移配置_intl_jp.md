CSSプッシュでは、デフォルトでタイムシフトが無効になっています。本書では、指定したプッシュドメイン名にタイムシフトテンプレートを関連付けて、タイムシフト機能を有効にする方法と、テンプレートをバインド解除しドメイン名のタイムシフト機能を無効にする方法を説明します。

[](id:limit)
## 使用制限
- テンプレート設定の完了後、約5分 - 10分経ってから有効になります。 
- テンプレートとの関連付けに成功すると、指定したプッシュドメイン名配下のプッシュアドレスに対して、タイムシフト機能が有効になります。
- ドメイン名ごとにタイムシフトテンプレートを1つだけ関連付けられます。関連付けられている場合、そのドメイン名配下のすべてのストリームは、テンプレートに従ってタイムシフトされます。

##  前提条件
-  [CSSコンソール](https://console.cloud.tencent.com/live)にログインし、 [プッシュドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加していること。
- タイムシフトテンプレートを作成していること。

[](id:conect)

## タイムシフトテンプレートとの関連付け
1. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)に進み、設定する**プッシュドメイン名**または**管理**をクリックしてドメイン名詳細ページに進みます。
2. **テンプレート設定**タグを選択し、**タイムシフト設定**タグの右上側の**編集**をクリックします。
3. タイムシフト設定テンプレートを選択し、**OK**をクリックします。

[](id:unite)
## タイムシフトテンプレートとのバインド解除
1. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)に進み、設定する**プッシュドメイン名**または**管理**をクリックしてドメイン名詳細ページに進みます。
2. **テンプレート設定**タグを選択し、**タイムシフト設定**タグの右上側の**編集**をクリックします。
3. 対応するテンプレートのチェックを外して、**OK**をクリックします。

>? タイムシフトテンプレートのバインド解除は、ライブストリーミング中のストリームには影響しません。