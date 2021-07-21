<span id="que1"></span>
CSSにドメイン名をどのように追加すればいいですか。

1. Tencent Cloud [Live Console](https://console.cloud.tencent.com/live)にログインし、【Domain Management】ページに入ります。
2. 独自のプッシュドメイン名または再生ドメイン名を追加します。操作の詳細については、[Domain Management](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。
3. ドメイン名を追加した後、CNAME設定操作を完了してください。詳細については、[Configuring CNAME](https://intl.cloud.tencent.com/document/product/267/31057)をご参照ください。
4. 設定が正常に完了したら、独自のドメイン名を使用してプッシュ・再生できます。

<span id="que2"></span>
### CNAMEを設定した後も、未設定のまま表示されるのはなぜですか。

ドキュメント[Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057)に従って、CNAMEの設定を完了した場合は、CNAMEの設定が有効になるまで15分～30分かかります。しばらくお待ちください。また、CANMEが成功したかどうかをご自分で確認できます。確認方法の詳細については、[Verifying the Effect of CNAME Record](https://intl.cloud.tencent.com/document/product/267/31057)をご参照ください。
>
> - Linux/Mac/Windowsシステムはパブリックネットワークを介してDNS解決する必要があります。
> - CNAME操作後に常に検出に失敗する場合は、ドメイン名登録サービスプロバイダにお問い合わせください。

<span id="que3"></span>
### 独自のドメイン名を追加しない場合、どのような影響がありますか。
2018年10月17日以降にCSSサービスをアクティブにした場合は、CSSでは再生には独自のドメイン名を追加する必要があります。追加しない場合、CSSコンテンツを再生できません。

それ以前CSSサービスをアクティブした場合、CSSによってデフォルトのドメイン名が提供されます。できるだけ早く独自のドメイン名に切り替えることをお勧めします。Tencent Cloudでは、2018年12月31日以降、デフォルトのドメイン名が順次に使用停止されます。

> デフォルトのドメイン名は、CSSによって割り当てられたシステムドメイン名です。`bizid.livepush.myqcloud.com`と `bizid.tlivecdn.com`ような形式となります。

<span id="que4"></span>
### すでにデフォルトのドメイン名で特別な設定を行いましたが、独自のドメイン名を元のデフォルトのドメイン名に解決できますか。
新しいドメイン名へのアクセスには、ライブブロードキャストのアクセスプロセスを踏むことをお勧めします。CSSコンソールを介して、独自のドメイン名を追加し、各設定項目を設定できます。

