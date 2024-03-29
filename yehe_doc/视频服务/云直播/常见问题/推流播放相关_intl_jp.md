[](id:que1)
### ライブストリーミングのオンライン人数に上限はありますか。   
Tencent Cloud CSSはデフォルトではライブストリーミングのオンライン視聴者数を制限していません。ネットワーク等の条件が許す限り、ライブストリーミングを視聴することができます。ユーザーが帯域幅の制限を設定しているときは、視聴者数が多すぎて帯域幅の制限を超えた場合、新しいユーザーは視聴できなくなりますので、この場合、オンラインの人数は制限されます。

[](id:que2)
### 再生時のトランスコードはどのように使用しますか。
異なるネットワークの要素を考慮し、様々なビットレートや様々な解像度を使用するニーズを満たすために、[トランスコーディング設定](https://console.cloud.tencent.com/live/config/transcode)で様々なビットレートや様々な解像度のトランスコードテンプレートを設定することができます。トランスコード関連の詳しい情報については、[CSSカプセル化とトランスコーディング](https://intl.cloud.tencent.com/document/product/267/31561)をご参照ください。

[](id:multirate)
#### オリジナル、HD、SDシナリオ
業務の再生シナリオでは、通常、オリジナル、HD、SDの3つのビットレートを使用します。
 - オリジナルストリーミングはプッシュのビットレート・解像度と同じです。
 - HDストリーミングに使用するビットレートは2000kbps、解像度は1080pを推奨します。
 - SDストリーミングに使用するビットレートは1000kbps、解像度は720pを推奨します。

[](id:que3)
### タイムシフト視聴はどのように利用しますか。
過去の特定時間の素晴らしいコンテンツを視聴したい場合にタイムシフト機能をご利用いただけます。タイムシフト機能は現在HLSプロトコルのみをサポートしています。タイムシフトに関連する具体的な説明とアクティブ化の方法については、 [CSSタイムシフト](https://intl.cloud.tencent.com/document/product/267/31565)をご参照ください。

[](id:que4)
### HTTPSによる再生はどのように行いますか。
再生ドメイン名をHTTPSに対応させたい場合は、有効な証明書と有効な秘密鍵のコンテンツを用意し、[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)に移動して、**再生ドメイン名管理**>**高度な設定**>**HTTPS設定**を選択し、設定を追加する必要があります。追加に成功した後、設定が有効になるまでには時間がかかります（2時間）。有効になるとCSSストリームのHTTPSプロトコルによる再生が可能になります。

[](id:que5)
### 海外のアクセラレーションノードによる再生方法はどのようにして行いますか。
CSSのCDNノードは中国大陸のリージョンに行き渡るだけでなく、全世界の各大陸もカバーしており、広域かつ安定的にカバーされています。お客様のユーザーが中国香港、中国マカオ、中国台湾または中国本土以外のその他の地域に分布している場合、[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)でのドメイン名設定時に、アクセラレーションリージョンに**グローバルアクセラレーション**または**中国香港・マカオ・台湾地区および海外地区**を選択すれば、海外ノードによるカバーがサポートされます。


[](id:que6)
### 再生リンク不正アクセス防止をどのようにして有効化しますか。
違法なユーザーがお客様の再生URLを盗んで他所で再生し、トラフィックの損失が生じるのを防ぐため、再生アドレスに再生リンク不正アクセス防止を追加し、リンクの不正使用による不要な損失を防止することを強く推奨します。CSSの再生リンク不正アクセス防止は主に、txTime、key（ハッシュキー）、txSecret、有効時間の4つのパラメータ値によって制御します。

| リンク不正アクセス防止パラメータ | 説明 | 補足説明 |
|---------|---------|---------|
| txTime | 再生URLの有効時間 |形式：16進数UNIX時間。<br> 現在のtxTimeの値がその時リクエストした時間より大きい場合は正常に再生できます。そうでない場合はバックエンドに拒否されます。|
| key | MD5計算方式のキー | カスタマイズ可能で、プライマリ/スタンバイの2つのkeyを設定できます。<br> プライマリkeyが意図せず漏洩したときは、スタンバイkeyを使用して再生URLをスプライシングでき、同時にプライマリkeyの値も変更できます。|
| txSecret | 再生URLの中の暗号化パラメータ | 値はkey、StreamName、txTimeを順番にスプライシングした文字列をMD5のアルゴリズムで暗号化して取得します。<br>txSecret = MD5（key+StreamName+txTime）。 |
| 有効時間 | アドレスの有効時間 | 有効時間の設定は0より大きくする必要があります。<br> txTimeの設定が現在の時間、有効時間の設定が300sとしたならば、再生URLの期限は現在の時間 + 300sとなります。|

[](id:calculate)
#### リンク不正アクセス防止の計算
リンク不正アクセス防止の計算には、key（ランダム文字列）、StreamName（ストリーム名）、txTime（形式：16進数）の3つのパラメータが必要です。
設定したkeyが**somestring**、ストリーム名（StreamName）が**test**、txTimeが **5c2acacc**（2019-01-01 10:05:00）だと仮定します。またHDビットレートは**900kbps**、トランスコードテンプレート名は**900**とします。
オリジナルストリーミング再生アドレス：
```
txSecret = MD5(somestringtest5c2acacc) = b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.flv?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
http://domain/live/test.m3u8?txTime=5c2acacc&txSecret=b77e812107e1d8b8f247885a46e1bd34
```
HDストリーミング再生アドレス：
```
txSecret = MD5(somestringtest_9005c2acacc) = 4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.flv?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
http://domain/live/test_900.m3u8?txTime=5c2acacc&txSecret=4beae959b16c77da6a65c7edda1dfefe
```

[](id:open)
#### 再生リンク不正アクセス防止の有効化
1. [ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)を選択し、認証設定を行いたい再生ドメイン名または管理をクリックして、ドメイン名管理ページに進みます。
2. **アクセス制御** > **Key認証**から、スイッチをクリックし、Key認証をオンにします。
3. 認証設定ページで設定を行います。
4. **保存**をクリックすると、設定が保存されます。

>!
>- 再生認証の設定に成功した後、設定が有効になるまでには**30分間**必要です。
>-  HTTP-FLV：再生中のURLはtxTimeの期限切れ後も依然として正常に再生できますが、txTimeの期限切れ後にあらためて再生をリクエストすると拒否されます。
>- HLS：HLSは短縮URLであることから、絶え間なくm3u8にリクエストして最新のtsセグメントを取得します。仮に設定したtxTimeの値が現在の時間 + 10分間だとすると、10分後にHLSの再生URLリクエストは拒否されます。この問題には、業務側でHLSのリクエストアドレスを動的に変更するか、またはHLSの再生アドレス期限を少し長めに設定することで対処できます。

[](id:que7)
### 再生認証設定の中のプライマリkeyの形式にはどのような要件がありますか。有効時間の長さに制限はありますか。
認証設定の中のプライマリkeyの値にサポートされているのは大文字アルファベット、小文字アルファベット、数字となり、長さは最大256文字です。アルファベットと数字のランダムな組み合わせで構成します。詳細については、[再生認証設定](https://intl.cloud.tencent.com/document/product/267/31060)をご参照ください。
有効時間は1回のライブストリーミング時間の長さに設定することを推奨します。


[](id:que8)
### 固定のCSSプッシュアドレスを作成できますか。アドレス有効時間は最長どのくらいまで設定が可能ですか。
プッシュアドレスの有効時間は、主に認証の盗難防止のために設定します。固定のプッシュアドレスを作成すると、プッシュアドレス盗難という事態が発生し、現行の業務に損失をもたらす恐れがあります。
CSSプッシュアドレスの有効時間に制限はなく、個人の業務のニーズに応じてアドレスの期限を設定できます。また、スプライシングルールによって有効期間がより長いプッシュアドレスを発行することもできます。具体的な接合方法については、[自身でのCSS URLの接合に関する質問](https://intl.cloud.tencent.com/document/product/267/38393)をご参照ください。

>? プッシュアドレス有効期間の設定を長くし過ぎることは推奨しません。長過ぎる場合、当該プッシュアドレスの使用中にエラーが発生し、認証の失敗が喚起されます。

[](id:que9)
###  ライブストリーミングサービスの中のビデオにはTencent Cloudのロゴが表示されますか。 
ライブストリーミングサービスの中のビデオにTencent Cloudのロゴが表示されることはありません。 

[](id:que10)
###  ライブストリーミングの遅延はどのくらいですか。 
正常な場合、RTMPプロトコルでプッシュしてFLVプロトコルで再生すると、遅延は2秒～3秒前後です。遅延時間が長すぎる場合は、通常、問題があります。ライブストリーミング遅延時間が特に長い場合の具体的な原因調査の考え方については、 [ライブストリーミング遅延のトラブルシューティング](https://intl.cloud.tencent.com/document/product/267/7971)をご参照ください。

[](id:que11)
###  ライブストリーミング時に最高ビットレートを設定できますか。
 できません。プッシュ側で自主的に設定しますが、プッシュ側で最高ビットレートを設定しても、お客様のネットワークのアップロード速度によって左右されます。ビットレート（最大ビットレートとも呼びます）は、上限がお客様のネットワークのアップロード速度となります。設定が高過ぎるとライブストリーミング画面のフレームが欠落し、ラグが生じます。 

[](id:que12)
###   Tencent Cloud CSSの不要なライブストリーミングルームはどうすれば削除できますか。 
現在CSSでは、CSSストリームidによってCSSプッシュと再生を関連付けしていますので、削除の操作は必要ありません。IMサービスを使用し、IMのルームを削除して上限に達するのを避けたい場合は、[グループの解散](https://intl.cloud.tencent.com/document/product/1047/34896)を参照して操作を行うことができます。
使用するモードがチャンネルモードの場合は、DeleteLVBChannel-ライブストリーミングチャンネル削除のインターフェースを呼び出して削除することができ、削除予定のライブストリーミングチャンネルのID番号を入力します（一括入力をサポートしています）。

> ! チャンネルモードは旧版のスキームとなり、現在はすでに更新、メンテナンスを行っていません。
 
[](id:que13)
 ### CSSプッシュの有効化/無効化のインターフェースは何に使用しますか。 
CSSプッシュの有効化/無効化インターフェースは主にポルノ検出時の再生禁止シナリオに使用します。例えば、特定のキャスターにポルノ関連または反動的コンテンツが認められた場合、バックエンドでそのストリームを随時中断または使用禁止にすることができます。具体的な呼び出し方法は、[CSSストリーム禁止プッシュ](https://intl.cloud.tencent.com/document/product/267/30794)をご参照ください。


[](id:que14)
### バックグラウンド再生はどのようにして実装しますか。
バックグラウンド再生は端末側の機能であり、クライアントの実際の業務ロジックに基づき開発する必要があります。CSSストリームが中断されない限り、音声のバックグラウンド再生がサポートされます。


[](id:que15)
### HTTPS設定の変更時、証明書情報を追加したところ、“不正な証明書”と表示されました。どうすればいいですか。 
 CSSの暗号化サービスはNginxを使用し、このため証明書のタイプがNginxである必要があります。現在の証明書のタイプが正しいかどうか確認してください。

[](id:que16)
###  再生ドメイン名の認証を無効にした後、元の発行した再生アドレスでは再生できませんでした。なぜですか。 
 再生認証は有効期間を設定でき、有効期間内でアクセスの認証を無効にしても、オリジナルのアドレスでは依然として再生できません。 

[](id:que17)
###  インターフェースのアクセス回数の制限とは何ですか。
CSSでは、アカウント下のすべてのSecretIdが送信するリクエストの総数に対してアクセス回数の制限があり、制限を超えたリクエストは正常にレスポンスされません。
例えば、1秒間に200回を超過できないとします。これは、お客様のアカウント下のすべてのSecretIdが送信するこのタイプのリクエストについて、Tencent CVMが1秒間に受信できるのは200回のみであることを指します。この200回が単一のクライアントが200回送信したものでも200のクライアントが1回ずつ送信したものでも、また照会するストリームが複数でも1つでも、これらについては制限されません。総リクエスト数のみがカウントされます。 

[](id:que18)
###  プッシュの最中に“RTMP close”と表示され、プッシュに失敗しましたが、ログではプッシュ成功と表示されました。どのような状況なのでしょうか。 
現在のプッシュアドレスに問題がある可能性があります。[TCToolkit App](https://intl.cloud.tencent.com/document/product/1071/38147)を使用してプッシュアドレスが正常にプッシュされているかどうかをテストすることをお勧めします。さらに詳細なトラブルシューティング方法については、 [プッシュ失敗時のトラブルシューティング](https://intl.cloud.tencent.com/document/product/267/33383) をご参照ください。

[](id:que19)
###  フレームレートを修正した後、正常にプッシュできなくなり、ローカルで何度もサービスを再起動しなければならず、切断が度々起きました。どのように対処すればいいですか。 
現在設定しているフレームレートが高過ぎる可能性があります。15フレーム以上あればビデオのLD再生が保証されます。フレームレートを下げることをお勧めします。  

[](id:que20)
###  システムが長時間データのないプッシュを自主的に切断するのはどのような場合ですか。 
プッシュ時にデバイスに問題が起きた場合にこのようなトラブルが発生します。
例えば、Appのクラッシュ、携帯電話のシャットダウンなどその他の非主観的な原因による異常によって、バックエンドで70s間データのプッシュをキャプチャできなくなると、システムが自主的に切断します。

[](id:que21)
### 新バージョンのコンソールでのAPIキーはどうやって設定すればよいですか。
API KEYは旧バージョンのAPIインターフェース認証で、現在の公式サイトのAPIインターフェースは3.0バージョンにアップグレードされています。**[APIキー管理](https://console.cloud.tencent.com/cam/capi)** を介してSecretIdとSecretkeyを取得すれば、最新のAPI3.0インターフェースを使用することができます。

[](id:que21)
### 再生時にH.265コードを再生できないのはなぜですか。
H.265はH.264ほどの互換性がないため、プレーヤーがH.265コードをサポートしておらず、再生に失敗した場合は、 [トランスコードテンプレート](https://intl.cloud.tencent.com/document/product/267/31071) を設定し、H.264コードにトランスコードして再生することができます。

[](id:que22)
### m3u8のファイルは中国語名をサポートしますか。
m3u8のファイル名はライブストリーミングのストリーム名に基づき自動で命名されたものでもあり、ストリーム名は中国語名を**サポートしません**。

[](id:que23)
### ライブストリーミングのオンライン視聴人数をどのように取得しますか。
[照会ストリームの再生情報リスト](https://intl.cloud.tencent.com/document/product/267/37297) APIによってリアルタイムオンライン人数の取得をリクエストすることができますが、このオンライン人数は特別正確なものではありません。3人のユーザーが同時に視聴し、全員が同じIPを使用している場合、ここではオンライン人数は1人として記録されます。このAPIが返したデータは再生プロトコルをRTMPとFLVにした場合のみ参考になり、再生プロトコルをHLSにした場合、このデータはオンライン人数の参考にはなりません。

[](id:que24)
### CSSはプライマリおよびバックアップストリームをサポートしていますか。
CSSはプライマリおよびバックアップストリーム機能をご提供しています。ユーザーが同時に1つのストリーム名に対して2本のストリームをプッシュした場合、プルの際には1本目のプッシュストリームの内容しか見ることができず、2本目のプッシュストリームはバックアップストリームとして、1本目のプッシュストリームが切断された場合にのみ見ることができます。プライマリおよびバックアップストリーム機能はデフォルトで有効になっています。

[](id:que25)
### CSSは同一のプッシュアドレスへの異なるウォーターマークの追加をサポートしていますか。
ライブストリーミングの同一プッシュアドレスへの異なるウォーターマークの追加はサポートしていません。1つのプッシュアドレスには1つのウォーターマークテンプレートのみバインドできます。

[](id:que26)
### CSSでユーザーの視聴時間を確認するにはどうすればよいですか。
CSSは現時点ではユーザーの視聴時間の照会はサポートしていません。

[](id:que27)
### CSSではトランスコードを行わないユーザーはライブストリーミングを視聴できますか。
CSSは再生アドレスに依存して再生を行うため、トランスコードを行わなくても正常に再生できます（CSSストリームアドレスが有効な場合）。

[](id:que28)
### CSSの最初の画面までにかかる時間はどのような要素で構成されていますか。
最初の画面までにかかる時間は主にCSSストリームの視聴者数が多いかどうかに関係します。ストリームがホットな場合はocキャッシュにヒットするため、最初の画面までにかかる時間はやや短縮されます。

[](id:que9)
### ライブストリーミング視聴側のブラックリスト/ホワイトリストを設定することはできますか。
IPブラックリスト/ホワイトリスト設定によってIPブラックリスト/ホワイトリストおよびルールと内容をカスタマイズすることができます。リクエストIPによってリクエストをフィルタリングし、アクセス制限を実現してライブストリーミングの内容を保護することが可能です。具体的な操作手順については[IPブラックリスト/ホワイトリストの設定](https://intl.cloud.tencent.com/document/product/267/46767#configuring-ip-allowlist.2Fblocklist)をご参照ください。
- **IPホワイトリストの設定**：設定したIPアドレスのみが現在のライブストリーミングコンテンツにアクセスできます。
- **IPブラックリストの設定**：設定したIPアドレスは現在のライブストリーミングコンテンツにアクセスできなくなります。

[](id:que30)
### CSSポルノ検出は、一定の時間内に何枚の画像をキャプチャすることができますか。
CSSポルノ検出はスクリーンキャプチャをベースにして操作するものです。スクリーンキャプチャの際にポルノ検出機能を有効化した場合、一定の時間内にキャプチャする数量はキャプチャの時間間隔に関連します。スクリーンキャプチャの時間間隔は、CSSコンソールの[**CSSスクリーンキャプチャ&ポルノ検出**](https://console.cloud.tencent.com/live/config/jtjh)で、ご自身の必要に応じて設定することができます。
>?プッシュ中の自動スクリーンキャプチャの時間間隔は、デフォルトでは2秒です。値の範囲は2秒～300秒です。

[](id:que31)
### CSSで課金帯域幅およびトラフィックデータを照会するにはどうすればよいですか。
[ライブストリーミング課金帯域幅およびトラフィックデータの照会](https://intl.cloud.tencent.com/document/product/267/36098)で、DescribeBillBandwidthAndFluxListインターフェースから照会できます。

[](id:que32)
### CSSでプッシュが成功したかどうかを確認するにはどうすればよいですか。
- プッシュが成功した場合は、コンソール上で対応するストリームが生成されます。**CSSコンソール** > [**ストリーム管理**](https://console.cloud.tencent.com/live/streammanage) > **オンラインストリーム**で確認できます。
- あるいはAPIインターフェースを呼び出して[ストリームのステータス情報を照会](https://intl.cloud.tencent.com/document/product/267/30796)することもできます。

>? プッシュ再生が失敗した場合は、[CSSコンソール](https://console.cloud.tencent.com/live/tools/selfcheck)でセルフチェック機能を使用し、一般的なCSSプッシュ/再生の問題を迅速に診断することができます。詳細については、[セルフチェック](https://intl.cloud.tencent.com/document/product/267/39467)をご参照ください。

[](id:que33)
### CSSはオーディオのみのプッシュをサポートしていますか。
CSSはオーディオのみのプッシュをサポートしています（端末のプッシュツールを併用する必要があります）。また、オーディオのみのトランスコード機能もサポートしており、トランスコードテンプレートで設定することができます。詳細については、以下をご参照ください。
- [OBSオーディオのみのプッシュ](https://intl.cloud.tencent.com/document/product/267/31569)
- [CSSトランスコードテンプレート作成](https://intl.cloud.tencent.com/document/product/267/30790)

[](id:que34)
### CSSでライブストリーミング時間の統計を取るにはどうすればよいですか。
REST APIインターフェースを使用して統計情報の照会を行うことができます。詳細については、[ストリームの再生情報リストの照会](https://intl.cloud.tencent.com/document/product/267/37297)をご参照ください。

[](id:que35)
### CSSでCSSストリームのオンライン時間を照会するにはどうすればよいですか。
CSSでは現在、CSSストリームのオンライン時間を照会できるインターフェースがありません。プッシュコールバックとプッシュ切断コールバックの時間を取得して、CSSストリームのオンライン時間を計算することができます。

[](id:que37)
### CSSでライブストリーミングの視聴者数を照会するにはどうすればよいですか。
次の2つの方法で、視聴者数を照会することができます。
- **CSSコンソール** > **データセンター** > [**ストリームデータの照会**](https://console.cloud.tencent.com/live/analysis/stream) > **同時接続数**に進んで確認します。
>? 再生プロトコルがRTMPおよびFLVの場合、同時接続数がオンライン人数となります。再生プロトコルがHLSの場合は、このデータをオンライン人数として参考にすることはできません。
- CSS API 3.0の、ストリームの再生情報リストの照会のインターフェースを呼び出して、[オンライン視聴者数を取得](https://intl.cloud.tencent.com/document/product/267/37297)することをお勧めします。

[](id:que38)
### CSSプッシュ後にネットワークが切断された場合はプッシュ切断コールバックが送信されますか。
先にプッシュ切断コールバックを設定しておく必要があります。ネットワークが切断されたCSSストリームは、通常は自動的に再開します。70s以内にプッシュできたデータは自動的に復元されます（プッシュコールバック、プッシュ切断コールバックは送信されません）。70sを越えた場合はこちらで接続を切断し、新たなストリームを再度プッシュします（プッシュコールバック、プッシュ切断コールバックを送信します）。

[](id:que39)
### CSSプッシュプロトコルはプルプロトコルと一致している必要がありますか。
必要ありません。例えばプッシュをRTMPプロトコル、プルをRTMPプロトコル、FLVプロトコル、 HLSプロトコル、UDPプロトコルなどとすることもできます。

[](id:que40)
### CSSで無線ネットワークを使用した場合にCDNからプルできないのは何が原因ですか。
CSSで無線ネットワークを使用した場合にCDNからプルできない原因については、下記の方法でトラブルシューティングを行うことができます。
- 現在の無線ネットワークがTencent CloudのIPに制限をかけていないかを確認します。
- 現在の携帯電話がiPhoneの場合は、AppがWi-Fiの権限承認を行っているかどうかを確認します。

上記の方法で問題を解決できない場合は、Tencent Cloud技術コンサルタントにご連絡ください。専任の担当者がご対応します。

[](id:que41)
### CSSドメイン名でHTTPSを設定すると、再生できません。
この状況が生じた場合は、以下に従ってトラブルシューティングを行ってください。
- 証明書がアップロードされているかどうかを確認します。
- 証明書のアップロード時間を確認し（証明書は提出から約2時間後に有効になります）、約2時間後にこのドメイン名にアクセスしてください。

>? それでも問題が解決しない場合は、[CSSコンソール](https://console.cloud.tencent.com/live/tools/selfcheck)でセルフチェック機能を使用し、一般的なCSSプッシュ/再生の問題を迅速に診断することができます。詳細については、[セルフチェック](https://intl.cloud.tencent.com/document/product/267/39467)をご参照ください。



[](id:que42)
### ライブイベントストリーミングでキャスター側の解像度を動的に調整するにはどうすればよいですか。
ライブイベントストリーミングは再生部分を担当し、キャスター側はプッシュ部分を担当します。解像度を調整したい場合は、プル前に関連の[CSSトランスコードテンプレート](https://intl.cloud.tencent.com/document/product/267/31071)を設定することができます。



