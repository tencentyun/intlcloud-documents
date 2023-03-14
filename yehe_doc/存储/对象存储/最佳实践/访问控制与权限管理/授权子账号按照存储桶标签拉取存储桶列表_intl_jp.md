## 概要

Cloud Object Storage（COS)コンソールは、バケットタグに基づいてバケットリストをフィルタリングする機能を提供しています。この機能は、Tencent Cloudのタグサービスに依存します。

企業アカウントがCompanyExample（OwnerUin 为100000000001，Owner_appid 为1250000000）で、サブアカウントDeveloperを持っていると仮定します。企業アカウントCompanyExampleはサブアカウントに対して、タグリストをプルする操作権限を承認する必要があります。権限承認の方法について、以下で詳しく説明します。



## 関連説明
サブアカウントがコンソールでバケットタグに基づきバケットリストをフィルタリングするには、サブアカウントがGetResourceTags、GetResourcesByTagsおよびGetTagsの操作権限を持つ必要があります。[CAM](https://console.cloud.tencent.com/cam/policy)コンソールにて、カスタムポリシーの形式で、サブアカウントにこれらの操作権限を承認します。



## 操作手順

1. 企業アカウントCompanyExampleを使用して、[CAM] (https://console.cloud.tencent.com/cam/policy) コンソールにログインし、ポリシー設定ページに移動します。
2. サブアカウントDeveloperが、タグリストをプルする権限を承認します。**ポリシージェネレーター**または**ポリシー構文**で実装できます。
<dx-tabs>
::: ポリシージェネレーターの承認
1. [CAM](https://console.cloud.tencent.com/cam/policy)のポリシー設定ページに進みます。
2. **カスタムポリシーの新規作成 > ポリシージェネレーターに従って作成**をクリックします。
3. 権限承認の設定ページに移動します。設定情報は以下のとおりです。
 - **タグ**：
    - **効果**：許可を選択します。デフォルトは変わりません。
    - **サービス**：タグを選択します。
    - **操作**：業務のニーズに基づいてチェックを入れます。ここではGetResourceTags、GetResourcesByTags、GetTagsの3つの操作権限にチェックを入れます。
    - **リソース**：**すべてのリソース**を選択します。
 - **権限の追加**：業務のニーズに基づいて設定します。
5. **次のステップ**をクリックし、ポリシー名を入力します。
6. **完了**をクリックすれば、作成完了です。
:::
::: ユーザーポリシー構文の承認
1. [CAM](https://console.cloud.tencent.com/cam/policy)のポリシー設定ページに進みます。
2. **カスタムポリシーの新規作成 > ポリシー構文に従って作成**をクリックします。
3. 空白テンプレート、または既存のタグテンプレートを選択することができます。ここでは、**QcloudTAGFullAccess**テンプレートを選択します。
4. **次へ**をクリックすると、テンプレートポリシーのデフォルト`tag:*`が表示されます。ここでは、actionを`name/tag:GetResourceTags`、`name/tag:GetResourcesByTags`、`name/tag:GetTags`の操作権限に変更します。ポリシー構文は以下のとおりです。
```
{
    "version": "2.0",
    "statement":[
        {
            "effect": "allow",
            "action":[
                "name/tag:GetResourceTags",
                "name/tag:GetResourcesByTags",
                "name/tag:GetTags"
            ],
            "resource":[
                "*"
            ]
        }
    ]
}
```
5. **完了**をクリックすれば、作成完了です。
:::
</dx-tabs>
3. ポリシーをサブアカウントDeveloperにバインドします。ポリシーページで、ステップ2で作成したポリシーを見つけ、右側の**ユーザー/グループ/ロールのバインド**をクリックします。
4. ポップアップウィンドウで、サブアカウントDeveloperにチェックを入れ、**OK**をクリックすると、サブアカウントDeveloperをそのポリシーにバインドできます。
5. サブアカウントDeveloperでコンソールにログインし、[バケットリスト](https://console.cloud.tencent.com/cos5/bucket)ページで**タグ**を選択し、**タグキー**で検索すると、これと同じタグのあるバケットリストを照会できます。

