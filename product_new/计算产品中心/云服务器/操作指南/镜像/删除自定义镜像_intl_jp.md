## ユースケース

このドキュメントでは、カスタムイメージを削除する方法について説明します。

## 注意事項
カスタムイメージを削除する前に、次の点に注意してください。
 - カスタムイメージを削除すると、それを使用して新しいCVMインスタンスを作成することはできなくなりますが、既に起動されているインスタンスには影響しません。このイメージから起動されたすべてのインスタンスを削除する場合は、 [インスタンスの回収](https://intl.cloud.tencent.com/document/product/213/4931)または[インスタンスの終了/リリース](https://intl.cloud.tencent.com/document/product/213/4930)をご参照ください。
 - 他のユーザーと共有されているカスタムイメージは削除できません。削除する前にすべての共有を解除する必要があります。詳細については、[カスタムイメージの共有解除方法](https://intl.cloud.tencent.com/document/product/213/7148)をご参照ください。
 - カスタムイメージのみを削除できます。パブリックイメージと共有イメージは削除できません。

## 操作手順
<dx-tabs>
::: コンソールからイメージを削除する
1. CVMコンソールにログインします。左側のナビゲーションバーで[イメージ](https://console.cloud.tencent.com/cvm/image)をクリックします。
2. **カスタムイメージ**タブを選択して、カスタムイメージ管理ページに進みます。
3. 実際のニーズに基づいてカスタムイメージを削除する方法を選択します。
 - **単一のイメージの削除**：イメージリストで削除するカスタムイメージを見つけて、【さらに】&gt;【削除】をクリックします。
  ![](https://qcloudimg.tencent-cloud.cn/raw/1211de56434b4b6034dccb1ff9ce4aa1.png)
 - **複数のイメージの削除**：イメージリストで削除するすべてのカスタムイメージを選択し、上部の【削除】をクリックします。
  ![](https://qcloudimg.tencent-cloud.cn/raw/9f002d5cce1cfa2c94931ea3bca25ac2.png)
4. [OK] をクリックします。
   削除できない場合は、理由が表示されます。
:::
::: API経由でイメージを削除する
ユーザーはDeleteImagesインターフェースを使用してイメージを削除します。詳細については、[イメージの削除](https://intl.cloud.tencent.com/document/product/213/33275)をご参照ください。
:::
</dx-tabs>
