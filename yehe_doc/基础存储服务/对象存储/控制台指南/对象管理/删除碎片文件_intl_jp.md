## 概要

指定したバケットを削除する必要があり、「**削除に失敗しました。バケット内の有効なデータを先に削除してください**」と表示された場合、**ファイルフラグメント**の管理項目に移動して、アップロードが完了していないファイルのフラグメントを確認し、削除することができます。バケット内の未完了のアップロードとアップロード済みのファイルがすべて削除されたことを確認した場合のみ、バケットを削除できます。

>!
> - オブジェクトのアップロード中に、アップロードを一時停止またはキャンセルしたファイルは、**ファイルフラグメント**の管理項目に表示されます。アップロードが完了すると、**ファイルリスト**でアップロード済みのファイルを検索できるようになります。
> - ファイルフラグメントは通常のオブジェクトと同じようにストレージスペースを占有しますので、ストレージ容量料金が発生します。
> 

## 操作手順
### ファイルフラグメントの手動削除

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリストページに進みます。
3. ファイルフラグメントを削除したいバケットを見つけ、そのバケット名をクリックし、バケット管理ページに進みます。
4. 左側ナビゲーションバーで**ファイルリスト**を選択し、ファイルリストページに進みます。
5. **ファイルフラグメント**をクリックします。
6. 開いたファイルフラグメントページで、アップロードが未完了のフラグメントファイルを確認できます。
7. ファイルフラグメントの右側にある**削除**をクリックすると、アップロードが未完了のフラグメントファイルを削除することができます。
あるいは、上部の**フラグメントのクリア**をクリックして、アップロードが未完了のフラグメントファイルをワンクリックで削除することもできます。
![](https://main.qcloudimg.com/raw/48ba3386157a800bb6896d655e52a975.png)
「フラグメントのクリア」または「削除」を行うと、表示されるリストは空になります。


### ファイルフラグメントを定期的にクリーンアップするようにライフサイクルを設定

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリストページに進みます。
3. ファイルフラグメントを削除したいバケットを見つけ、そのバケット名をクリックし、バケット管理ページに進みます。
4. 左側ナビゲーションバーで**基本設定 > ライフサイクル**をクリックし、ライフサイクル管理ページに進みます。
![](https://main.qcloudimg.com/raw/f9ba822a0f34eae84ede38d302f22092.png)
5. **ルールの追加**をクリックし、下図のように情報を設定します。ここでは、バケットの全範囲でフラグメントが作成されてから7日後に削除するようにルールを設定します。
![](https://main.qcloudimg.com/raw/9bb0397b0a87e5dadbdf40183329de5e.png)
6. **OK**をクリックすると、設定が成功したライフサイクルルールをコンソールで確認できます。
![](https://main.qcloudimg.com/raw/48ba0e8a81fa2a8eda8bcff276503fbe.png)
