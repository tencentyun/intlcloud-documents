遅延再生は、ユーザー側にプルする際の再生を遅延させる機能です。ユースケースは主に重要なライブストリーミングイベントに対してのもので、ライブストリーミング中に突発的な状況が発生することを回避し、対応する処理を事前にコントロールします。また、直接パラメータで設定できます。

## 注意事項
遅延再生は現在2つの方法で実現できます。
- [遅延再生インターフェース](https://intl.cloud.tencent.com/document/product/267/30850)を呼び出して遅延再生機能を実現します。
- **プッシュアドレス**の後ろにtxDelayTimeパラメータを追加すると、遅延再生機能をすぐに実現できます。詳細は、[プッシュ設定](#push_delay)をご参照ください。

>? インターフェースを呼び出すと、設定キャッシュが関連し、有効化時間の制御が難しいため、現在インターフェースを使用する方法は推奨していません。すぐに実現するには、プッシュアドレスの後ろにパラメータを直接追加する方法をお勧めします。

## 準備作業
1. [Tencent CSSサービス](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)をアクティブにし、 [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了します。
2. CSSコンソールにログインし、[【ドメイン名管理】](https://console.cloud.tencent.com/live/domainmanage)を選択して、【ドメイン名の追加】をクリックし、ICP登録したプルストリーミングドメイン名を追加します。詳細については、[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。

[](id:push_delay)
## プッシュ設定
1. CSSコンソールの【CSSツールボックス】>[【アドレスジェネレーター】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)に移動し、プッシュアドレスを発行します。
![](https://main.qcloudimg.com/raw/025aeea991996ddc35e6b61341714282.png)
2. プッシュアドレスの後ろに`txDelayTime`パラメータを追加し、OBSでプッシュを行います。具体的なプッシュ操作については、[OBSプッシュ](https://intl.cloud.tencent.com/document/product/267/31569)をご参照ください。
![](https://main.qcloudimg.com/raw/11cc2aee28d263e5740b1b6d0701652f.png)
>! txDelayTime、すなわち遅延再生時間を入力します。単位：秒、上限：600秒、Integer型。


## 遅延再生
1. CSSコンソールの【CSSツールボックス】>[【アドレスジェネレーター】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)に移動し、対応するプルストリーミングアドレスを発行します。設定は次のとおりです。
2. [VLC](https://intl.cloud.tencent.com/document/product/267/32483)、FFmepgなどのツールを使用して再生を行うことができます。具体的な再生の詳細は、[CSS再生](https://intl.cloud.tencent.com/document/product/267/31559)をご参照ください。
![]

 以上の再生比較から、再生画面の遅延は34秒であることがわかります。しかし、設定した遅延再生時間は30秒です。プッシュアドレスにtxDelayTimeパラメータを追加する方法で、遅延再生効果を実現できます。
